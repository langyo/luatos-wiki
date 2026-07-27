# exs_yhm2712a - exs_yhm2712a扩展库

**示例**

```lua
-- 应用场景
本扩展库适用于集成了YHM2712A充电IC的设备，使用前需要手动配置YHM2712A的CMD引脚。

-- 用法实例
本扩展库对外提供了以下7个接口：
1）初始化YHM2712A通信引脚并设置参数 exs_yhm2712a.setup(init_cfg)
2）开启充电 exs_yhm2712a.start()
3）关闭充电 exs_yhm2712a.stop()
4）获取充电系统状态信息 exs_yhm2712a.status()
5）注册事件回调函数 exs_yhm2712a.on(func)
6）进入船运模式 exs_yhm2712a.ship_mode()
7）获取库版本信息 exs_yhm2712a.version()

-- 版本更新说明
-- 版本号：202607201900
-- 1、更新时间：2026-07-20 19:00
-- 2、更新内容
--    实现 YHM2712A 充电管理芯片的完整驱动功能
--    提供充电状态查询、事件回调、船运模式等功能
--    新增 exs_yhm2712a.version() 接口，提供库版本查询功能


其中，开启充电 exs_yhm2712a.start() 和 关闭充电 exs_yhm2712a.stop() 默认自动执行，用户可以不用操作；
当碰到某些需要手动关闭或开启充电功能的场景时，大家可以自行控制，当前仅为预留；

以下为exs_yhm2712a扩展库函数的详细说明及代码实现：

1、开启充电
必须在task中运行，最大阻塞时间大概为700ms, 阻塞主要由sys.waitUntil("YHM27XX_REG", 500)和sys.wait(200)产生。
@api exs_yhm2712a.start()
@return boolean: true=成功, false=失败

2、关闭充电
必须在task中运行，最大阻塞时间大概为700ms, 阻塞主要由sys.waitUntil("YHM27XX_REG", 500)和sys.wait(200)产生。
@api exs_yhm2712a.stop()
@return boolean: true=成功, false=失败

3、初始化YHM2712A充电管理芯片
必须在task中运行,最大阻塞时间大概为700ms, 阻塞主要由sys.waitUntil("YHM27XX_REG", 500)和sys.wait(200)产生。
@api exs_yhm2712a.setup(init_cfg)
@param init_cfg table 初始化配置表
    pin:number, YHM2712A CMD引脚，必选
    v_battery:number, 电池充电截止电压, 取值范围：4200或4350可选, 单位(mV), 必须传入
    cap_battery:number, 电池容量, 取值范围：>= 100, 单位(mAh)，必须传入。
    i_charge:string, 充电电流, 取值范围：exs_yhm2712a.CCMIN(最小电流) 或 exs_yhm2712a.CCDEFAULT(默认电流) 或 exs_yhm2712a.CCMAX(最大电流)，三个可选参数，不传入时默认值为exs_yhm2712a.CCDEFAULT。
@return boolean 成功返回true，失败返回false
@usage
local setup_ok = exs_yhm2712a.setup({
    pin = 25,
    v_battery = 4200,
    cap_battery = 400,
    i_charge = exs_yhm2712a.CCMIN
})
if setup_ok then
    log.info("exs_yhm2712a", "传感器初始化成功")
end

4、获取充电系统状态信息
必须在task中运行，最大阻塞时间(包括超时重试时间)大概为20s。
该函数用于获取当前充电系统的完整状态，包括电池电压、充电阶段、充电状态、电池在位状态、充电器在位状态以及IC过热状态等信息。
其中充电器是否在位，中断触发，触发回调事件为CHARGER_STATE_EVENT，附带的参数 true表示充电器在位，false表示充电器不在位。
@api exs_yhm2712a.status()
@return table 状态信息表
{
    result = boolean,       -- true: 成功, false: 失败
    vbat_voltage = number,  -- 电池电压值（单位：mV），特殊值含义：
                            -- -1: 当前阶段不需要测量
                            -- -2: 电压测量失败
                            -- -3: 仅充电器就绪（无电池）
    charge_stage = number,  -- 当前充电阶段描述，可能值：
                            -- 0 : 放电模式
                            -- 1 : 预充电模式    
                            -- 2 : 涓流充电     
                            -- 3 : 恒流快速充电
                            -- 4 : 预留状态     
                            -- 5 : 恒压快速充电 
                            -- 6 : 预留状态    
                            -- 7 : 充电完成  
                            -- 8 : 未知状态
    charge_complete = boolean, -- true: 充电完成, false: 充电未完成
    battery_present = boolean, -- true: 电池在位, false: 电池不在位
    charger_present = boolean, -- true: 充电器在位, false: 充电器不在位
    ic_overheat = boolean     -- true: 充电IC过热, false: 充电IC未过热
}

5、注册事件回调函数
@api exs_yhm2712a.on(func)
@function: 回调方法，回调时传入参数有exs_yhm2712a.OVERHEAT, exs_yhm2712a.CHARGER_IN, exs_yhm2712a.CHARGER_OUT, exs_yhm2712a.SHIPPING_MODE
@return nil 无返回值
@usage
local function exs_yhm2712a_callback(event)
    if event == exs_yhm2712a.OVERHEAT then
        log.info("警告：设备温度过高！")
    elseif event == exs_yhm2712a.CHARGER_IN then
        log.info("充电器已插入")
    elseif event == exs_yhm2712a.CHARGER_OUT then
        log.info("充电器已拔出")
    elseif event == exs_yhm2712a.SHIPPING_MODE then
        log.info("已进入船运模式")
    end
end
-- 注册回调
exs_yhm2712a.on(exs_yhm2712a_callback)

6、进入船运模式
必须在task中运行，最大阻塞时间大概为2200ms, 阻塞主要由sys.wait(2000)和sys.waitUntil("YHM27XX_REG", 500)产生。
在船运模式下，电池FET断开，设备仅消耗约150nA电流，适用于产品运输和存储。
@api exs_yhm2712a.ship_mode()
@return boolean: true=成功, false=失败
@usage
exs_yhm2712a.ship_mode() -- 进入船运模式

7、获取库版本信息
获取exs_yhm2712a扩展库的版本号，用于版本管理和兼容性检查。
@api exs_yhm2712a.version()
@return string: 库版本号，格式为"年月日"
@usage
log.info("exs_yhm2712a", "version:", exs_yhm2712a.version())

```

