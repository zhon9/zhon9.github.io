---
title: XHProf windows 安装
date: 2017-03-11 19:30:13
tags: [tool,php,windows]
---
XHProf 是一个分层PHP性能分析工具，可以看到php程序各个函数的执行次数和执行时间等数据，帮助优化php程序。
<!-- more -->

## 下载
XHProf 扩展、[XHProf 调试输出页面](http://pecl.php.net/package/xhprof)、[Graphviz(非必须)](http://www.graphviz.org/Download_windows.php)

### XHProf 扩展放到 php的ext目录 下面
### XHProf 调试输出页面放到 服务器根目录
### 配置 php.ini ，然后重启Apache

在文件末尾加

```bash
[xhprof]
extension=php_xhprof.dll
xhprof.output_dir="E:\phpStudy\WWW\xhprof\xhprof_log"	//日志输出目录
```

## 安装 Graphviz

目录不要带中文或者中文字符

## 调试代码

```php
xhprof_enable();
//xhprof_enable(XHPROF_FLAGS_CPU+XHPROF_FLAGS_MEMORY);
//加上这个参数可以使得xhprof显示cpu和内存相关的数据。

...		//很多代码

$data = xhprof_disable();
include_once "E:\phpStudy\WWW\xhprof\xhprof-0.9.4\xhprof_lib\utils\xhprof_lib.php";
include_once "E:\phpStudy\WWW\xhprof\xhprof-0.9.4\xhprof_lib\utils\xhprof_runs.php";
$objXhprofRun = new XHProfRuns_Default();
$run_id = $objXhprofRun->save_run($data, "xhprof");
var_dump($run_id);    //输出日志的id
//访问 http://localhost/xhprof/xhprof-0.9.4/xhprof_html/
```

## 错误解决

在view full callgraph，查看图表分析的时候，出现错误
>failed to execute cmd: “dot -Tpng”. stderr: `’dot’ 不是内部或外部命令，也不是可运行的程序 或批处理文件。

在xhprof调试输出目录，找到 xhprof_generate_image_by_dot 函数

```php
$descriptorspec = array(
       // stdin is a pipe that the child will read from
       0 => array("pipe", "r"),
       // stdout is a pipe that the child will write to
       1 => array("pipe", "w"),
       // stderr is a pipe that the child will write to
       2 => array("pipe", "w")
);
$cmd = "dot -T".$type;
$process = proc_open($cmd, $descriptorspec, $pipes, "/tmp", array());
```

$cmd = "dot -T".$type; 这里加入Graphviz的bin路径 改成 $cmd = "D:/Graphviz2.38/bin/dot -T".$type;
