# 记一次linux被挖矿
1. 服务器一直卡顿，但是通过`top`命令查看不到高消耗cpu的进程
2. 通过命令`vim /etc/ld.so.preload`查看是否有被屏蔽的进程
> `/etc/ld.so.preload`文件中的命令可以将`top`命令下的进程屏蔽
3. 在步骤【2】中查看到被屏蔽的进程，将内容清空既可以在`top`命令中看到对应的高消耗进程
4. 通过`ps -ef | grep pid`查看的到具体的执行命令，将对应的执行文件删除掉，发现过一会重复出现
5. `kill -9 pid`掉进程后，过一会服务器又卡顿
6. 查看服务器的定时器`vim /etc/crontab`，发现有定时任务，里边的定时器就是病毒的定时任务，将该定时任务删除掉即可
7. 查看防火墙状态`systemctl  status firewall.service`
8. 开启防火墙`systemctl restart firewalld.service`
> 查了资料，大部分建议关闭redis对外开放端口，可以将redis对外端口关闭
