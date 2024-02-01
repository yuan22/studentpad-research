# 科大讯飞AI学习机破解安装第三方应用教程

* 本项目欢迎各位读者开issue

### 第三方应用安装（又称：升级软件法）

##### 思路

* 制作可以打开隐藏的activity的apk（包名得是应用商店可下载的软件的包名，且将版本号更改为9999999999），然后拿钉钉、QQ、微信等聊天软件传上去，进行“更新”，后面通过这个途径达到开启adb的效果。

##### 实践

###### 第一步：确认cpu的厂商

打开平板上的“设置”app，点到“我的设备”，看到“处理器”一栏，一般这里会显示“Unisoc”“Qualcomm”等字样，那你就完成了第一步，且证明了该设备系统版本为安卓9

###### 第1.1步（通过UI猜安卓版本）：看平板右上角的状态栏，如果像![1706627508990](image/1/1706627508990.png)一样，那就是安卓12，如果是其他样子的，那就是安卓9

###### 第二步：修改得到apk

至于要用到的文件，我放到了该仓库的Release中，下载双击安装即可。**（其中，exe文件是修改APK的工具；创建快捷方式.apk是需要修改的apk；zip文件是adb工具包，你需要将它解压）**

然后，打开APK Editor Studio

![1706707610274](image/1/1706707610274.png)

![1706707825974](image/1/1706707825974.png)

![1706708094229](image/1/1706708094229.png)

自此，准备工具的制备告一段落，你需要点“保存apk”来保存你来之不易的成果。

###### 第三步：在平板上实施”调虎离山“之计，并做到

3.1：通过某种方式将你的劳动成果从电脑上传到平板上（QQ、微信、钉钉，甚至是USB传输也行），打开下载好的apk文件，此时正常会弹出软件更新，点击继续，然后直接返回桌面，****长按被替换的软件并卸载，卸载之后会看到之前的应用更新**，一路无脑安装即可**，*打开创建快捷方式后右上角菜单把三个方框勾上*

3.2.1（"设置-我的设备"中看到自己是”Qualcomm“的情况）：在”打开快捷方式“app中搜索”搜索建议“，点右边绿色的”详情“按钮，点”打开“然后如下图操作

![1706713223387](image/1/1706713223387.png)

然后点几次"版本号"就能打开开发者，进而打开"USB 调试"

3.2.2（"设置-我的设备"中看到自己是"Unisoc"的情况）：在**步骤3.1完成后**直接在"打开快捷方式"中向下翻到***EngineerMode*那一项(包名为com.sprd.engineermode)**，然后点"活动列表"，点开最顶上那一个的"详情"，然后点"打开"，切换到"DEBUG&LOG"选项卡，向下滑找到"USB Debug"并打开该选项

**到这里，你已经成功开启了adb，可以进入下一个步骤了！加油，达瓦里氏，胜利就在眼前！**

3.3  安装adb驱动和爱玩机工具箱，并授予工具箱MDM权限，来实现软件安装的本地化、自主可控化

