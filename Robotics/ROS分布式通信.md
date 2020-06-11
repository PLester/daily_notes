# Robotics

## ROS分布式通信
### 1. 设置IP 和 .bashrc
    通过一台无线路由器组建局域网，主机和从机均连接此网络 
1. 确认系统IP地址： ```$ ifconfig```  \
技巧：\
有线网络，etho  部分  inet addr 是 IP 地址；\
无线网络，wlan0 部分的 inet addr 是 IP 地址。

2. 确认hostname：```$ hostname```

### 2. 修改hosts文件内容
```$ sudo gedit /etc/hosts```

    例子：
    A电脑(主机)
    127.0.0.1     localhost
    127.0.1.1     hostname_A

    IP_A          hostname_A
    IP_B          hostname_B

    B电脑(从机)
    127.0.0.1     localhost
    127.0.1.1     hostname_B

    IP_B          hostname_B
    IP_A          hostname_A

技巧：
可以ping一下看看是否连通(在主机)：```$ ping hostnameB```

### 3. 修改.bashrc文件
在主机中添加如下命令：
```
export ROS_HOSTNAME=hostname_A
export ROS_MASTER_URI=http://hostname_A:11311
```
在从机中添加如下命令：
```
export ROS_HOSTNAME=hostname_B
export ROS_MASTER_URI=http://hostname_A:11311
```


### 测试
主机A:
```
$ roscore
$ rosrun turtlesim turtlesim_node
```
从机B:
```
$ rosrun turtlesim turtle_teleop_key
```
