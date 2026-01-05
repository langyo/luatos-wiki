# easylvgl - EasyLVGL图像库 (LVGL 9.4) - 重构版本

## easylvgl.init(width, height, color_format)

* 初始化 EasyLVGL

**参数**

|传入值类型|解释|
|-|-|
|int|width 屏幕宽度，默认 480|
|int|height 屏幕高度，默认 320|
|int|color_format 颜色格式，可选，默认 RGB565|

**返回值**

无

**例子**

无

---

## easylvgl.deinit()

* 反初始化 EasyLVGL

**参数**

|传入值类型|解释|
|-|-|
|return|nil|

**返回值**

无

**例子**

无

---

## easylvgl.refresh()

* 刷新 LVGL 显示（执行定时器处理）

**参数**

|传入值类型|解释|
|-|-|
|return|nil|

**返回值**

无

**例子**

无

---

## easylvgl.indev_bind_touch(tp_cfg)

* 绑定触摸输入配置到 BK7258 平台

**参数**

|传入值类型|解释|
|-|-|
|userdata|tp_cfg luat_tp_config_t*（lightuserdata）|

**返回值**

|返回值类型|解释|
|-|-|
|bool|绑定是否成功|

**例子**

无

---

## easylvgl.font_load(config)

* 加载字体

**参数**

|传入值类型|解释|
|-|-|
|table|config 配置表|
|string|config.type 字体类型，"hzfont" 或 "bin"|
|string|config.path 字体路径，对于 "hzfont"，传 nil 则使用内置字库|
|int|config.size 可选，TTF 字体大小，默认 16|
|int|config.cache_size 可选，TTF 缓存数量，默认 256|
|int|config.antialias 可选，TTF 抗锯齿等级，默认 -1（自动）|

**返回值**

|返回值类型|解释|
|-|-|
|userdata|字体指针|

**例子**

无

---

