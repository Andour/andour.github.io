---
title: mysql_connect 速度测试:localhost & 127.0.0.1
date: 2017-04-16
author: Andour
tags: php mysql

---

> {% for item in page.tags %}  {{item}} {% endfor %}

源码1：

```php
<?php

$start_time = microtime(true);
for ($i=0; $i<10; $i++){
	$con = mysql_connect("localhost","root","root");
	//$con = mysql_connect("127.0.0.1","root","root");
	if (!$con)
		die('Could not connect: ' . mysql_error());
	else
		echo "Success<br />";
	mysql_close($con);
}
$end_time = microtime(true);
echo 'Time: '.($end_time-$start_time).' s';

?>
```

运行1：

![](http://wx3.sinaimg.cn/mw690/006dXdWxgy1feo3zk0ijwj30h80b9t92.jpg)

![](http://wx1.sinaimg.cn/mw690/006dXdWxgy1feo3zkfqjgj30bb05r3yj.jpg)

源码2：

```php
<?php

$start_time = microtime(true);
for ($i=0; $i<10; $i++){
	//$con = mysql_connect("localhost","root","root");
	$con = mysql_connect("127.0.0.1","root","root");
	if (!$con)
		die('Could not connect: ' . mysql_error());
	else
		echo "Success<br />";
	mysql_close($con);
}
$end_time = microtime(true);
echo 'Time: '.($end_time-$start_time).' s';

?>
```



运行2：

![](http://wx3.sinaimg.cn/mw690/006dXdWxgy1feo3zkvw0nj30hf0bf74n.jpg)

![](http://wx2.sinaimg.cn/mw690/006dXdWxgy1feo3zlbilhj30b406uq31.jpg)

10s VS 34ms，近**300倍**的差距！

---
<br />
<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/88x31.png" /></a><br />本<span xmlns:dct="http://purl.org/dc/terms/" href="http://purl.org/dc/dcmitype/Text" rel="dct:type">作品</span>由<a xmlns:cc="http://creativecommons.org/ns#" href="http://andour.me" property="cc:attributionName" rel="cc:attributionURL">Andour</a>采用<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/">知识共享署名-非商业性使用-禁止演绎 4.0 国际许可协议</a>进行许可。<br />本许可协议授权之外的使用权限可以从 <a xmlns:cc="http://creativecommons.org/ns#" href="http://andour.me" rel="cc:morePermissions">http://andour.me </a>处获得。
