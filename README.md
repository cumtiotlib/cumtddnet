# 矿大哆点网络路由器自动登陆教程
>（以斐讯K2为例，版本V22.6.507.43）
## **刷机有风险，且刷且珍惜**
# 第一部分：刷入openwrt固件
## 第一步
路由器恢复出厂设置。方法：用网线连接路由器的LAN口和电脑网线插口，保证可以正常进入斐讯K2管理。（访问p .to 或者 192.168.2.1 进入）
成功恢复成功后，再次访问会出现以下的页面（不要进行设置）：

![](/imgs/1.png)
## 第二步
打开路由器刷breed_Web控制台助手v5.9版本，K2的设置如下图，检查无误，点击开始刷机即可。

![](/imgs/2.png)

如果提示Windows安全警报，如下图，点击允许即可。

![](/imgs/3.png)

可能遇到的问题：
+ 未开启telnet，打开“开启telnet”文件夹中的文件，再次尝试刷机，或者搜索“Win10打开telnet”的方法。
+ 若提示刷机失败，请更换K2固件，再次尝试。
如果没有问题的话，就会有刷机完成的提示。
## 第三步
拔掉路由器的电源，按住复位键不要松开，连接路由器电源，等待5-10秒后松开按钮，然后浏览器访问192.168.1.1就可以进入breed web恢复控制台，如下图（若打不开此页面，请重新操作第三步）

![](/imgs/4.png)

## 第四步
点击固件更新，找到openwrt-18.06.2-ramipsXXX.bin文件

![](/imgs/5.png)
![](/imgs/6.png)

点击上传

![](/imgs/7.png)

出现上面这个页面表示刷机完成，刷机完成后多等2到3分钟，即可访问第三方固件的后台。
# 第二部分：进行openwrt配置
## 一：进入openwrt后台
浏览器输入 192.168.1.1 进入openwrt后台（因为我已经装入中文支持包所以显示为中文），首次登陆密码默认为空。

![](/imgs/8.png)

## 二：连接网络（只为方便配置与软件包）
方法1、再找一根网线将WAN接口与一体化网络连接，打开 http://10.2.5.251/ 登陆账号连接网络；
方法2、按下图所示操作连接stu无线网络

![](/imgs/9.png)
![](/imgs/10.png)
![](/imgs/11.png)
![](/imgs/12.png)
![](/imgs/13.png)

成功后，打开 http://10.2.5.251/ 登陆账号连接网络；

**注：后期配置完python后台后，将此无线网连接断开（操作方法如下图，目前不需操作，K2连接stu无线网作为中转网速很慢）**

![](/imgs/14.png)

## 三：连接路由器后台
安装文件夹中的finalshell_install.exe，成功后打开此应用，

![](/imgs/15.png)
![](/imgs/16.png)

成功连接后，如下图

![](/imgs/17.png)

## 四：开启sftp，方便传输文件，
依次输入以下命令（一行一行输入，粘贴快捷键Ctrl+Shift+V）：

![](/imgs/18.png)

```
opkg update
opkg install vsftpd openssh-sftp-server
/etc/init.d/vsftpd enable
/etc/init.d/vsftpd start
```
每次执行完一个命令后，会再次出现 **root@OpenWrt:~#**

然后关闭连接，重新连接路由器，可以看到如下图所示的界面

![](/imgs/19.png)

## 五：安装python2环境
依次输入以下命令：
```
opkg install python-base
opkg install python-light
opkg install python-logging
```
注：安装过程较为缓慢，请耐心等待
安装完成后可以进入下面所示页面查看是否成功

![](/imgs/20.png)
![](/imgs/21.png)

如果显示结果如上图所示，则表明安装成功。
## 六：上传python后台。

![](/imgs/22.png)

编辑duodian2.py文件

![](/imgs/23.png)

保存后在上一步新建的py文件夹中右键点击上传，选择编辑好的py文件，上传即可。
## 七：路由器通电启动py脚本并保持后台

![](/imgs/24.png)
![](/imgs/25.png)

在此页面最下面 **exit 0** 上面加上 **python /www/py/duodian2.py** 即可。

注：前面通过stu无线网连接网络的，请将此无线网移除。
## 八：开启热点

![](/imgs/26.png)
![](/imgs/27.png)

**网络选择LAN接口**，密码设置如下图：

![](/imgs/28.png)

保存并应用，并启用热点即可。

![](/imgs/29.png)

路由器断电后，再次开启，即可享受无线网络了（启动可能较慢）。

> 编辑：[Pandalzy](https://github.com/Pandalzy) 审核：像风一样

> 加入“矿大物联数据讨论群”，了解更多大创项目信息。

> 群号：753871737

**资料仅供参考学习，请勿用于非法用途或者盈利，违者责任自负**