## exs_yhm2712a.on(func)

注册exs_yhm2712a事件回调

**参数**

|传入值类型|解释|
|-|-|
|function|回调方法，回调时传入参数有exs_yhm2712a.OVERHEAT, exs_yhm2712a.CHARGER_IN, exs_yhm2712a.CHARGER_OUT|

**返回值**

|返回值类型|解释|
|-|-|
|nil|无返回值|

**例子**

```lua
local function exs_yhm2712a_callback(event)
    if event == exs_yhm2712a.OVERHEAT then
        log.info("警告：设备温度过高！")
    elseif event == exs_yhm2712a.CHARGER_IN then
        log.info("充电器已插入")
    elseif event == exs_yhm2712a.CHARGER_OUT then
        log.info("充电器已拔出")
    end
end
-- 注册回调
exs_yhm2712a.on(exs_yhm2712a_callback)

```

---

## exs_yhm2712a.setup(init_cfg)

初始化YHM2712A充电管理芯片,必须在task中运行,最大阻塞时间大概为700ms, 阻塞主要由sys.waitUntil("YHM27XX_REG", 500)和sys.wait(200)产生。

**参数**

|传入值类型|解释|
|-|-|
|param|init_cfg table 初始化配置表|

**返回值**

无

**例子**

无

---

## exs_yhm2712a.start()

开始充电(必须在task中运行，最大阻塞时间大概为700ms, 阻塞主要由sys.waitUntil("YHM27XX_REG", 500)和sys.wait(200)产生。)

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|boolean:|true=成功, false=失败|

**例子**

```lua
exs_yhm2712a.start() -- 开始充电

```

---

## exs_yhm2712a.stop()

停止充电(必须在task中运行，最大阻塞时间大概为700ms, 阻塞主要由sys.waitUntil("YHM27XX_REG", 500)和sys.wait(200)产生。)

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|boolean:|true=成功, false=失败|

**例子**

```lua
exs_yhm2712a.stop() -- 停止充电

```

---

## exs_yhm2712a.ship_mode()

进入船运模式(必须在task中运行，最大阻塞时间大概为2200ms, 阻塞主要由sys.waitUntil("YHM27XX_REG", 500)和sys.wait(2000)产生。)

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|boolean:|true=成功, false=失败|

**例子**

```lua
exs_yhm2712a.ship_mode() -- 进入船运模式

```

---

## exs_yhm2712a.status()

获取充电系统状态信息(必须在task中运行，最大阻塞时间(包括超时重试时间)大概为20s)。该函数用于获取当前充电系统的完整状态，包括电池电压、充电阶段、充电状态、电池在位状态、充电器在位状态以及IC过热状态等信息。其中充电器是否在位，中断触发，触发回调事件为CHARGER_STATE_EVENT，附带的参数 true表示充电器在位，false表示充电器不在位。

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|table|状态信息表，包含result字段指示操作是否成功|

**例子**

无

---

## exs_yhm2712a.version()

获取库版本信息

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|string|库版本号，格式：年月日时分|

**例子**

```lua
log.info("exs_yhm2712a", "version:", exs_yhm2712a.version())

```

---

