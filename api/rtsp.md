# rtsp - RTSP 直播推流

**示例**

```lua
-- RTSP推流示例
local rtsp = rtsp.create("rtsp://example.com:554/stream")
rtsp:setCallback(function(state, ...)
    if state == rtsp.STATE_CONNECTED then
        print("已连接到推流服务器")
    elseif state == rtsp.STATE_PLAYING then
        print("已开始推流")
    elseif state == rtsp.STATE_ERROR then
        print("出错:", ...)
    end
end)
rtsp:connect()

-- 开始处理
rtsp:start()

-- 30秒后停止
sys.wait(30000)
rtsp:stop()

-- 断开连接
rtsp:disconnect()
rtsp:destroy()

```

## rtsp.create(url)

创建RTSP推流上下文

**参数**

|传入值类型|解释|
|-|-|
|string|url RTSP服务器地址, 格式: rtsp://host:port/stream|

**返回值**

|返回值类型|解释|
|-|-|
|userdata|RTSP上下文对象|

**例子**

```lua
local rtsp = rtsp.create("rtsp://example.com:554/stream")

```

---

## rtsp:setCallback(func)

设置RTSP状态回调函数

**参数**

|传入值类型|解释|
|-|-|
|function|func 回调函数, 参数为 (state, ...) |

**返回值**

|返回值类型|解释|
|-|-|
|nil|无返回值|

**例子**

```lua
rtsp:setCallback(function(state, ...)
    if state == rtsp.STATE_IDLE then
        print("空闲状态")
    elseif state == rtsp.STATE_CONNECTING then
        print("正在连接")
    elseif state == rtsp.STATE_OPTIONS then
        print("发送OPTIONS")
    elseif state == rtsp.STATE_DESCRIBE then
        print("发送DESCRIBE")
    elseif state == rtsp.STATE_SETUP then
        print("发送SETUP")
    elseif state == rtsp.STATE_PLAY then
        print("发送PLAY请求")
    elseif state == rtsp.STATE_PLAYING then
        print("正在推流")
    elseif state == rtsp.STATE_DISCONNECTING then
        print("正在断开")
    elseif state == rtsp.STATE_ERROR then
        print("错误:", ...)
    end
end)

```

---

## rtsp:connect()

连接到RTSP服务器

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|boolean|成功返回true, 失败返回false|

**例子**

```lua
local ok = rtsp:connect()
if ok then
    print("连接请求已发送")
else
    print("连接失败")
end

```

---

## rtsp:disconnect()

断开RTSP连接

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|boolean|成功返回true, 失败返回false|

**例子**

```lua
rtsp:disconnect()

```

---

## rtsp:start()

处理RTSP事件

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|nil|无返回值|

**例子**

```lua
rtsp:start()

```

---

## rtsp:stop()

停止处理RTSP事件

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|nil|无返回值|

**例子**

```lua
rtsp:stop()

```

---

## rtsp:getState()

获取RTSP连接状态

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|int|当前状态值|

**例子**

```lua
local state = rtsp:getState()
if state == rtsp.STATE_CONNECTED then
    print("已连接")
elseif state == rtsp.STATE_PLAYING then
    print("正在推流")
end

```

---

## rtsp:setSPS(sps_data)

设置H.264 SPS参数

**参数**

|传入值类型|解释|
|-|-|
|string|sps_data 或 |
|userdata|sps_data H.264序列参数集数据|

**返回值**

|返回值类型|解释|
|-|-|
|boolean|成功返回true, 失败返回false|

**例子**

```lua
local sps = string.fromBinary("\x67\x42...") -- H.264 SPS数据
rtsp:setSPS(sps)

```

---

## rtsp:setPPS(pps_data)

设置H.264 PPS参数

**参数**

|传入值类型|解释|
|-|-|
|string|pps_data 或 |
|userdata|pps_data H.264图像参数集数据|

**返回值**

|返回值类型|解释|
|-|-|
|boolean|成功返回true, 失败返回false|

**例子**

```lua
local pps = string.fromBinary("\x68\xCB...") -- H.264 PPS数据
rtsp:setPPS(pps)

```

---

## rtsp:pushFrame(frame_data, timestamp)

推送H.264视频帧

**参数**

|传入值类型|解释|
|-|-|
|string|frame_data 或 |
|userdata|frame_data H.264编码的视频帧数据|
|int|timestamp 时间戳(毫秒), 可选，为0则使用内部时间戳|

**返回值**

|返回值类型|解释|
|-|-|
|int|成功时返回已发送或已入队的字节数, 失败返回负数|

**例子**

```lua
-- 持续推送H.264帧
local frame_data = ... -- 获取H.264帧数据
local timestamp = sys.now() % 0x100000000
local ret = rtsp:pushFrame(frame_data, timestamp)
if ret >= 0 then
    print("已发送", ret, "字节")
else
    print("发送失败:", ret)
end

```

---

## rtsp:getStats()

获取RTSP统计信息

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|table|统计信息表|

**例子**

```lua
local stats = rtsp:getStats()
print("已发送字节数:", stats.bytes_sent)
print("已发送视频帧数:", stats.video_frames_sent)
print("已发送RTP包数:", stats.rtp_packets_sent)

```

---

## rtsp:setTransportMode(mode)

设置RTP传输模式

**参数**

|传入值类型|解释|
|-|-|
|string|mode 传输模式: "udp", "tcp", "udp_fec"|

**返回值**

|返回值类型|解释|
|-|-|
|boolean|成功返回true，失败返回false|

**例子**

```lua
-- 使用TCP传输模式（适合外网）
rtsp:setTransportMode("tcp")
-- 使用UDP传输模式（适合局域网，默认）
rtsp:setTransportMode("udp")
-- 使用UDP+FEC传输模式（平衡方案）
rtsp:setTransportMode("udp_fec")

```

---

## rtsp:getNetworkStats()

获取网络质量统计信息

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|table|网络统计信息，包含:|

**例子**

无

---

## rtsp:setNetworkStatsCallback(func)

设置网络统计回调函数

**参数**

|传入值类型|解释|
|-|-|
|function|func 回调函数，参数为统计信息table|

**返回值**

|返回值类型|解释|
|-|-|
|boolean|成功返回true，失败返回false|

**例子**

```lua
rtsp:setNetworkStatsCallback(function(stats)
    print("丢包率:", stats.packet_loss_rate)
    print("延迟:", stats.rtt_ms)
end)

```

---

## rtsp:setFECParam(param, value)

设置FEC参数

**参数**

|传入值类型|解释|
|-|-|
|string|param 参数名称: "redundancy"|
|number|value 参数值 (redundancy: 0-100)|

**返回值**

|返回值类型|解释|
|-|-|
|boolean|成功返回true，失败返回false|

**例子**

```lua
-- 设置FEC冗余度为30%
rtsp:setFECParam("redundancy", 30)

```

---

## rtsp:destroy()

销毁RTSP上下文，释放所有资源

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|nil|无返回值|

**例子**

```lua
rtsp:destroy()

```

---

