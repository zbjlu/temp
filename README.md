# temp

vscode:

GitHub Gist: 5f9cb7fb115c2f9283a0667c79c4d26a

ubuntu tools:

http://wps-community.org/download.html


个人所得税：

若当月没能获取到的专项附加扣除金额,可在第二个月累计计算
扣除。
请大家填写时务必谨慎,根据税务机关目前的通知,专项附加扣
除的扣除方式等信息一旦提交后在一个纳税年度内不能变更。
国家税务总局官网有关个人所得税法实施条例及专项附加扣除
暂行办法的专栏链接中包含了相关政策文件/培训辅导/热点问答/个
税 APP,供大家参考。
http://www.chinatax.gov.cn/n810219/n810744/n3752930/index.html
如填写中有任何问题,可直接拨打 12366 纳税服务热线或当地
税务机关办税服务厅咨询


++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++


repeater apps:

https://unisoc.github.io/demos/wifi_repeater/



+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Great!

From: Zhang, Stephen (张斌) 
Sent: Thursday, January 24, 2019 3:36 PM
To: Zhang, Keguang (张可光) <keguang.zhang@unisoc.com>
Subject: RE: SmartRepeater新需求


So easy! 有时间我用最新12月google发布的flutter hybird替换这个native app,用html5写 ，那样不仅界面更炫，而且将界面跟业务逻辑分离，以后修改交互界面就只需要改html5文件就可以了，不会影响到业务逻辑


From: Zhang, Keguang (张可光) 
Sent: Thursday, January 24, 2019 3:32 PM
To: Zhang, Stephen (张斌)
Subject: FW: SmartRepeater新需求



From: Zhang, Keguang (张可光) 
Sent: Tuesday, January 22, 2019 2:25 PM
To: Zhu, Clay (朱咸刚) <clay.zhu@unisoc.com>; Yu, Ivan (余琰知) <Ivan.Yu@unisoc.com>
Cc: Chen, Steven (陈龙) <steven.chen@unisoc.com>; Zhou, Ling (周灵) <ling.zhou@unisoc.com>; Wei, Bub (魏雪波) <Bub.Wei@unisoc.com>; Xiang, Dong (向东) <dong.xiang@unisoc.com>; Zhu, Gui (祝贵) <Gui.Zhu@unisoc.com>
Subject: Re: SmartRepeater新需求

Hi Clay, Ling,
更新一下autorun部分:
一.3.    在STA栏中增加autorun按钮和时间输入框(类型为int, 单位为秒), 具体请参考二.1.e
一.8.    在AP栏中增加autorun按钮和时间输入框(类型为int, 单位为秒), 具体请参考二.2.g

二.1.e. 当autorun为正数时, 显示ENABLE AUTORUN按钮和DISABLE AUTORUN按钮, 输入框显示之前调用.get_conf获得的autorun的时间值；
           当autorun为负数时, 显示ENABLE AUTORUN按钮和DISABLE AUTORUN按钮, 输入框显示空；
           当填写时间值n后,点击ENABLE AUTORUN按钮时调用.set_conf(WIFIMGR_IFACE_NAME_STA, ..., n);
           当点击DISABLE AUTORUN按钮时调用.set_conf(WIFIMGR_IFACE_NAME_STA, ..., -1);

二.2.g. 当autorun为正数时, 显示ENABLE AUTORUN按钮和DISABLE AUTORUN按钮, 输入框显示之前调用.get_conf获得的autorun的时间值；
           当autorun为负数时, 显示ENABLE AUTORUN按钮和DISABLE AUTORUN按钮, 输入框显示空；
           当填写时间值n后,点击ENABLE AUTORUN按钮时调用.set_conf(WIFIMGR_IFACE_NAME_AP, ..., n);
           当点击DISABLE AUTORUN按钮时调用.set_conf(WIFIMGR_IFACE_NAME_AP, ..., -1);
Best regards,

Keguang Zhang
On 2019年01月17日 14:29, Zhang, Keguang (张可光) wrote:
Hi Clay, Ling,
补充一下, 下面两条中的channel不用获取和显示了.
    二.1.d. 当为Connected状态时, 在状态栏显示已连接的Router的SSID, BSSID, channel, security, 并显示CLOSE, SCAN, DISCONNECT按钮,
    二.2.b. 当为Started状态时, 在状态栏增加显示AP的SSID, BSSID, channel, security, 显示STOP,BLOCK_ALL,UNBLOCK_ALL按钮
