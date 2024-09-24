# otp - OTP操作库

{bdg-success}`已适配` {bdg-primary}`Air780E` {bdg-primary}`Air780EP` {bdg-primary}`Air780EPS` {bdg-primary}`Air201`

```{note}
本页文档由[这个文件](https://gitee.com/openLuat/LuatOS/tree/master/luat/modules/luat_lib_otp.c)自动生成。如有错误，请提交issue或帮忙修改后pr，谢谢！
```


**示例**

```lua
----------------------------
--- 本库已经废弃, 不要使用 ---
----------------------------

```

## otp.read(zone, offset, len)



读取指定OTP区域读取数据

**参数**

|传入值类型|解释|
|-|-|
|int|区域, 通常为0/1/2/3, 与具体硬件相关|
|int|偏移量|
|int|读取长度, 单位字节, 必须是4的倍数, 不能超过4096字节|

**返回值**

|返回值类型|解释|
|-|-|
|string|成功返回字符串, 否则返回nil|

**例子**

```lua

local otpdata = otp.read(0, 0, 64)
if otpdata then
    log.info("otp", otpdata:toHex())
end

```

---

## otp.write(zone, data, offset)



往指定OTP区域写入数据

**参数**

|传入值类型|解释|
|-|-|
|int|区域, 通常为0/1/2/3, 与具体硬件相关|
|string|数据, 长度必须是4个倍数|
|int|偏移量|

**返回值**

|返回值类型|解释|
|-|-|
|booL|成功返回true,否则返回false|

**例子**

无

---

## otp.erase(zone)



擦除指定OTP区域

**参数**

|传入值类型|解释|
|-|-|
|int|区域, 通常为0/1/2/3, 与具体硬件相关|

**返回值**

|返回值类型|解释|
|-|-|
|bool|成功返回true,否则返回false|

**例子**

无

---

## otp.lock(zone)



锁定OTP区域. 特别注意!!一旦加锁即无法解锁,OTP变成只读!!!

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|bool|成功返回true,否则返回false|

**例子**

无

---

