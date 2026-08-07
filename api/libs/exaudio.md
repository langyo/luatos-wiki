# exaudio - exaudio扩展库

**示例**

```lua

-- 版本更新说明
-- 版本号：202608061100
-- 1、更新时间：2026-08-06 11:00
--    新音频框架play_start()播放前主动exaudio.pm(audio.RESUME)恢复ES8311工作模式
--    新音频框架play_stop()手动停止时exaudio.pm(audio.SHUTDOWN)下电ES8311省电
--    同时exaudio.vol()同步更新voice_vol变量，修复CC铃声无法设置问题
-- 版本号：202608031526
-- 1、更新时间：2026-08-03 15:26
--    play_start()文件播放新增文件头损坏预检功能
--    对mp3/amr/wav格式，播放前先解析文件头，文件不存在或头损坏时停止播放并提示"播放文件损坏，请更换文件播放"
-- 版本号：202607171800
-- 1、更新时间：2026-07-17 18:00
--    改造parse_audio_info，支持文件路径和缓冲数据两种方式输入
-- 版本号：202607161030
-- 1、更新时间：2026-07-16 10:30
--    移除新音频框架初始化audio_v2_setup中的make_probe_id+set_default_driver操作
--    各BSP有默认驱动，无需手动设置，特殊情况可通过exaudio.set_default_driver接口设置
-- 版本号：202607141800
-- 1、更新时间：2026-07-14 18:00
--    新增codec_voltage参数控制ES8311电平
--    codec_voltage=1(默认3.3V)，codec_voltage=0(1.8V，适配Air8201等特殊板型)
-- 版本号：202607081647
-- 1、更新时间：2026-07-08 16:47
--    移除exaudio.shutdown()，统一合并到exaudio.pm()中
--    exaudio.pm()新增新音频框架支持
--    新增exaudio.make_probe_id()函数，用于合成音频驱动ID
--    新增Air700/Air1780系列模组检测
-- 版本号：202607021200
-- 1、更新时间：2026-07-02 12:00
-- 2、更新内容
--    新增exaudio.version()接口
--    支持exaudio库文件版本号管理功能，版本号的格式为：yyyymmddhhmm，表示yyyy年mm月dd日hh时mm分发布的版本

```

## exaudio.parse_audio_info(input, codec_id[, pos])

@description 从音频文件或缓冲数据解析播放信息（采样率、位宽、声道数等）

**参数**

|传入值类型|解释|
|-|-|
|string/zbuff|input 音频文件路径（string）或二进制数据（string/zbuff）|
|number|codec_id 编解码器ID (0=PCM, 1=WAV, 2=AMR_NB, 3=AMR_WB, 5=MP3)|
|number|pos 可选，数据偏移位置（字节），仅传入二进制数据时有效，默认0|

**返回值**

|返回值类型|解释|
|-|-|
|table|成功返回包含音频信息的table，失败返回nil|

**例子**

```lua
-- 方式1：传入文件路径
local info = exaudio.parse_audio_info("/luadb/test.mp3", 5)
if info then
    log.info("采样率:", info.sample_rate)
    log.info("位宽:", info.data_bits)
    log.info("声道数:", info.channel_nums)
end

-- 方式2：传入缓冲数据
local info = exaudio.parse_audio_info(buff_data, 5)
if info then
    log.info("采样率:", info.sample_rate)
end
注意：此函数仅在audio_v2模式下可用

```

---

