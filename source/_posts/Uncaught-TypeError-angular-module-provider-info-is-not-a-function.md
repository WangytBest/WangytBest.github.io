---
title: 'Uncaught TypeError: angular.module(...).provider(...).info is not a function'
date: 2017-09-14 15:27:19
tags: [ Angular, ngSanitize]
categories: Angular
# thumbnail: http://cloud.xuww.wang/nianshaodeni.png
---

> package.json中angular版本与ngSanitize版本不一致导致错误：
> Uncaught TypeError: angular.module(...).provider(...).info is not a function

[#github issue 上问题解答](https://github.com/angular/angular.js/issues/15791)

<!-- more -->

* 尬，angular版本必须要与ngSanitize版本一致！

> We do not support running core AngularJS that are at different versions. Can you explain why you would upgrade angular.js to 1.6.x but leave angular-sanitize.js at 1.5.x?