[下载：爱玩机工具箱(com.byyoung.setting) - S-22.0.8.1 - 应用 - 酷安 (coolapk.com)](https://www.coolapk.com/apk/com.byyoung.setting)

[Download SPD Driver R4.20.4201 (UniSoc Driver) (androiddatahost.com)](https://androiddatahost.com/dsa6h)

你在**第二部准备工作**还下了一个压缩包（.zip）文件，你需要把它解压到一个目录。然后将下载的爱玩机工具箱移到那个解压的目录中，并在上方的地址栏输入"cmd",能打开一个窗口，你需要输入如下内容

```
adb install <apk文件路径（我更建议你打个空格，然后直接将apk文件拖进来，windows会自动识别路径）>
```

然后，点开平板上的“爱玩机工具箱”app，你需要进到“权限中心”，并照着应用提示，启用最下面的“高级设备管理员（带防卸载）”即可。后面，你可以在“导航——应用相关——应用安装器”中自行启用“激活此安装器”，本篇不过多赘述。

建议在破解后删除“系统更新”应用，命令如下：

```
adb shell pm uninstall -k --user 0 com.iflytek.study.ota
```

这样是为了防止KDXF官方后续对该方法完全的封杀

## 自此，第三方应用安装的教程结束！完结撒花~

---

# AI学习机高阶教程（Experimental | 未完工警告）

Warning：下列操作较为危险，有几率导致平板变砖，三思而行（我们现在暂时还没有出刷机包，救不回来，官方刷机费一次要60大洋）

## 获取学习机的root（即刷入Magisk）

##### 为何要把root部分拿出来讲呢？因为这学习机的boot无法patch（原因是没有ramdisk）

有两种可能的方法：system分区植入magisk法和patch rec镜像法

##### system分区植入magisk法

system分区植入magisk法的大概思路就是将magisk安装到安卓system分区，可以参考[某酷安大佬写的方案（Magisk system root部分）](https://github.com/TomKing062/CVE-2022-38694_unlock_bootloader/wiki/Magisk)

原文如下（防删）：

> # Magisk system mode
>
> this can be turned to a github action, but currently this needs another device rooted with Magisk Delta (system mode)
>
> ## part 1
>
> find which file is used by your system
>
> * /vendor/etc/selinux/precompiled_sepolicy
> * /system_root/odm/etc/selinux/precompiled_sepolicy
> * /system/etc/selinux/precompiled_sepolicy
> * /system_root/sepolicy
> * /system_root/sepolicy_debug
> * /system_root/sepolicy.unlocked
>
> patch your sepolicy
>
> ```
> magiskinit --patch-sepol sepol.in sepol.out
> ```
>
> ## part 2 (use unpack tool or mount image on linux)
>
> overwrite sepol.out back to device partition
>
> cp /system/etc/init/bootanim.rc and /system/etc/init/magisk from rooted device to unrooted device's partition
>
> remember to add/change properties(owner, permission, selinux context) for them
>
> write partition back by spd_dump or fastboot(d)
>
> owner and permission
>
> ```
> system/system/etc/init/magisk/magisk32 0 0 0700
> system/system/etc/init/magisk/magisk64 0 0 0700
> system/system/etc/init/magisk/magiskpolicy 0 0 0700
> system/system/etc/init/magisk/magiskinit 0 0 0700
> system/system/etc/init/magisk/stub.apk 0 0 0700
> system/system/etc/init/magisk/config 0 0 0700
> system/system/etc/init/magisk 0 0 0700
> ```
>
> selinux context
>
> ```
> /system/system/etc/init/magisk u:object_r:system_file:s0
> /system/system/etc/init/magisk/config u:object_r:system_file:s0
> /system/system/etc/init/magisk/magisk32 u:object_r:system_file:s0
> /system/system/etc/init/magisk/magisk64 u:object_r:system_file:s0
> /system/system/etc/init/magisk/magiskinit u:object_r:system_file:s0
> /system/system/etc/init/magisk/magiskpolicy u:object_r:system_file:s0
> /system/system/etc/init/magisk/stub\.apk u:object_r:system_file:s0
> ```
>
> content of config
>
> ```
> SYSTEMMODE=true
> RECOVERYMODE=false
> ```
>
> content added to original bootanim.rc
>
> ```
> on post-fs-data
>     start logd
>     exec u:r:su:s0 root root -- /system/etc/init/magisk/magiskpolicy --live --magisk
>     exec u:r:magisk:s0 root root -- /system/etc/init/magisk/magiskpolicy --live --magisk
>     exec u:r:update_engine:s0 root root -- /system/etc/init/magisk/magiskpolicy --live --magisk
>     exec u:r:su:s0 root root -- /system/etc/init/magisk/magisk64 --auto-selinux --setup-sbin /system/etc/init/magisk /sbin
>     exec u:r:su:s0 root root -- /sbin/magisk --auto-selinux --post-fs-data
>
> on nonencrypted
>     exec u:r:su:s0 root root -- /sbin/magisk --auto-selinux --service
>
> on property:vold.decrypt=trigger_restart_framework
>     exec u:r:su:s0 root root -- /sbin/magisk --auto-selinux --service
>
> on property:sys.boot_completed=1
>     mkdir /data/adb/magisk 755
>     exec u:r:su:s0 root root -- /sbin/magisk --auto-selinux --boot-complete
>    
> on property:init.svc.zygote=restarting
>     exec u:r:su:s0 root root -- /sbin/magisk --auto-selinux --zygote-restart
>    
> on property:init.svc.zygote=stopped
>     exec u:r:su:s0 root root -- /sbin/magisk --auto-selinux --zygote-restart
> ```

##### 修补rec法

就是把recovery分区用RD提出来，然后用magisk修补下，但可惜，修补后的镜像无法用fastboot\spd_dump工具刷进去

### 附录：一些资源及其使用方法/作用

#### SPD_Driver

Link：[Download SPD Driver R4.20.4201 (UniSoc Driver) (androiddatahost.com)](https://androiddatahost.com/dsa6h)

作用：ADB驱动+展讯下载模式的驱动

使用方法：下载安装即可

注：macOS、Linux不需要安装这个东西

#### Research Download

Link：[Research Tool - SPD Flash Tool](https://spdflashtool.com/category/research-tool)

作用：读取分区、刷入分区（很危险！）

我推荐用R25.20.3901这个版本，因为它比较稳定

用法：[使用ResearchDownload为展讯机型提取镜像 - 哔哩哔哩 (bilibili.com)](https://www.bilibili.com/read/cv24981169/?jump_opus=1)

    总之就是你需要pac刷机包才能用

弊端：你必须得先做个包或者先拿同SoC（比如ud710）的fdl才行，还有每次回读操作都太麻烦了，但如果不遵守就有很大可能性会出问题（比如刷砖。售后刷机一次60）

#### spd_dump及CVE-2022-38694_unlock_bootloader项目

Link：[GitHub - TomKing062/CVE-2022-38694_unlock_bootloader](https://github.com/TomKing062/CVE-2022-38694_unlock_bootloader)

作用：提供了第二种进行读写设备分区操作的工具，但它是命令行的；提供了一种强解bootloader的方法（SoC漏洞），研究出来可以搞升级软件法不支持的机型安装软件；可以用这个读取平板的分区表（数据单位为MB）

用法（对于我们学习机而言）

```
spd_dump fdl fdl1.bin 0x5500 fdl fdl2.bin 0x9efffe00 exec <read_part/write_part/erase_part> <partition_name（分区名称）>  0 <size（分区大小，是个单位都行，比如M（MB）、K（KB），等等）>
```

注：write_part\erase_part 不需要写 0 `<size>` 这一部分
