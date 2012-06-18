---
layout    : post
permalink : /test-connection-speed-from-command-line
title     : Test connection speed from command line
comments  : true
author    : thehong
category  : Documentations
---
{% include JB/setup %}

Dạo này, tôi chán speed mấy con con VPS của mình ghê gớm. Tôi thử tìm và thấy lệnh này đơn
giản mà hay, (sử dụng tính năng stats của wget):

> wget --output-document=/dev/null http://speedtest.wdc01.softlayer.com/downloads/test500.zip

Tham khảo [Stackoverflow](http://stackoverflow.com/questions/426272/how-to-test-internet-connection-speed-from-command-line).
