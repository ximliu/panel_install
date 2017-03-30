centos 6 定时脚本
-----------------------------------------------
yum -y install vixie-cron crontabs
rm -rf /var/spool/cron/root
echo 'SHELL=/bin/bash' >> /var/spool/cron/root
echo 'PATH=/sbin:/bin:/usr/sbin:/usr/bin' >> /var/spool/cron/root
echo '0 */12 * * * reboot' >> /var/spool/cron/root
/sbin/service crond restart
-----------------------------------------------
说明：
vixie-cron软件包是cron的主程序；
crontabs软件包是用来安装、卸装、或列举用来驱动 cron 守护进程的表格的程序。
//+++++++++++++++++++++++++++++++++++
cron 是linux的内置服务，但它不自动起来，可以用以下的方法启动、关闭这个服务：
/sbin/service crond start //启动服务
/sbin/service crond stop //关闭服务
/sbin/service crond restart //重启服务
/sbin/service crond reload //重新载入配置
查看crontab服务状态：service crond status
手动启动crontab服务：service crond start
查看crontab服务是否已设置为开机启动，执行命令：ntsysv
没有就加入开机自动启动:免得每次手动启动麻烦：chkconfig --level 35 crond on

加入
测试
echo '*/1 * * * * /etc/init.d/shadowsocks status > /root/sslog.txt' >> /var/spool/cron/root
rm /var/spool/cron/root
echo '0 */12 * * * reboot' >> /var/spool/cron/root

查看内容
cat /var/spool/cron/root
crontab -l
