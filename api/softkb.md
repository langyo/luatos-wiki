# softkb - 软件键盘矩阵

{bdg-secondary}`适配状态未知`

```{note}
本页文档由[这个文件](https://gitee.com/openLuat/LuatOS/tree/master/luat/../components/soft_keyboard/luat_lib_softkeyboard.c)自动生成。如有错误，请提交issue或帮忙修改后pr，谢谢！
```


## softkb.init(port, key_in, key_out)



初始化软件键盘矩阵

**参数**

|传入值类型|解释|
|-|-|
|int|预留, 当前填0|
|table|矩阵输入按键表|
|table|矩阵输出按键表|

**返回值**

无

**例子**

```lua
    key_in = {pin.PD10,pin.PE00,pin.PE01,pin.PE02}
    key_out = {pin.PD12,pin.PD13,pin.PD14,pin.PD15}
    softkb.init(0,key_in,key_out)

sys.subscribe("SOFT_KB_INC", function(port, data, state)
    -- port 当前固定为0, 可以无视
    -- data, 需要配合init的map进行解析
    -- state, 1 为按下, 0 为 释放
    -- TODO 详细介绍
end)

```

---

## softkb.deinit(port)



删除软件键盘矩阵

**参数**

|传入值类型|解释|
|-|-|
|int|预留, 当前填0|

**返回值**

无

**例子**

```lua
    softkb.deinit(0)

```

---

