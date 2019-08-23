# RasPi3B

### 系统安装：无屏幕无键鼠无网线无HDMI，自动激活ssh和wifi

> - 树莓派3B
> - SD卡，读卡器
> - wifi环境（文中所有涉及网络操作的设备必须连入同一wifi）
> - 运行Mac OS的电脑
> - 手机（非必需）

1. 官网下载镜像并解压，建议选择带桌面及常用软件的版本：https://www.raspberrypi.org/downloads/raspbian/

2. 格式化SD卡，命名保持默认即可，格式为**MS-DOS(FAT)**，方案为**主引导记录**

3. 使用**Etcher**将镜像烧入SD卡，没有这个软件的可以在这里下载：https://www.balena.io/etcher/

4. 烧入完成后SD卡会被自动弹出，将它重新插入电脑

5. 打开终端定位至SD卡的根目录，向其中添加ssh和wpa_supplicant.conf文件

   ```bash
   touch ssh # 这个文件是为了激活ssh
   touch wpa_supplicant.conf # 这个文件是为了启用wifi
   ```

6. 第一个ssh文件不用碰，用任意编辑器打开wpa_supplicant.conf后写入以下内容

   > 注：这里给出的内容仅适用于无密码wifi
   >
   > 如果wifi有密码，请参照以下链接进行适当修改，或使用手机热点（选择不需要密码，并且确保电脑连着热点）
   >
   > http://shumeipai.nxez.com/2017/09/13/raspberry-pi-network-configuration-before-boot.html

   ```bash
   country=us
   update_config=1
   ctrl_interface=/var/run/wpa_supplicant
   
   # 注意：本例中的wifi没有密码，有密码时请参照以上链接，虽然可以但是不建议在此时添加多个wifi
   network={
       ssid="******" # wifi名称
       key_mgmt=NONE # wifi加密方式
   }
   ```

   保存修改后弹出SD卡

7. 扫描此时局域网中的主机，记住都有哪些（可以用手机任意下载一个ip扫描软件，iPhone推荐iNetTools）

8. 将SD卡插入树莓派，接上电源，等待树莓派开机（保险起见2分钟）

9. 树莓派开机之后会自动连上之前设置的wifi，此时重新扫描局域网内的所有主机，多出来的那个就是树莓派的ip

10. 打开终端，通过ssh连接树莓派

    ```bash
    ssh pi@树莓派的ip
    ```

11. 第一次ssh连接会有警告，回答yes确认即可。接着会要求输入树莓派的密码，默认密码都是

    ```bash
    raspberry
    ```

    输入时终端为了安全不会显示密码，输入完成按回车，就正式连接上树莓派啦～

12. 两个有用的小命令：

    ```bash
    sudo raspi-config # 进入树莓派的系统设置
    sudo poweroff # 关机，输入后等到只有红色LED灯（电源灯）亮时就表明关机结束，可以断开电源
    ```
