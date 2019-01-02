---
layout:              post
title:                  "Hello test"
subtitle:            " \"Hello TEST,\""
date:                 2019-01-02 11:08:00 +0800
author:             "SNLO"
header-img:     "img/header_code.jpg"
catalog:            true
tags:
- 生活
---
## 正文

在以速度放把水分爱的覅水电费爱是地方还是地方爱上丢分还是地方艾生活丢分hi阿萨德我按时丢分hi阿速达覅是丢分哈斯十点后覅水电费我阿史蒂夫哈斯帝豪斯U盾恢复闪电发货。

#### 家家爱建设大街将发送

拉卡萨诺的开发商

一段加载bundle中的国际化文字函数

```swift
+ (NSString *)sn_localizedStringForKey:(NSString *)key table:(NSString *)table bundle:(NSString *)bundle {
    if (!table) {
        table = @"SNToolStrings";
    }
    if (!bundle) {
        bundle = @"SNTool";
    }

    NSString *language = [NSLocale preferredLanguages].firstObject;
    if ([language hasPrefix:@"en"]) {
        language = @"en";
    } else if ([language hasPrefix:@"zh"]) {
        if ([language rangeOfString:@"Hans"].location != NSNotFound) {
            language = @"zh-Hans";
        }
    } else {
        language = @"en";
    }

    NSBundle * bundleKit = [NSBundle bundleWithPath:[[NSBundle mainBundle] pathForResource:bundle ofType:@"bundle"]];
    NSBundle * bundles = [NSBundle bundleWithPath:[bundleKit pathForResource:language ofType:@"lproj"]];

    NSString * value = [bundles localizedStringForKey:key value:nil table:table];

    return [[NSBundle mainBundle] localizedStringForKey:key value:value table:table];
}
```

##### 后记

阿斯蒂芬阿萨德你过分，爱三点半覅是。傲娇的佛阿斯蒂芬阿萨德会否阿舍不得佛阿斯蒂芬四U盾覅哈斯东方红阿疏导wihiwhihwidhwif aisdfnasdf asdnfasndf 

