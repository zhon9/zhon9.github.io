---
title: php debug
date: 2019-10-09 14:19:08
tags: [tool,php,windows]
---
### 利用symfony/var-dumper包中的dump()函数，格式化输出变量

1. 执行 composer global require symfony/var-dumper ，全局安装var-dumper包，默认会安装到${HOME}/.config/composer目录。

2. 在php.ini文件中加入一行:
```c
auto_prepend_file = ${HOME}/.config/composer/vendor/autoload.php
//auto_prepend_file可以简单地理解成：执行所有的php代码之前先include你指定的文件
```
从此以后，在你任意的php项目中调用dump()

### windows安装xdebug

1. 下载 xdebug.dll，地址：https://xdebug.org/download.php

2. 放到php安装目录的ext下

3. 配置php.ini
```c
extension="扩展的绝对路径"
//代码跟踪日志文件位置,注意要先新建这个traces目录，并设置777
xdebug.trace_output_dir = /tmp/traces
//代码跟踪日志文件名格式 
xdebug.trace_output_name = trace.%c.%p
//trace中显示函数的参数值，这个很有用，待会细说
xdebug.collect_params = 4
xdebug.collect_includes = On
xdebug.collect_return = On
xdebug.show_mem_delta = On
//var_display_max_depth这个参数也很有用。用来设置数组或者对象显示的最大层级。
//默认是3。参见官方文档的说明：Controls how many nested levels of array elements 
//and object properties are when variables are displayed 
//with either xdebug_var_dump(), xdebug.show_local_vars or through Function Traces.
xdebug.var_display_max_depth = 2
```

```php
xdebug_start_trace();
/* 业务代码     */
xdebug_stop_trace();
```