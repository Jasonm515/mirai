1.cnc端的mysql
账户root
密码root
2.cnc端要使用
/etc/init.d/mysql start
先开启mysql数据库才可以正常运行mirai
3.DNS端，也就是TargetA端，在changeme.com.zone的域名解析文件中，
cnc以及report都是cnc端的ip地址
4.TargetA端的nmcli con mod ens33 ipv4.dns "x.x.x.x"
指令中更改dns服务器中的ip地址为TargetA端自己的ip