### 约定
将 『具有完整计算机功能并带有多个ethernet网口的微型机』 简称为 『op设备』<br/>
将『以太网线』简称为『网线』

### 初始配置op设备：
第一阶段：使用键盘鼠标显示器连接op设备。这个阶段的任务是通过U盘启动，刷openwrt系统到op设备<br/>
第二阶段：用网线连接电脑和op设备的eth0口，然后登录192.168.2.1（LAN口静态ip，在/etc/config/network设置，见图1），现在就可以进入openwrt的管理界面。同时用网线连接光猫和op设备eth1口。在openwrt的管理界面就可以配置WAN口的上网方式（PPPoE或者自动获取ip等），配置好后，就可以上网了<br/>
第三阶段：使用网线连接路由器的LAN口，进入路由器的管理界面，将路由器改为AP模式，作用是将路由器变二层设备。然后按照 路由器 --- 网线 --- op设备 eth2 连线。此时就可以将连接电脑和op设备的网线拔掉，然后使用wifi上网。同时因为路由器现在只是二层设备，因此依然可以通过192.168.2.1进到op设备的管理界面<br/>

### op设备配置完成后的拓扑
使用的op设备一共有4个网口，eth0 ~ eth3, 其中 eth1 设置为 wan 口，其余三个设置为 lan 口并设置了桥接（可以理解为绑定为一个逻辑LAN口）。<br/>
连线拓扑是：<br/>
光猫 --- 网线 --- op设备 eth1<br/>
路由器 --- 网线 --- op设备 eth2<br/>
路由器设置为了AP模式（变为二层设备，相当于所有接口都是LAN口，并且所有通过wifi连接路由器的设备也是属于同一个二层网络）<br/>

### op设备配置
op设备的管理界面是192.168.2.1，这个地址是在/etc/config/network设置的（图1）。路由器的管理界面ip是op设备给他分配的ip地址。（路由模式或者强改的ap模式后台管理地址都是独立的，ap模式，中继模式，桥接模式是看上级分配的ip地址进）

<p align="center">
  <img src="https://github.com/405028157/Notebook/blob/main/imgs/network_config.png">
</p>
<p align="center">图1</p>

### 固件
使用saka大佬编译的固件：[Zheaoli/Auto-OpenWrt](https://github.com/Zheaoli/Auto-OpenWrt)
