# exs_adxl34x - ADXL345/ADXL346 三轴加速度传感器扩展库

**示例**

```lua
本文件为 ADXL345/ADXL346 三轴加速度传感器（ADI 出品）的 LuatOS 扩展库。

=== 对外接口 ===
1、exs_adxl34x.setup(model, config)  初始化 ADXL345/ADXL346
2、exs_adxl34x.get_data()            读取三轴加速度数据
3、exs_adxl34x.set_range(range)      切换量程
4、exs_adxl34x.set_odr(hz)           切换输出速率
5、exs_adxl34x.int_config(int, cfg)  配置中断事件
6、exs_adxl34x.get_int_source()      读取中断源
7、exs_adxl34x.sleep()               进入待机模式
8、exs_adxl34x.wakeup()              从待机模式唤醒
9、exs_adxl34x.close()               关闭传感器
10、exs_adxl34x.version()            获取版本号

=== 版本更新说明 ===
版本号：202607180900
1、更新时间：2026-07-18
2、更新内容：
        修复 close() 未注销 GPIO 中断，传感器关闭后 INT 引脚变化导致死机
        新增常量中文注释

版本号：202607170900
1、更新时间：2026-07-17
2、更新内容：
        i2c_bus_recovery 增加 SDA 释放检测，提前结束脉冲循环
        i2c_write/i2c_read 增加 I2C 总线卡死自动检测与恢复
        硬件 I2C 恢复后自动重新 i2c.setup()
        新增 exs_adxl34x.close() 接口，关闭传感器并释放资源
        新增 exs_adxl34x.sleep()/wakeup() 低功耗接口，替换 soft_reset()

版本号：202607141200
1、更新时间：2026-07-14
2、更新内容：
        初版，实现 ADXL345/ADXL346 驱动所有基础功能
        初始化接口使用 setup 命名，统一 TM16xx 系列命名规范
        支持软件 I2C 和硬件 I2C 两种通信模式（SPI 未适配）
        支持量程切换（±2g / ±4g / ±8g / ±16g）
        支持输出速率切换（0.78Hz~3200Hz）
        支持自动器件地址检测
        支持软件复位

=== 使用示例 ===
-- I2C 软件模式 + 中断
local function adxl34x_cb(data)
    log.info("exs_adxl34x", string.format("X=%.3f Y=%.3f Z=%.3f g", data.x, data.y, data.z))
end
local result = exs_adxl34x.setup("I2C", {
    scl = 31, sda = 30,
    range = "2g", odr = 100,
    int1 = {int_gpio = 10, data_ready = true, cb = adxl34x_cb},
})

```

## exs_adxl34x.setup(model, config)

初始化 ADXL345/ADXL346 加速度传感器

**参数**

|传入值类型|解释|
|-|-|
|string|model 通信模式，当前仅支持 "I2C"（SPI 未适配）|
|return|boolean|

**返回值**

无

**例子**

无

---

## exs_adxl34x.get_data()

读取三轴加速度数据

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|table|or nil {x, y, z} 单位 g|

**例子**

无

---

## exs_adxl34x.set_range(range)

切换量程

**参数**

|传入值类型|解释|
|-|-|
|string|range "2g"、"4g"、"8g"、"16g"|

**返回值**

无

**例子**

无

---

## exs_adxl34x.set_odr(hz)

切换输出数据速率

**参数**

|传入值类型|解释|
|-|-|
|number|hz 0.78~3200|

**返回值**

无

**例子**

无

---

## exs_adxl34x.int_config(int, config)

配置中断事件

**参数**

|传入值类型|解释|
|-|-|
|string|int "int1" 或 "int2"|
|table|config 事件配置|

**返回值**

无

**例子**

无

---

## exs_adxl34x.get_int_source()

读取中断源

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|table|or nil 事件名称数组|

**例子**

无

---

## exs_adxl34x.sleep()

进入待机模式（低功耗）

**参数**

无

**返回值**

无

**例子**

无

---

## exs_adxl34x.wakeup()

从待机模式唤醒

**参数**

无

**返回值**

无

**例子**

无

---

## exs_adxl34x.close()

关闭传感器

**参数**

无

**返回值**

无

**例子**

无

---

## exs_adxl34x.version()

获取版本号

**参数**

|传入值类型|解释|
|-|-|
|return|string|

**返回值**

无

**例子**

无

---

