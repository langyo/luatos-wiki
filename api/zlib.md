# zlib - zlib压缩/解压缩(已废弃)

{bdg-secondary}`适配状态未知`

```{note}
本页文档由[这个文件](https://gitee.com/openLuat/LuatOS/tree/master/luat/../components/zlib/luat_lib_zlib.c)自动生成。如有错误，请提交issue或帮忙修改后pr，谢谢！
```


**示例**

```lua
-- 这个库已经废弃了, 请使用miniz或者fastlz库

```

## zlib.c(input_file,output_file)



zlib压缩(需要大约270k内存，大部分mcu不支持)

**参数**

|传入值类型|解释|
|-|-|
|string|input_file  输入文件|
|string|output_file 输出文件|

**返回值**

|返回值类型|解释|
|-|-|
|bool|正常返回 ture  失败返回 false|

**例子**

```lua
zlib.c("/sd/1.txt","/sd/zlib")

```

---

## zlib.d(input_file,output_file)



zlib解压缩(需要大约18k内存，大部分mcu都支持)

**参数**

|传入值类型|解释|
|-|-|
|string|input_file  输入文件|
|string|output_file 输出文件|

**返回值**

|返回值类型|解释|
|-|-|
|bool|正常返回 ture  失败返回 false|

**例子**

```lua
zlib.d("/sd/zlib","/sd/1.txt")

```

---

