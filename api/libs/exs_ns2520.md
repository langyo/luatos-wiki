# exs_ns2520 - NS2520 气压传感器扩展库（NS2520）

**示例**

```lua
本文件为 NS2520 气压传感器的 LuatOS 扩展库，核心功能为：
1、初始化 NS2520，配置 I2C 通信参数和过采样率
2、读取气压和温度数据，自动完成补偿计算
3、动态调整过采样率
4、关闭传感器（进入待机）

本文件的对外接口有 7 个：
1、exs_ns2520.setup(init_cfg)：初始化 NS2520
2、exs_ns2520.get_data()：读取气压和温度
3、exs_ns2520.get_pressure()：单次读取气压（hPa）
4、exs_ns2520.get_temperature()：单次读取温度（℃）
5、exs_ns2520.set_osr(prs_osr, tmp_osr)：设置过采样率
6、exs_ns2520.close()：关闭传感器（进入待机）
7、exs_ns2520.version()：获取版本号

-- 版本更新说明
-- 版本号：202607161400
-- 1、更新时间：2026-07-16 14:00
-- 2、更新内容
--    初版，实现 NS2520 驱动所有基础功能
--    遵循 exs_ 扩展库设计规范
--    支持 I2C 通信重试机制
--    支持校准系数自动读取和补偿计算
--    支持过采样率动态配置（0~7 共 8 级）
--    支持单次读取气压/温度，支持同时读取两项数据
--    支持关闭/待机模式

```

## exs_ns2520.setup(init_cfg)

初始化 NS2520 气压传感器，配置 I2C 通信参数和过采样率

**参数**

|传入值类型|解释|
|-|-|
|table|init_cfg 初始化配置表|

**返回值**

无

**例子**

无

---

## exs_ns2520.get_data()

读取气压和温度数据，一次I2C通信获取两项数据

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|table/nil|成功返回{pressure:气压值(number,300~1200hPa),temperature:温度值(number,-40~85℃)}，失败返回nil|

**例子**

```lua
local data = exs_ns2520.get_data()
if data then
    log.info("ns2520", string.format("气压:%.2f hPa, 温度:%.2f ℃", data.pressure, data.temperature))
end

```

---

## exs_ns2520.get_pressure()

单次读取气压值

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|number/nil|补偿后的气压值(hPa)，失败返回nil|

**例子**

```lua
local pressure = exs_ns2520.get_pressure()
if pressure then
    log.info("ns2520", string.format("气压:%.2f hPa", pressure))
end

```

---

## exs_ns2520.get_temperature()

单次读取温度值

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|number/nil|补偿后的温度值(℃)，失败返回nil|

**例子**

```lua
local temp = exs_ns2520.get_temperature()
if temp then
    log.info("ns2520", string.format("温度:%.2f ℃", temp))
end

```

---

## exs_ns2520.set_osr(prs_osr, tmp_osr)

设置过采样率，在线修改气压和温度的过采样率，无需重新初始化

**参数**

|传入值类型|解释|
|-|-|
|param|prs_osr number 气压过采样率0~7，可选，不传保持当前值。手册Table9推荐：0=1x(5Pa/3μA)、4=16x(~1.2Pa/22μA)、6=64x(~0.6Pa/200μA)|
|param|tmp_osr number 温度过采样率0~7，可选，不传保持当前值。手册推荐1x即可满足所有场景精度要求，更大值可提高温度精度但增加测量时间|
|return|nil|

**返回值**

无

**例子**

```lua
exs_ns2520.set_osr(6, 6)   -- 64x高精度，适合厘米级高度分辨率场景
exs_ns2520.set_osr(0, 0)   -- 1x低功耗，适合仅判断气压趋势场景

```

---

## exs_ns2520.close()

关闭传感器（进入待机模式），关闭后需重新setup才能使用

**参数**

|传入值类型|解释|
|-|-|
|return|nil|

**返回值**

无

**例子**

```lua
exs_ns2520.close()

```

---

## exs_ns2520.version()

获取 exs_ns2520 库的版本号

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|string|版本号字符串，格式为 "yyyymmddhhmm"|

**例子**

```lua
local ver = exs_ns2520.version()
log.info("exs_ns2520", "版本号:", ver)

```

---

