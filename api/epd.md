# epd - 墨水屏操作库

## epd.open(model, opts[, spi_device])

打开墨水屏

**参数**

|传入值类型|解释|
|-|-|
|int\|string|model 面板型号，如 epd.MODEL_1IN54、epd.MODEL_1IN54G_V2、"custom" 等|
|table|opts 配置表，port="device" 时需 pin_dc/pin_rst/pin_busy，可选 busy_pull/busy_poll_ms/rotation|
|userdata|spi_device 可选，port="device" 时传入 spi.deviceSetup() 返回的对象|

**返回值**

|返回值类型|解释|
|-|-|
|userdata|panel 成功时返回墨水屏对象|
|nil,string|失败时返回 nil 和错误信息|

**例子**

```lua
local spi_epd = spi.deviceSetup(0, 8, 0, 0, 8, 20 * 1000 * 1000, spi.MSB, 1, 0)
local panel, err = epd.open(epd.MODEL_1IN54,
    {port = "device", pin_dc = 10, pin_rst = 1, pin_busy = 22}, spi_epd)
assert(panel, err)
assert(panel:init())

```

---

## panel:init()

初始化墨水屏

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|boolean|成功返回true，失败返回false和错误信息|

**例子**

无

---

## panel:clear([color])

清屏

**参数**

|传入值类型|解释|
|-|-|
|int|color 可选，默认使用当前背景色，也可显式传调色板颜色|

**返回值**

|返回值类型|解释|
|-|-|
|boolean|成功返回true，失败返回false和错误信息|

**例子**

无

---

## panel:pixel(x, y[, color])

绘制像素点

**参数**

|传入值类型|解释|
|-|-|
|int|x X坐标|
|int|y Y坐标|
|int|color 可选，默认使用当前前景色，也可显式传调色板颜色|

**返回值**

|返回值类型|解释|
|-|-|
|boolean|成功返回true，失败返回false和错误信息|

**例子**

无

---

## panel:setColor(fg, bg)

设置当前前景色和背景色

**参数**

|传入值类型|解释|
|-|-|
|int|fg 前景颜色|
|int|bg 背景颜色|

**返回值**

|返回值类型|解释|
|-|-|
|boolean|成功返回true，颜色不受当前面板支持时返回false和错误信息|

**例子**

```lua
assert(panel:setColor(epd.RED, epd.WHITE))

```

---

## panel:getColor()

获取当前前景色和背景色

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|int|fg 前景颜色|
|int|bg 背景颜色|

**例子**

无

---

## panel:supportsColor(color)

查询颜色是否受当前面板支持

**参数**

|传入值类型|解释|
|-|-|
|int|color 逻辑颜色|

**返回值**

|返回值类型|解释|
|-|-|
|boolean|支持返回true，否则返回false|

**例子**

无

---

## panel:refresh([mode[, x, y, w, h]])

刷新屏幕（异步）

**参数**

|传入值类型|解释|
|-|-|
|int|mode 刷新模式，epd.FULL(默认)/FAST/PARTIAL/PARTIAL_RECT/AUTO|
|int|x 可选，PARTIAL_RECT 时的区域起点X|
|int|y 可选，PARTIAL_RECT 时的区域起点Y|
|int|w 可选，PARTIAL_RECT 时的区域宽度|
|int|h 可选，PARTIAL_RECT 时的区域高度|

**返回值**

|返回值类型|解释|
|-|-|
|cwait|通过 .wait() 获取结果：true 或 false,错误信息|

**例子**

```lua
assert(panel:refresh(epd.FULL).wait())
panel:pixel(12, 18, epd.BLACK)
assert(panel:refresh(epd.PARTIAL_RECT).wait())

```

---

## panel:sleep([mode])

进入休眠

**参数**

|传入值类型|解释|
|-|-|
|string\|int|mode 可选，"auto"(默认)/"standby"/"deep" 或对应常量|

**返回值**

|返回值类型|解释|
|-|-|
|boolean|成功返回true，失败返回false和错误信息|

**例子**

无

---

## panel:info()

获取面板信息

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|table|面板信息表，含width/height/native_width/native_height/stride/format/color_count/palette/caps/rotate等|

**例子**

无

---

## panel:close()

关闭并释放墨水屏

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|boolean|成功返回true|

**例子**

无

---

## panel:setRotation(rotate)

设置画布旋转方向

**参数**

|传入值类型|解释|
|-|-|
|int|rotate 旋转角度0/90/180/270，或索引0/1/2/3|

**返回值**

|返回值类型|解释|
|-|-|
|boolean|成功返回true，失败返回false和错误信息|

**例子**

```lua
panel:setRotation(90)
panel:line(0, 0, 100, 100, epd.BLACK)

```

