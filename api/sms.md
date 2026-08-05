# sms - 短信

**示例**

```lua
-- 注意, Air780E/Air600E/Air780EG/Air780EG均不支持电信卡的短信!!
-- 意思是, 当上述模块搭配电信SIM卡, 无法从模块发出短信, 也无法在模块接收短信
-- 如果是联通卡或者移动卡, 均可收取短信, 但实名制的卡才能发送短信

```

## sms.send(phone, msg, auto_phone_fix, need_report)

异步发送短信

**参数**

|传入值类型|解释|
|-|-|
|string|电话号码,必填|
|string|短信内容,必填|
|bool|是否自动处理电话号号码的格式,默认是按短信内容和号码格式进行自动判断, 设置为false可禁用|
|bool|是否请求短信回执(状态报告),默认false不请求,设为true时接收方成功接收后会收到SMS_REPORT消息|

**返回值**

|返回值类型|解释|
|-|-|
|bool|成功返回true,否则返回false或nil|

**例子**

```lua
-- 短信号码支持2种形式
-- +XXYYYYYYY 其中XX代表国家代码, 中国是86, 推荐使用这种
-- YYYYYYYYY  直接填目标号码, 例如10010, 10086, 或者国内的手机号码
log.info("sms", sms.send("+8613416121234", "Hi, LuatOS - " .. os.date()))

-- 直接使用目标号码, 不做任何自动化处理. 2023.09.21新增
log.info("sms", sms.send("85513416121234", "Hi, LuatOS - " .. os.date()), false)

-- 请求短信回执, 接收方成功接收后会收到 SMS_REPORT 消息
sms.send("+8613416121234", "Hi, LuatOS", true, true)

```

---

## sms.sendLong(phone, msg, auto_phone_fix, need_report).wait()

同步发送短信

**参数**

|传入值类型|解释|
|-|-|
|string|电话号码,必填|
|string|短信内容,必填|
|bool|是否自动处理电话号号码的格式,默认是按短信内容和号码格式进行自动判断, 设置为false可禁用|
|bool|是否请求短信回执(状态报告),默认false不请求,设为true时接收方成功接收后会收到SMS_REPORT消息|

**返回值**

|返回值类型|解释|
|-|-|
|bool|异步等待结果 成功返回true, 否则返回false或nil|

**例子**

```lua
sys.taskInit(function()
    local str = string.rep("1234567890", 50)
    sys.waitUntil("IP_READY")
    -- 发送500bytes的短信
    sms.sendLong("+8613416121234", str).wait()
end)

```

---

## sms.setNewSmsCb(func)

设置新SMS的回调函数

**参数**

|传入值类型|解释|
|-|-|
|function|回调函数, 3个参数, num, txt, metas|

**返回值**

|返回值类型|解释|
|-|-|
|nil|传入是函数就能成功,无返回值|

**例子**

```lua

sms.setNewSmsCb(function(num, txt, metas)
    -- num 手机号码
    -- txt 文本内容
    -- metas 短信的元数据,例如发送的时间,长短信编号
    -- 注意, 长短信会自动合并成一条txt
    log.info("sms", num, txt, metas and json.encode(metas) or "")
end)

```

---

## sms.autoLong(mode)

设置长短信的自动合并功能

**参数**

|传入值类型|解释|
|-|-|
|bool|是否自动合并,true为自动合并,为默认值|

**返回值**

|返回值类型|解释|
|-|-|
|bool|设置后的值|

**例子**

```lua
-- 禁用长短信的自动合并, 一般不需要禁用
sms.autoLong(false)

```

---

## sms.clearLong()

清除长短信缓存

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|int|清理掉的片段数量|

**例子**

```lua
sms.clearLong()

```

---

## sms.unpack(pdu_data)

PDU短信解包

**参数**

|传入值类型|解释|
|-|-|
|string|pdu_data PDU格式的短信数据(hex字符串)|

**返回值**

|返回值类型|解释|
|-|-|
|table|解包后的短信内容|

**例子**

```lua
-- 仅PC模拟器包含这个函数, 真机不需要这个函数
local pdu = "0491680010F50400069110102143650008024F60"
local phone, txt, metas = sms.unpack(pdu)
log.info("sms unpack", phone, txt, metas and json.encode(metas) or "")

```

---

## sms.debug(enable)

设置短信模块的调试模式

**参数**

|传入值类型|解释|
|-|-|
|bool|enable 是否启用调试模式,true为启用,false为禁用|

**返回值**

|返回值类型|解释|
|-|-|
|nil|无返回值|

**例子**

```lua
-- 启用短信调试模式,会输出更多日志信息
sms.debug(true)
-- 禁用短信调试模式
sms.debug(false)

```

---

## sms.setReportCb(func)

设置短信回执(状态报告)回调函数

**参数**

|传入值类型|解释|
|-|-|
|function|回调函数, 5个参数: msg_ref, status, status_str, phone, discharge_time|

**返回值**

|返回值类型|解释|
|-|-|
|nil|传入是函数就能成功,无返回值|

**例子**

```lua
sms.setReportCb(function(msg_ref, status, status_str, phone, discharge_time)
    -- msg_ref:        消息参考号(number), 用于匹配发送的短信
    -- status:         状态码(number), 0=成功送达
    -- status_str:     状态描述(string), 如 "SUCCESS"/"FAILED_TEMP_*"/"FAILED_PERM_*"
    -- phone:          接收方手机号(string)
    -- discharge_time: 送达/失败时间(string), 格式 "YY-MM-DD HH:MM:SS"
    log.info("sms report", msg_ref, status, status_str, phone, discharge_time)
end)

```

---

