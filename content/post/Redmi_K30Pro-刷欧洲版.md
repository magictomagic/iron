---
title: "Redmi_K30Pro-刷欧洲版"
date: 2020-08-21T01:37:56+08:00
lastmod: 2020-08-21T01:37:56+08:00
draft: false
tags: ["搞机", "刷机"]
categories: [ "notes"]
author: "magictomagic"
contentCopyright: '<a rel="license noopener" href="https://en.wikipedia.org/wiki/Wikipedia:Text_of_Creative_Commons_Attribution-ShareAlike_3.0_Unported_License" target="_blank">Creative Commons Attribution-ShareAlike License</a>'
---

# 效果
![](/img/Screenshot_2020-08-21-06-02-31-659_com.miui.home.jpg)
![](/img/Screenshot_2020-08-21-06-02-19-044_com.miui.home.jpg)
![](/img/Screenshot_2020-08-21-07-14-29-368_com.miui.home.jpg)

# 刷机流程
## Unlock BL 锁
去[官网][3]下载工具，小米账号需要绑定手机号 24 小时后才有刷机权限，登录，解锁。
## 下载 ADB
[点击下载][6]，然后添加环境变量，ADB能用就行。
## 下载 TWRP（选择你手机版本的TWRP）
到[最正宗的地方][5]下载需要的版本，

然后，转载[这篇博文][1]:
进入设置→更多设置→开发者选项开启USB调试后，用传输线连接电脑，手机会询问USB用途，请选传输档。
打开windows系统或附属应用程式的命令提示字元（cmd），跟着输入以下命令重启手机到Bootloader。（萤幕显示是米兔修理安卓机器人）
adb reboot bootloader

重启至Bootloader后，继续输入命令：
fastboot devices -l

如果看到以下提示，证明手机与电脑连接正常，按任意键正式开始导入，否则请检查驱动是否正确安装，手机是否正确连接导入recovery时，请一定保证手机和电脑的连接正常

e5435c2d7d62 fastboot
↑↑↑↑↑↑↑
每只手机的号码不一样

接着为方便操作，请将刚刚下载好的TWRP档案重命名为twrp.img，依次输入下列两条命令：
fastboot flash recovery twrp.img

是否看见类似以下提示，是的话请执行下一步

＝ ＝＝＝＝＝＝＝＝＝＝

sending 'recovery' (XXXX KB)...
OKAY [ 0.500s]
writing 'recovery'...
OKAY [ 0.560s]
finished. total time: 2.455s

＝＝＝＝＝＝＝＝＝＝＝

fastboot boot twrp.img

如看见类似如下提示，正常您的手机已经重新启动，进入TWRP

＝＝＝＝＝＝＝＝＝＝＝

downloading 'twrp.img'. ..
OKAY [ 0.838s]
booting...
OKAY [ 0.025s]
finished. total time: 0.864s

＝＝＝＝＝＝＝＝＝＝＝
## 下载欧版 MIUI12（选择你手机对应版本的ROM）
还是到[最正宗的地方][7]下载需要的版本，去那里慢慢找，要找到文件名和之前成功的 TWRP 一样的 .zip 包。给个例子：
![](../img/Snipaste_2020-08-21_09-13-53.png)

然后，还是转载[这篇博文][1]:
进入TWRP时，会问你密码解密用户，选取消然后请滑动滑块，确认允许修改system分区，进入TWRP后，依次进入清除→格式化Data分区→输入yes格式化；返回上一层功能表，进入高级清除选项，勾选Dalvik/ART Cache，Cache，并滑动滑块确认清除。返回TWRP首页，依次进入重启→Recovery。
如果这时候您选错，重新启动系统，刚刚刷入的第三方Recovery会被覆盖。
请您再重新执行步骤四，刷入TWRP 重启进入TWRP首页后，再把手机连接电脑，将下好的卡刷包rom(zip档案)复制放进手机内部目录。然后选择安装→选择您的rom…点右下角的刷入Image镜像等候重新开机就完成了。