---

## panel:line(x0, y0, x1, y1[, color])

绘制直线

**参数**

|传入值类型|解释|
|-|-|
|int|x0 起点X坐标|
|int|y0 起点Y坐标|
|int|x1 终点X坐标|
|int|y1 终点Y坐标|
|int|color 可选，默认使用当前前景色|

**返回值**

|返回值类型|解释|
|-|-|
|boolean|成功返回true，失败返回false和错误信息|

**例子**

```lua
panel:line(0, 0, 100, 100, epd.BLACK)

```

---

## panel:rect(x, y, x2, y2[, color[, fill]])

绘制矩形

**参数**

|传入值类型|解释|
|-|-|
|int|x 左上角X坐标|
|int|y 左上角Y坐标|
|int|x2 右下角X坐标|
|int|y2 右下角Y坐标|
|int|color 可选，默认使用当前前景色|
|int|fill 可选，0空心(默认)，1实心|

**返回值**

|返回值类型|解释|
|-|-|
|boolean|成功返回true，失败返回false和错误信息|

**例子**

```lua
panel:rect(0, 0, 199, 199, epd.BLACK, 1)
panel:rect(20, 20, 80, 80, epd.BLACK, 0)

```

---

## panel:circle(x, y, r[, color[, fill]])

绘制圆形

**参数**

|传入值类型|解释|
|-|-|
|int|x 圆心X坐标|
|int|y 圆心Y坐标|
|int|r 半径，0-255|
|int|color 可选，默认使用当前前景色|
|int|fill 可选，0空心(默认)，1实心|

**返回值**

|返回值类型|解释|
|-|-|
|boolean|成功返回true，失败返回false和错误信息|

**例子**

```lua
panel:circle(100, 100, 50, epd.BLACK, 0)
panel:circle(100, 100, 20, epd.BLACK, 1)

```

---

## panel:drawXbm(x, y, width, height, data[, fg[, bg]])

绘制XBM位图

**参数**

|传入值类型|解释|
|-|-|
|int|x 位图左上角X坐标，允许负值，屏幕外自动裁剪|
|int|y 位图左上角Y坐标，允许负值，屏幕外自动裁剪|
|int|width 位图像素宽度|
|int|height 位图像素高度|
|string|data XBM数据，逐行存储，每行ceil(width/8)字节，低位在左|
|int|fg 可选，置位像素颜色，默认当前前景色|
|int\|nil|bg 可选，清零像素颜色，默认当前背景色，传nil表示透明|

**返回值**

|返回值类型|解释|
|-|-|
|boolean|成功返回true，失败返回false和错误信息|

**例子**

```lua
local xbm = string.char(0x81, 0x42, 0x24, 0x18, 0x24, 0x42, 0x81, 0x00)
assert(panel:drawXbm(20, 30, 8, 8, xbm))
assert(panel:drawXbm(20, 30, 8, 8, xbm, epd.BLACK, nil))

```

---

## panel:qrcode(x, y, str[, size[, color]])

绘制二维码

**参数**

|传入值类型|解释|
|-|-|
|int|x 左上角X坐标|
|int|y 左上角Y坐标|
|string|str 二维码内容|
|int|size 可选，二维码像素边长，0表示按剩余区域自动适配|
|int|color 可选，默认使用当前前景/背景色|

**返回值**

|返回值类型|解释|
|-|-|
|boolean|成功返回true，失败返回false和错误信息|

**例子**

```lua
panel:qrcode(10, 10, "https://openluat.com", 120, epd.BLACK)

```

---

## panel:drawHzfont(x, y, text, size[, style])

绘制UTF-8文本（需固件启用HzFont）

**参数**

|传入值类型|解释|
|-|-|
|int|x X坐标|
|int|y 基线Y坐标|
|string|text UTF-8文本，支持中文|
|int|size 字号，1-255|
|table|style 可选样式表，支持fg/bg/antialias/threshold/dither，省略时使用当前前景/背景色|

**返回值**

|返回值类型|解释|
|-|-|
|boolean|成功返回true，失败返回false和错误信息|

**例子**

```lua
assert(panel:drawHzfont(10, 36, "合宙LuatOS", 24))
assert(panel:drawHzfont(10, 68, "Hello世界", 20,
    {fg = epd.BLACK, bg = epd.WHITE, dither = epd.DITHER_BAYER4}))

```

---

## panel:getHzfontWidth(text, size)

获取文本像素宽度

**参数**

|传入值类型|解释|
|-|-|
|string|text UTF-8文本|
|int|size 字号，1-255|

**返回值**

|返回值类型|解释|
|-|-|
|int|文本像素宽度，失败返回0|

**例子**

无

---

