## 1.利用ipconfig /all获取路由器ip（默认网关）

## 2.首先保证你的电脑可以ping通你的路由器，然后在路由器管理页面系统管理-服务内开启ssh

## 3.打开putty，填写路由器ip，端口默认22，ssh，确认
弹出安全警告选择确认，登陆即可

## 4.执行以下命令（一行）
wget -O- （订阅地址） | bash && echo -e "\n0 */3 * * * wget -O- （订阅地址） | bash\n">> /etc/storage/cron/crontabs/admin && killall crond && crond

## 事实上，在路由器管理页面ss功能内直接配置也可以
