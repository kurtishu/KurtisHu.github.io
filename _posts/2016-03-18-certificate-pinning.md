--- 
published: true
title: 数字签名
layout: post
author: Kurtis Hu
category: 
  - security
tags: 
- Android SSL Certificate Pinning
---

> http://www.mobilephonedevelopment.com/archives/1762
> http://www.tuicool.com/articles/2MVJb2


在SSL/TLS通信中，客户端通过数字证书判断服务器是否可信，并采用证书的公钥与服务器进行加密通信。

然而，在开发者在代码中不检查服务器证书的有效性，或选择接受所有的证书时，这种做法可能导致的问题是中间人攻击。  攻击者可以伪造证书，或者盗用证书，以来达到和客户端建立通信的目地。 目前Google已经针对不验证服务器证书的app给出了警告，这些app将来是会有被Play Store拒之门外的危险的。(参考)[https://support.google.com/faqs/answer/6346016?hl=en]

### 开发者常见信任所有证书的错误做法
实现一个X509TrustManager接口，将其中的CheckServerTrusted()方法实现为空，即不检查服务器是否可信或者在SSLSoketFactory的实例中，通过setHostnameVerifier(SSLSocketFactory.ALLOW_ALL_HOSTNAME_VERIFIET),接受所有证书。做出这种选择的可能原因是，使用了自己生成了证书，客户端发现证书没有和可信CA 形成信任链，出现 了CertificateException等异常。

####  使用Apache的HttpClient  
``` java
public static DefaultHttpClient getHttpClient(int httpPort,
			int httpsPort) {
		try {
			SSLSocketFactory sf = getSocketFactory();
			sf.setHostnameVerifier(SSLSocketFactory.ALLOW_ALL_HOSTNAME_VERIFIER);

			HttpParams params = new BasicHttpParams();
			HttpProtocolParams.setVersion(params, HttpVersion.HTTP_1_1);
			HttpProtocolParams.setContentCharset(params, HTTP.UTF_8);
			HttpProtocolParams.setUseExpectContinue(params, true);

			// set connection timeout.
			ConnManagerParams.setTimeout(params, DEFAULT_TIMEOUT);
			HttpConnectionParams.setConnectionTimeout(params,
					DEFAULT_CONN_TIMEOUT);
			HttpConnectionParams.setSoTimeout(params, DEFAULT_SOCKET_TIMEOUT);
			// set socket buffer size
			HttpConnectionParams.setSocketBufferSize(params,
					DEFAULT_SOCKET_BUFFER_SIZE);
			// set max connections per host
			ConnManagerParams.setMaxConnectionsPerRoute(params,
					new ConnPerRouteBean(DEFAULT_MAX_CONN_PER_ROUTE));
			// set max total connections
			ConnManagerParams.setMaxTotalConnections(params,
					DEFAULT_MAX_CONNECTIONS);

			SchemeRegistry registry = new SchemeRegistry();
			registry.register(new Scheme("http", PlainSocketFactory
					.getSocketFactory(), httpPort));
			registry.register(new Scheme("https", sf, httpsPort));

			ClientConnectionManager ccm = new ThreadSafeClientConnManager(
					params, registry);
			return new DefaultHttpClient(ccm, params);
		} catch (Exception e) {
			return new DefaultHttpClient();
		}
	}

	public static void setCredentials(DefaultHttpClient httpClient,
			String host, int port, String realm, String username, String password) {
		httpClient.getCredentialsProvider().setCredentials(
				new AuthScope(host, port, realm, "basic"),
				new UsernamePasswordCredentials(username, password));
	}

```      
 
 重点是在MySSLSocketFactory，马上贴上代码     

``` java  
    // 获取SocketFactory
	private SSLSocketFactory getSocketFactory() {
	  final TrustManager[] trustManagers = new TrustManager[] { new X509TrustManager() {
            @Override
            public void checkClientTrusted(
                    java.security.cert.X509Certificate[] chain,
                    String authType) throws CertificateException {
            }

            @Override
            public void checkServerTrusted(
                    java.security.cert.X509Certificate[] chain,
                    String authType) throws CertificateException {

            }

            @Override
            public java.security.cert.X509Certificate[] getAcceptedIssuers() {
                return null;
            }
        } };

        // Install the all-trusting trust manager
        final SSLContext sslContext = SSLContext.getInstance("TLS");
        sslContext.init(null, trustManagers, new java.security.SecureRandom());
        // Create an ssl socket factory with our all-trusting manager
        return sslContext.getSocketFactory();
	}
```

####    使用Square的OKHttp

``` java
 private void getOKHttpClient() throws Exception {
        OkHttpClient okHttpClient = new OkHttpClient();
        final TrustManager[] trustManagers = new TrustManager[] { new X509TrustManager() {
            @Override
            public void checkClientTrusted(
                    java.security.cert.X509Certificate[] chain,
                    String authType) throws CertificateException {
            }

            @Override
            public void checkServerTrusted(
                    java.security.cert.X509Certificate[] chain,
                    String authType) throws CertificateException {

            }

            @Override
            public java.security.cert.X509Certificate[] getAcceptedIssuers() {
                return null;
            }
        } };

        // Install the all-trusting trust manager
        final SSLContext sslContext = SSLContext.getInstance("TLS");
        sslContext.init(null, trustManagers, new java.security.SecureRandom());
        // Create an ssl socket factory with our all-trusting manager
        final SSLSocketFactory sslSocketFactory = sslContext.getSocketFactory();
        okHttpClient.setSslSocketFactory(sslSocketFactory);

        // Sets the verifier used to confirm that response certificates
        okHttpClient.setHostnameVerifier(new HostnameVerifier() {
            @Override
            public boolean verify(String hostname, SSLSession session) {
                return true;
            }
        });
    }
```    

###   Certificate Pinning   
事实上，在移动软件大多只和固定的服务器通信，因此可以在代码更精确地直接验证是否某张特定的证书，这种方法称为“证书锁定”（certificate pinning）。   
实现证书的方法有二种：一种是前文提到的实现X509TrustManager接口，另一种则是使用keystore。    

####    方法一：   
实现X509TrustManager接口，在方法checkClientTrusted中可以获取到服务器端的证书，证书里面有包括版本号， 序列号， 创建时间，过期时间，公钥，签名等信息，一般情况下我们是那公钥验证。      
常规做法是先获取到证书上的公钥，然后hash或者MD5，或者加上其他的处理，当每次请求时在方法checkClientTrusted中获取公钥做同样的处理，比较两次处理后的结果是否一致，如果一直说明访问的Server是可信的，否则是不可信的。     

**OKHttp ** 针对Certificate Pinning 做了一个封装，它的原理是，可以对特定的host做证书验证，其实也是验证证书的公钥，不过有自己特定的规则{Public Key}经过Sha1算法hash一下，然后Base64加密一次，然后在结果前面加上字符串"sha1/".                  

``` java       
  
  CertificatePinner certificatePinner = new CertificatePinner.Builder()
                    .add("127.0.0.1", "sha1/xxxxx")
                    .build();
            okHttpClient.setCertificatePinner(certificatePinner);
			
  // 在	checkClientTrusted方法中通过以下方法可以获取上面"xxxxx"	的内容	
  Util.sha1(ByteString.of(chain[0].getPublicKey().getEncoded())).base64()			
```   

####    方法二：   
使用keystone， 具体如果使用，且听下回分解。   
<br/>
