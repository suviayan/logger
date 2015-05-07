# logger
logger -p local1.notice -t 'dir' ‘content’

之前在代码里看到有这样记log的命令,学习了下~~~~

logger [-isd] [-f file] [-p pri] [-t tag] [-u socket] [message ...]

-i 逐行记录每一次logger的进程ID.
-s 记录消息到标准错误, 包括系统日志.
-f file 记录特定的文件.
-p pri 输入消息的特定优先级. 优先级可以是自定义的数值或者诸如 ``facility.level'' 的格式.

可用的facility名有:
auth, authpriv (for security information of a
sensitive nature), cron, daemon, ftp, kern, lpr, mail, news, security
(deprecated synonym for auth), syslog, user, uucp, and local0 to local7,
inclusive.

可用的level名用: 
alert, crit, debug, emerg, err, error (deprecated
synonym for err), info, notice, panic (deprecated synonym for emerg),
warning, warn (deprecated synonym for warning).

具体的示例，请查看example分支


