# **Linux常用操作**

## ssh连接
	ssh <用户名>@<IP> [-p <端口>]  (回车后输入密码)
	例: ssh root@192.0.0.1:20
#### 检查目标服务器网络是否通畅
	ping <ip> [-c <链接次数>] [-i <间隔时间，单位秒>]
---

## scp传输
	1. 当前传至目标服务器：scp [-P 端口号] [-r 传文件夹加此参数] <当前服务器需传输文件目录>  <用户名>@<IP>:/<目标服务器储存文件目录> 
	例: scp ./1.txt root@172.0.0.1:/home/work/nltk_data/
	2. 从目标服务器下载至当前：scp [-P 端口号] [-r 传文件夹加此参数] <用户名>@<IP>:/<目标服务器下载文件目录> <当前服务器需储存文件目录>
	例: scp -r root@172.0.0.1:/home/work/nltk_data/ ./
---

## 基础操作
### 切换目录
	1.指定目录 cd <目录>
	2.当前用户根目录 cd
	3.返回上一级目录 cd ..
### 查看
	ls [-a 全部文件，包括隐藏] [-l 查看详细信息]
更多属性 > https://www.runoob.com/linux/linux-comm-ls.html
### 查看当前路径
	pwd [-P 显示出确实的路径，而非使用link路径]
---

## 用户管理
### 创建用户
	adduser [-g <用户组> 该参数用户指定用户组] [-d <路径> 指定home目录] <用户名>
### 切换用户
	su <用户名>
### 权限管理
#### 用户组
	chown <属主名>[: <属组名>] <文件名>
#### 用户
	chmod 777 <文件名> (给所有用户组/用户读、写、执行权限)
---

## 文档操作
### 查看文档
	1. 从第一行开始查看: cat <文件路径>
	2. 从最后一行开始查看: tac <文件路径>
	3. 查看头部: head [-n <行数>] <文件路径>
	4. 查看尾部: tail [-n <行数>] <文件路径>
---

## vi/vim
	打开查看: vi/vim <文件路径>
	进入输入模式: i
	退出输入模式: esc
### 查找字符串
	/<string>
### 返回上一步操作
	u
### 替换字符串
	: + <% 替换所有，否者替换当前行，也可x,y指定x至y行>s/<替换string>/<需替换string>[/g 替换所有匹配，否则替换第一个]
### 跳转
	1. 跳转文件头: gg
	2. 跳转文件尾: G
	3. 跳转当前页头: H
	4. 跳转当前页尾: L
	5. 光标移动当前行头: 
	6. 光标移动当前行尾: 
### 删除
	1. 删除当前行: dd
	2. 删除x至y些行: : + <x,y> + 空格 + d + 回车
	3. 清空: : + %d + 回车
### 保存/退出
	1. 保存文件: : + w + 回车
	2. 退出: : + q + 回车
	3. 强制退出: : + q! + 回车
	4. 保存并退出: : + wq + 回车
---

## 文件操作
### 创建
	1.文件夹: mkdir <路径/名称>
### 复制
	cp [-r 文件夹带此参数] <文件/文件夹路径> <复制到的路径>
### 移动
	mv <文件/文件夹路径> <移动到的路径>
### 删除
	rm [-r 文件夹带此参数] <文件/文件夹路径>
---

## 防火墙
### 端口
	1. 查看端口占用情况: netstat -anp |grep <端口号>
	2. 开放端口: firewall-cmd --zone=public --add-port=<端口号>/tcp --permanent
	3. 关闭端口: firewall-cmd --zone=public --remove-port=<端口号>/tcp --permanent 
	(2,3执行后 需执行firewall-cmd --reload  使配置生效)
	4. 查看防火墙所有开放的端口:
	5. 查看监听的端口: netstat -lnpt
---

## 常用下载安装
### wget
	wget [-b 后台下载] <下载链接>
### yum
	1. 安装依赖包: yum install <package_name>
	2. 更新依赖包: yum update <package_name>
	3. 列出所有可安裝的软件清单命令: yum list
	4. 删除软件包命令: yum remove <package_name>
	5. 查找软件包命令: yum search <keyword>
#### 配置本地镜像

### apt
	1. 安装依赖包: sudo apt install <package_name>
	2. 更新依赖包: sudo apt update <package_name>
	3. 列出所有可安裝的软件清单命令: apt list --installed
	4. 删除软件包命令: sudo apt remove <package_name>
	5. 查找软件包命令: sudo apt search <keyword>
### brew(macos)
---

## GPU操作
### 查看GPU使用情况
	1. 查看当前状态：nvidia-smi
	2. 每X秒刷新：nvidia-smi -l <秒数>
---

## 任务查看/退出
### 任务查看
	1.查看当前用户下所有： ps -u
	2.根据名称查看： ps -ef|grep <名称>
### 任务退出
	1.结束单个任务 kill -9 <pid>
---

## Shell脚本
### 执行
	bash <脚本路径>
---

## Conda操作
### 查看版本
	conda --version
### 创建环境
	conda create --name <your_env_name> [python=X.X 指定版本]
### 查看环境列表
	conda info --envs
	或 conda env list
### 激活环境
	conda activate <环境名>
### 退出环境
	deactivate
### 删除环境
	conda remove --name <your_env_name> --all
---

## 后台启动
### Screen
	1. 创建窗口: screen -S <窗口名>
	2. 进入窗口: screen -r <窗口名/PID>
	3. 关闭窗口: screen -X -S <窗口名>
	4. 查看所有窗口列表: screen -ls
	5. 退出当前窗口: Ctrl + a + d
	6. 杀死当前窗口: Ctrl + a + k
### nohup
	1. 后台运行: nohup <command> >> <输出的log路径> 2>&1 &
	2. 查看后台运行程序: jobs -l