另外, 还是在.get_sta_status_cb中加回了bssid, 所以STA连接的Router的BSSID信息以.get_sta_status_cb中的bssid为准,
即无论.get_sta_conf_cb中的bssid是否为空, 都以.get_sta_status_cb中的bssid为准.
谢谢!
Best regards,

Keguang Zhang
On 2019年01月16日 17:22, Zhang, Keguang (张可光) wrote:
Hi Clay, Ling
为了支持开机自动运行和SoftAP黑名单, 需要对APK增加新需求:

零. BT设备名字与实际MAC地址保持一致
     现在所有的板子的BT设备名都叫usp5661_6D6D, 可否与实际MAC地址的后三个byte保持一致, 以便区分

一. 界面方面:
     1. 将提示内容WiFi SSID和WiFi PASSWORD改为SSID和PASSWORD
     2. 根据.notify_scan_res上报的扫描结果中的security, 在扫描列表中的SSID后面显示对应的加密类型(OPEN) / (WPA/WPA2) / (OTHERS), seccurity的定义如下:
enum wifimgr_security {
        WIFIMGR_SECURITY_OPEN = 1,
        WIFIMGR_SECURITY_PSK,
        WIFIMGR_SECURITY_OTHERS,
};
     3. 在STA栏中增加autorun按钮, 具体请参考二.1.e
     4. 将AP的状态由STARTED/CLOSED改为Started/Closed
     5. 将AP MAC改为AP BSSID
     6. 分别添加BLOCK_ALL和UNBLOCK_ALL按钮, 具体请参考二.2和三
     7. 增加SoftAP的blacklist
     8. 在AP栏中增加autorun按钮, 具体请参考二.2.g
 
二. 开机自启动方面
点击APK中的WiFi Manager时, 通过.get_status获取STA的status和own MAC, 并调用.get_conf获取已连接的Router的SSID, BSSID, security, channel, autorun, 并在界面上显示相应状态和按钮(红色按钮为灰显,不能点击).
1. STA部分:
    a. 当为Closed状态时, 显示OPEN, SCAN, CONNECT按钮； AP栏显示START按钮
    b. 当为Ready状态时, 显示CLOSE, SCAN, CONNECT按钮； AP栏显示START按钮
    c. 若所选Router为OPEN模式, 则当SSID栏已配置后(不为空), 显示CLOSE, SCAN, CONNECT按钮
        若所选Router为WPA/WPA2模式, 则当SSID和PASSWORD栏均已配置后(都不为空), 显示CLOSE, SCAN, CONNECT按钮
        若所选Router为OTHERS模式, 则无论SSID和PASSWORD栏是否配置, 都显示CLOSE, SCAN, CONNECT按钮
    d. 当为Connected状态时, 在状态栏显示已连接的Router的SSID, BSSID, channel, security, 并显示CLOSE, SCAN, DISCONNECT按钮,
    e. 当autorun为0时, 显示ENABLE AUTORUN按钮, 点击时调用.set_conf(WIFIMGR_IFACE_NAME_STA, ..., 1); 当autorun为1时, 显示DISABLE AUTORUN按钮, 点击时调用.set_conf(WIFIMGR_IFACE_NAME_STA, ..., 0);
 
2. AP部分:
点击APK中的WiFi Manager时, 通过.get_status获取AP的status和own MAC, 并调用.get_conf获取SSID, BSSID, channel, security, autorun, 并在界面上显示相应状态和按钮(红色按钮为灰显,不能点击).
    a. 当为Closed状态时, 显示START,BLOCK_ALL,UNBLOCK_ALL按钮
    b. 当为Started状态时, 在状态栏增加显示AP的SSID, BSSID, channel, security, 显示STOP,BLOCK_ALL,UNBLOCK_ALL按钮
    c. 当Station list和blacklist为空时, 显示BLOCK_ALL,UNBLOCK_ALL按钮
    d. 当Station list不为空且blacklist为空时, 显示BLOCK_ALL,UNBLOCK_ALL按钮
    e. 当Station list和blacklist均不为空时, 显示BLOCK_ALL,UNBLOCK_ALL按钮
    f. 当Station list为空且blacklist不为空时, 显示BLOCK_ALL,UNBLOCK_ALL按钮
    g. 当autorun为0时, 显示ENABLE AUTORUN按钮, 点击时调用.set_conf(WIFIMGR_IFACE_NAME_AP, ..., 1); 当autorun为1时, 显示DISABLE AUTORUN按钮, 点击时调用.set_conf(WIFIMGR_IFACE_NAME_AP, ..., 0);
 
