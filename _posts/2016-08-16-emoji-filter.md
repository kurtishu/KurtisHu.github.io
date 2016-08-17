--- 
published: true
title: Realm 让移动开发更简单
layout: post
author: Kurtis Hu
category: 
  - Android
tags: 
- Database
- ORM
---
 
Emoji filter for Openfire

```java

    protected boolean checkCodePoint(char codePoint) {
        if ((codePoint == 0x0) ||
                (codePoint == 0x9) ||
                (codePoint == 0xA) ||
                (codePoint == 0xD) ||
                ((codePoint >= 0x20) && (codePoint <= 0xD7FF)) ||
                ((codePoint >= 0xE000) && (codePoint <= 0xFFFD)) ||
                ((codePoint >= 0x10000) && (codePoint <= 0x10FFFF))) {
            return true;
        }

        return false;
    }
	
	// 配合正则表达式则可以过滤更多的emoji图片
	private static final String EMOJI_RANGE_REGEX =
            "[\uD83C\uDF00-\uD83D\uDDFF]|[\uD83D\uDE00-\uD83D\uDE4F]|[\uD83D\uDE80-\uD83D\uDEFF]|[\u2600-\u26FF]|[\u2700-\u27BF]";

    Pattern emojiPattern = Pattern.compile(EMOJI_RANGE_REGEX, Pattern.UNICODE_CASE | Pattern.CASE_INSENSITIVE);
	
```
