# pwm - PWM模块

## pwm.open(channel, period, pulse, pnum, precision)

开启指定的PWM通道

**参数**

|传入值类型|解释|
|-|-|
|int|PWM通道|
|int|频率, 1-1000000hz|
|int|占空比 0-分频精度|
|int|输出周期 0为持续输出, 1为单次输出, 其他为指定脉冲数输出|
|int|分频精度, 100/256/1000, 默认为100, 若设备不支持会有日志提示|

**返回值**

|返回值类型|解释|
|-|-|
|boolean|处理结果,成功返回true,失败返回false|

**例子**

```lua
-- 打开PWM5, 频率1kHz, 占空比50%
pwm.open(5, 1000, 50)
-- 打开PWM5, 频率10kHz, 分频为 31/256
pwm.open(5, 10000, 31, 0, 256)

```

---

## pwm.close(channel)

关闭指定的PWM通道

**参数**

|传入值类型|解释|
|-|-|
|int|PWM通道|

**返回值**

|返回值类型|解释|
|-|-|
|nil|无处理结果|

**例子**

```lua
-- 关闭PWM5
pwm.close(5)

```

---

## pwm.capture(channel)

PWM捕获

**参数**

|传入值类型|解释|
|-|-|
|int|PWM通道|
|int|捕获频率|

**返回值**

|返回值类型|解释|
|-|-|
|boolean|处理结果,成功返回true,失败返回false|

**例子**

```lua
-- PWM0捕获
while 1 do
    pwm.capture(0,1000)
    local ret,channel,pulse,pwmH,pwmL  = sys.waitUntil("PWM_CAPTURE", 2000)
    if ret then
        log.info("PWM_CAPTURE","channel"..channel,"pulse"..pulse,"pwmH"..pwmH,"pwmL"..pwmL)
    end
end

```

---

