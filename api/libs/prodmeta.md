# prodmeta - 使用 OTP 按 key=value 格式存储产品元数据

**示例**

```lua
local prodmeta = require("prodmeta")
-- 写入,应该尽量使用短的 key 和 value, 以节省空间
prodmeta.set("PROD", "Air8302")
prodmeta.set("PCB", "V1.2")
-- 读取
log.info("prodmeta", prodmeta.get("PROD"), prodmeta.get("PCB"))
-- 全部读取
local t = prodmeta.get_all()
log.info("prodmeta", json.encode(t))

```

## prodmeta.get(key)

获取指定 key 的值

**参数**

|传入值类型|解释|
|-|-|
|string|key|

**返回值**

|返回值类型|解释|
|-|-|
|string|值，不存在返回 nil|

**例子**

无

---

## prodmeta.get_all()

获取所有 key-value

**参数**

|传入值类型|解释|
|-|-|
|return|table|

**返回值**

无

**例子**

无

---

## prodmeta.clear()

清空所有数据（仅移芯平台有效）

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|bool|成功返回 true, 失败返回 false, reason|

**例子**

无

---

## prodmeta.info()

获取当前平台配置

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|table|{platform, zone, max_len, append_only}|

**例子**

无

---

