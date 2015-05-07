# logger
logger -p local1.notice -t 'dir' ‘content’

之前在代码里看到有这样记log的命令,学习了下~~~~

logger [-isd] [-f file] [-p pri] [-t tag] [-u socket] [message ...]

-i 逐行记录每一次logger的进程ID.
-s 记录消息到标准错误, 包括系统日志.
-f file 记录特定的文件.
-p pri 输入消息的特定优先级. 优先级可以是自定义的数值或者诸如 ``facility.level'' 的格式.

可用的facility名有: auth, authpriv (for security information of a
sensitive nature), cron, daemon, ftp, kern, lpr, mail, news, security
(deprecated synonym for auth), syslog, user, uucp, and local0 to local7,
inclusive.

可用的level名用: alert, crit, debug, emerg, err, error (deprecated
synonym for err), info, notice, panic (deprecated synonym for emerg),
warning, warn (deprecated synonym for warning).

举例：logger -p local3.info'' local3 facility这个设备的消息级别为info. 默认是 ``user.notice.''

-t tag 打上特定的标志.
-u sock 以特定的socket代替内嵌系统常规工作
-d 使用一个数据进程代替一个流连接到这个socket.
-- 结束参数列表. 这个允许消息以一个“-”开始
message 写入log文件的内容消息，可以与-f配合使用

logger 以0退出表示成功, 大于0表示失败.

[root@yanyuping ~]# vim /etc/rsyslog.conf #在Centos6之前的版本这个文件对应的应该是/etc/syslog.conf,对应的进程为syslogd
修改这一行：增加local3.none,表示local3上的任何消息都不记录到/var/log/messages 中
复制代码代码示例:
*.info;mail.none;authpriv.none;cron.none;local3.none /var/log/messages


增加这一行：意思是来自local3的所有消息都记录到/var/log/my_test.log ,前面加个“-”,说明要启用写入缓冲
复制代码代码示例:
local3.* -/var/log/my_test.log

[root@yanyuping ~]# service rsyslog restart
Shutting down system logger: [ OK ]
Starting system logger: [ OK ]

[root@yanyuping ~]# cat my_test.sh
 
复制代码代码示例:
#/bin/bash
#some other scripts goes here …
logger -i -t my_test.sh -p local3.notice ” my_test.sh find some error in …”
echo “Hello world”
 
[root@yanyuping~]# bash my_test.sh
Hello world
[root@yanyuping ~]# cat /var/log/my_test.log
Aug 14 23:15:19 localhost my_test.sh[31996]: my_test.sh find some error in …
Aug 14 23:32:41 localhost my_test.sh[32096]: my_test.sh find some error in …
