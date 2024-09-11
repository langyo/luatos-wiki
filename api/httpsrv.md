# httpsrv - http服务端

{bdg-success}`已适配` {bdg-primary}`Air780E` {bdg-primary}`Air780EP` {bdg-primary}`Air780EPS`

```{note}
本页文档由[这个文件](https://gitee.com/openLuat/LuatOS/tree/master/luat/../components/network/httpsrv/src/luat_lib_httpsrv.c)自动生成。如有错误，请提交issue或帮忙修改后pr，谢谢！
```

```{tip}
本库有专属demo，[点此链接查看httpsrv的demo例子](https://gitee.com/openLuat/LuatOS/tree/master/demo/wlan)
```

## httpsrv.start(port, func)



启动并监听一个http端口

**参数**

|传入值类型|解释|
|-|-|
|int|端口号|
|function|回调函数|

**返回值**

|返回值类型|解释|
|-|-|
|bool|成功返回true, 否则返回false|

**例子**

```lua

-- 监听80端口
httpsrv.start(80, function(client, method, uri, headers, body)
    -- method 是字符串, 例如 GET POST PUT DELETE
    -- uri 也是字符串 例如 / /api/abc
    -- headers table类型
    -- body 字符串
    log.info("httpsrv", method, uri, json.encode(headers), body)
    if uri == "/led/1" then
        LEDA(1)
        return 200, {}, "ok"
    elseif uri == "/led/0" then
        LEDA(0)
        return 200, {}, "ok"
    end
    -- 返回值的约定 code, headers, body
    -- 若没有返回值, 则默认 404, {} ,""
    return 404, {}, "Not Found" .. uri
end)
-- 关于静态文件
-- 情况1: / , 映射为 /index.html
-- 情况2: /abc.html , 先查找 /abc.html, 不存在的话查找 /abc.html.gz
-- 若gz存在, 会自动以压缩文件进行响应, 绝大部分浏览器支持.
-- 当前默认查找 /luadb/xxx 下的文件,暂不可配置

```

---

## httpsrv.stop(port)



停止http服务

**参数**

|传入值类型|解释|
|-|-|
|int|端口号|

**返回值**

|返回值类型|解释|
|-|-|
|nil|当前无返回值|

**例子**

无

---

