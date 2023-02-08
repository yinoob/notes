[The Cloudflare Blog](https://blog.cloudflare.com/)

[Qualys SSL Labs](https://www.ssllabs.com/)

密码学Hash算法有很多，比如MD5算法、SHA族类算法，MD5早已被证明是不安全的Hash算法了，目前使用最广泛的Hash算法是SHA族类算法。



对称加密算法有两种类型，分别是块密码算法（block ciphers)和流密码算法（stream ciphers)。



美国国家标准与技术研究院（National Institute of Standards and Technology,NIST）对众多的对称加密算法进行了考核，从安全性和效率进行了多方面评测，最终选取Rijndael算法作为对称加密算法的标准。以Rijndael算法为原型，创建了AES（Advanced Encryption Standard）算法，AES就是最终的对称加密算法标准。



对称加密算法可以保证消息的机密性，MAC算法可以保证消息的完整性，将两者结合起来，就可以保证消息同时具备机密性和完整性。



对称加密算法虽然有很多的算法和加密机制，但主要用于加密和解密。而公开密钥算法的功能比较多，可以进行加密解密、密钥协商、数字签名。



公开密钥算法中，所有的网络通信都会存在中间人攻击，这是务必要记住的一点，在HTTPS协议中必须引入PKI技术解决身份验证的问题，PKI技术的核心就是证书。



[高级加密标准 - 维基百科，自由的百科全书 (wikipedia.org)](https://zh.wikipedia.org/wiki/高级加密标准)

[RSA加密算法 - 维基百科，自由的百科全书 (wikipedia.org)](https://zh.wikipedia.org/wiki/RSA加密演算法)

[数字签名算法 - 维基百科，自由的百科全书 (wikipedia.org)](https://zh.wikipedia.org/zh-hans/数字签名算法)



首先明确一点，PKI技术不是TLS/SSL协议的一部分，但是在HTTPS中，必须引入PKI技术才能保证安全。简单地说，PKI技术能够确保客户端接收到的服务器公钥（比如www.example.com网站的公钥）确实是www.example.com网站的公钥。

[5分钟让你知道什么是PKI - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/30136885)

[深入浅出 HTTPS：从原理到实战-虞卫东-微信读书 (qq.com)](https://weread.qq.com/web/bookDetail/a5532800716ce830a55b317)