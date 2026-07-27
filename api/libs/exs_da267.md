# exs_da267 - DA267 三轴加速度传感器扩展库（DA267）

**示例**

```lua
本文件为 DA267 三轴加速度传感器的 LuatOS 扩展库，核心功能为：
1、初始化 DA267，配置 I2C 通信参数和测量量程
2、读取加速度原始数据和转换后的重力加速度值（g值）
3、读取计步数并清零计步器
4、配置运动检测中断和阈值
5、启用/禁用计步器功能
6、实现运动状态管理，支持静止/运动状态判断

本文件的对外接口有 15 个：
1、exs_da267.setup(init_cfg)：初始化 DA267
2、exs_da267.get_data()：读取三轴加速度数据（单位：g）
3、exs_da267.get_steps()：读取计步数
4、exs_da267.reset_steps()：清零计步器
5、exs_da267.set_range(range)：设置测量量程
6、exs_da267.set_int_threshold(x, y, z)：设置运动检测中断阈值
7、exs_da267.enable_step_counter(enable)：启用/禁用计步器
8、exs_da267.set_callback(callback)：设置中断回调函数
9、exs_da267.get_chip_id()：获取芯片ID
10、exs_da267.enable_motion(enable)：启用/禁用运动状态管理
11、exs_da267.is_moving()：获取当前运动状态
12、exs_da267.set_motion_params(params)：设置运动状态管理参数
13、exs_da267.get_config()：获取当前配置信息
14、exs_da267.close()：关闭传感器
15、exs_da267.version()：获取版本号

-- 版本更新说明
-- 版本号：202607201700
-- 1、更新时间：2026-07-20 17:00
-- 2、更新内容
--    优化 DA267 运动状态判断机制，去掉运动状态管理中的超时参数

-- 版本号：202607171813700
-- 1、更新时间：2026-07-17 18:13
-- 2、更新内容
--    初版，实现 DA267 传感器驱动所有基础功能
--    支持 I2C 通信接口
--    支持 ±2g/±4g/±8g/±16g 四档量程
--    支持读取三轴加速度数据（单位：g）
--    支持计步器功能，包括读取和清零计步数
--    支持运动状态管理，基于中断历史窗口判断静止/运动状态
--    支持设置运动检测中断阈值
--    支持启用/禁用计步器功能
--    支持获取传感器配置信息

```

## exs_da267.version()

获取库版本信息

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|string|库版本号，格式：年月日时分|

**例子**

```lua
log.info("da267", "version:", exs_da267.version())

```

---

## exs_da267.setup(param)

初始化 DA267 传感器

**参数**

|传入值类型|解释|
|-|-|
|param|param table 初始化参数配置表|

**返回值**

无

**例子**

无

---

## exs_da267.get_data()

读取三轴加速度数据

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|table|or nil {x, y, z} 单位 g，失败返回nil|

**例子**

```lua
local data = exs_da267.get_data()
if data then
    log.info("da267", string.format("X=%.3f Y=%.3f Z=%.3f g", data.x, data.y, data.z))
end

```

---

## exs_da267.get_steps()

读取计步数

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|number/nil|成功返回计步数，失败返回nil|

**例子**

```lua
local steps = exs_da267.get_steps()
if steps then
    log.info("da267", "steps:", steps)
end

```

---

## exs_da267.reset_steps()

清零计步数

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|boolean|成功返回true，失败返回false|

**例子**

```lua
exs_da267.reset_steps()
if exs_da267.reset_steps() then
    log.info("da267", "计步数已清零")
end

```

---

## exs_da267.set_range(range)

设置测量量程

**参数**

|传入值类型|解释|
|-|-|
|param|range number 量程，支持2/4/8/16（±g）|

**返回值**

|返回值类型|解释|
|-|-|
|boolean|成功返回true，失败返回false|

**例子**

```lua
exs_da267.set_range(exs_da267.RANGE_4G)  -- 设置为±4g量程
@note 量程选择建议：
      - RANGE_2G (±2g, 3.91mg/LSB)：微小震动检测，用于检测轻微震动的场景，例如用手敲击桌面
      - RANGE_4G (±4g, 7.81mg/LSB)：运动检测，用于电动车或汽车行驶时的检测和人行走和跑步时的检测
      - RANGE_8G (±8g, 15.63mg/LSB)：跌倒检测，用于人或物体瞬间跌倒时的检测，加速度量程8g；
      - RANGE_16G (±16g, 31.25mg/LSB)：适合高冲击场景（如安全监测、碰撞检测）

```

---

## exs_da267.set_int_threshold(x, y, z)

设置运动检测中断阈值

**参数**

|传入值类型|解释|
|-|-|
|param|x number X轴阈值，范围1-255，越小越敏感，可选，默认6|
|param|y number Y轴阈值，范围1-255，越小越敏感，可选，默认6|
|param|z number Z轴阈值，范围1-255，越小越敏感，可选，默认6|

**返回值**

