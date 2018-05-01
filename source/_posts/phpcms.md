---
title: phpcms
date: 2018-04-27 20:22:20
tags: [phpcms]
---

常用标签，使用记录

<!-- more -->

``` php
// 调用一个栏目链接
{$CATEGORYS[21][url]}

// 三级栏目
{pc:content action="category" catid="0" num="25" siteid="$siteid" order="listorder ASC"}
{loop $data $c}
    <li class="{if $parentid == $c['catid'] || $catid == $c['catid']}active{/if}"><a href="{$c[url]}">{$c[catname]}</a>
    {if $c[child]}
        {loop subcat($c['catid']) $c2}
        <ul><li> {$c2['catname']}</li>
            {loop subcat($c2['catid']) $c3}
                <li> <a href="{$c3['url']}">{$c3['catname']}</a> </li>
            {/loop}
        </ul>
        {/loop}
    {/if}
    </li>
{/loop}
{/pc}

// 文章列表 ，content字段在{pc}加  moreinfo="1"
{pc:content action="lists" catid="$catid" num="10" order="id DESC" page="$page"}   
{loop $data $r}
    {$r[url]}
    {$r[thumb]}
    {$r[title]}
    {str_cut($r[description],200)}
    {date('Y-m-d H:i:s',$r[inputtime])}
    {$pages}
{/loop}
{/pc}

// 面包屑导航
{catpos($catid,' » ')}

// 调用父栏目列表
1.
{loop subcat($catid) $v}
  <li>{$v[catname]}</li>
{/loop}
2.
{pc:content action="category" catid="$CATEGORYS[$parentid][parentid]" num="25" siteid="$siteid" order="listorder ASC"}
{loop $data $c}
{/loop}
{/pc}

// 调用header
{template "content","header"}

// title keywords description
<title>{if isset($SEO['title']) && !empty($SEO['title'])}{$SEO['title']}{/if}{$SEO['site_title']}</title>
<meta name="keywords" content="{$SEO['keyword']}">
<meta name="description" content="{$SEO['description']}">

// js_path css_path img_path
{JS_PATH}
{CSS_PATH}
{IMG_PATH}

// 上一篇下一篇
<strong>上一篇：</strong><a href="{$previous_page[url]}">{$previous_page[title]}</a><br />
<strong>下一篇：</strong><a href="{$next_page[url]}">{$next_page[title]}</a>

// 表单
<form method="post" action="?m=formguide&c=index&a=show&formid={$formid}&siteid=<?php echo $this->siteid;?>" name="myform" id="myform">
  <input type="text" name="info['uname']" >
  <input type="submit" name="dosubmit" id="dosubmit" value=" 提交 ">
</form>

// SQL标签
{pc:get sql="SELECT COUNT(*) AS count,title,updatetime FROM li_news WHERE catid=$catid"}
{loop $data $k $v}
    {$v[count]}
{/loop}
{/pc}

```