# Top secret news

Веб-сайт:
![Site](/img/3.png)

1. Go to the news website, see news Windows and macOS. Try go to the tab LINUX.
2. In the category Linux, see: Access is denied
3. Web-site have not user authentication, no inputs, comments. There is only the GET requests (/post.php?id= , index.php?category=) and cookie (id, token).
4. All GET requests protected for XSS and SQL injection.
5. So something to do with the token. Change cookies, for example, using https://addons.mozilla.org/ru/firefox/addon/cookies-manager-plus/developers Try XSS - nothing.
6. Try SQL-injection. Token change for `your_token' or id='1"`
7. Updated the page. News of Linux appeared. Watch every news, and in one of them http://10.0.92.33:25362/post.php?id=8