## Phobos
Phobos勒索软件家族与2016年出现的CrySIS/Dharma勒索软件家族所使用的加密方式、部分代码段、勒索信外观与内容，以及用于加密文件的命名方式都较为相似。

但不排除为同一作者或Phobos勒索软件攻击者购买、利用CrySIS/Dharma勒索软件相关代码的情况

**加密流程和特征**
- 使用RC4算法解密出RSA公钥
- 使用RDTST读取CPU启动时间周期，使用RSA公钥的SHA1对获得的时间随机数进行更新得到256位AES密钥，用于加密文件
- 结合CPU启动周期得到16字节随机数，结合RSA公钥的SHA1对此值进行更新，得到随机的AES IV，用于加密文件
- 使用2和3中得到的密钥和IV对文件进行加密
- 使用硬编码RSA公钥加密步骤2中得到的AES密钥，将此加密后的结果和步骤3中生成的IV写入被加密文件

**变种后缀**
```
    .phobos;.phobos;.help;.deal;.Caleb;.wiki;.dewar;devil;Devos;.eight;.eking;
```

[其他变种](https://bbs.360.cn/thread-15781213-1-1.html)

黑客邮箱：`weberkristofer@aol.com`
被加密文件后缀：`.JDM`

黑客邮箱：`decrptsupp@keemail.me`
被加密文件后缀:`.Banta`

黑客邮箱：`churiladr@cock.li`
被加密文件后缀：`.adage`

黑客邮箱：`devie.e@aol.com`
被加密文件后缀：`acton`

黑客邮箱/Url：`saveisos@aol.com`
被加密文件后缀:`isos`

黑客邮箱/Url：`WTF2000@cock.li`
被加密文件后缀: `actin`

黑客邮箱：`bowen.bord@aol.com`
被加密文件后缀:`.phoenix`

黑客邮箱：`decrypt@files.mn`
被加密文件后缀:`.Banks`

黑客邮箱：`beautydonkey@protonmail.com`
被加密文件后缀:`.bitdonkey`

黑客邮箱: `support@qbmail.biz`
被加密文件后缀：`.nqix`

黑客邮箱：`lockhelp@qq.com`
被加密文件后缀：`.acute`

黑客邮箱:`horsesecret@xmpp.jp`
被加密文件后缀：`.horseliker`

黑客邮箱：`recovermyfiles2019@thesecure.biz`
被加密文件后缀：`.Adme`

黑客邮箱：`panindogliker@protonmail.com`
被加密文件后缀：`.PISCA`



**勒索信息**

![](./勒索信息/Phobos病毒.png)

**是否可解**
```
    综上除非知道RSA私钥，否则在正常情况下无法解密
```


**其他防护建议**
- 多台机器，不要使用相同的账号和口令
- 登录口令要有足够的长度和复杂性，并定期更换登录口令
- 重要资料的共享文件夹应设置访问权限控制，并进行定期备份
- 定期检测系统和软件中的安全漏洞，及时打上补丁。
- 定期到服务器检查是否存在异常。查看范围包括：
    a)是否有新增账户
    b) Guest是否被启用
    c) Windows系统日志是否存在异常
    d)杀毒软件是否存在异常拦截情况
- 安装安全防护软件，并确保其正常运行。
- 从正规渠道下载安装软件。
- 对不熟悉的软件，如果已经被杀毒软件拦截查杀，不要添加信任继续运行。