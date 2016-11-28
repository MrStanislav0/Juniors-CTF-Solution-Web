# Крипто-магазин

Веб-сайт:
![Site](/img/2.png)

1. We go to the shop. What do we have? Cookies: wallet and gravitycoin; button "Оплатить и скачать".
2. Open the cookie and see that "Ваш счет криптовалюты gravitycoin:" match the value wallet. May be gravitycoin is the value 0? But no, there is base64.
3. Decode base64 string, we get strange characters. It is a crypto-shop, then gravitycoin is somehow encrypted.
4. Look the page code, nothing useful there. Remember that the sites have robots.txt. Go to robots.txt see in the list any file rsa.html.
5. Go to the page rsa.html but something redirects to 403.html.
6. Disable JS in your browser and go to rsa.html.
7. See public key. Use google, what is the RSA.
8. Online or write a program/script that will encrypt the number 140.3. https://habrahabr.ru/post/255799/
9. The encrypted text is encode to base64 and insert in the cookies gravitycoin.
10. Download file.