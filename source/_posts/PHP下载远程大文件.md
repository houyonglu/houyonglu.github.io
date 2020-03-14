---
title: PHP 下载远程大文件
date: 2017-12-28 15:40:50
tags:
---

通过为 `cURL` 设置一个可写的文件流解决文件被写入磁盘之前占用过多内存的问题。

``` php
/**
 * 下载远程大文件
 * @param  string $url 远程 URL
 * @param  resource $dist 本地路径或 resource 句柄
 * @return boolean true 或错误信息
 */
function downloadDistantFile($url, $dist)
{
  $ch = curl_init();

  curl_setopt_array($ch, [
    CURLOPT_FILE => is_resource($dist) ? $dist : fopen($dist, 'w'),
    CURLOPT_FOLLOWLOCATION => true,  // 处理重定向
    CURLOPT_MAXREDIRS => 10,  // 限制最大重定向次数
    CURLOPT_URL => $url,
    CURLOPT_FAILONERROR => true,  // 大于400的状态码将抛出错误           
  ]);

  return curl_exec($ch) === false ? curl_error($ch) : true;
}
```
