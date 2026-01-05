# exremotecam - exremotecam 远程摄像头OSD控制扩展库，提供摄像头OSD文字显示设置和拍照功能。

**示例**

```lua
注：在使用exremotecam 扩展库时，需要确保网络连接正常，能够访问到目标摄像头。

本文件的对外接口有2个：
1、exremotecam.OSDsetup(Brand, Host, channel, text, X, Y)：设置摄像头OSD文字显示
-- 参数说明：
--   Brand: 摄像头品牌，当前仅支持"Dhua"(大华)
--   Host: 摄像头/NVR的IP地址
--   channel: 摄像头通道号
--   text: OSD文本内容，需用竖线分隔，格式如"1111|2222|3333|4444"
--   X: 显示位置的X坐标
--   Y: 显示位置的Y坐标

2、exremotecam.getphoto(Brand, Host, channel)：控制摄像头拍照
-- 参数说明：
--   Brand: 摄像头品牌，当前仅支持"Dhua"(大华)
--   Host: 摄像头/NVR的IP地址
--   channel: 摄像头通道号
-- 返回：若SD卡可用，则图片保存为/sd/1.jpeg

```

## split_string_by_pipe(input_str,return_type)

按竖线(|)分割字符串，支持多种返回格式

**参数**

|传入值类型|解释|
|-|-|
|string|input_str 要分割的字符串，格式如"1111\|2222\|3333"|
|string/number|return_type 返回类型，可选值：|

**返回值**

无

**例子**

无

---

## ElementJudg(Data, number)

解析并验证OSD显示元素，确保不超出最大显示行数

**参数**

|传入值类型|解释|
|-|-|
|string|Data 竖线分隔的OSD文本内容，格式如"1111\|2222\|3333"|
|number|number 最大允许显示的行数|

**返回值**

|返回值类型|解释|
|-|-|
|table|分割后的所有OSD元素数组|

**例子**

```lua
local osd_elements = ElementJudg("行1|行2|行3|行4", 3)
-- 输出: "超出显示的范围,只能显示3行"
-- 返回: {"行1", "行2", "行3", "行4"}

注意事项:
1. 函数会打印所有解析到的元素及其索引
2. 当元素数量超过最大行数时，会记录警告日志
3. 无论是否超出限制，都会返回完整的元素数组

```

---

## urlencode(str)

URL编码函数，用于将字符串转换为符合URL标准的编码格式

**参数**

|传入值类型|解释|
|-|-|
|string|str 需要进行URL编码的字符串|

**返回值**

|返回值类型|解释|
|-|-|
|string|编码后的URL安全字符串，如果输入为nil则返回空字符串|

**例子**

```lua
    local encoded = urlencode("Hello World!")
    -- 输出: "Hello+World%21"

```

---

## CameraHA1(username,realm,password)

计算Digest认证中的HA1值，用于网络摄像头的身份验证

**参数**

|传入值类型|解释|
|-|-|
|string|username 用户名|
|string|realm 认证域，由服务器在401响应中提供|
|string|password 用户密码|

**返回值**

|返回值类型|解释|
|-|-|
|string|计算得到的HA1值（小写的MD5哈希值）|

**例子**

```lua
    local ha1 = CameraHA1("admin", "realm", "123456")
    -- 输出: md5("admin:realm:123456")的小写哈希值

```

---

## handle_digest_auth(Host,url,params,headers,HA2)

处理Digest认证，仅在收到401响应时调用

**参数**

|传入值类型|解释|
|-|-|
|string|Host 摄像头的IP地址|
|string|url 请求的URL路径|
|string|params 请求参数|
|table|headers 第一次HTTP请求返回的头部信息|
|string|HA2 预先计算好的HA2值|

**返回值**

|返回值类型|解释|
|-|-|
|boolean,|table 认证是否成功, 更新后的请求头部|

**例子**

```lua
    local code, headers, body = http.request("GET", "http://192.168.1.100/cgi-bin/test", initial_headers).wait()
    if code == 401 then
        local success, updated_headers = handle_digest_auth("192.168.1.100", "/cgi-bin/test", "param=value", headers, "ha2_value")
        if success then
            -- 使用更新后的头部发送第二次请求
        end
    end

```

---

## DH_set_osd_module(Host,Data,TextAlign,channel,x,y)

设置大华(Dahua)摄像头的OSD(屏幕显示)模块

**参数**

|传入值类型|解释|
|-|-|
|string|Host 摄像头的IP地址|
|string|Data 要显示的OSD文本内容|
|number|TextAlign OSD文本对齐方式，默认为全局的DH_TextAlign|
|number|channel 摄像头通道号，默认为全局的DH_channel|
|number|x OSD显示的X坐标，默认为0|
|number|y OSD显示的Y坐标，默认为0|

**返回值**

|返回值类型|解释|
|-|-|
|nil|无返回值，函数通过日志输出执行结果|

**例子**

```lua
    DH_set_osd_module("192.168.1.100", "温度: 25℃", 0, 1, 100, 200)
    -- 功能: 在IP为192.168.1.100的摄像头通道1上，坐标(100,200)处显示"温度: 25℃"

```

---

## OSDsetup(Brand,Host,channel,text,X,Y)

设置摄像头OSD(屏幕显示)文字功能

**参数**

|传入值类型|解释|
|-|-|
|string|Brand 摄像头品牌，当前仅支持: "Dhua" - 大华|
|string|Host 摄像头/NVR的IP地址|
|number|channel 摄像头通道号（主要用于NVR）|
|string|text OSD文本内容，需用竖线分隔，格式如"1111\|2222\|3333\|4444"，大华最多显示13行|
|number|X 显示位置的X坐标|
|number|Y 显示位置的Y坐标|

**返回值**

|返回值类型|解释|
|-|-|
|无|无返回值|

**例子**

```lua
-- 大华摄像头OSD测试
OSDsetup("Dhua", "192.168.0.163", 0, "行1|行2|行3", 0, 2000)

-- 多通道NVR示例
OSDsetup("Dhua", "192.168.0.200", 1, "温度: 25℃|湿度: 60%", 100, 50)

```

---

## DHPicture(Host,channel)

大华摄像头拍照功能，获取指定通道的快照图片

**参数**

|传入值类型|解释|
|-|-|
|string|Host 摄像头/NVR的IP地址|
|number|channel 摄像头通道号|

**返回值**

|返回值类型|解释|
|-|-|
|无|无返回值，若SD卡可用则图片保存为/sd/1.jpeg|

**例子**

```lua
-- 获取大华摄像头通道0的快照图片
DHPicture("192.168.1.108", 0)

-- 获取大华NVR通道1的快照图片
DHPicture("192.168.0.200", 1)

```

---

## getphoto(Brand,Host,channel)

多品牌摄像头拍照通用接口，根据品牌调用对应厂商的拍照功能

**参数**

|传入值类型|解释|
|-|-|
|string|Brand 摄像头品牌，当前仅支持: "Dhua" - 大华|
|string|Host 摄像头/NVR的IP地址|
|number|channel 摄像头通道号|

**返回值**

|返回值类型|解释|
|-|-|
|无|无返回值，若SD卡可用则图片保存为/sd/1.jpeg|

**例子**

```lua
-- 获取大华摄像头通道0的快照图片
getphoto("Dhua", "192.168.1.108", 1)

-- 获取大华NVR通道1的快照图片
getphoto("Dhua", "192.168.0.200", 1)

```

---

