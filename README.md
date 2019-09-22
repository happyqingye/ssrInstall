1、安装
shadowsocks的部署分客户端和服务器端，我们通过ssh在远程服务器上部署服务端。方便起见使用teddysun提供的一键部署方案。
1	wget --no-check-certificate https://raw.githubusercontent.com/happyqingye/ssrInstall/master/shadowsocks.sh
2	chmod +x shadowsocks.sh
3	./shadowsocks.sh 2>&1 | tee shadowsocks.log

2、按提示输入密码和算法
Congratulations, Shadowsocks-python server install completed!
Your Server IP        :  140.82.43.232
Your Server Port      :  9086 
Your Password         :  5tgb%^&* 
Your Encryption Method:  aes-256-gcm 
3、使用命令
启动：/etc/init.d/shadowsocks start 
停止：/etc/init.d/shadowsocks stop 
重启：/etc/init.d/shadowsocks restart 
状态：/etc/init.d/shadowsocks status
配置文件路径：/etc/shadowsocks.json 
日志文件路径：/var/log/shadowsocks.log
 代码安装目录：/usr/local/shadowsocks
4、多用户配置示例
vi /etc/shadowsocks.json
{
    "server":"0.0.0.0",
    "local_address":"127.0.0.1",
    "local_port":1080,
    "port_password":{
       "9080":"5tgb%^&*",
       "9086":"6yhn%^&*"
    },
    "timeout":300,
    "method":"aes-256-gcm",
    "fast_open":false
}

5、设置防火墙
Vultr控制台防火墙有时不好使，还是原生配置吧
1	firewall-cmd --zone=public --add-port=80/tcp --permanent # 开80端口
2	
3	firewall-cmd --zone=public --add-port=1433/tcp --permanent # 开23333 TCP端口
4	
5	firewall-cmd --zone=public --add-port=1433/udp --permanent # 开23333 UDP端口
	
	firewall-cmd --reload  # 重载配置
	iptables -L -n  # 查询防火墙规则
*到这里vpn就已经配通了
