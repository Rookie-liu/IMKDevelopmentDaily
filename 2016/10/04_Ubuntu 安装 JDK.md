**注意! 本文部分内容的可用性, 有待进一步核实!**

# 安装
## SunJDK/OracleJDK (版本号可以换)
``` bash
sudo add-apt-repository ppa:webupd8team/java
sudo apt update
sudo apt install oracle-java8-installer

# 这句话 貌似可以 自动同意 安装协议, 可选
# echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | sudo /usr/bin/debconf-set-selections
```

- 配置环境变量 (可选)
  - 查看 已安装的版本 (还会包括 `OpenJDK`)  
  `update-java-alternatives -l`
  - 设置成 默认版本  
  `sudo apt-get install oracle-java8-set-default`
  - 切换成 其他版本 (前提是得安装吧)  
  `sudo update-java-alternatives -s java-7-oracle`

## OpenJDK (版本号可以换)
``` bash
sudo add-apt-repository ppa:openjdk-r/ppa
sudo apt-get update
sudo apt-get install openjdk-8-jdk
```

- Ubuntu 16.xx 安装 OpenJDK 7  
http://askubuntu.com/a/803616/626522

- 配置环境变量
参考: 
- http://askubuntu.com/questions/464755/how-to-install-openjdk-8-on-14-04-lts
- [SunJDK/OracleJDK (版本号可以换)](https://github.com/imknown/IMKDevelopmentDaily/blob/master/2016/10/04_Ubuntu%20%E5%AE%89%E8%A3%85%20JDK.md#sunjdkoraclejdk-版本号可以换)
  
## 官网下载(适合自己折腾)
http://www.oracle.com/technetwork/java/javase/downloads/index.html  

- 配置环境变量  
https://github.com/imknown/IMKDevelopmentDaily/blob/master/2016/10/14_Ubuntu%2016%20配置%20ADB%20环境变量.md#手动方式

最下面加入
``` bash
export JAVA_HOME="/your_unzip_location"
export PATH=$JAVA_HOME/bin:$PATH
```

如果 配置不生效,  
先用 `sudo update-alternatives --config java` 查看安装情况.  
再用 `sudo update-alternatives --display java` 查看版本优先级, 找一个 更高的数字,  
例如 现在是 `665`, 那就写 `666` 就可以了.  
最后用 `sudo update-alternatives --install /usr/bin/java java your_unzip_location/bin/java 666` 替换.  
失败的话, 尝试 `注销` 或者 `重启` 后重试.

# 验证是否配置成功
先刷新环境变:  
https://github.com/imknown/IMKDevelopmentDaily/blob/master/2016/10/14_Ubuntu%2016%20配置%20ADB%20环境变量.md#刷新生效

然后执行:
``` bash
echo $JAVA_HOME
echo $PATH
java -version
javac -version
```

# 卸载 (参考)
``` bash
# openjdk
sudo apt purge openjdk*

# oracle jdk
sudo rm /var/lib/dpkg/info/oracle-java8-installer*
sudo apt purge oracle-java8-installer*
sudo rm /etc/apt/sources.list.d/*java*
sudo apt update
```

# 参考
- http://wiki.ubuntu.org.cn/Java  
- http://blog.sina.com.cn/s/blog_53a99cf30102v6o4.html  
