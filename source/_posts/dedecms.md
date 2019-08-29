---
title: dedecms
date: 2017-08-08 20:22:20
tags: [dedecms]
---
常用标签，使用记录
<!-- more -->

``` bash
// 站点更目录
{dede:global.cfg_basehost/}

// 模板目录
{dede:global.cfg_templets_skin/}	

// 模板引入文件
{dede:include filename="head.htm"/}		

// 和文章有关的表
dede_addonarticle
dede_arctiny
dede_archives

// dedecms自定义标签，在/include/taglib/demotag.lib.php，有个演示标签

// 循环二级栏目
{dede:channelartlist typeid='top' noself='yes'}
  <li id="menu-{dede:field name='id'/}"><a htef="{dede:field name='typeurl'/}"><span>{dede:field name='typename'/}</span></a>
    <ul>
      {dede:channel type='son' noself='yes'}
        <li id='menu-[field:id/]'><a href='[field:typelink/]'><span>[field:typename/]</span></a></li>
      {/dede:channel}
    </ul>
  </li>
{/dede:channelartlist}

// if 标签
{dede:field name=id runphp='yes'}if(@me==44){@me='current-menu-parent';}else{@me='';}{/dede:field}

// 当前位置
{dede:field name='position'/}

// 文章发表日期
{dede:field.pubdate function="MyDate('Y-m-d H:i',@me)

// 循环外部链接栏目
5.7可以找include/taglib/channelartlist.lib.php第67行左右
$tpsql = " reid=0 AND ispart<>2 AND ishidden<>1 AND channeltype>0 ";
改成
$tpsql = " reid=0 AND ishidden<>1 AND channeltype>0 ";

// 系统-系统基本参数-其它选项，默认 模板引擎禁用标签 禁用 php标签

// 去掉验证码认证
/data/safe/inc_safe_config.php 里 $safe_gdopen = '1,2,3,4,5,7';  //1 注册会员 2前台登陆 6后台登陆 有就要验证

// 后台变量表
dede_sysconfig

//调用某栏目链接
{dede:type typeid='35'}[field:typeurl/]{/dede:type}

//文章列表
{dede:arclist typeid='23' titlelen='60' row='10'}
<a href="[field:arcurl/]">[field:image/]</a>
{/dede:arclist}

//分页
{dede:pagelist listitem="info,index,end,pre,next,pageno,option" listsize="5"/}

//首页调用其他栏目
{dede:arclist channelid='17' addfields='forex,silver,gold,oil' }
<li>
<div><a href="[field:arcurl/]">[field:image/]</a></div>
<a href="[field:arcurl/]">外汇[field:forex/]$ 白银[field:silver/]$<br/>
黄金[field:gold/]$ 原油[field:oil/]$</a> </li>
{/dede:arclist}
```