**插入一下我的总结教训：数字签名验证可以不勾选，但之后如果遇到“E3004: This package is for device: ......; this device is .......”这种错误，千万不要到，不要到，不要到 .zip 中的 META-INF/com/google/android/目录，找到 updater-script 里删去第一行机型验证的脚本，而是要仔细看看你的 .zip 包是否找错了，下错了，我之前删去脚本刷机后，手机就砖了。去了维修店里用专用的线才刷回来，维修人员跟我说这种线外面买不到，即使买到了也没有他这里的好，这种线整个店里只有一根。我估计这种线是直接刷9008端口的。而且他们的刷机包和软件都是专用的，傻瓜式操作，可惜刷机包都是大陆包，而且格式和官网下载的非常不一样**

以下为twrp团队建议的步骤
↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓ ↓↓↓↓↓↓↓↓
TWRP Recovery Zip DOWNLOAD or TWRP.ME
1.FORMAT /data partition (NEVER wipe System or Persist!)
2.Copy our ROM to the internal storage
3.Install our ROM
4.Reboot
done
↑↑ ↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑

**放一下[官网链接][4], TWRP，MIUI12 与刷机的步骤都可以去[官网][4]找。**
## 初始设置
因为是欧洲版，初始设置需要连接外网，如果在大陆，就需要无线网翻墙了。经过搜索与思考，我总结了几个方法。详述我成功的方法。
#### 出国
难。
#### 买国外电话卡
贵。
#### 路由器翻墙
需要智能路由器，还要租机场或节点，比较麻烦。
#### SSTap + Connectify Hotspot
使用 ss/ssr 翻墙的可以参考[这篇博文][8]。总之，开了全局再开 Connectify Hotspot.

个人不推荐 ss/ssr, 因为自己搭建容易被封，大平台贵，小平台不放心，免费的浪费时间。

Connectify Hotspot 是个好东西，我电脑本来开不了热点，但用了它以后就可以开了，如用它来实现 热点/WIFI 翻墙，注意要把流量开到全局。好处是比如之前你只买的翻墙账号只支持一个设备，用了它之后一个宿舍的人都可以连你的 WIFI 翻墙了，遗憾的是 Connectify Hotspot 太贵了，不过可以试用，时间足够把手机的初始设置好了。
#### 可能可行的方法
> 未尝试，搬运网上的。

到检查更新那一步时，按一下返回键，然后长按电源键，在电源菜单中，选择飞行模式，然后就可以跳过检查更新了。
#### 我的解决办法
我买的 VPN 是 LetsVpn，感觉它工作得更底层，在 Pycharm 下载国外包时不用像 V2Ray 一样设端口，且速度也快，不过设全局加速需要铂金会员。可能是为了防止我这种 一人翻墙，全寝吃饱的操作吧。

![](../img/Snipaste_2020-08-21_05-41-36.png) ![](../img/Snipaste_2020-08-21_05-41-24.png)

然后，绑定 google 账号，一步一步走，就进去了。
## 待解决
只能通过 google play 下载应用，无法安装第三方应用。

microg, Youtube advanced 去广告。

Android install Connectify Hotspot, share 翻墙-WiFi to others.


[1]: https://www.mobile01.com/topicdetail.php?f=634&t=6124515
[2]: https://zhuanlan.zhihu.com/p/91640318
[3]: http://www.miui.com/unlock/index.html
[4]: https://xiaomi.eu/community/threads/20-8-13.57009/
[5]: https://androidfilehost.com/?w=files&flid=316048
[6]: https://dl.google.com/android/repository/platform-tools-latest-windows.zip
[7]: https://sourceforge.net/projects/xiaomi-eu-multilang-miui-roms/files/xiaomi.eu/MIUI-WEEKLY-RELEASES/20.8.13/
[8]: https://10101.io/2018/12/16/share-vpn-connection-over-w
