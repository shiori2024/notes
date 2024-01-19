# 

## 一些Linux操作系统命令
```sh
# 查看文件和目录占用容量信息
df -h
# 查看GPU监控信息
nvidia-smi
```

## 
```py
import torch
# 查看框架版本信息
torch.__version__

# 安装依赖



# 不确定自己的代码需要执行多久结束，希望执行完成后立马关机。这类场景可以通过shutdown (最好使用命令完整路径: /usr/bin/shutdown)命令来解决。
# 假设您的程序原执行命令为
python train.py

# 那么可以在您的程序后跟上shutdown命令
python train.py; /usr/bin/shutdown      # 用;拼接意味着前边的指令不管执行成功与否，都会执行shutdown命令
python train.py && /usr/bin/shutdown    # 用&&拼接表示前边的命令执行成功后才会执行shutdown。请根据自己的需要选择
```