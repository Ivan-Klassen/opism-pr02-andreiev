# Практична робота № 2

**Дисципліна:** Основи побудови інформаційних систем та мереж (ОК-13)

**Тема:** Структура повідомлень прикладного протоколу HTTP. Формування запиту вручну

| Поле | Значення |
|---|---|
| Студент (прізвище, ім'я, по батькові) | Андреєв Іван Олегович |
| Група | ІПЗ-1.01 |
| Номер варіанта | 1 |
| Індивідуальний домен | fsf.org |
| «Чужий» домен для завдання A.3.1 (варіант ± 20) | arin.net |
| Середовище виконання | Killercoda Ubuntu Playground (Ubuntu 22.04 LTS) |
| Дата виконання | 08.10.2026 |

> Бланк заповнюють, не змінюючи структури розділів. Порожні заготовки блоків коду замінюють власними виводами. Позначки-підказки в кутових дужках вилучають.

---

## Частина A. Збір експериментальних даних

### Завдання A.1. Формування запиту вручну

**Команда:**

```
nc -C fsf.org 80
```

**Набраний запит:**

```
GET / HTTP/1.1
Host: fsf.org
Connection: close

```

**Відповідь:**

```
HTTP/1.0 301 Moved Permanently
Server: nginx
Date: Wed, 07 Oct 2026 17:45:38 GMT
Content-Type: text/html
Content-Length: 178
Location: https://www.fsf.org/
X-Cache: MISS from www.fsf.org
X-Cache-Lookup: MISS from www.fsf.org:3128
Via: 1.0 www.fsf.org (squid/3.1.19)
Connection: close

<html>
<head><title>301 Moved Permanently</title></head>
<body bgcolor="white">
<center><h1>301 Moved Permanently</h1></center>
<hr><center>nginx</center>
</body>
</html>
```

---

### Завдання A.2. Запит без поля `Host` у версії 1.1

**Команда:**

```
printf 'GET / HTTP/1.1\r\nConnection: close\r\n\r\n' | nc fsf.org 80
```

**Вивід:**

```
HTTP/1.0 301 Moved Permanently
Server: nginx
Date: Wed, 07 Oct 2026 17:46:00 GMT
Content-Type: text/html
Content-Length: 178
Location: https://www.fsf.org/
X-Cache: MISS from www.fsf.org
X-Cache-Lookup: MISS from www.fsf.org:3128
Via: 1.0 www.fsf.org (squid/3.1.19)
Connection: close

<html>
<head><title>301 Moved Permanently</title></head>
<body bgcolor="white">
<center><h1>301 Moved Permanently</h1></center>
<hr><center>nginx</center>
</body>
</html>
```

---

### Завдання A.3. Вплив поля `Host` на відповідь сервера

#### A.3.1. Чуже доменне ім'я в полі `Host`

**Команда:**

```
printf 'GET / HTTP/1.1\r\nHost: arin.net\r\nConnection: close\r\n\r\n' | nc fsf.org 80
```

**Вивід:**

```
HTTP/1.0 503 Service Unavailable
Server: squid/3.1.19
Mime-Version: 1.0
Date: Wed, 07 Oct 2026 17:46:10 GMT
Content-Type: text/html
Content-Length: 3239
X-Squid-Error: ERR_CANNOT_FORWARD 0
Vary: Accept-Language
Content-Language: en
X-Cache: MISS from www.fsf.org
X-Cache-Lookup: MISS from www.fsf.org:3128
Via: 1.0 www.fsf.org (squid/3.1.19)
Connection: close

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
<html><head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title>ERROR: The requested URL could not be retrieved</title>
<style type="text/css"><!-- 
 /*
 Stylesheet for Squid Error pages
 Adapted from design by Free CSS Templates
 http://www.freecsstemplates.org
 Released for free under a Creative Commons Attribution 2.5 License
*/

/* Page basics */
* {
        font-family: verdana, sans-serif;
}

html body {
        margin: 0;
        padding: 0;
        background: #efefef;
        font-size: 12px;
        color: #1e1e1e;
}

/* Page displayed title area */
#titles {
        margin-left: 15px;
        padding: 10px;
        padding-left: 100px;
        background: url('http://www.squid-cache.org/Artwork/SN.png') no-repeat left;
}

/* initial title */
#titles h1 {
        color: #000000;
}
#titles h2 {
        color: #000000;
}

/* special event: FTP success page titles */
#titles ftpsuccess {
        background-color:#00ff00;
        width:100%;
}

/* Page displayed body content area */
#content {
        padding: 10px;
        background: #ffffff;
}

/* General text */
p {
}

/* error brief description */
#error p {
}

/* some data which may have caused the problem */
#data {
}

/* the error message received from the system or other software */
#sysmsg {
}

pre {
    font-family:sans-serif;
}

/* special event: FTP / Gopher directory listing */
#dirmsg {
    font-family: courier;
    color: black;
    font-size: 10pt;
}
#dirlisting {
    margin-left: 2%;
    margin-right: 2%;
}
#dirlisting tr.entry td.icon,td.filename,td.size,td.date {
    border-bottom: groove;
}
#dirlisting td.size {
    width: 50px;
    text-align: right;
    padding-right: 5px;
}

/* horizontal lines */
hr {
        margin: 0;
}

/* page displayed footer area */
#footer {
        font-size: 9px;
        padding-left: 10px;
}


body
:lang(fa) { direction: rtl; font-size: 100%; font-family: Tahoma, Roya, sans-serif; float: right; }
:lang(he) { direction: rtl; }
 --></style>
</head><body id=ERR_CANNOT_FORWARD>
<div id="titles">
<h1>ERROR</h1>
<h2>The requested URL could not be retrieved</h2>
</div>
<hr>

<div id="content">
<p>The following error was encountered while trying to retrieve the URL: <a href="http://arin.net/">http://arin.net/</a></p>

<blockquote id="error">
<p><b>Unable to forward this request at this time.</b></p>
</blockquote>

<p>This request could not be forwarded to the origin server or to any parent caches. The most likely cause for this error is that the cache administrator does not allow this cache to make direct connections to origin servers, and all configured parent caches are currently unreachable.</p>

<p>Your cache administrator is <a href="mailto:webmaster?subject=CacheErrorInfo%20-%20ERR_CANNOT_FORWARD&amp;body=CacheHost%3A%20www.fsf.org%0D%0AErrPage%3A%20ERR_CANNOT_FORWARD%0D%0AErr%3A%20%5Bnone%5D%0D%0ATimeStamp%3A%20Wed,%2007%20Oct%202026%2017%3A46%3A10%20GMT%0D%0A%0D%0AClientIP%3A%2074.220.26.7%0D%0A%0D%0AHTTP%20Request%3A%0D%0AGET%20%2F%20HTTP%2F1.1%0AHost%3A%20arin.net%0D%0AConnection%3A%20close%0D%0A%0D%0A%0D%0A">webmaster</a>.</p>

<br>
</div>

<hr>
<div id="footer">
<p>Generated Wed, 07 Oct 2026 17:46:10 GMT by www.fsf.org (squid/3.1.19)</p>
<!-- ERR_CANNOT_FORWARD -->
</div>
</body></html>
```

#### A.3.2. Неіснуюче ім'я в полі `Host`

**Команда:**

```
printf 'GET / HTTP/1.1\r\nHost: opism-pr02.invalid\r\nConnection: close\r\n\r\n' | nc fsf.org 80
```

**Вивід:**

```
HTTP/1.0 503 Service Unavailable
Server: squid/3.1.19
Mime-Version: 1.0
Date: Wed, 07 Oct 2026 17:46:13 GMT
Content-Type: text/html
Content-Length: 3269
X-Squid-Error: ERR_CANNOT_FORWARD 0
Vary: Accept-Language
Content-Language: en
X-Cache: MISS from www.fsf.org
X-Cache-Lookup: MISS from www.fsf.org:3128
Via: 1.0 www.fsf.org (squid/3.1.19)
Connection: close

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
<html><head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title>ERROR: The requested URL could not be retrieved</title>
<style type="text/css"><!-- 
 /*
 Stylesheet for Squid Error pages
 Adapted from design by Free CSS Templates
 http://www.freecsstemplates.org
 Released for free under a Creative Commons Attribution 2.5 License
*/

/* Page basics */
* {
        font-family: verdana, sans-serif;
}

html body {
        margin: 0;
        padding: 0;
        background: #efefef;
        font-size: 12px;
        color: #1e1e1e;
}

/* Page displayed title area */
#titles {
        margin-left: 15px;
        padding: 10px;
        padding-left: 100px;
        background: url('http://www.squid-cache.org/Artwork/SN.png') no-repeat left;
}

/* initial title */
#titles h1 {
        color: #000000;
}
#titles h2 {
        color: #000000;
}

/* special event: FTP success page titles */
#titles ftpsuccess {
        background-color:#00ff00;
        width:100%;
}

/* Page displayed body content area */
#content {
        padding: 10px;
        background: #ffffff;
}

/* General text */
p {
}

/* error brief description */
#error p {
}

/* some data which may have caused the problem */
#data {
}

/* the error message received from the system or other software */
#sysmsg {
}

pre {
    font-family:sans-serif;
}

/* special event: FTP / Gopher directory listing */
#dirmsg {
    font-family: courier;
    color: black;
    font-size: 10pt;
}
#dirlisting {
    margin-left: 2%;
    margin-right: 2%;
}
#dirlisting tr.entry td.icon,td.filename,td.size,td.date {
    border-bottom: groove;
}
#dirlisting td.size {
    width: 50px;
    text-align: right;
    padding-right: 5px;
}

/* horizontal lines */
hr {
        margin: 0;
}

/* page displayed footer area */
#footer {
        font-size: 9px;
        padding-left: 10px;
}


body
:lang(fa) { direction: rtl; font-size: 100%; font-family: Tahoma, Roya, sans-serif; float: right; }
:lang(he) { direction: rtl; }
 --></style>
</head><body id=ERR_CANNOT_FORWARD>
<div id="titles">
<h1>ERROR</h1>
<h2>The requested URL could not be retrieved</h2>
</div>
<hr>

<div id="content">
<p>The following error was encountered while trying to retrieve the URL: <a href="http://opism-pr02.invalid/">http://opism-pr02.invalid/</a></p>

<blockquote id="error">
<p><b>Unable to forward this request at this time.</b></p>
</blockquote>

<p>This request could not be forwarded to the origin server or to any parent caches. The most likely cause for this error is that the cache administrator does not allow this cache to make direct connections to origin servers, and all configured parent caches are currently unreachable.</p>

<p>Your cache administrator is <a href="mailto:webmaster?subject=CacheErrorInfo%20-%20ERR_CANNOT_FORWARD&amp;body=CacheHost%3A%20www.fsf.org%0D%0AErrPage%3A%20ERR_CANNOT_FORWARD%0D%0AErr%3A%20%5Bnone%5D%0D%0ATimeStamp%3A%20Wed,%2007%20Oct%202026%2017%3A46%3A13%20GMT%0D%0A%0D%0AClientIP%3A%2074.220.26.7%0D%0A%0D%0AHTTP%20Request%3A%0D%0AGET%20%2F%20HTTP%2F1.1%0AHost%3A%20opism-pr02.invalid%0D%0AConnection%3A%20close%0D%0A%0D%0A%0D%0A">webmaster</a>.</p>

<br>
</div>

<hr>
<div id="footer">
<p>Generated Wed, 07 Oct 2026 17:46:13 GMT by www.fsf.org (squid/3.1.19)</p>
<!-- ERR_CANNOT_FORWARD -->
</div>
</body></html>
```

#### A.3.3. Запит без поля `Host` у версії 1.0

**Команда:**

```
printf 'GET / HTTP/1.0\r\n\r\n' | nc fsf.org 80
```

**Вивід:**

```
HTTP/1.0 301 Moved Permanently
Server: nginx
Date: Wed, 07 Oct 2026 17:46:18 GMT
Content-Type: text/html
Content-Length: 178
Location: https://www.fsf.org/
X-Cache: MISS from www.fsf.org
X-Cache-Lookup: MISS from www.fsf.org:3128
Via: 1.0 www.fsf.org (squid/3.1.19)
Connection: close

<html>
<head><title>301 Moved Permanently</title></head>
<body bgcolor="white">
<center><h1>301 Moved Permanently</h1></center>
<hr><center>nginx</center>
</body>
</html>
```

Зведення результатів наведено в **Додатку Д**.

---

### Завдання A.4. Два запити в одному з'єднанні

**Команда:**

```
printf 'GET /opism-pr02-12345 HTTP/1.1\r\nHost: fsf.org\r\n\r\nGET / HTTP/1.1\r\nHost: fsf.org\r\nConnection: close\r\n\r\n' | nc -C fsf.org 80
```

**Вивід:**

```
HTTP/1.0 301 Moved Permanently
Server: nginx
Date: Wed, 07 Oct 2026 17:46:22 GMT
Content-Type: text/html
Content-Length: 178
Location: https://www.fsf.org/opism-pr02-12345
X-Cache: MISS from www.fsf.org
X-Cache-Lookup: MISS from www.fsf.org:3128
Via: 1.0 www.fsf.org (squid/3.1.19)
Connection: keep-alive

<html>
<head><title>301 Moved Permanently</title></head>
<body bgcolor="white">
<center><h1>301 Moved Permanently</h1></center>
<hr><center>nginx</center>
</body>
</html>
HTTP/1.0 301 Moved Permanently
Server: nginx
Date: Wed, 07 Oct 2026 17:46:22 GMT
Content-Type: text/html
Content-Length: 178
Location: https://www.fsf.org/
X-Cache: MISS from www.fsf.org
X-Cache-Lookup: MISS from www.fsf.org:3128
Via: 1.0 www.fsf.org (squid/3.1.19)
Connection: close

<html>
<head><title>301 Moved Permanently</title></head>
<body bgcolor="white">
<center><h1>301 Moved Permanently</h1></center>
<hr><center>nginx</center>
</body>
</html>
```

**Кількість отриманих відповідей:** 2

**Коди стану отриманих відповідей:**  301 Moved Permanently, 301 Moved Permanently

---

### Завдання A.5. Запит за допомогою клієнтської програми

**Команда:**

```
curl -v --http1.1 http://fsf.org/ -o /dev/null
```

**Вивід:**

```
% Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0* Host fsf.org:80 was resolved.
* IPv6: 2001:470:142:4::a
* IPv4: 209.51.188.174
*   Trying 209.51.188.174:80...
* Connected to fsf.org (209.51.188.174) port 80
> GET / HTTP/1.1
> Host: fsf.org
> User-Agent: curl/8.5.0
> Accept: */*
> 
* HTTP 1.0, assume close after body
< HTTP/1.0 301 Moved Permanently
< Server: nginx
< Date: Wed, 07 Oct 2026 17:46:25 GMT
< Content-Type: text/html
< Content-Length: 178
< Location: https://www.fsf.org/
< X-Cache: MISS from www.fsf.org
< X-Cache-Lookup: MISS from www.fsf.org:3128
< Via: 1.0 www.fsf.org (squid/3.1.19)
* HTTP/1.0 connection set to keep alive
< Connection: keep-alive
< 
{ [178 bytes data]
100   178  100   178    0     0    842      0 --:--:-- --:--:-- --:--:--   843
* Connection #0 to host fsf.org left intact
```

---

### Завдання A.6. Запит через захищене з'єднання

**Ресурс, на якому виконано завдання:** fsf.org

**Підстава для використання резервного ресурсу (заповнюють за потреби):**

**Команда:**

```
openssl s_client -connect fsf.org:443 -servername fsf.org -crlf -quiet
```

**Набраний запит:**

```
GET / HTTP/1.1
Host: fsf.org
Connection: close

```

**Вивід:**

```
depth=3 C = US, O = Internet Security Research Group, CN = ISRG Root X1
verify return:1
depth=2 C = US, O = ISRG, CN = Root YR
verify return:1
depth=1 C = US, O = Let's Encrypt, CN = YR2
verify return:1
depth=0 CN = *.fsf.org
verify return:1
HTTP/1.0 301 Moved Permanently
Server: nginx
Date: Wed, 07 Oct 2026 17:46:43 GMT
Content-Type: text/html
Content-Length: 178
Location: https://www.fsf.org/
X-Cache: MISS from www.fsf.org
X-Cache-Lookup: MISS from www.fsf.org:3128
Via: 1.0 www.fsf.org (squid/3.1.19)
Connection: close

<html>
<head><title>301 Moved Permanently</title></head>
<body bgcolor="white">
<center><h1>301 Moved Permanently</h1></center>
<hr><center>nginx</center>
</body>
</html>
```

---

## Частина B. Розбір полів заголовка

Розбирається відповідь, отримана в завданні A.1.

**Загальна кількість полів заголовка у відповіді:** 9

| № | Поле заголовка | Значення | Призначення (власне формулювання) | Походження: сервер / проміжний вузол / не визначено | Обґрунтування |
|---|---|---|---|---|---|
| 1 | Server | nginx | Назва вебсервера | Сервер | Сторінку створив сервер і вказав це в HTML |
| 2 | Date | Wed, 07 Oct 2026 17:45:38 GMT | Час відповіді | Не визначено | Сервер і проксі може надати час відповіді, тому не визначено |
| 3 | Content-Type | text/html | Формат тіла відповіді | Сервер | Якщо сторінку створив сервер, то він визначає її формат. Формат був визначений як HTML |
| 4 | Content-Length | 178 | Розмір тіла відповіді в байтах | Сервер | Тіло згенерував сервер, тому він порахував його розмір |
| 5 | Location | https://www.fsf.org/ | Локація перенаправлення клієнта | Сервер | Сервер надав код відповіді 301 Moved Permanently. Вказав куди зробити редирект |
| 6 | X-Cache | MISS from www.fsf.org | Статус кешування | Проміжний вузол | "X-" - це заголовок кешування проксі. "MISS" - це промах кешу зі сторони проксі |
| 7 | X-Cache-Lookup | MISS from www.fsf.org:3128 | Результат пошуку в кеші | Проміжний вузол | 3128 - порт проксі Squid |
| 8 | Via | 1.0 www.fsf.org (squid/3.1.19) | Проходження запиту через проксі | Проміжний вузол | Проксі слугує проміжним вузлом і це поле повідомляє про це |
| 9 | Connection | close | Закриття з'єднання після запиту | Не визначено | Не відомо хто закрив з'єднання запиту | 

## Частина D. Висновки

Обсяг — 150–300 слів. Висновки спираються на власні спостереження.

**D.1.** Що з поведінки сервера виявилося неочевидним або несподіваним. Конкретно, з посиланням на рядок виводу.

У завданні A.4 я надсилав запит до неіснуючого шляху, тому я думав, що буде отримано помилку 404 Not Found. Було неочікувано, що сервер замість цього зробить редирект і не захоче перевіряти наявність шляхів на порту 80. Сервер у відповідь повернув: "HTTP/1.0 301 Moved Permanently". "Location: https://www.fsf.org/opism-pr02-12345" - тут сервер переніс неіснуючий шлях у безпечне HTTPS посилання.

**D.2.** Яке з полів заголовка викликало найбільше утруднення при визначенні походження (частина B) та з якої причини.

Утруднення викликало поле "X-Cache: MISS from www.fsf.org" - тут я не зрозумів, що означає значення "MISS" та префікс "X-", тому я спитав це у ШІ. ШІ пояснив, що значення "MISS" означає промах кешу, а "X-" - це нестандартний заголовок та ознака проміжного проксі-сервера Squid (бо він самостійно заявив про себе за допомогою заголовка "Server: squid/3.1.19"). Через це походження було визначено як проміжний вузол, оскільки ці дії виконував проксі.

**D.3.** Яке питання залишилося без відповіді після виконання роботи.

Якщо сервер на порту 80 зробив редирект на безпечний HTTPS та проігнорував неіснуючий шлях, то чи видасть сервер помилку "404 Not Found", якщо надіслати такий же запит на неіснуючий шлях, але вже через захищений порт 443? Також цікаво, чому під час надсилання без поля Host, замість сервера запрацював проксі та зробив редирект. Чи є проксі обов'язковим при роботі звичайного сайту і що виконує в цьому випадку проксі Squid?

---

## Контрольні питання

**1.** У завданні A.1 сервер не надсилав відповіді, доки не було введено порожній рядок. Чим це зумовлено?

Цей порожній рядок є повідомленням, що це кінець введення заголовків. Сервер повинен отримати цей порожній рядок, щоб переконатися, що всі заголовки були введені.

**2.** Порівняйте результати завдань A.1, A.2 та A.3.1–A.3.3 (таблиця Додатка Д). За яких значень поля `Host` і за якої версії протоколу сервер обслуговує запит, а за яких — ні? Яку задачу розв'язує поле `Host`? Відповідь має посилатися на конкретні рядки ваших виводів.

Наприклад, коли йде редирект (HTTP/1.0 301 Moved Permanently), то сервер обслуговує, а коли повертається (HTTP/1.0 503 Service Unavailable), він не обслуговує запит, бо просто не може його обробити. Редирект відбувається, коли Host є правильним або коли він відсутній. Помилка з кодом 503 відбувається тоді, коли вказано чужий або вигаданий домен. Тому заголовок Host допомагає серверу визначити, до якого саме сайту звертається клієнт серед кількох на одній IP-адресі.

**3.** Скільки відповідей надійшло у завданні A.4 і з якими кодами стану? Чи залежить відповідь сервера на порту 80 від запитаного шляху — і що це говорить про роль цього сервера? Якщо надійшла одна відповідь, знайдіть у ній поле заголовка, яке це пояснює, або зазначте, що такого поля немає. Якщо надійшло дві — що це означає для клієнтської програми, яка завантажує сторінку з великою кількістю вкладених ресурсів?

Було дві відповіді з редиректом (301 Moved Permanently). Від запитаного шляху відповідь не залежить, бо сервер на порту 80 ігнорує перевірку файлів у незахищеному середовищі, тому він не надав код 404, а замість цього зробив редирект на захищений порт 443. 80-й порт є небажаним, але замість того, щоб надавати це як повідомлення-помилку та взагалі перевіряти вміст запиту, було просто зроблено редирект. Було два запити, тому надіслано дві відповіді, але через одне підключення. Це економія часу та ресурсів, бо все вже відбувається в одному з'єднанні і не потрібно робити для цього нове повторно.

**4.** Які поля заголовка програма `curl` додала самостійно (завдання A.5)? Ці поля не є обов'язковими — сервер відповів і без них у завданні A.1. З якою метою їх додано?

curl додала два заголовки HTTP. "User-Agent: curl/8.5.0" - повідомляє про програму та її версію. "Accept: */*" - інформує про прийняття будь-якого формату.

**5.** За якими ознаками у вашому виводі виявляється присутність проміжного вузла? Якщо таких ознак не виявлено, поясніть, що з цього випливає.

Ознаками були прямі повідомлення у виводі: заголовок "Via: 1.0 www.fsf.org (squid/3.1.19)", який показує назву та версію Squid; заголовки "X-Cache" та "X-Cache-Lookup: MISS from www.fsf.org:3128", які містять префікс "X-", статус кешу та порт 3128; також у завданні A.3 у заголовку "Server: squid/3.1.19" замість відповіді від сервера було отримано відповідь прямо від проміжного вузла (проксі).

**6.** Три рядки, про які не йшлося на лекції, наведено в **Додатку В**.

---

## Додаток В. Відповіді на питання 6

| № | Рядок виводу | Джерело (номер завдання) |
|---|---|---|
| 1 | Location: https://www.fsf.org/ | Завдання A.1 |
| 2 | X-Cache: MISS from www.fsf.org | Завдання A.1 |
| 3 | User-Agent: curl/8.5.0 | Завдання A.5 |
| 4 | Accept: */* | Завдання A.5 |
---

## Додаток Д. Зведення результатів завдання A.3

**Вузол, з яким установлювалося з'єднання (у всіх пробах однаковий):** fsf.org

| Проба | Значення поля `Host` | Версія | Код стану | Обсяг тіла відповіді | Збігається з A.1 (так / ні) |
|---|---|---|---|---|---|
| A.1 (вихідна) | fsf.org | 1.1 | 301 | 178 байт | — |
| A.2 | поле відсутнє | 1.1 | 301 | 178 байт | так |
| A.3.1 | arin.net | 1.1 | 503 | 3239 байт | ні |
| A.3.2 | `opism-pr02.invalid` | 1.1 | 503 | 3269 байт | ні |
| A.3.3 | поле відсутнє | 1.0 | 301 | 178 байт | так |

**Висновок за таблицею (2–4 речення):** що саме змінювалося у запиті від проби до проби і як на це реагував сервер.

При зміні поля Host на чуже або на неіснуючий домен було повернуто код 503. Проксі заблокував запит, тому він не надійшов до Nginx. Він блокує цей запит, оскільки прив'язаний до fsf.org.

---

## Декларування використання технологій штучного інтелекту

Для цієї роботи встановлено **рівень Р3 — ШІ як співвиконавець**.

Виводи команд частини A не можуть бути згенеровані та мають бути отримані внаслідок фактичного виконання команд.

**Чи використовувалися технології ШІ під час виконання роботи:** <так / ні>

Якщо так, заповнюють таблицю. Якщо ні, таблицю вилучають.

| № | Інструмент (назва, версія) | Етап роботи | Дослівний текст запиту (промпту) | Як використано результат |
|---|---|---|---|---|
| 1 | Google AI Studio (Gemini 3.8 Flash) | Підготовка до виконання практичної роботи та вибір серидовища | напиши покроков як мені виконувати практичну роботу. в якому середовищі робити краще всього. чому рекомендується Killercoda. чому просто не використовувати powershell | Було обрано Killercoda замість PowerShell. Отримано покрокове пояснення виконання практичної роботи |
| 2 | Google AI Studio (Gemini 3.8 Flash) | Частина B | а miss це що. як мені це пояснити бо я не розумію що це за кешування | Отриманно пояснення заголовку "X-", кешування проксі-сервером та значення "MISS" |

**Підтвердження:** усі виводи команд, наведені в частині A, отримано внаслідок фактичного виконання команд на зазначеному індивідуальному домені.

---

*ОПІСМ (ОК-13) · Практична робота № 2 · бланк звіту*
