# ubuntu操作
Linux命令  

```shell
# 切换用户
su xxx
# 退出当前用户
exit
# 切换目录
cd
# 查看目录
ls
# 查看操作系统版本
uname -a
```
## 当前用户
whoami

## sudo
管理员权限命令

- sudo apt-get update 读取软件仓库的所有源列表，然后保存在本机。方便本机用户检索、对比。
- sudo apt-get install docker.io  [安装docker](https://zhuanlan.zhihu.com/p/90474818)
- sudo docker version 查看docker安装版本
- sudo systemctl start docker 启动docker服务
- netstat


## 查询端口占用
https://www.runoob.com/w3cnote/linux-check-port-usage.html
## lsof
```
lsof -i:端口号
```
更多 lsof 的命令如下
```
lsof -i:8080：查看8080端口占用
lsof abc.txt：显示开启文件abc.txt的进程
lsof -c abc：显示abc进程现在打开的文件
lsof -c -p 1234：列出进程号为1234的进程所打开的文件
lsof -g gid：显示归属gid的进程情况
lsof +d /usr/local/：显示目录下被进程开启的文件
lsof +D /usr/local/：同上，但是会搜索目录下的目录，时间较长
lsof -d 4：显示使用fd为4的进程
lsof -i -U：显示所有打开的端口和UNIX domain文件
```

## netstat
```
netstat -tunlp | grep 端口号
```

## kill进程
```sh
#在查到端口占用的进程后，如果你要杀掉对应的进程可以使用 kill 命令：

kill -9 PID
#如上实例，我们看到 8000 端口对应的 PID 为 26993，使用以下命令杀死进程：

kill -9 26993
```