[TOC]

#### 1.配置App的URL Scheme
iOS系统中App之间是相互隔离的，通过URL Scheme，App之间可以相互调用，并且可以传递参数。

选中Target->Info->URL Types，配置URL Scheme（比如：jmlink）

在Safari中输入URL Scheme://（比如：jmlink://）如果可以唤起App，说明该URL Scheme配置成功

#### 2.配置Universal link
Universal link是iOS9的一个新特性，通过Universal link，App可以无需打开Safari，直接从微信等应用中跳转到App，真正的实现一键直达