三. SoftAP的黑名单
保留之前的Station List, 在之下显示blacklist
以前的.del station已经替换为设置黑名单调用.set_mac_acl(char subcmd, char *mac), 设置黑名单同步动作, 类似与.get_status_cb, 调用后会立刻触发WiFi manager的回调.set_mac_acl_cb(ret),
subcmd为操作类型, 定义如下:
#define WIFIMGR_SUBCMD_ACL_BLOCK              (1)    /* 屏蔽单个STA */
#define WIFIMGR_SUBCMD_ACL_UNBLOCK         (2)    /* 屏蔽所有已连接的STA, mac = NULL; */
#define WIFIMGR_SUBCMD_ACL_BLOCK_ALL       (3)    /* 解除屏蔽单个STA */
#define WIFIMGR_SUBCMD_ACL_UNBLOCK_ALL  (4)    /* 解除所有已屏蔽的STA, mac = NULL; */

具体流程:
1. 点击Station list中的某个STA时触发.set_mac_acl(WIFIMGR_SUBCMD_ACL_BLOCK, mac), 等待回调.set_mac_acl_cb(ret),
若ret == 0, 表明设置黑名单成功, 调用.get_status获取更新后的Station list和blacklist； ret != 0, 表明设置失败, 无后续操作

2. 点击blacklist中的某个STA时触发.set_mac_acl(WIFIMGR_SUBCMD_ACL_UNBLOCK, mac), 等待回调.set_mac_acl_cb(ret),
若ret == 0, 表明设置黑名单成功, 调用.get_status获取更新后的Station list和blacklist； ret != 0, 表明设置失败, 无后续操作

3. 点击BLOCK_ALL按钮触发.set_mac_acl(WIFIMGR_SUBCMD_ACL_BLOCK_ALL, NULL), 等待回调.set_mac_acl_cb(ret),
若ret == 0, 表明设置黑名单成功, 调用.get_status获取更新后的Station list和blacklist； ret != 0, 表明设置失败, 无后续操作

4. 点击UNBLOCK_ALL按钮触发.set_mac_acl(WIFIMGR_SUBCMD_ACL_UNBLOCK_ALL, NULL), 等待回调.set_mac_acl_cb(ret),
若ret == 0, 表明设置黑名单成功, 调用.get_status获取更新后的Station list和blacklist； ret != 0, 表明设置失败, 无后续操作

麻烦帮忙实现, 感谢!
 
Best regards,

Keguang Zhang
On 2019年01月04日 16:17, Zhang, Keguang (张可光) wrote:
谢谢!
Best regards,

Keguang Zhang
On 2019年01月04日 16:03, Zhu, Clay (朱咸刚) wrote:
HI Keguang，
 
         SmartRepeater APK的新版本更新，代码已上github，请知悉！
 
 
=================================================================
Thanks
Mobile：15656008623
Email： clay.zhu@unisoc.com
Office: 021-20360600 - 2006
Clay Zhu（朱咸刚）
 
From: Zhu, Clay (朱咸刚) 
Sent: Wednesday, December 26, 2018 11:31 PM
To: Zhang, Keguang (张可光); Yu, Ivan (余琰知)
Cc: Chen, Steven (陈龙); Zhou, Ling (周灵); Wei, Bub (魏雪波); Li, Bing (李兵); Xiang, Dong (向东); Zhu, Gui (祝贵)
Subject: RE: SmartRepeater新需求
 
HI  Keguang，
 
         这边先编了一个版本，满足你之前提的所有的要求，因为你说后面还有需求，这边就先发一个内部测试的正式版本，有什么问题大家可以随时提出来。
 
备注：
         1. 因为手机界面大小有限，有些UI的改动没有完全按照你提的要求去做；
2. AP  Client的断开没有加del按钮，直接点击列表就可以断开；
 
感谢支持！
 
 
=================================================================
Thanks
Mobile：15656008623
Email：clay.zhu@unisoc.com
Office: 021-20360600 - 2006
Clay Zhu（朱咸刚）
 
From: Zhang, Keguang (张可光) 
Sent: Thursday, December 13, 2018 8:59 PM
To: Zhu, Clay (朱咸刚); Yu, Ivan (余琰知)
Cc: Chen, Steven (陈龙); Zhou, Ling (周灵); Wei, Bub (魏雪波); Li, Bing (李兵); Xiang, Dong (向东); Zhu, Gui (祝贵)
Subject: Re: SmartRepeater新需求
 
