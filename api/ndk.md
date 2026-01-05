# ndk - 在沙盒化的RV32环境中运行MiniRV32IMA镜像

**示例**

```lua
-- 载入一个RV32镜像并执行若干步
local ctx, err = ndk.rv32i("/luadb/app.bin", 32 * 1024, 1024)
if not ctx then
    log.error("ndk", err)
    return
end
local ok, ret = ndk.exec(ctx, {steps = 100000, elapsed = 500})
if ok then
    log.info("ndk", "retval", ret)
end

```

## ndk.rv32i(path, mem_size, exchange_size)

创建并加载一个RV32镜像

**参数**

|传入值类型|解释|
|-|-|
|string|path 镜像路径|
|int|mem_size 可选，沙盒RAM大小，默认 LUAT_NDK_DEFAULT_RAM_SIZE|
|int|exchange_size 可选，交换区大小，默认 LUAT_NDK_DEFAULT_EXCHANGE_SIZE|

**返回值**

|返回值类型|解释|
|-|-|
|userdata|ctx 成功返回上下文，失败返回 nil,err|

**例子**

无

---

## ndk.setData(ctx, data, offset)

向交换区写入数据

**参数**

|传入值类型|解释|
|-|-|
|userdata|ctx ndk.rv32i 返回的上下文|
|string\|userdata|data 字符串或zbuff，写入交换区|
|int|offset 可选，起始偏移，默认0|

**返回值**

|返回值类型|解释|
|-|-|
|int|写入的字节数，失败返回 false,err|

**例子**

无

---

## ndk.getData(ctx, buff, len, offset)

从交换区读取数据

**参数**

|传入值类型|解释|
|-|-|
|userdata|ctx ndk.rv32i 返回的上下文|
|userdata|buff 可选，zbuff输出缓冲|
|int|len 可选，读取长度，默认交换区大小或buff长度|
|int|offset 可选，起始偏移，默认0|

**返回值**

|返回值类型|解释|
|-|-|
|string\|int|默认返回字符串，传入buff时返回读取字节数；失败返回 false,err|

**例子**

无

---

## ndk.exec(ctx, opts, elapsed_us)

同步执行镜像指令

**参数**

|传入值类型|解释|
|-|-|
|userdata|ctx ndk.rv32i 返回的上下文|
|int\|table|opts 步数或表 {steps=步数, elapsed=每步时间us}，步数为0使用默认预算|
|int|elapsed_us 可选，opts为数字时的步时间us|

**返回值**

|返回值类型|解释|
|-|-|
|boolean,int|成功返回 true,retval；失败返回 false,err,mcause,mtval|

**例子**

无

---

## ndk.reset(ctx)

重置沙箱并重新加载镜像

**参数**

|传入值类型|解释|
|-|-|
|userdata|ctx ndk.rv32i 返回的上下文|

**返回值**

|返回值类型|解释|
|-|-|
|boolean|成功返回 true，失败返回 false,err|

**例子**

无

---

## ndk.thread(ctx, opts, elapsed_us)

在独立线程异步执行镜像

**参数**

|传入值类型|解释|
|-|-|
|userdata|ctx ndk.rv32i 返回的上下文|
|int\|table|opts 步数或表 {steps=步数, elapsed=每步时间us}|
|int|elapsed_us 可选，opts为数字时的步时间us|

**返回值**

|返回值类型|解释|
|-|-|
|int|线程ID，失败返回 nil,err|

**例子**

无

---

## ndk.stop(ctx, wait_ms)

请求停止异步线程

**参数**

|传入值类型|解释|
|-|-|
|userdata|ctx ndk.rv32i 返回的上下文|
|int|wait_ms 可选，等待超时时间，默认1000|

**返回值**

|返回值类型|解释|
|-|-|
|boolean|成功返回 true，失败返回 false,err|

**例子**

无

---

## ndk.info(ctx)

获取当前运行状态

**参数**

|传入值类型|解释|
|-|-|
|userdata|ctx ndk.rv32i 返回的上下文|

**返回值**

|返回值类型|解释|
|-|-|
|table|包含 mem/exchange/exchange_addr/image/running/mcause/mtval|

**例子**

无

---

