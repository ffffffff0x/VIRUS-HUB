## Sodinokibi
Sodinokibi勒索病毒在国内首次被发现于2019年4月份,2019年5月24日首次在意大利被发现，
使用了RDP攻击的方式进行传播感染，这款病毒被称为GandCrab勒索病毒的接班人，

**加密流程和特征**
- 生成一组密钥对，公钥直接存储在注册表中
- 使用攻击者在配置文件中的公钥加密1中生成的私钥，并将其存储在注册表中
- 使用软件的硬编码公钥加密1中生成的私钥，并将其存储在注册表中
- 针对每个文件使用基于1中公钥生成的Salsa20流密码加密文件
- 主动清理内存，防止RAM扫描


**传播渠道**
Sodinokibi勒索病毒，又被称作a.k.a Revil和“小蓝屏”，该勒索病毒于2019年4月底首次出现，从2019年4月份到2019年11月份目前所发现的主要有以下几个渠道：
- Web漏洞，曾利用 Oracle WebLogic漏洞中编号为CVE-2019-2725的漏洞。
- 带有链接或附件的恶意垃圾邮件或网络钓鱼活动。
- 使用RIG 漏洞利用工具包传播。
- 通过暴力破解获取到远程桌面的密码后手动投毒。并由被攻陷机器作为跳板攻击内网其它机器。


**变种后缀**
```
    随机后缀
```

**勒索信息**

![](./勒索信息/Sodinokibi勒索.png)

**是否可解**
```
    按照技术手段来说无法解密，网络上报道出售的解密工具很可能包含了作者的RSA的私钥，但是根据网络消息，该工具已经出售但并未公开。
```