Hi Clay, Ling,
现在WiFi manager已经支持开机时根据之前保存的配置自动运行,
所以SmartRepeater在刚开始get_status时除了获取own MAC之外, 还需要获取额外的信息来决定界面的显示:
STA在Connected状态时, 还需要获取所连接router的SSID和BSSID, 并在状态栏旁显示这两项信息, STA STATE: Connected (SSID, BSSID)
AP在Started状态时, 还需要获取已连接上来的station列表, 即Client List, 
相应的回调wifimgr_ctrl_iface_get_status_cb已经拆分为wifimgr_ctrl_iface_get_sta_status_cb和wifimgr_ctrl_iface_get_ap_status_cb, 详见https://github.com/unisoc/apps/pull/49
 
Hi Bing, Bub,
目前STA的GET_STATION和AP的DEL_STATION这两个命令还没有, 麻烦尽快实现.
谢谢!
Best regards,
 
Keguang Zhang
On 2018年12月11日 09:53, Zhu, Clay (朱咸刚) wrote:
HI Ivan,
 
         之前的版本上有这个bug, 已经fix了,等待下个版本发布.
 
HI Keguang,
 
         请问之前说的Start AP的问题是否已经修复?
 
From: Yu, Ivan (余琰知) 
Sent: Monday, December 10, 2018 4:50 PM
To: Zhang, Keguang (张可光); Zhu, Clay (朱咸刚)
Cc: Chen, Steven (陈龙); Zhou, Ling (周灵); Wei, Bub (魏雪波); Li, Bing (李兵); Xiang, Dong (向东); Zhu, Gui (祝贵)
Subject: RE: SmartRepeater新需求
 
现在界面上scan回来的BSSID都显示为00:00:00:00:00:00，是没传过来还是显示问题？
 
From: Keguang Zhang (张可光) 
Sent: Wednesday, December 05, 2018 12:50 PM
To: Clay Zhu (朱咸刚)
Cc: Steven Chen (陈龙); Ling Zhou (周灵); Bub Wei (魏雪波); Bing Li (李兵); Dong Xiang (向东); Ivan Yu (余琰知); Gui Zhu (祝贵)
Subject: Re: SmartRepeater新需求
 
Hi Clay, Ling,
更正AP部分需求:
3. 将START AP和CLOSE AP两个按钮整合为一个按钮START/STOP, 仿照STA的OPEN/CLOSE按钮
    在Ready状态时变为START按钮, 点击时先发open再发start_ap命令； 在Started状态时变为STOP按钮, 点击时先发stop_ap再发close命令(wifi_manager_service.c中需要同步添加).
Best regards,
 
Keguang Zhang
On 2018年12月05日 10:33, Keguang Zhang (张可光) wrote:
Hi Clay, Ling,
SmartRepeater的新需求如下:
一. STA部分:
1. 将OPEN WIFI/CLOSE WIFI按钮名称修改OPEN/CLOSE
2. 将WIFI SCAN按钮名称修改为SCAN
3. 将STATE ADDR改名为STA MAC
4. 将WIFI STATE:和CONNECTED WIFI:这两行整合为一行: STA STATE, 显示STA的状态(共3种): --/Ready/Connected
5. 修改CONNECT按钮, 做成类似OPEN/CLOSE按钮,
    在Ready状态时变为CONNECT按钮； 在Connected状态时变为DISCONNECT按钮, 点击时发disconnect命令
二. AP部分
1. 将AP ADDR改名为AP MAC
2. 在AP MAC的上一行增加一行AP STATE, 显示AP的状态(共3种): --/Ready/Started
3. 将START AP和CLOSE AP两个按钮整合为一个按钮, 做成类似OPEN/CLOSE按钮,
    在Ready状态时变为START按钮, 点击时先发open再发start_ap命令； 在Started状态时变为STOP按钮, 点击时先发stop_ap再发close命令(wifi_manager_service.c中需要同步添加).
4. 增加AP的SSID设置, 使用户可以配置AP的SSID(wifi_manager_service.c中需要同步修改)
5. 在本页面最后增加Client List, 显示当前已连接的STA的MAC, 每行一条, 最多支持16个STA, 所以最多显示16行, 在STA的MAC之后放置一个DEL按钮, 
    每次有新的STA连接时, WiFi manger会调用notify_new_station通知wifi_manager_service.c, 其中包含该STA的MAC(wifi_manager_service.c中需要同步实现notify_new_station).
    点击DEL按钮时发del_station命令(wifi_manager_service.c中需要同步实现del_station).
    del station成功之后, WiFi manger会调用notify_new_station通知wifi_manager_service.c, APK上需同步删除改STA对应的条目.
 
麻烦帮忙实现, AP的第5点改动较大, 可以稍后再实现.
感谢!
-- 
 
Best regards,
 
Keguang Zhang




