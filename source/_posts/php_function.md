---
title: php function
date: 2020-06-21
---
php function
<!-- more -->
```php
/**
 * 扫描文件夹并筛选
 * @param $dir
 * @param $filter array('file_name')
 * @param $type all,dir,file
 */
function scan($dir,$filter=array(),$type="all"){
    $result=array();
    if(is_dir($dir)){
        $list = scandir($dir);
        foreach($list as $dirname){
            if($dirname == '.' || $dirname == '..' || in_array($dirname,$filter)){
                continue;
            }
            if($type=="dir" && is_file($dir.'/'.$dirname)){
                continue;
            }
            if($type=="file" && is_dir($dir.'/'.$dirname)){
                continue;
            }
            $result[]=$dirname;
        };
    }
    return $result;
}

/**
 * 删除文件夹
 * @param $dirName
 */
function removeDir($dirName) 
{ 
    if(! is_dir($dirName)) 
    { 
        return false; 
    } 
    $handle = @opendir($dirName); 
    while(($file = @readdir($handle)) !== false) 
    { 
        if($file != '.' && $file != '..') 
        { 
            $dir = $dirName . '/' . $file; 
            is_dir($dir) ? removeDir($dir) : @unlink($dir); 
        } 
    } 
    closedir($handle); 
      
    return rmdir($dirName) ; 
}

/**
 * 复制文件夹
 * @param $source
 * @param $dest
 */
function copyDir($source, $dest)
{
    if (!file_exists($dest)) mkdir($dest);
    $handle = opendir($source);
    while (($item = readdir($handle)) !== false) {
        if ($item == '.' || $item == '..') continue;
        $_source = $source . '/' . $item;
        $_dest = $dest . '/' . $item;
        if (is_file($_source)) copy($_source, $_dest);
        if (is_dir($_source)) copyDir($_source, $_dest);
    }
    closedir($handle);
}
```