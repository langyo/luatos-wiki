# 📮 sys系统消息


此处列举了LuatOS框架中自带的系统消息列表



## sys



[sys接口文档页](https://wiki.luatos.com/api/sys.html)



### 以 0x01 为第一个字节开头

用于 luatos 内部的系统消息传递

**额外返回参数**

|返回参数类型|解释|
|-|-|
|args|返回的数据|

**例子**

```lua
--此为系统内部使用的消息，请勿在外部使用

```

---

## keyboard



[keyboard接口文档页](https://wiki.luatos.com/api/keyboard.html)



### KB_INC

键盘矩阵消息

**额外返回参数**

|返回参数类型|解释|
|-|-|
|number|port, keyboard id 当前固定为0, 可以无视|
|number|data, keyboard 按键 需要配合init的map进行解析|
|number|state, 按键状态 1 为按下, 0 为 释放|

**例子**

```lua
sys.subscribe("KB_INC", function(port, data, state)
    -- port 当前固定为0, 可以无视
    -- data, 需要配合init的map进行解析
    -- state, 1 为按下, 0 为 释放
    log.info("keyboard", port, data, state)
end)

```

---

## pm



[pm接口文档页](https://wiki.luatos.com/api/pm.html)



### DTIMER_WAKEUP

deep sleep timer定时时间到回调

**额外返回参数**

无

**例子**

```lua
sys.subscribe("DTIMER_WAKEUP", function(timer_id)
    log.info("deep sleep timer", timer_id)
end)

```

---

## pm 



[pm 接口文档页](https://wiki.luatos.com/api/pm .html)



### YHM27XX_REG

YHM27XX芯片寄存器信息更新回调

**额外返回参数**

无

**例子**

```lua
sys.subscribe("YHM27XX_REG", function(data)
    -- 注意, 会一次性读出0-9,总共8个寄存器值
    log.info("yhm27xx", data and data:toHex())
end)

```

---

## touchkey



[touchkey接口文档页](https://wiki.luatos.com/api/touchkey.html)



### TOUCHKEY_INC

触摸按键消息

**额外返回参数**

|返回参数类型|解释|
|-|-|
|number|port, 传感器id|
|number|state, 计数器,触摸次数统计|

**例子**

```lua
sys.subscribe("TOUCHKEY_INC", function(id, count)
    -- 传感器id
    -- 计数器,触摸次数统计
    log.info("touchkey", id, count)
end)

```

---

## uart



[uart接口文档页](https://wiki.luatos.com/api/uart.html)



### VUART_STATE

虚拟串口(USB CDC)的连接状态变化

**额外返回参数**

|返回参数类型|解释|
|-|-|
|number|串口id|
|boolean|连接状态, true为已连接|

**例子**

```lua
sys.subscribe("VUART_STATE", function(id, state)
    log.info("uart", "vuart state", id, state)
end)

```

---

## airlink



[airlink接口文档页](https://wiki.luatos.com/api/airlink.html)



### AIRLINK_PING_RESULT

airlink ping的结果

**额外返回参数**

|返回参数类型|解释|
|-|-|
|number|本次ping的包id|
|boolean|是否ping通|
|any|成功时为往返耗时ms(number); 失败时为"timeout"(string)或错误码(number)|
|string|成功时为回显数据, 失败时为nil|

**例子**

```lua
sys.subscribe("AIRLINK_PING_RESULT", function(pkgid, ok, rtt, echo)
    log.info("airlink", "ping result", pkgid, ok, rtt)
end)

```

---

### AIRLINK_SFOTA_DONE

AIRLINK升级结束消息 2025/10/24启用

**额外返回参数**

|返回参数类型|解释|
|-|-|
|bool|result, 升级成功为true，否则为false|
|string|reason, 失败原因，当前取值有"no_memory" 内存不足, "file_error" 文件打开异常|

**例子**

```lua
-- 订阅式
sys.subscribe("AIRLINK_SFOTA_DONE", function(result, reason)
    log.info("airlink fota", result, reason)
end)

```

---

### AIRLINK_SDATA

收到airlink对端设备发来的自定义数据(sdata)

**额外返回参数**

|返回参数类型|解释|
|-|-|
|string|数据内容|

**例子**

```lua
sys.subscribe("AIRLINK_SDATA", function(data)
    log.info("airlink", "sdata", data)
end)

```

---

## wlan



[wlan接口文档页](https://wiki.luatos.com/api/wlan.html)



### WLAN_SCAN_DONE

WIFI扫描结束

**额外返回参数**

无

**例子**

```lua
sys.taskInit(function()
    sys.waitUntil("WLAN_SCAN_DONE")
    log.info("wlan", "scan done")
end)

```

---

### WLAN_STA_INC

WLAN的STA事件, 连接上AP或断开连接时上报

**额外返回参数**

|返回参数类型|解释|
|-|-|
|string|事件类型, 例如 "CONNECTED" 已连接, "DISCONNECTED" 已断开|
|any|事件为"CONNECTED"时为已连接的SSID(string); 否则为断开原因码(number)|
|string|事件为"CONNECTED"时为AP的BSSID(6字节二进制), 其他事件无此参数|

**例子**

```lua
sys.subscribe("WLAN_STA_INC", function(event, arg1, arg2)
    log.info("wlan", "sta event", event, arg1, arg2)
end)

```

---

### WLAN_AP_INC

WLAN的AP热点事件, 有设备连接/断开本机热点时上报

**额外返回参数**

|返回参数类型|解释|
|-|-|
|string|事件类型, 例如 "CONNECTED" 有设备连入, "DISCONNECTED" 有设备断开|
|string|对端设备的MAC地址(6字节二进制), 可能为空字符串|

**例子**

```lua
sys.subscribe("WLAN_AP_INC", function(event, mac)
    log.info("wlan", "ap event", event, mac and mac:toHex() or "")
end)

```

---

## w5500



[w5500接口文档页](https://wiki.luatos.com/api/w5500.html)



### IP_READY

已联网

**额外返回参数**

无

**例子**

```lua
-- 联网后会发一次这个消息
sys.subscribe("IP_READY", function(ip, adapter)
    log.info("w5500", "IP_READY", ip, (adapter or -1) == socket.LWIP_GP)
end)

```

---

### IP_LOSE

已断网

**额外返回参数**

无

**例子**

```lua
-- 断网后会发一次这个消息
sys.subscribe("IP_LOSE", function(adapter)
    log.info("w5500", "IP_LOSE", (adapter or -1) == socket.ETH0)
end)

```

---

### W5500_IND

w5500状态变化

**额外返回参数**

无

**例子**

```lua
sys.subscribe("W5500_IND", function(status)
    -- status的取值有:
    -- CABLE_INSERT 网线插入
    -- CABLE_REMOVE 网线拔出
	-- DHCP_TIMEOUT 获取IP超时
    log.info("w5500 status", status)
end)

```

---

## ioqueue



[ioqueue接口文档页](https://wiki.luatos.com/api/ioqueue.html)



### IO_QUEUE_DONE_N

io操作队列执行完成, topic尾部的N为硬件定时器id

**额外返回参数**

无

**例子**

```lua
sys.subscribe("IO_QUEUE_DONE_0", function()
    log.info("io_queue", "done")
end)

```

---

### IO_QUEUE_EXTI_N

io队列捕获到外部电平变化, topic尾部的N为引脚号

**额外返回参数**

|返回参数类型|解释|
|-|-|
|number|电平值, 0或1|
|string|捕获时刻的时间戳, 8字节二进制的64bit整数|

**例子**

```lua
sys.subscribe("IO_QUEUE_EXTI_7", function(val, tick)
    log.info("io_queue", "exti", val, tick)
end)

```

---

## lora



[lora接口文档页](https://wiki.luatos.com/api/lora.html)



### LORA_TX_DONE

LORA 发送完成

**额外返回参数**

无

**例子**

```lua
sys.subscribe("LORA_TX_DONE", function()
    lora.recive(1000)
end)

```

---

### LORA_RX_DONE

LORA 接收完成

**额外返回参数**

无

**例子**

```lua
sys.subscribe("LORA_RX_DONE", function(data, size, rssi, snr)
    -- rssi 和  snr 于 2023-09-06 新增
    log.info("LORA_RX_DONE: ", data, size, rssi, snr)
    lora.send("PING")
end)

```

---

### LORA_TX_TIMEOUT

LORA 发送超时

**额外返回参数**

无

**例子**

```lua
sys.subscribe("LORA_TX_TIMEOUT", function()
    lora.recive(1000)
end)

```

---

### LORA_RX_TIMEOUT

LORA 接收超时

**额外返回参数**

无

**例子**

```lua
sys.subscribe("LORA_RX_TIMEOUT", function()
    lora.recive(1000)
end)

```

---

### LORA_RX_ERROR

LORA 接收错误

**额外返回参数**

无

**例子**

```lua
sys.subscribe("LORA_RX_ERROR", function()
    lora.recive(1000)
end)

```

---

## libgnss



[libgnss接口文档页](https://wiki.luatos.com/api/libgnss.html)



### GNSS_STATE

GNSS状态变化

**额外返回参数**

无

**例子**

```lua
sys.subscribe("GNSS_STATE", function(event, ticks)
    -- event取值有
    -- FIXED 定位成功
    -- LOSE  定位丢失
    -- ticks是事件发生的时间,一般可以忽略
    log.info("gnss", "state", event, ticks)
end)

```

---

## mobile



[mobile接口文档页](https://wiki.luatos.com/api/mobile.html)



### SIM_IND

sim卡状态变化

**额外返回参数**

无

**例子**

```lua
sys.subscribe("SIM_IND", function(status, value)
    -- status的取值有:
    -- RDY SIM卡就绪, value为nil
    -- NORDY 无SIM卡, value为nil
    -- SIM_PIN 需要输入PIN, value为nil
    -- GET_NUMBER 获取到电话号码(不一定有值), value为nil
    -- SIM_WC SIM卡的写入次数统计,掉电归0, value为统计值
    log.info("sim status", status, value)
end)

```

---

### CELL_INFO_UPDATE

基站数据已更新

**额外返回参数**

无

**例子**

```lua
-- 订阅式
sys.subscribe("CELL_INFO_UPDATE", function()
    log.info("cell", json.encode(mobile.getCellInfo()))
end)

```

---

### SCELL_INFO

服务小区额外信息更新

**额外返回参数**

无

**例子**

```lua
-- 订阅式
sys.subscribe("SCELL_INFO", function()
    log.info("service cell", mobile.scell()))
end)

```

---

### IP_READY

已联网

**额外返回参数**

无

**例子**

```lua
-- 联网后会发一次这个消息
sys.subscribe("IP_READY", function(ip, adapter)
    log.info("mobile", "IP_READY", ip, (adapter or -1) == socket.LWIP_GP)
end)

```

---

### IP_LOSE

已断网

**额外返回参数**

无

**例子**

```lua
-- 断网后会发一次这个消息
sys.subscribe("IP_LOSE", function(adapter)
    log.info("mobile", "IP_LOSE", (adapter or -1) == socket.LWIP_GP)
end)

```

---

### NTP_UPDATE

时间已经同步

**额外返回参数**

无

**例子**

```lua
-- 对于电信/移动的卡, 联网后,基站会下发时间,但联通卡不会,务必留意
sys.subscribe("NTP_UPDATE", function()
    log.info("mobile", "time", os.date())
end)

```

---

### CSCON

RRC状态

**额外返回参数**

无

**例子**

```lua
-- state 1 CONNECT 0 IDLE
sys.subscribe("CSCON", function(state)
	log.info("mobile", "CSCON", state)
end)

```

---

### SMS_READY

SMS就绪状态变化

**额外返回参数**

无

**例子**

```lua
-- id 为SIM卡的索引
sys.subscribe("SMS_READY", function(id)
	log.info("mobile", "SMS_READY", id)
end)

```

---

### CC_IND

通话状态变化

**额外返回参数**

无

**例子**

```lua
sys.subscribe("CC_IND", function(status, value)
    log.info("cc status", status, value)
end)

```

---

### RRC_IND

RRC部分信息上报,2025/9/15启用

**额外返回参数**

无

**例子**

```lua
sys.subscribe("RRC_IND", function(event, value, ...)
	log.info("rrc status", event, value, ...)
end)
event目前有
1、"DRX",DRX周期值,后续跟1个参数为具体的DRX周期值,单位ms,目前只有320,640,1280,2560
2、"IDLE_MEAS_THRESHOLD",RRC IDLE下邻区测量阈值,后续跟4个参数为具体的测量阈值,单位dbm
4个参数分别为sIntraSearchP, sNonIntraSearchP, sIntraSearchQ, sNonIntraSearchQ
当rsrp <= sIntraSearchP,启动同频邻区测量,低功耗下功耗有所升高
当rsrp <= sNonIntraSearchP,启动异频邻区测量,低功耗下功耗显著升高
如果sIntraSearchQ不为0,当rsrq <= sIntraSearchQ,启动同频邻区测量,低功耗下功耗有所升高
如果sNonIntraSearchQ不为0,当rsrq <= sNonIntraSearchQ,启动异频邻区测量,低功耗下功耗显著升高

```

---

## icmp



[icmp接口文档页](https://wiki.luatos.com/api/icmp.html)



### PING_RESULT

ping的应答结果

**额外返回参数**

|返回参数类型|解释|
|-|-|
|number|网络适配器id|
|number|往返耗时, 单位ms|
|string|目标IP地址|
|number|TTL值|

**例子**

```lua
sys.subscribe("PING_RESULT", function(adapter, time_used, ip, ttl)
    log.info("icmp", "ping", ip, time_used, ttl)
end)

```

---

## iperf



[iperf接口文档页](https://wiki.luatos.com/api/iperf.html)



### IPERF_REPORT

iperf测试的报告

**额外返回参数**

|返回参数类型|解释|
|-|-|
|number|传输的总字节数|
|number|测试时长, 单位ms|
|number|带宽, 单位kbps|

**例子**

```lua
sys.subscribe("IPERF_REPORT", function(bytes, ms, kbps)
    log.info("iperf", "report", bytes, ms, kbps)
end)

```

---

## mqtt



[mqtt接口文档页](https://wiki.luatos.com/api/mqtt.html)



### MQTT_PONG

收到MQTT服务器的PING响应

**额外返回参数**

|返回参数类型|解释|
|-|-|
|userdata|mqtt客户端对象|

**例子**

```lua
sys.subscribe("MQTT_PONG", function(mqtt_client)
    log.info("mqtt", "pong")
end)

```

---

## socket



[socket接口文档页](https://wiki.luatos.com/api/socket.html)



### NTP_UPDATE

时间已经同步

**额外返回参数**

无

**例子**

```lua
sys.subscribe("NTP_UPDATE", function()
    log.info("socket", "sntp", os.date())
end)

```

---

### NTP_ERROR

时间同步失败

**额外返回参数**

无

**例子**

```lua
sys.subscribe("NTP_ERROR", function()
    log.info("socket", "sntp error")
end)

```

---

## websocket



[websocket接口文档页](https://wiki.luatos.com/api/websocket.html)



### WEBSOCKET_CONNACK

websocket连接建立成功

**额外返回参数**

|返回参数类型|解释|
|-|-|
|userdata|websocket对象|

**例子**

```lua
sys.subscribe("WEBSOCKET_CONNACK", function(wsc)
    log.info("websocket", "connected")
end)

```

---

## nimble



[nimble接口文档页](https://wiki.luatos.com/api/nimble.html)



### BLE_CONN_STATUS

BLE连接状态变化

**额外返回参数**

|返回参数类型|解释|
|-|-|
|boolean|是否已连接, true为连接成功|
|number|底层状态码, 0为成功, 0xff为断开|
|number|附加参数, 保留|

**例子**

```lua
sys.subscribe("BLE_CONN_STATUS", function(connected, status, arg2)
    log.info("ble", "conn status", connected, status)
end)

```

---

### BLE_SCAN_RESULT

BLE扫描到周边设备

**额外返回参数**

|返回参数类型|解释|
|-|-|
|string|设备地址, 7字节二进制(6字节MAC+1字节地址类型)|
|string|设备名称, 无名设备为空字符串|
|table|附加信息, 含rssi(number)字段, 可能含uuids16(table)字段|
|string|厂商自定义数据, 无则为nil|

**例子**

```lua
sys.subscribe("BLE_SCAN_RESULT", function(addr, name, info, mfg_data)
    log.info("ble", "scan", addr:toHex(), name, info.rssi)
end)

```

---

### BLE_CONN_RESULT

BLE发起连接的结果

**额外返回参数**

|返回参数类型|解释|
|-|-|
|boolean|是否成功|
|number|底层状态码, 0为成功|
|number|附加参数, 保留|

**例子**

```lua
sys.subscribe("BLE_CONN_RESULT", function(ok, status, arg2)
    log.info("ble", "conn result", ok, status)
end)

```

---

### BLE_CHR_DISC_RESULT

BLE特征发现(discovery)的结果

**额外返回参数**

|返回参数类型|解释|
|-|-|
|boolean|是否成功|
|number|底层状态码, 0为成功|
|number|已发现的特征数量|

**例子**

```lua
sys.subscribe("BLE_CHR_DISC_RESULT", function(ok, status, count)
    log.info("ble", "chr disc", ok, status, count)
end)

```

---

### BLE_GATT_READ_CHR

BLE读取特征的回调数据(主机/central模式)

**额外返回参数**

|返回参数类型|解释|
|-|-|
|string|读取到的数据内容, 失败为nil. 注意: 从机(peripheral)模式下此消息无额外参数|

**例子**

```lua
sys.subscribe("BLE_GATT_READ_CHR", function(data)
    log.info("ble", "read chr", data and data:toHex() or "nil")
end)

```

---

### BLE_GATT_TX_DATA

BLE收到对端发来的数据(notify/indicate, 主机/central模式)

**额外返回参数**

|返回参数类型|解释|
|-|-|
|string|数据内容, 无数据为nil|

**例子**

```lua
sys.subscribe("BLE_GATT_TX_DATA", function(data)
    log.info("ble", "rx data", data and data:toHex() or "nil")
end)

```

---

### BLE_GATT_WRITE_CHR

BLE特征被对端写入(从机/server模式)

**额外返回参数**

|返回参数类型|解释|
|-|-|
|table|特征信息, 含chr_uuid(string)字段|
|string|对端写入的数据内容|

**例子**

```lua
sys.subscribe("BLE_GATT_WRITE_CHR", function(chr, data)
    log.info("ble", "write", chr.chr_uuid, data:toHex())
end)

```

---

### BLE_SERVER_STATE_UPD

BLE从机(server)状态更新

**额外返回参数**

|返回参数类型|解释|
|-|-|
|number|状态码|

**例子**

```lua
sys.subscribe("BLE_SERVER_STATE_UPD", function(state)
    log.info("ble", "server state", state)
end)

```

---

## sms



[sms接口文档页](https://wiki.luatos.com/api/sms.html)



### SMS_SENT

短信发送结果

**额外返回参数**

|返回参数类型|解释|
|-|-|
|result|boolean 发送结果，成功为true, 失败为false|
|number|rp_cause RP-Cause错误码(3GPP TS 24.011), 0=成功, 1=空号, 30=未知用户, 50=未开通服务(停机)|
|string|rp_cause_str RP-Cause描述字符串|
|number|msg_ref 最后一段的消息参考号, 用于匹配后续的SMS_REPORT回执消息|
|number|error_code SDK错误码(0=成功, 300=设备故障, 330=短信中心未知, 332=无网络服务, 333=网络超时, 500=未知错误)|
|table|msg_refs 所有段的消息参考号列表, 如{10,11,12}, 短信为单段时{5}; 用于匹配每段短信的SMS_REPORT回执|

**例子**

```lua
sys.subscribe("SMS_SENT", function(result, rp_cause, rp_cause_str, msg_ref, error_code, msg_refs)
    log.info("sms send", result, rp_cause, rp_cause_str, msg_ref, error_code)
    if msg_refs then
        for i, ref in ipairs(msg_refs) do
            log.info("sms send", "段", i, "msg_ref", ref)
        end
    end
end)

```

---

### SMS_INC

收到短信

**额外返回参数**

|返回参数类型|解释|
|-|-|
|string|手机号|
|string|短信内容，UTF8编码|

**例子**

```lua
--使用的例子，可多行
-- 接收短信, 支持多种方式, 选一种就可以了
-- 1. 设置回调函数
--sms.setNewSmsCb( function(phone,sms)
    log.info("sms",phone,sms)
end)
-- 2. 订阅系统消息
--sys.subscribe("SMS_INC", function(phone,sms)
    log.info("sms",phone,sms)
end)

```

---

### SMS_REPORT

短信回执(状态报告)

**额外返回参数**

|返回参数类型|解释|
|-|-|
|number|msg_ref 消息参考号, 用于匹配发送的短信|
|number|status 状态码, 0=成功送达, 其他为失败(3GPP TS 23.040 9.2.3.15)|
|string|status_str 状态描述, 如 "SUCCESS"/"FAILED_TEMP_*"/"FAILED_PERM_*"|
|string|phone 接收方手机号|
|string|discharge_time 送达/失败时间, 格式 "YY-MM-DD HH:MM:SS"|

**例子**

```lua
sys.subscribe("SMS_REPORT", function(msg_ref, status, status_str, phone, discharge_time)
    log.info("sms report", msg_ref, status, status_str, phone, discharge_time)
end)

```

---

## softkeyboard



[softkeyboard接口文档页](https://wiki.luatos.com/api/softkeyboard.html)



### SOFT_KB_INC

软件键盘矩阵消息

**额外返回参数**

|返回参数类型|解释|
|-|-|
|number|port, keyboard id 当前固定为0, 可以无视|
|number|data, keyboard 按键 需要配合init的map进行解析|
|number|state, 按键状态 1 为按下, 0 为 释放|

**例子**

```lua
sys.subscribe("SOFT_KB_INC", function(port, data, state)
    -- port 当前固定为0, 可以无视
    -- data, 需要配合init的map进行解析
    -- state, 1 为按下, 0 为 释放
    log.info("keyboard", port, data, state)
end)

```

---

## usbapp



[usbapp接口文档页](https://wiki.luatos.com/api/usbapp.html)



### USB_HID_INC

USB虚拟HID设备的状态变化

**额外返回参数**

|返回参数类型|解释|
|-|-|
|number|事件id: 0未就绪, 1就绪, 2发送完成, 3收到新数据|

**例子**

```lua
sys.subscribe("USB_HID_INC", function(event)
    log.info("usbapp", "hid event", event)
end)

```

---

