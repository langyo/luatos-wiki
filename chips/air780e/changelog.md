# Ec618系列固件发行注记

## V1108

待发布

兼容性变化:
1. 修正CPU温度的单位
   1.1 影响, 之前的版本返回的CPU温度是摄氏度, 其他BSP均为1/1000摄氏度
   1.2 解决办法: 新数据/1000 即得到原有的数据值

## V1107

兼容性变化:
1. 不再自动查询基站信息
   1.1 影响: 如没有调用mobile.reqCellInfo函数, mobile.cellInfo()会返回空数组
   1.1 解决办法: 按需调用或定时调用 `mobile.reqCellInfo(60)`
2. 软件DAC音频的音量配置生效
   2.1 影响: 使用Air780E的软件DAC功能时, `audio.vol(0, 50)`可能会听不清楚
   2.2 解决办法: 设置音量到100或以上

功能新增:
* uart.read支持读取指定长度
* 新增 mcu.iomux 函数,支持配置uart/spi/i2c复用
* 新增 pm.ioVol 函数, 支持配置io电压
* 新增 合宙 PSM+ 超低功耗模式, 集成在 pm.power 函数
* 扩展 gpio.setup 函数,添加alt_func参数, 支持配置复用
* 扩展 http.request 函数, 支持fota和下载过程回调
* 新增 iotcloud库, 一键对接阿里云/腾讯云/华为云/Onenet等云平台
* 新增 mobile.config 函数, 可设置网络静态优化
* 新增 lora2 库, 支持挂载多个lora设备
* 新增 mobile.setPin 函数, 支持对SIM卡的PIN码的相关操作
* 新增多款传感器/外设驱动, ina226/ak8963/mpu9250/st7565等
* 新增 repl 库, 支持从串口直接输入lua语句,执行后输出结果
* 新增 adc.set 库支持分压设置
* 新增demo
   * 低功耗演示      demo/psm
   * 钉钉机器人      demo/dingding
   * 飞书机器人      demo/feishu
   * 云平台对接      demo/iotcloud
   * 部标jt808对接   demo/jt808
   * 录音功能        demo/record
   * 虚拟串口上位机  demo/usb_uart
   * 中国电信ctwing  demo/ctwing

更详细的更新内容请查阅git的提交日志

## V1106

1. 新增: mobile库添加网络特殊配置功能
2. 新增: 获取当前服务小区的cellid，不需要重新搜索
3. 新增: websocket库添加sent/disconnect事件
4. 新增: http支持fota
5. 新增: 腾讯云demo
6. 新增: fota.file(path)
7. 新增: mobile增加一个网络搜索中的常量mobile.SEARCH
8. 新增: mqtt库支持qos2的消息下发
9. 新增: mqtt增加verify参数，可选是否强制校验证书
10. 新增: luatos usb串口增加sent事件回调，但是仅代表数据写入底层缓存
11. 新增: 添加httpsrv
12. 新增: TF卡上电控制
13. 新增: 域名解析，socket.connect里remote_port设置成0则只进行DNS，不做连接，DNS完成后直接返回ON_LINE 
14. 优化: 优化云编译配置，增加uart0释放、字体等
15. 优化: 调整luat_uart_setup的缓冲区默认大小,设置最小值2k, 最大值8k,解决大数量场景下uart缓冲区不够的问题, 尤其是Air780EG的uart2
16. 优化: 增大UART的RX DMA缓存区数量，并可以随用户的RX缓存做调节
17. 优化: string.fromhex()过滤掉非法字符
18. 优化: 更均匀的使用socket id
19. 优化: lcd默认清屏为黑色更合理一些，主要作用避免初始化后显示时有花屏
20. 优化: gnss处理转到lua任务里
21. 优化: 在加载内置库和require前后执行gc,对内存消耗进行削峰
22. 优化: 允许cid1设置用户的apn，用于无法用公网APN激活的专网卡
23. 优化: lpuart异常处理
24. 优化: luatos开机打印完整硬件版本号
25. 优化: luatos uart rs485如果转换超时设置小于1ms会强制改成1ms
26. 优化: luat_websocket_ping先判断一下连接状态再发
27. 优化:优化luatos音量调节
28. 优化: 改进task的mailbox减少内存消耗
29. 优化: mp3解码器重新封装
30. 优化: 加快硬件协议的网卡本地端口的分配
31. 优化: 减少ftp的ram消耗
32. 修复: lwip小概率会对同一个tcp释放两次
33. 修复: luatos wdt重新初始化失效
34. 修复: 修复gc9306 90°方向设置错误
35. 修复: zbuff:unpack、pack.unpack添加lua虚拟栈检测
36. 修复: luatos 获取cellinfo有时候会失败
37. 修复: json库在浮点数0.0的时候会变成科学计数法
38. 修复: libgnss.clear()未能正确清除历史定位数据
39. 修复: I2C读写失败后，内部硬件状态机不能自动恢复
40. 修复: 修复i2c1默认引脚错误
41. 修复: 开启低功耗串口后，再关闭仍然会有中断，串口关闭会死机
42. 修复: uart0输出EPAT log时，如果rx上有杂波，可能会死机
43. 修复: http库的timeout_timer存在多次free的可能性
44. 修复: mqtt库设置will应允许payload为空
45. 修复: http Content-Length=0时异常问题
46. 修复: sntp_connect的判断不正确

## LuatOS-SoC@EC618 V1105

1. 新增: 添加软件DAC (PWM音频输出) **注意：现有版本开发板不支持此功能**