|返回值类型|解释|
|-|-|
|boolean|成功返回true，失败返回false|

**例子**

```lua
-- 设置默认敏感度（6）
exs_da267.set_int_threshold(6, 6, 6)

-- 检测微小振动（3）
exs_da267.set_int_threshold(3, 3, 3)

-- 检测较大动作（16）
exs_da267.set_int_threshold(16, 16, 16)

@note 阈值单位为LSB（最低有效位），实际触发加速度=阈值×量程LSB系数
        各量程LSB系数：±2g=3.91mg, ±4g=7.81mg, ±8g=15.63mg, ±16g=31.25mg
        示例(阈值=6)：6*(±2g)→23.5mg, 6*(±4g)→46.9mg, 6*(±8g)→93.8mg, 6*(±16g)→187.5mg
        规律：量程越大，相同阈值的触发加速度越大，灵敏度越低
        阈值与量程的关系说明：
        - 量程决定了传感器测量加速度的范围（如±2g、±4g等）
        - 阈值决定了触发运动检测中断的加速度变化幅度
        - 相同阈值在不同量程下，实际触发加速度不同（量程越大，触发加速度越大）

        各阈值范围对应使用场景：
        - 1-8：高灵敏（微小震动检测，用于检测轻微震动的场景，例如用手敲击桌面）
        - 9-24：中灵敏（运动检测，用于电动车或汽车行驶时的检测和人行走和跑步时的检测）
        - 25-48：较高灵敏（跌倒检测，用于人或物体瞬间跌倒时的检测）
        - 49-255：低灵敏（高冲击场景检测，如安全监测、碰撞检测）

```

---

## exs_da267.enable_step_counter(enable)

启用/禁用计步器功能

**参数**

|传入值类型|解释|
|-|-|
|param|enable boolean true启用，false禁用|

**返回值**

|返回值类型|解释|
|-|-|
|boolean|成功返回true，失败返回false|

**例子**

```lua
exs_da267.enable_step_counter(true)  -- 启用计步器
if exs_da267.enable_step_counter(false) then
    log.info("da267", "计步器已禁用")
end

```

---

## exs_da267.set_callback(callback)

设置中断回调函数

**参数**

|传入值类型|解释|
|-|-|
|param|callback function 中断回调函数|

**返回值**

|返回值类型|解释|
|-|-|
|boolean|成功返回true，失败返回false|

**例子**

```lua
-- 定义回调函数
local function da267_interrupt_callback()
    log.info("da267", "中断触发")
    local data = exs_da267.get_data()
    if data then
        log.info("da267", string.format("X=%.3f Y=%.3f Z=%.3f g", data.x, data.y, data.z))
    end
end

-- 设置回调函数
exs_da267.set_callback(da267_interrupt_callback)

```

---

## exs_da267.get_chip_id()

获取 DA267 芯片ID（用于芯片识别和自检）

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|number/nil|成功返回芯片ID（DA267 为 0x13），失败返回nil|

**例子**

```lua
local id = exs_da267.get_chip_id()
if id then
    log.info("da267", "chip_id:", string.format("0x%02X", id))
end
local chip_id = exs_da267.get_chip_id()
if chip_id == 0x13 then
    log.info("da267", "芯片ID验证成功")
else
    log.error("da267", "芯片ID验证失败")
end

```

---

## exs_da267.enable_motion(enable)

启用/禁用运动状态管理

**参数**

|传入值类型|解释|
|-|-|
|param|enable boolean 是否启用运动状态管理|

**返回值**

|返回值类型|解释|
|-|-|
|boolean|操作成功返回true，失败返回false|

**例子**

```lua
exs_da267.enable_motion(true)  -- 启用运动状态管理
exs_da267.enable_motion(false) -- 禁用运动状态管理
if exs_da267.enable_motion(true) then
    log.info("da267", "运动状态管理已启用")
end

```

---

## exs_da267.is_moving()

获取当前运动状态

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|boolean|当前运动状态，true=运动，false=静止|

**例子**

```lua
local state = exs_da267.is_moving()
log.info("exs_da267", "运动状态:", state)
if exs_da267.is_moving() then
    log.info("da267", "设备正在运动")
else
    log.info("da267", "设备处于静止状态")
end

```

---

## exs_da267.set_motion_params(params)

设置运动状态管理参数

**参数**

|传入值类型|解释|
|-|-|
|table|params 参数配置表|

**返回值**

无

**例子**

无

---

## exs_da267.get_config()

获取当前配置信息

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|table/nil|成功返回当前配置表，失败返回nil|

**例子**

```lua
local config = exs_da267.get_config()
if config then
    log.info("da267", "range:", config.range, "sensitivity:", config.sensitivity)
end
local config = exs_da267.get_config()
if config then
    log.debug("da267", json.encode(config))
end

```

---

## exs_da267.close()

关闭 DA267 传感器

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|boolean|成功返回true，失败返回false|

**例子**

```lua
exs_da267.close()

```

---

