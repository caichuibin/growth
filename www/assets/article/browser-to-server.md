如果你的操作系统带有cURL[^cURL]这个软件(在GNU/Linux、Mac OS都自带这个工具，Windows用户可以从[http://curl.haxx.se/download.html](http://curl.haxx.se/download.html)下载到)，那么我们可以直接用下面的命令来看这看这个过程[^HTTP2cURL](-v 参数可以显示一次http通信的整个过程)：

```
curl -v https://www.phodal.com
```

我们就会看到下面的响应过程:

```bash
* Rebuilt URL to: https://www.phodal.com/
*   Trying 54.69.23.11...
* Connected to www.phodal.com (54.69.23.11) port 443 (#0)
* TLS 1.2 connection using TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
* Server certificate: www.phodal.com
* Server certificate: COMODO RSA Domain Validation Secure Server CA
* Server certificate: COMODO RSA Certification Authority
* Server certificate: AddTrust External CA Root
> GET / HTTP/1.1
> Host: www.phodal.com
> User-Agent: curl/7.43.0
> Accept: */*
>
< HTTP/1.1 403 Forbidden
< Server: phodal/0.19.4
< Date: Tue, 13 Oct 2015 05:32:13 GMT
< Content-Type: text/html; charset=utf-8
< Content-Length: 170
< Connection: keep-alive
<
<html>
<head><title>403 Forbidden</title></head>
<body bgcolor="white">
<center><h1>403 Forbidden</h1></center>
<hr><center>phodal/0.19.4</center>
</body>
</html>
* Connection #0 to host www.phodal.com left intact
```

我们尝试用cURL去访问我的网站，会根据访问的域名找出其IP，通常这个映射关系是来源于ISP缓存DNS（英语：Domain Name System）服务器[^DNSServer]。

以“\*”开始的前8行是一些连接相关的信息，称为**响应首部**。我们向域名 [https://www.phodal.com/](https://www.phodal.com/)发出了请求，接着DNS服务器告诉了我们网站服务器的IP，即54.69.23.11。出于安全考虑，在这里我们的示例，我们是以HTTPS协议为例，所以在这里连接的端口是443。因为使用的是HTTPS协议，所以在这里会试图去获取服务器证书，接着获取到了域名相关的证书信息。

随后以“>”开始的内容，便是向Web服务器发送请求。Host即是我们要访问的主机的域名，GET / 则代表着我们要访问的是根目录，如果我们要访问 [https://www.phodal.com/about/](https://www.phodal.com/about/)页面在这里，便是GET资源文件/about。紧随其后的是HTTP的版本号（HTTP/1.1）。User-Agent通过指向的是使用者行为的软件，通常会加上硬件平台、系统软件、应用软件和用户个人偏好等等的一些信息。Accept则指的是告知服务器发送何种媒体类型。