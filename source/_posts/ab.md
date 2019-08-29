---
title: windows使用ApacheBench（ab）做网站压力测试
date: 2017-02-28 19:30:13
tags: [tool]
---
Apache Bench是著名Web服务器软件apache附带的一个小工具，它可以同时模拟多个并发请求，测试apache等Web服务器的最大承载压力，同时也可以根据Apache Bench提供的测试结果对服务器性能参数进行调整。
<!-- more -->

## 在Windows系统的命令行下，cd到 Apache/bin 目录下

``` bash
E:\phpStudy\Apache\bin>ab -n 1000 -c 100 http://192.168.0.188/
```

### 必须在后方加上“/”，或指定相应文件。

-n后面的1000代表总共发出1000个请求；-c后面的100表示采用100个并发（模拟100个人同时访问），后面的网址表示测试的目标URL。

## 测试结果

``` bash
This is ApacheBench, Version 2.3 <$Revision: 1604373 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/
Benchmarking 192.168.0.188 (be patient)
Completed 100 requests
Completed 200 requests
Completed 300 requests
Completed 400 requests
Completed 500 requests
Completed 600 requests
Completed 700 requests
Completed 800 requests
Completed 900 requests
Completed 1000 requests
Finished 1000 requests
Server Software:        nginx/1.6.3
#测试的服务器版本
Server Hostname:        192.168.0.188
Server Port:            80
Document Path:          /
Document Length:        169004 bytes
Concurrency Level:      100
Time taken for tests:   15.170 seconds
Complete requests:      1000
#完成的请求数量
Failed requests:        3
#失败的请求数量
   (Connect: 0, Receive: 0, Length: 3, Exceptions: 0)
Non-2xx responses:      3
Total transferred:      168791239 bytes
HTML transferred:       168498599 bytes
Requests per second:    65.92 [#/sec] (mean)
#重要的指标之一，相当于LR中的每秒事务数，后面括号中的mean表示这是一个平均值
Time per request:       1516.954 [ms] (mean)
#重要的指标之二，相当于LR中的平均事务响应时间，后面括号中的mean表示这是一个平均值
Time per request:       15.170 [ms] (mean, across all concurrent requests)
#每个连接请求实际运行时间的平均值
Transfer rate:          10866.19 [Kbytes/sec] received
#平均每秒网络上的流量，可以帮助排除是否存在网络流量过大导致响应时间延长的问题
Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0   10   8.8     16      36
Processing:    78 1478 494.6   1516    2283
Waiting:       47  779 543.9    628    2079
Total:         78 1489 495.4   1524    2283
Percentage of the requests served within a certain time (ms)
  50%   1524
  66%   1799
  75%   1957
  80%   2006
  90%   2085
  95%   2127
  98%   2161
  99%   2205
 100%   2283 (longest request)
```