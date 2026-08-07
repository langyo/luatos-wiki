# exs_opt3001 - OPT3001 数字环境光传感器驱动扩展库

**示例**

```lua
本扩展库提供 TI OPT3001 数字环境光传感器的 LuatOS 驱动，功能包括：
1、初始化（I2C 通信配置、厂商 ID/设备 ID 校验、默认配置加载）
2、数据读取（单次/连续测量模式、照度 lux 值计算）
3、阈值中断（上限/下限阈值设置与报警）
4、配置管理（测量模式、转换时间、满量程、中断极性等）
5、软件复位（恢复默认配置）

对外接口 9 个：
- exs_opt3001.setup(config)：初始化
- exs_opt3001.get_data()：读取数据
- exs_opt3001.close()：释放资源
- exs_opt3001.version()：获取版本号
- exs_opt3001.set_threshold(low, high)：设置阈值
- exs_opt3001.get_threshold()：读取阈值
- exs_opt3001.set_config(cfg)：配置参数
- exs_opt3001.get_config()：读取配置
- exs_opt3001.soft_reset()：软件复位

=== 版本更新说明 ===
-- 版本号：202608061000
-- 1、更新时间：2026-08-06
-- 2、更新内容：
--   - 正式发布版本
--   - 支持硬件 I2C 和软件 I2C
--   - 支持单次/连续测量模式
--   - 支持自动/手动满量程选择
--   - 支持阈值中断功能
--   - 支持 I2C 总线恢复（9 时钟脉冲 + SDA 释放检测）
--   - 支持 9 个对外接口（setup/get_data/close/version/set_threshold/get_threshold/set_config/get_config/soft_reset）

```

## exs_opt3001.setup(config)

初始化 OPT3001

**参数**

|传入值类型|解释|
|-|-|
|param|table config|

**返回值**

无

**例子**

无

---

## exs_opt3001.get_data()

读取环境光照度

**参数**

|传入值类型|解释|
|-|-|
|return|table/nil|

**返回值**

无

**例子**

无

---

## exs_opt3001.close()

释放资源

**参数**

无

**返回值**

无

**例子**

无

---

## exs_opt3001.set_threshold(low, high)

设置照度阈值

**参数**

|传入值类型|解释|
|-|-|
|param|number low|

**返回值**

无

**例子**

无

---

## exs_opt3001.get_threshold()

读取当前阈值

**参数**

|传入值类型|解释|
|-|-|
|return|table/nil|

**返回值**

无

**例子**

无

---

## exs_opt3001.set_config(cfg)

配置测量参数

**参数**

|传入值类型|解释|
|-|-|
|param|table cfg|

**返回值**

无

**例子**

无

---

## exs_opt3001.get_config()

读取当前配置

**参数**

|传入值类型|解释|
|-|-|
|return|table/nil|

**返回值**

无

**例子**

无

---

## exs_opt3001.version()

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