2. 修复: 回滚V1103升级到V1104的fskv库读写整型/浮点型数据的差异

   **此版本同样包含[V1104](https://gitee.com/openLuat/LuatOS/releases/tag/v0007.ec618.v1104)修改所有更新**
## LuatOS-SoC@EC618 V1104

## V1104

tag: v0007.ec618.v1104
date: 2023-03-13

1. 新增: 新增gmssl库，支持国密sm2/sm3/sm4
2. 新增: 软件uart
3. 新增: 支持w5500,可以外挂以太网模块了
4. 新增: uart1在600,1200,2400,4800,9600波特率情况下，自动启用LPUART功能，休眠时，数据接收不丢失
5. 新增: luatos增加amr编码功能
6. 新增: 支持iconv库
7. 新增: fatfs
8. 新增: luatos可以选择开启powerkey防抖
9. 新增: luatos增加cam_vcc控制
10. 新增: audio.config增加设置音频播放完毕后关闭pa和dac的时间间隔，消除可能存在的pop音
11. 新增: 添加基站+wifi定位demo lcsLoc.lau
12. 新增: mqtt添加断开事件
13. 新增: 如果未刷入脚本则进行打印提示
14. 新增: 添加fdb/fskv库的iter和next函数
15. 新增: 免boot下载脚本
16. 优化: adc的id兼容一下老的10/11配置
17. 优化: 解除了用户log单次并发条数的限制
18. 优化: 优化usb串口输出
19. 优化: 优化RRC释放的时机
20. 优化: 动态ram分配优化
21. 优化: 将中断服务函数，高实时性函数和一些常用函数全部放到ram中,提升运行效率
22. 优化: uart rx在正常模式下用DMA接收，大幅度提升高波特率下大数据接收的稳定性
23. 优化: luatos的fota防御内存不足无法初始化的情况
24. 优化: 遇到伪基站时，快速切换到正常基站
25. 优化: SPI开启内部上下拉提高稳定性
26. 优化: http忽略自定义Content-Length
27. 优化: 网络遇到致命错误时可以自动重启协议栈来恢复，需要手动开启
28. 优化: 完善apn激活的操作
29. 优化: http库 url长度无限制
30. 优化: audio任务优先级提升，提高播放的稳定性
31. 修复: luatos socket dtls模式下死机问题
32. 修复: audio_play_stop判断不完整
33. 修复: 修复弱网环境下，dns查询接口阻塞无返回的问题
34. 修复: 修复luat_fs_fopen打开包含不存在目录的路径时会崩溃问题
35. 修复: tls握手完成后，如果一段时间无数据交互会超时
36. 修复: sntp自定义域名为3个时候处理异常
37. 修复: protobuf库无法正确解码64bit的数据
38. 修复: miniz库常量重复导致pairs时死循环
39. 修复: 深度休眠唤醒后无法识别模块类型

# ChangeLog for LuatOS@EC618 V1103

## V1103

tag: v0007.ec618.v1103
date: 2023-02-06

**注意：因socket接口返回值与之前不兼容，特此版本号由v1002升至v1103以作提醒**

**此版本已完整支持Air780EG**

1. 新增: 支持ipv6，需调用mobile.ipv6开启，默认不开启，前提开卡时需要支持ipv6 （对此有什么应用场景的好点子可以和我们反馈呦）
2. 新增: 支持ftp
3. 新增: 支持fskv
4. 新增: libfota.lua封装库，fota更简单
5. 新增: mobile 添加IP_LOSE消息
6. 新增: mobile允许开机优先使用SIM0
7. 新增: lbsLoc.lua封装库，基站定位更简单
8. 新增: sms库支持清理长短信片段 sms.clearLong()
9. 新增: http添加超时参数
10. 新增: 添加rtc.timezone函数
11. 新增: 录音功能
12. 新增: sms库支持禁用长短信的自动合并
13. 新增: i2s回调和异步接收功能
14. 新增: 添加mlx90614驱动
15. 新增: 添加新的ram文件系统
16. 新增: pm.lastReson()更详细的开机原因可用
17. 新增: 支持gtfont
18. 新增: 支持用户自定义APN并激活使用
19. 优化: 485等待发送完成
20. 优化: USB虚拟串口单次发送长度不再限制512
21. 优化: SPI底层驱动优化，启用DMA
22. 优化: I2C底层驱动优化
23. 优化: UART底层驱动优化
24. 优化: 调整iotauth库的代码,使其不使用静态内存，调整默认时间戳，修正输出秘钥长度
25. 修改: GPIO14/15 映射到PAD 13/14的ALT 4, 从而避免与UART0冲突
26. 修改:socket接口规范返回值（与之前版本不兼容，重要！！！！！）
27. 修复: udp接收会有内存泄露
28. 修复: http库未支持自定义Host
29. 修复: sntp自定义地址table处理异常
30. 修复: fota只更新脚本且很小时候有概率失败
31. 修复: sms库在修正多条长短信合并时判断错误
32. 修复: sms库连续收到多条长短信,且顺序混乱时,短信内容合并错误 
33. 修复: 虚拟UART的rx回调
34. 修复: mqtt库在publish消息时,若qos=0,返回的pkgid不合理,应该固定为0
35. 修复: UDP接收数据不全
36. 修复: rtc库未正确实现
37. 修复: http chunk编码异常

**core_V1103.zip** 就是固件文件, 其余两个是底层源码,无需下载.
** Air780EG测试定位效果_搭配公众号文章.zip** 是用于测Air780EG定位效果的
