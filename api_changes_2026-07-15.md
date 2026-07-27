# API 文档今日修改内容（2026-07-15）

> 用于报文档 issue，按库/模块列出实际 diff 内容。

## 提交记录

| 时间 | Commit | 作者 | 消息 |
|------|--------|------|------|
| 2026-07-15 11:19 +0800 | `110223c0` | Wendal Chen | ... |
| 2026-07-15 11:24 +0800 | `8404ca16` | Wendal Chen | ... |

## 文件清单

- [修改] `api/adc.md` （提交: 110223c0）
- [修改] `api/airlink.md` （提交: 110223c0）
- [修改] `api/airui.md` （提交: 110223c0）
- [修改] `api/audio.md` （提交: 110223c0）
- [修改] `api/camera.md` （提交: 110223c0, 8404ca16）
- [修改] `api/cc.md` （提交: 110223c0）
- [新增] `api/gbc.md` （提交: 110223c0）
- [修改] `api/gmssl.md` （提交: 110223c0）
- [修改] `api/index.md` （提交: 110223c0）
- [修改] `api/ioqueue.md` （提交: 110223c0）
- [修改] `api/lcdseg.md` （提交: 110223c0）
- [修改] `api/libs/air153C_wtd.md` （提交: 110223c0）
- [修改] `api/libs/airlbs.md` （提交: 110223c0）
- [修改] `api/libs/dhcam.md` （提交: 110223c0）
- [修改] `api/libs/dhcpsrv.md` （提交: 110223c0）
- [修改] `api/libs/dnsproxy.md` （提交: 110223c0）
- [新增] `api/libs/exaudio.md` （提交: 110223c0）
- [修改] `api/libs/exgnss.md` （提交: 110223c0）
- [修改] `api/libs/exlcd.md` （提交: 110223c0）
- [修改] `api/libs/exmodbus.md` （提交: 110223c0）
- [修改] `api/libs/exmtn.md` （提交: 110223c0）
- [修改] `api/libs/exnetif.md` （提交: 110223c0）
- [修改] `api/libs/exremotecam.md` （提交: 110223c0）
- [修改] `api/libs/exremotefile.md` （提交: 110223c0）
- [修改] `api/libs/exsip.md` （提交: 110223c0）
- [修改] `api/libs/exsipproto.md` （提交: 110223c0）
- [修改] `api/libs/extp.md` （提交: 110223c0）
- [修改] `api/libs/exvib.md` （提交: 110223c0）
- [修改] `api/libs/httpdns.md` （提交: 110223c0）
- [修改] `api/libs/httpplus.md` （提交: 110223c0）
- [修改] `api/libs/index.md` （提交: 110223c0）
- [修改] `api/libs/lbsLoc.md` （提交: 110223c0）
- [修改] `api/libs/lbsLoc2.md` （提交: 110223c0）
- [修改] `api/libs/libfota.md` （提交: 110223c0）
- [修改] `api/libs/libfota2.md` （提交: 110223c0）
- [删除] `api/libs/netLed.md` （提交: 110223c0）
- [修改] `api/libs/udpsrv.md` （提交: 110223c0）
- [修改] `api/libs/xmodem.md` （提交: 110223c0）
- [修改] `api/little_flash.md` （提交: 110223c0）
- [修改] `api/mcu.md` （提交: 110223c0）
- [修改] `api/miniz.md` （提交: 110223c0）
- [修改] `api/mobile.md` （提交: 110223c0）
- [删除] `api/natp.md` （提交: 110223c0）
- [修改] `api/ndk.md` （提交: 110223c0）
- [修改] `api/netdrv.md` （提交: 110223c0）
- [修改] `api/pm.md` （提交: 110223c0）
- [修改] `api/socket.md` （提交: 110223c0）
- [修改] `api/supported.md` （提交: 110223c0）
- [修改] `api/touchkey.md` （提交: 110223c0）
- [修改] `api/tp.md` （提交: 110223c0）
- [修改] `api/u8g2.md` （提交: 110223c0）
- [删除] `api/ulwip.md` （提交: 110223c0）

## api/adc.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/adc.md b/api/adc.md
index 35c79113..7cd1480e 100644
--- a/api/adc.md
+++ b/api/adc.md
@@ -24,8 +24,8 @@ adc.close(adc.CH_VBAT)
 
 |常量|类型|解释|
 |-|-|-|
-|adc.ADC_RANGE_3_6|number|air105的ADC分压电阻开启，范围0~3.76V|
-|adc.ADC_RANGE_1_8|number|air105的ADC分压电阻关闭，范围0~1.88V|
+|adc.ADC_RANGE_3_6|number|ADC分压电阻开启，范围0~3.76V|
+|adc.ADC_RANGE_1_8|number|ADC分压电阻关闭，范围0~1.88V|
 |adc.ADC_RANGE_3_8|number|air780E开启ADC0,1分压电阻，范围0~3.8V，将要废弃，不建议使用|
 |adc.ADC_RANGE_1_2|number|air780E关闭ADC0,1分压电阻，范围0~1.2V，将要废弃，不建议使用|
 |adc.ADC_RANGE_MAX|number|ADC开启内部分压后所能到达最大量程，由具体芯片决定|
@@ -68,13 +68,13 @@ adc.close(4) -- 若需要持续读取, 则不需要close, 功耗会高一点.
 
 ## adc.setRange(range)
 
-设置ADC的测量范围，注意这个和具体芯片有关，目前只支持air105/Air780EXXX系列
+设置ADC的测量范围
 
 **参数**
 
 |传入值类型|解释|
 |-|-|
-|int|range参数,与具体设备有关,比如air105填adc.ADC_RANGE_1_8和adc.ADC_RANGE_3_6|
+|int|range参数,与具体设备有关|
 
 **返回值**
 
@@ -87,12 +87,6 @@ adc.close(4) -- 若需要持续读取, 则不需要close, 功耗会高一点.
 ```lua
 -- 本函数要在调用adc.open之前就调用, 之后调用无效!!!
 
--- 关闭air105内部分压
-adc.setRange(adc.ADC_RANGE_1_8)
--- 打开air105内部分压
-adc.setRange(adc.ADC_RANGE_3_6)
-
-
 -- Air780EXXX支持多种，但是建议用以下2种
 adc.setRange(adc.ADC_RANGE_MIN) -- 关闭分压
 adc.setRange(adc.ADC_RANGE_MAX) -- 启用分压
```

## api/airlink.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/airlink.md b/api/airlink.md
index f405b3f5..5854139d 100644
--- a/api/airlink.md
+++ b/api/airlink.md
@@ -23,6 +23,7 @@
 |airlink.MODE_SPI_SLAVE|number|airlink.start参数, SPI从机模式|
 |airlink.MODE_SPI_MASTER|number|airlink.start参数, SPI主机模式|
 |airlink.MODE_UART|number|airlink.start参数, UART模式|
+|airlink.MODE_HSPI_MASTER|number|airlink.start参数, XT804 HSPI主机模式|
 |airlink.CONF_SPI_ID|number|SPI配置参数, 设置SPI的ID|
 |airlink.CONF_SPI_CS|number|SPI配置参数, 设置SPI的CS脚的GPIO|
 |airlink.CONF_SPI_RDY|number|SPI/UART配置参数, 设置RDY脚的GPIO|
```

## api/airui.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/airui.md b/api/airui.md
index e116e791..f6d4127f 100644
--- a/api/airui.md
+++ b/api/airui.md
@@ -91,7 +91,9 @@
 |传入值类型|解释|
 |-|-|
 |table|opts 可选配置|
+|int\|string|opts.mode 可选，休眠模式，支持 airui.SLEEP_MODE_LIGHT / airui.SLEEP_MODE_DEEP，或 "light" / "deep"|
 |bool|opts.power_down_lcd 休眠时是否关闭 LCD 背光，默认 true|
+|note|默认进入深度睡眠|
 
 **返回值**
 
@@ -182,7 +184,7 @@
 
 |返回值类型|解释|
 |-|-|
-|table|状态表，包含 rotation/w/h|
+|table|状态表，包含 rotation/w/h/sleeping/sleep_mode|
 
 **例子**
 
```

## api/audio.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/audio.md b/api/audio.md
index aed81296..a4753c66 100644
--- a/api/audio.md
+++ b/api/audio.md
@@ -28,6 +28,45 @@
 |audio.VOLTAGE_3300|number|可配置的codec工作电压，3.3V|
 |audio.RECORD_MONO|number|录音使用单声道|
 |audio.RECORD_STEREO|number|录音使用立体声|
+|audio.REQUEST_START|number|audio_v2.on回调函数传入消息值，表示开始处理请求块，可以传入更多数据|
+|audio.REQUEST_DRIVER_START|number|audio_v2.on回调函数传入消息值，表示请求块驱动开始|
+|audio.REQUEST_TTS_START|number|audio_v2.on回调函数传入消息值，表示请求块TTS开始|
+|audio.REQUEST_NEED_NEW_DATA|number|audio_v2.on回调函数传入消息值，表示请求块需要新的数据，需要传入新的数据|
+|audio.REQUEST_GET_NEW_DATA|number|audio_v2.on回调函数传入消息值，表示请求块获取新的数据|
+|audio.REQUEST_DECODE_DONE|number|audio_v2.on回调函数传入消息值，表示请求块解码完成|
+|audio.REQUEST_END|number|audio_v2.on回调函数传入消息值，表示请求块处理完成|
+|audio.EXT_SRC_DONE|number|audio_v2.on回调函数传入消息值，表示外部音频源处理完成|
+|audio.DRIVER_TYPE_NONE|number|驱动类型无|
+|audio.DRIVER_TYPE_I2S|number|驱动类型I2S|
+|audio.DRIVER_TYPE_DAC|number|驱动类型DAC|
+|audio.DRIVER_TYPE_ADC|number|驱动类型ADC|
+|audio.DRIVER_TYPE_USB|number|驱动类型USB声卡|
+|audio.DATA_CODEC_TYPE_RAW|number|编解码器类型RAW, 用于直接播放PCM数据流|
+|audio.DATA_CODEC_TYPE_WAV|number|编解码器类型WAV|
+|audio.DATA_CODEC_TYPE_AMR_NB|number|编解码器类型AMR_NB|
+|audio.DATA_CODEC_TYPE_AMR_WB|number|编解码器类型AMR_WB       |
+|audio.DATA_CODEC_TYPE_TTS|number|编解码器类型TTS|
+|audio.DATA_CODEC_TYPE_MP3|number|编解码器类型MP3|
+|audio.DATA_CODEC_TYPE_OPUS|number|编解码器类型OPUS|
+|audio.DATA_CODEC_TYPE_G711_ULAW|number|编解码器类型G711_ULAW|
+|audio.DATA_CODEC_TYPE_G711_ALAW|number|编解码器类型G711_ALAW|
+|audio.DATA_CODEC_TYPE_HW|number|编解码器类型-硬件编解码器优先模式|
+|audio.DSP_TYPE_SPEEXDSP|number|dsp类型speexdsp|
+|audio.CONFIG_PARAM_I2S_MODE|number|驱动私有参数的I2S模式|
+|audio.CONFIG_PARAM_I2S_FRAME_BITS|number|驱动私有参数的I2S帧位宽，需要和外部codec匹配|
+|audio.CONFIG_PARAM_I2S_CHANNEL_TYPE|number|驱动私有参数的I2S通道类型，需要和外部codec匹配|
+|audio.CONFIG_PARAM_DAC_BIT_WIDTH|number|驱动私有参数的DAC位宽|
+|audio.CONFIG_VALUE_I2S_MODE_I2S|number|驱动私有参数的I2S模式可选值，I2S标准模式|
+|audio.CONFIG_VALUE_I2S_MODE_LSB|number|驱动私有参数的I2S模式可选值，LSB|
+|audio.CONFIG_VALUE_I2S_MODE_MSB|number|驱动私有参数的I2S模式可选值，MSB|
+|audio.CONFIG_VALUE_I2S_MODE_PCMS|number|驱动私有参数的I2S模式可选值，PCMS|
+|audio.CONFIG_VALUE_I2S_MODE_PCML|number|驱动私有参数的I2S模式可选值，PCML|
+|audio.CONFIG_VALUE_I2S_CHANNEL_TYPE_LEFT|number|驱动私有参数的I2S通道类型可选值，左声道|
+|audio.CONFIG_VALUE_I2S_CHANNEL_TYPE_RIGHT|number|驱动私有参数的I2S通道类型可选值，右声道|
+|audio.CONFIG_VALUE_I2S_CHANNEL_TYPE_STEREO|number|驱动私有参数的I2S通道类型可选值，立体声|
+|audio.DRIVER_PARAM_TX_MAX_LEN|number|驱动放音单个buffer最大长度|
+|audio.DRIVER_PARAM_RX_MAX_LEN|number|驱动录音单个buffer最大长度|
+|audio.DATA_CODEC_PARAM_ENCODE_INPUT_LEN|number|编码1帧需要的输入数据长度|
 
 
 ## audio.start(id, audio_format, num_channels, sample_rate, bits_per_sample, is_signed)
@@ -536,3 +575,777 @@ audio.pm(multimedia_id,audio.RESUME)
 
 ---
 
+## audio_v2.play(path, err_stop, priority, driver_probe_id, codec_id)
+
+播放N个文件。考虑到读SD卡速度比较慢而拖累luavm进程的速度，所以尽量使用本API
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|string/table/zbuff|如果是string，则表示文件名，如果是table，则表示连续播放多个文件，如果是zbuff，则表示播放zbuff中的数据|
+|boolean|是否在文件解码失败后停止解码，只有在连续播放多个文件时才有用，默认true，遇到解码错误自动停止|
+|int|优先级，0~255，值越大，优先级越高，默认0|
+|int|驱动id，在不使用默认驱动时填写，绝大部分情况下都不需要填写。驱动id需要通过audio.make_probe_id合成|
+|int|解码器id，在需要指定解码器时填写，绝大部分情况下都不需要填写，见audio_v2.DATA_CODEC_TYPE_XXX|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|boolean|成功返回true,否则返回false|
+|int|request_index 请求索引，用于后续操作，如暂停、恢复，回调信息判断等|
+
+**例子**
+
+```lua
+audio_v2.play("xxxxxx")        --开始播放某个文件
+
+```
+
+---
+
+## audio_v2.tts(text, priority, driver_probe_id)
+
+播放tts语音
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|string/zbuff|需要播放的内容|
+|int|优先级，0~255，值越大，优先级越高，默认0|
+|int|驱动id，在不使用默认驱动时填写，绝大部分情况下都不需要填写。驱动id需要通过audio.make_probe_id合成|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|boolean|成功返回true,否则返回false|
+|int|request_index 请求索引，用于后续操作，如暂停、恢复，回调信息判断等|
+
+**例子**
+
+```lua
+audio_v2.tts("xxxxxx")        --开始播放某个文本
+
+```
+
+---
+
+## audio_v2.stream(codec_id, sample_rate, data_bits, channel_nums, is_signed, priority, driver_probe_id)
+
+流模式播放，需要提前指定解码器和音频参数
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|int|解码器id，见audio_v2.DATA_CODEC_TYPE_XXX，不能留空|
+|int|采样率，不能留空|
+|int|数据位数，8,16,24,32，不能留空|
+|int|通道数，1,2，不能留空|
+|boolean|是否有符号数据，默认true|
+|int|优先级，0~255，值越大，优先级越高，默认0|
+|int|驱动id，在不使用默认驱动时填写，绝大部分情况下都不需要填写。驱动id需要通过audio.make_probe_id合成|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|boolean|成功返回true,否则返回false|
+|int|request_index 请求索引，用于后续操作，如暂停、恢复，回调信息判断等|
+
+**例子**
+
+```lua
+audio_v2.stream(audio_v2.DATA_CODEC_TYPE_RAW, 16000, 16, 2, true, 0, nil) --播放16000Hz, 16bit, 2ch, 有符号的PCM数据流
+
+```
+
+---
+
+## audio_v2.get_play_info(data, codec_id, pos)
+
+获取播放信息
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|string/zbuff|输入数据|
+|int|解码器id，见audio_v2.DATA_CODEC_TYPE_XXX，不能留空|
+|int|当前输入数据在整个文件的位置，单位字节|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|boolean|无错误返回true,否则返回false, 返回true还需要看后续音频数据中采样率是否为0，不为0则说明获取成功了|
+|int|需要跳转到的新位置，单位字节，如果获取成功了，则跳转的位置为音频数据的真正起始位置，需要seek这个位置|
+|int|需要获取的数据长度，单位字节，如果本次没有获取到有效信息，但是也没有返回false，说明还需要更多数据才能判断|
+|int|采样率，如果为0，则说明没有获取到有效信息|
+|int|数据位数，8,16,24,32|
+|int|通道数，1,2|
+|boolean|是否有符号数据，默认true|
+
+**例子**
+
+```lua
+local no_error, next_pos, need_len, sample_rate, data_bits, channel_nums, is_signed = audio_v2.get_play_info(data, codec_id, pos)
+
+```
+
+---
+
+## audio_v2.input(request_or_source_index, data, is_end)
+
+流模式播放输入数据
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|int|request_or_source_index 请求索引或外部源索引，通过audio_v2.stream或者audio_v2.extern_source返回的索引|
+|string/zbuff|输入数据，如果为空，则不输入任何数据|
+|boolean|是否是最后一帧数据，默认false|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|boolean|成功返回true,否则返回false|
+|int|实际写入的长度，如果数据为空或者写入失败，则返回0，单位字节。如果数据是zbuff形式，写入成功后会自动删除zbuff中的数据|
+|int|输入缓冲的剩余空间，单位字节|
+
+**例子**
+
+```lua
+local result, write_len, free_len = audio_v2.input(request_index, data, is_end)
+
+```
+
+---
+
+## audio_v2.record(codec_id, save_buffer, record_callback_cnt, priority, sample_rate, data_bits, channel_nums, driver_probe_id)
+
+录音请求，包括2种模式，1. 保存到文件，2. 保存到buffer并回调给用户
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|string/zbuff|保存路径，string为保存成文件，zbuff为保存到buffer并回调给用户|
+|int|如果是保存文件，则为整体录音时间，单位秒，时间到后自动停止录音。如果是保存到buffer，则为每次回调的帧数，每一帧时间由编码器决定|
+|int|编码器id，见audio_v2.DATA_CODEC_TYPE_XXX，如果留空，则直接返回原始PCM数据。如果不留空，会检查sample_rate和data_bits是否符合解码器的要求|
+|int|优先级，0~255，值越大，优先级越高，默认0|
+|int|希望的采样率，如果指定了codec_id，则可以留空，由编码器自己决定|
+|int|希望的数据位数，8,16,24,32，如果指定了codec_id，则可以留空，由编码器自己决定|
+|int|希望的通道数，1,2，如果指定了codec_id，则可以留空，由编码器自己决定|
+|int|驱动id，在不使用默认驱动时填写，绝大部分情况下都不需要填写。驱动id需要通过audio.make_probe_id合成|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|boolean|成功返回true,否则返回false|
+|int|request_index 请求索引，用于后续操作，如暂停、恢复，回调信息判断等|
+
+**例子**
+
+```lua
+-- 录音到buffer并回调给用户，编码器为AMR_WB，优先级为0，每10帧回调一次
+local result, request_index = audio_v2.record(save_buffer, 10, audio_v2.DATA_CODEC_TYPE_AMR_WB)
+-- 录音到文件，编码器为AMR_WB，优先级为0，录音10秒结束
+local result, request_index = audio_v2.record("/save.amr", 10, audio_v2.DATA_CODEC_TYPE_AMR_WB)
+
+```
+
+---
+
+## audio_v2.make_head(record_codec_id, total_len, sample_rate, data_bits, channel_nums)
+
+* @brief 生成音频文件的头信息
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|int|record_codec_id 录音编码器id，见audio_v2.DATA_CODEC_TYPE_XXX，绝对不可以留空|
+|int|total_len 总数据长度，单位字节|
+|int|sample_rate 编码器的采样率，如果是固定采样率的编码器，可以留空，由编码器自己决定|
+|int|data_bits 编码器的数据位数，8,16,24,32，如果是固定数据位数的编码器，可以留空，由编码器自己决定|
+|int|channel_nums 编码器的通道数，1,2，如果是固定通道数的编码器，可以留空，由编码器自己决定|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|boolean|成功返回true,否则返回false|
+|string|头信息,如果失败，返回NIL|
+
+**例子**
+
+无
+
+---
+
+## audio_v2.speech(record_codec_id, save_buffer, record_callback_cnt, play_codec_id,one_play_block_len, sample_rate, data_bits, channel_nums, driver_probe_id, dsp_type)
+
+全双工模式，可用于对讲
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|int|录音编码器id，见audio_v2.DATA_CODEC_TYPE_XXX，如果留空，则直接返回原始PCM数据。如果不留空，会检查sample_rate和data_bits是否符合解码器的要求|
+|zbuff|录音数据回调时保存的buffer|
+|int|每次录音回调的帧数，每一帧时间由编码器决定|
+|int|播放解码器id，见audio_v2.DATA_CODEC_TYPE_XXX，如果留空，则和录音编码器相同|
+|int|希望的采样率，如果指定了codec_id，则可以留空，由编码器自己决定|
+|int|希望的数据位数，8,16,24,32，如果指定了codec_id，则可以留空，由编码器自己决定|
+|int|希望的通道数，1,2，如果指定了codec_id，则可以留空，由编码器自己决定|
+|int|驱动id，在不使用默认驱动时填写，绝大部分情况下都不需要填写。驱动id需要通过audio.make_probe_id合成|
+|int|dsp类型，见audio_v2.DSP_TYPE_XXX，如果留空，则由BSP决定具体使用哪个dsp类型|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|boolean|成功返回true,否则返回false|
+|int|request_index 请求索引，用于后续操作，如暂停、恢复，回调信息判断等|
+
+**例子**
+
+```lua
+-- 双工对讲模式，编码器为AMR_WB，每10帧回调一次
+local result, request_index = audio_v2.speech(audio_v2.DATA_CODEC_TYPE_AMR_WB, save_buffer, 10)
+
+```
+
+---
+
+## audio_v2.extern_source(request_index, source, is_add_record,codec_id, sample_rate, data_bits, channel_nums, is_signed)
+
+对讲中附加额外的音频数据，额外音频的参数必须和对讲的参数一致，否则会失败而没有任何作用
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|int|request_index 请求索引，通过audio_v2.speech返回的|
+|table/string/zbuff|输入数据，table表示播放文件，string表示播放tts，zbuff表示播放音频数据，如果只播放一个文件也要用table|
+|boolean|是否添加到录音通道，false添加到播放通道，true添加到录音通道，默认false|
+|boolean|是否在文件解码失败后停止解码，只有在连续播放多个文件时才有用，默认true，遇到解码错误自动停止|
+|int|解码器id，见audio_v2.DATA_CODEC_TYPE_XXX，如果留空则通过输入数据自行判断|
+|int|采样率，如果指定解码器是RAW，不能留空|
+|int|数据位数，8,16,24,32，如果指定解码器是RAW，不能留空|
+|int|通道数，1,2，如果指定解码器是RAW，不能留空|
+|boolean|是否有符号数据，默认true|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|boolean|成功返回true,否则返回false|
+|int|外部音频源索引，用于后续操作，如停止播放|
+
+**例子**
+
+```lua
+local result, request_index = audio_v2.speech(audio_v2.DATA_CODEC_TYPE_AMR_WB, save_buffer, 10)
+audio_v2.extern_source(request_index, {"/test_16k.mp3"})
+
+```
+
+---
+
+## audio_v2.stop(request_index)
+
+停止指定的音频请求
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|int|request_index 请求索引，通过audio_v2.play_files，audio_v2.stream，audio_v2.speech，audio_v2.record, audio_v2.tts或者audio_v2.extern_source返回|
+|return|nil|
+
+**返回值**
+
+无
+
+**例子**
+
+```lua
+local result, index = audio_v2.play("xxxxxx")
+audio_v2.stop(index)
+
+```
+
+---
+
+## audio_v2.shutdown(driver_power_off, codec_power_off, pa_power_off, driver_probe_id)
+
+关闭音频驱动
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|boolean|driver_power_off 是否关闭驱动，true关闭驱动，false不关闭驱动|
+|boolean|codec_power_off 是否关闭外部codec，true关闭外部codec，false不关闭外部codec|
+|boolean|pa_power_off 是否关闭pa，true关闭pa，false不关闭pa|
+|int|驱动id，在不使用默认驱动时填写，绝大部分情况下都不需要填写。驱动id需要通过audio.make_probe_id合成|
+|return|nil|
+
+**返回值**
+
+无
+
+**例子**
+
+```lua
+audio_v2.shutdown(true, true, true)
+@usage
+
+```
+
+---
+
+## audio_v2.pause(request_index, pause)
+
+暂停播放文件或者tts对应的音频通道
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|int|request_index 请求索引，通过audio.play_files或audio.tts返回|
+|boolean|pause 是否暂停，默认false|
+|return|nil|
+
+**返回值**
+
+无
+
+**例子**
+
+```lua
+audio_v2.pause(request_index, true)
+
+```
+
+---
+
+## audio_v2.is_all_done()
+
+判断所有请求是否完成
+
+**参数**
+
+无
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|boolean|所有请求是否完成|
+
+**例子**
+
+```lua
+is_all_done = audio_v2.is_all_done()
+
+```
+
+---
+
+## audio_v2.soft_volume(volume, driver_probe_id)
+
+设置软件音量增益，0~1000，值越大，音量越高，默认100，1000就是10倍音量
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|int|volume 软件音量增益，0~1000，值越大，音量越高，默认100|
+|int|driver_probe_id 驱动id，在不使用默认驱动时填写，绝大部分情况下都不需要填写。驱动id需要通过audio.make_probe_id合成|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|boolean|成功返回true,否则返回false|
+
+**例子**
+
+```lua
+audio_v2.soft_volume(75)
+
+```
+
+---
+
+## audio_v2.make_probe_id(tx_bus_type, tx_bus_id, rx_bus_type, rx_bus_id)
+
+合成音频驱动id
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|int|tx_bus_type 发送总线类型，见DRIVER_TYPE_xxx常量|
+|int|tx_bus_id 发送总线id，见DRIVER_TYPE_xxx常量|
+|int|rx_bus_type 接收总线类型，见DRIVER_TYPE_xxx常量|
+|int|rx_bus_id 接收总线id，见DRIVER_TYPE_xxx常量|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|int|驱动id|
+
+**例子**
+
+```lua
+probe_id = audio_v2.make_probe_id(audio_v2.DRIVER_TYPE_I2S, 0, audio_v2.DRIVER_TYPE_I2S, 0) --i2s0双工
+probe_id = audio_v2.make_probe_id(audio_v2.DRIVER_TYPE_DAC, 0, audio_v2.DRIVER_TYPE_NONE, 0) --dac0单工
+
+```
+
+---
+
+## audio_v2.set_default_driver(driver_probe_id)
+
+设置默认音频驱动
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|int|driver_probe_id 驱动id，驱动id需要通过audio.make_probe_id合成|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|boolean|成功返回true,否则返回false|
+
+**例子**
+
+```lua
+local driver_probe_id = audio_v2.make_probe_id(LUAT_AUDIO_DRIVER_TYPE_I2S, 0, LUAT_AUDIO_DRIVER_TYPE_I2S, 0) 
+audio_v2.set_default_driver(driver_probe_id)
+driver_probe_id = audio_v2.make_probe_id(LUAT_AUDIO_DRIVER_TYPE_DAC, 0, LUAT_AUDIO_DRIVER_TYPE_NONE, 0) --dac0单工
+audio_v2.set_default_driver(driver_probe_id)
+
+```
+
+---
+
+## audio_v2.get_driver_info()
+
+获取音频驱动数量和默认音频驱动索引
+
+**参数**
+
+无
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|int|all_nums 所有音频驱动数量|
+|int|default_driver_index 默认音频驱动索引，从0开始|
+
+**例子**
+
+```lua
+local all_nums, default_driver_index = audio_v2.get_driver_info()
+log.info(all_nums, default_driver_index)
+
+```
+
+---
+
+## audio_v2.get_driver_id(index)
+
+获取音频驱动id
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|int|index 驱动索引，从0开始|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|int|驱动id|
+
+**例子**
+
+```lua
+-- 打印出默认音频驱动信息
+local all_nums, default_driver_index = audio_v2.get_driver_info()
+local driver_probe_id = audio_v2.get_driver_id(default_driver_index)
+log.info(audio_v2.print_probe_id(driver_probe_id, true))
+
+```
+
+---
+
+## audio_v2.get_driver_param(driver_probe_id, param)
+
+获取音频驱动参数
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|int|driver_probe_id 驱动id，驱动id需要通过audio.make_probe_id合成，留空就获取默认音频驱动参数|
+|int|param 驱动参数，见DRIVER_PARAM_xxx常量|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|int|驱动参数值|
+
+**例子**
+
+```lua
+local result = audio_v2.get_driver_param(driver_probe_id, audio_v2.DRIVER_PARAM_RX_MAX_LEN)
+log.info(result)
+
+```
+
+---
+
+## audio_v2.print_probe_id(driver_probe_id, is_string)
+
+分解音频驱动id，并返回详细信息
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|int|driver_probe_id 驱动id，驱动id需要通过audio.make_probe_id合成|
+|boolean|is_string 是否返回字符串，true返回字符串，false返回常量|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|any|tx_bus_type 发送总线类型，见DRIVER_TYPE_xxx常量。is_string为true时，返回字符串，否则返回常量类型名称|
+|any|tx_bus_id 发送总线id|
+|any|rx_bus_type 接收总线类型，见DRIVER_TYPE_xxx常量。is_string为true时，返回字符串，否则返回常量类型名称|
+|any|rx_bus_id 接收总线id|
+
+**例子**
+
+```lua
+local tx_bus_type, tx_bus_id, rx_bus_type, rx_bus_id = audio_v2.print_probe_id(probe_id, true)
+log.info(tx_bus_type, tx_bus_id, rx_bus_type, rx_bus_id)
+
+```
+
+---
+
+## audio_v2.config(config_param, config_value1, config_value2, driver_probe_id)
+
+配置音频驱动的私有参数，采样率和数据位宽是通用参数，不能在这里配置
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|int|config_param 驱动私有参数索引，见audio_v2.CFG_PARAM_xxx常量|
+|int|config_value1 驱动私有参数值1，见audio_v2.CFG_VALUE_xxx常量或者直接填写数值|
+|int|config_value2 驱动私有参数值2，见audio_v2.CFG_VALUE_xxx常量或者直接填写数值，通常情况下只需要1个参数，不需要填写config_value2|
+|int|driver_probe_id 驱动id，在不使用默认驱动时填写，绝大部分情况下都不需要填写。驱动id需要通过audio.make_probe_id合成|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|boolean|成功返回true,否则返回false|
+
+**例子**
+
+```lua
+audio_v2.config(audio_v2.CFG_PARAM_I2S_MODE, audio_v2.CFG_VALUE_I2S_MODE_LSB)
+audio_v2.config(audio_v2.CFG_PARAM_I2S_FRAME_BITS, 16)
+audio_v2.config(audio_v2.CFG_PARAM_I2S_CHANNEL_TYPE, audio_v2.CFG_VALUE_I2S_CHANNEL_TYPE_RIGHT)
+
+```
+
+---
+
+## audio_v2.config_pa_power_ctrl(pa_power_ctrl_enable, pa_power_pin, pa_power_on_level, pa_power_on_delay_time_ms, driver_probe_id)
+
+配置音频驱动的pa电源控制
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|boolean|pa_power_ctrl_enable 是否使能pa电源控制|
+|int|pa_power_pin pa电源引脚|
+|int|pa_power_on_level pa电源电平，1表示高电平，0表示低电平|
+|int|pa_power_on_delay_time_ms pa电源开启延时时间，单位毫秒|
+|int|driver_probe_id 驱动id，在不使用默认驱动时填写，绝大部分情况下都不需要填写。驱动id需要通过audio.make_probe_id合成|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|boolean|成功返回true,否则返回false|
+
+**例子**
+
+```lua
+audio_v2.config_pa_power_ctrl(true, 12, 1, 100)
+
+```
+
+---
+
+## audio_v2.config_codec_power_ctrl(codec_power_ctrl_enable, codec_power_pin, codec_power_on_level, codec_ready_after_wakeup_time_ms, codec_power_off_delay_time_ms, driver_probe_id)
+
+配置音频驱动的codec电源控制
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|boolean|codec_power_ctrl_enable 是否使能codec电源控制|
+|int|codec_power_pin codec电源引脚|
+|int|codec_power_on_level codec电源电平，1表示高电平，0表示低电平|
+|int|codec_ready_after_wakeup_time_ms codec电源开启延时时间，单位毫秒|
+|int|codec_power_off_delay_time_ms codec电源关闭延时时间，单位毫秒|
+|int|driver_probe_id 驱动id，在不使用默认驱动时填写，绝大部分情况下都不需要填写。驱动id需要通过audio.make_probe_id合成|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|boolean|成功返回true,否则返回false|
+
+**例子**
+
+```lua
+audio_v2.config_codec_power_ctrl(true, 11, 1, 200, 10)
+
+```
+
+---
+
+## audio_v2.get_codec_param(id,param)
+
+获取编解码器的参数
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|int|id 编解码器id|
+|int|param 编解码器参数，见audio_v2.DATA_CODEC_PARAM_xxx常量|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|int|codec参数值|
+
+**例子**
+
+```lua
+local len = audio_v2.get_codec_param(audio_v2.DATA_CODEC_PARAM_ENCODE_INPUT_LEN)    --获取编码1帧需要的输入数据长度
+
+```
+
+---
+
+## audio_v2.on(func)
+
+注册audio事件回调
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|function|回调方法|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|nil|无返回值|
+
+**例子**
+
+```lua
+audio_v2.on(function(request_index, event, param)
+    log.info(request_index, event, param)
+end)
+--回调函数参数说明
+---@param int 请求索引
+---@param int 事件类型, 见audio_v2.REQUEST_xxx常量
+---@param int 附加参数, 根据事件类型不同, 有不同的含义, 有如下组合
+event和param可能出现的值
+  audio_v2.REQUEST_START     开始处理请求, param无意义
+  audio_v2.REQUEST_NEED_NEW_DATA     需要新的数据, param无意义
+  audio_v2.REQUEST_GET_NEW_DATA     获取到新数据, param为本次回调获取到的驱动数据大小
+  audio_v2.REQUEST_DECODE_DONE         请求处理完成, param无意义
+  audio_v2.REQUEST_END     请求块处理完成, param无意义
+
+```
+
+---
+
+## audio_v2.is_busy(request_index)
+
+判断请求块是否正在处理
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|int|request_index 请求索引|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|boolean|是否正在处理|
+
+**例子**
+
+```lua
+local is_busy = audio_v2.is_busy(1)    --判断请求块1是否正在处理
+
+```
+
+---
+
+## audio_v2.debug(on_off)@boolean true开 false关
+
+配置调试信息输出
+
+**参数**
+
+无
+
+**返回值**
+
+无
+
+**例子**
+
+无
+
+---
+
```

## api/camera.md

- 状态：修改
- 提交：110223c0, 8404ca16

```diff
diff --git a/api/camera.md b/api/camera.md
index 6ca13b0a..1e75a800 100644
--- a/api/camera.md
+++ b/api/camera.md
@@ -434,7 +434,7 @@ camera输出/停止数据流
 |id|camera id|
 |app_id|如果是usb摄像头，则输入usb应用id，其他留空|
 |int|跳帧，针对USB摄像头，跳过N帧后上报，一般情况正常传输是30fps，如果脚本处理不过来，可以跳过N帧上报，默认是0，即不跳|
-|int|图像数据最小长度，针对USB摄像头ISO传输可能漏数据的情况，只有大于最小长度的图像帧会上报，默认是10KB|
+|int|图像数据最小长度，针对USB摄像头ISO传输可能漏数据的情况，只有大于最小长度的图像帧会上报，默认是1KB|
 
 **返回值**
 
diff --git a/api/camera.md b/api/camera.md
index 1e75a800..6aa838eb 100644
--- a/api/camera.md
+++ b/api/camera.md
@@ -423,7 +423,7 @@ camera.reset_pin(camera_id, 1)
 
 ---
 
-## camera.stream(id, app_id)
+## camera.stream(id, app_id, jump_frame_cnt, min_data_len)
 
 camera输出/停止数据流
 
@@ -431,9 +431,9 @@ camera输出/停止数据流
 
 |传入值类型|解释|
 |-|-|
-|id|camera id|
-|app_id|如果是usb摄像头，则输入usb应用id，其他留空|
-|int|跳帧，针对USB摄像头，跳过N帧后上报，一般情况正常传输是30fps，如果脚本处理不过来，可以跳过N帧上报，默认是0，即不跳|
+|int|camera id|
+|int|app_id 如果是usb摄像头，则输入usb应用id，其他留空|
+|int|跳帧，针对USB摄像头，跳过N帧后上报，一般情况正常传输是摄像头最高帧率，如果脚本处理不过来，可以跳过N帧上报，默认是0，即不跳|
 |int|图像数据最小长度，针对USB摄像头ISO传输可能漏数据的情况，只有大于最小长度的图像帧会上报，默认是1KB|
 
 **返回值**
@@ -445,8 +445,8 @@ camera输出/停止数据流
 **例子**
 
 ```lua
-=
-camera.stream(camera.USB, app_id)
+camera.stream(camera.USB, app_id)       --默认不跳帧
+camera.stream(camera.USB, app_id, 1)    --跳过1帧上报
 
 ```
 
```

## api/cc.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/cc.md b/api/cc.md
index 94c065ce..f8ac1975 100644
--- a/api/cc.md
+++ b/api/cc.md
@@ -4,6 +4,7 @@
 
 ```lua
 -- 选型手册上支持VoLTE通话功能的模组支持
+-- 选型手册上支持VoLTE通话功能的模组支持
 
 ```
 
@@ -198,3 +199,226 @@ end)
 
 ---
 
+## cc.lastNum()
+
+获取最后一次通话的号码
+
+**参数**
+
+无
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|string|获取最后一次通话的号码|
+
+**例子**
+
+无
+
+---
+
+## cc.dial(sim_id, number)
+
+拨打电话
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|number|sim_id|
+|string|电话号码|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|bool|拨打电话成功与否|
+
+**例子**
+
+无
+
+---
+
+## cc.hangUp(sim_id)
+
+挂断电话
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|number|sim_id|
+
+**返回值**
+
+无
+
+**例子**
+
+无
+
+---
+
+## cc.accept(sim_id)
+
+接听电话
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|number|sim_id|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|bool|接听电话成功与否|
+
+**例子**
+
+无
+
+---
+
+## cc.init(multimedia_id)
+
+初始化电话功能
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|number|multimedia_id 多媒体id|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|bool|成功与否|
+
+**例子**
+
+无
+
+---
+
+## cc.record(on_off,upload_zbuff1, upload_zbuff2, download_zbuff1, download_zbuff2)
+
+录音通话
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|boolean|开启关闭通话录音功能，false或者nil关闭，其他开启|
+|zbuff|上行数据保存区1,zbuff创建时的空间容量必须是640的倍数,下同|
+|zbuff|上行数据保存区2,和上行数据保存区1组成双缓冲区|
+|zbuff|下行数据保存区1|
+|zbuff|下行数据保存区2,和下行数据保存区1组成双缓冲区|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|bool|成功与否，如果处于通话状态，会失败|
+
+**例子**
+
+```lua
+buff1 = zbuff.create(6400,0,zbuff.HEAP_AUTO)
+buff2 = zbuff.create(6400,0,zbuff.HEAP_AUTO)
+buff3 = zbuff.create(6400,0,zbuff.HEAP_AUTO)
+buff4 = zbuff.create(6400,0,zbuff.HEAP_AUTO)
+cc.on("record", function(type, buff_point)
+ log.info(type, buff_point) -- type==true是下行数据，false是上行数据 buff_point指示双缓存中返回了哪一个
+end)
+cc.record(true, buff1, buff2, buff3, buff4)
+
+```
+
+---
+
+## cc.quality()
+
+获取当前通话质量
+
+**参数**
+
+无
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|int|1为低音质(8K)，2为高音质(16k)，0没有在通话,其他值为具体的音频采样率|
+
+**例子**
+
+无
+
+---
+
+## cc.on(event, func)
+
+注册通话回调
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|string|事件名称 音频录音数据为"record"|
+|function|回调方法|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|nil|无返回值|
+
+**例子**
+
+```lua
+cc.on("record", function(type, buff_point)
+ log.info(type, buff_point) -- type==true是下行数据，false是上行数据 buff_point指示双缓存中返回了哪一个
+end)
+
+```
+
+---
+
+## cc.extern_source(source, is_add_record, codec_id, sample_rate, data_bits, channel_nums, is_signed)
+
+通话中附加额外的音频数据，额外音频的参数必须和通话的参数一致，否则会失败而没有任何作用
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|table/string/zbuff/nil|输入数据，table表示播放文件，string表示播放tts，zbuff表示播放音频数据，如果只播放一个文件也要用table,nil表示停止当前第三方数据播放|
+|boolean|是否添加到上行通道，true添加到上行通道，false添加到下行通道，默认true，往对端播放第三方数据源，目前只支持上行通道|
+|boolean|是否在文件解码失败后停止解码，只有在连续播放多个文件时才有用，默认true，遇到解码错误自动停止|
+|int|解码器id，见audio_v2.DATA_CODEC_TYPE_XXX，如果留空则通过输入数据自行判断|
+|int|采样率，如果指定解码器是RAW，不能留空|
+|int|数据位数，8,16,24,32，如果指定解码器是RAW，不能留空|
+|int|通道数，1,2，如果指定解码器是RAW，不能留空|
+|boolean|是否有符号数据，默认true|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|boolean|成功返回true,否则返回false|
+
+**例子**
+
+```lua
+cc.extern_source({"/test_16k.mp3"})
+
+```
+
+---
+
```

## api/gbc.md

- 状态：新增
- 提交：110223c0

```diff
diff --git a/api/gbc.md b/api/gbc.md
new file mode 100644
index 00000000..56f1ced7
--- /dev/null
+++ b/api/gbc.md
@@ -0,0 +1,108 @@
+# gbc - GBC模拟器
+
+## 常量
+
+|常量|类型|解释|
+|-|-|-|
+|gbc.Up|number|按键上|
+|gbc.Down|number|按键下|
+|gbc.Left|number|按键左|
+|gbc.Right|number|按键右|
+|gbc.A|number|按键A|
+|gbc.B|number|按键B|
+|gbc.Start|number|按键开始|
+|gbc.Select|number|按键选择|
+
+
+## gbc.init(file_path[, opts])
+
+gbc模拟器初始化
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|string|file_path ROM文件路径|
+|table[opt]|opts 配置项，可选字段：|
+
+**返回值**
+
+无
+
+**例子**
+
+无
+
+---
+
+## gbc.deinit()
+
+gbc模拟器反初始化，释放资源
+
+**参数**
+
+无
+
+**返回值**
+
+无
+
+**例子**
+
+```lua
+gbc.deinit()
+
+```
+
+---
+
+## gbc.key(key, val)
+
+GBC按键控制
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|number|key 按键常量|
+|number|val 状态 1按下 0抬起|
+
+**返回值**
+
+无
+
+**例子**
+
+```lua
+gbc.key(gbc.Up, 1)
+gbc.key(gbc.Up, 0)
+
+```
+
+---
+
+## gbc.quit_requested()
+
+查询GBC是否已退出
+
+**参数**
+
+无
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|bool|已退出则返回true|
+
+**例子**
+
+```lua
+if gbc.quit_requested() then
+    gbc.deinit()
+end
+
+```
+
+---
+
```

## api/gmssl.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/gmssl.md b/api/gmssl.md
index 65e72c5d..e1dcda4b 100644
--- a/api/gmssl.md
+++ b/api/gmssl.md
@@ -290,3 +290,177 @@ end
 
 ---
 
+## gmssl.sm2pointmul(k, px, py)
+
+SM2标量点乘: R = k * P
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|string|标量k, HEX字符串(64字符)|
+|string|点P的x坐标, HEX字符串(64字符)|
+|string|点P的y坐标, HEX字符串(64字符)|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|string|结果点R的x坐标, HEX字符串(64字符)|
+|string|结果点R的y坐标, HEX字符串(64字符)|
+
+**例子**
+
+```lua
+-- 计算 R = k * P (核心用于 GBT 32918.3-2016 SM2密钥交换)
+local rx, ry = gmssl.sm2pointmul(kHex, pxHex, pyHex)
+-- 本函数于2026.02.02新增,用于支持SM2密钥交换协议
+
+```
+
+---
+
+## gmssl.sm2ecdh(private, peerPx, peerPy)
+
+SM2 ECDH密钥协商: S = d * P
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|string|己方私钥, HEX字符串(64字符)|
+|string|对方公钥X, HEX字符串(64字符)|
+|string|对方公钥Y, HEX字符串(64字符)|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|string|协商结果点的x坐标, HEX字符串(64字符)|
+|string|协商结果点的y坐标, HEX字符串(64字符)|
+
+**例子**
+
+```lua
+-- ECDH协商: 己方私钥 * 对方公钥
+local sx, sy = gmssl.sm2ecdh(privateKey, peerPkx, peerPky)
+-- 用于 GBT 32918.3-2016 SM2密钥交换协议
+-- 本函数于2026.02.02新增
+
+```
+
+---
+
+## gmssl.sm2pointadd(px1, py1, px2, py2)
+
+SM2椭圆曲线点加运算: R = P + Q
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|string|点P的x坐标, HEX字符串(64字符)|
+|string|点P的y坐标, HEX字符串(64字符)|
+|string|点Q的x坐标, HEX字符串(64字符)|
+|string|点Q的y坐标, HEX字符串(64字符)|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|string|结果点R的x坐标, HEX字符串(64字符), 失败返回nil|
+|string|结果点R的y坐标, HEX字符串(64字符), 失败返回nil|
+
+**例子**
+
+```lua
+-- 计算 R = P + Q (用于 GBT 32918.3-2016 SM2密钥交换协议的 [h*t]*(P+Q) 步骤)
+local rx, ry = gmssl.sm2pointadd(px1, py1, px2, py2)
+-- 本函数用于 SM2 密钥交换协议 GB/T 32918.3-2016
+
+```
+
+---
+
+## gmssl.sm2pointisoncurve(px, py)
+
+SM2判断点是否在椭圆曲线上
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|string|点P的x坐标, HEX字符串(64字符)|
+|string|点P的y坐标, HEX字符串(64字符)|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|boolean|点在曲线上返回true, 否则返回false|
+
+**例子**
+
+```lua
+-- 用于 GBT 32918.3-2016 SM2密钥交换协议的公钥合法性校验
+local ok = gmssl.sm2pointisoncurve(px, py)
+-- 本函数用于 SM2 密钥交换协议, 协议要求校验对方临时公钥是否在曲线上
+
+```
+
+---
+
+## gmssl.sm2bnadd(a, b)
+
+SM2 GF(n)模加: r = (a + b) mod n
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|string|操作数a, HEX字符串(64字符), 256-bit大整数|
+|string|操作数b, HEX字符串(64字符), 256-bit大整数|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|string|结果r, HEX字符串(64字符), (a+b) mod SM2曲线阶n|
+
+**例子**
+
+```lua
+-- GBT 32918.3-2016 SM2密钥交换协议中的模n大数运算
+local r = gmssl.sm2bnadd(aHex, bHex)
+
+```
+
+---
+
+## gmssl.sm2bnmul(a, b)
+
+SM2 GF(n)模乘: r = (a * b) mod n
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|string|操作数a, HEX字符串(64字符), 256-bit大整数|
+|string|操作数b, HEX字符串(64字符), 256-bit大整数|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|string|结果r, HEX字符串(64字符), (a*b) mod SM2曲线阶n|
+
+**例子**
+
+```lua
+-- GBT 32918.3-2016 SM2密钥交换协议中的模n大数运算
+local r = gmssl.sm2bnmul(aHex, bHex)
+
+```
+
+---
+
```

## api/index.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/index.md b/api/index.md
index 2e9f31b1..b353503d 100644
--- a/api/index.md
+++ b/api/index.md
@@ -33,6 +33,7 @@ fonts
 fota
 fskv
 ftp
+gbc
 gmssl
 gpio
 gtfont
@@ -69,7 +70,6 @@ mlx90640
 mobile
 modbus
 mqtt
-natp
 ndk
 nes
 netdrv
@@ -107,7 +107,6 @@ touchkey
 tp
 u8g2
 uart
-ulwip
 usb
 usbapp
 videoplayer
```

## api/ioqueue.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/ioqueue.md b/api/ioqueue.md
index 305759e1..90bbc895 100644
--- a/api/ioqueue.md
+++ b/api/ioqueue.md
@@ -8,7 +8,7 @@
 
 |传入值类型|解释|
 |-|-|
-|int|硬件定时器id，默认用0，根据实际MCU确定，air105为0~5，与pwm共用，同一个通道号不能同时为pwm和ioqueue|
+|int|硬件定时器id，默认用0|
 |int|一个完整周期需要的命令，可以比实际的多|
 |int|重复次数,默认是1，如果写0则表示无限次数循环|
 
```

## api/lcdseg.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/lcdseg.md b/api/lcdseg.md
index 9d57361b..dda8c811 100644
--- a/api/lcdseg.md
+++ b/api/lcdseg.md
@@ -1,5 +1,12 @@
 # lcdseg - 段式lcd
 
+**示例**
+
+```lua
+-- 本库当前没有任何主推模组是支持的
+
+```
+
 ## 常量
 
 |常量|类型|解释|
@@ -28,8 +35,8 @@
 |-|-|
 |int|bias值,通常为 1/3 bias, 对应 lcdseg.BIAS_ONETHIRD|
 |int|duty值,通常为 1/4 duty, 对应 lcdseg.DUTY_ONEFOURTH|
-|int|电压, 单位100mV, 例如2.7v写27. air103支持的值有 27/29/31/33|
-|int|COM脚的数量, 取决于具体模块, air103支持1-4|
+|int|电压, 单位100mV, 例如2.7v写27|
+|int|COM脚的数量, 取决于具体模块|
 |int|刷新率,通常为60, 对应60HZ|
 |int|COM启用与否的掩码, 默认为0xFF,全部启用.若只启用COM0/COM1, 则0x03|
 |int|seg启用与否的掩码, 默认为0xFFFFFFFF,即全部启用. 若只启用前16个, 0xFFFF|
```

## api/libs/air153C_wtd.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/libs/air153C_wtd.md b/api/libs/air153C_wtd.md
index dfb52e72..d047d1ef 100644
--- a/api/libs/air153C_wtd.md
+++ b/api/libs/air153C_wtd.md
@@ -10,6 +10,12 @@
 --     air153C_wtd.feed_dog(28,10)--28为看门狗引脚，10为设置喂狗时间
 --     --air153C_wtd.set_time(1)--开启定时模式再打开此代码，否则无效
 -- end)
+-- 版本更新说明
+-- 版本号：202607011722
+-- 1、更新时间：2026-07-01 17:22
+-- 2、更新内容
+--    新增air153C_wtd.version()接口
+--    支持air153C_wtd库文件版本号管理功能，版本号的格式为：yyyymmddhhmm，表示yyyy年mm月hh日hh时mm分发布的版本
 
 ```
 
```

## api/libs/airlbs.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/libs/airlbs.md b/api/libs/airlbs.md
index 93835ef5..cfd3c079 100644
--- a/api/libs/airlbs.md
+++ b/api/libs/airlbs.md
@@ -9,6 +9,13 @@
 -- lbsloc 和 lbsloc2 都是免费LBS定位的实现方式；
 -- airlbs 扩展库是收费 LBS 的实现方式。
 
+-- 版本更新说明
+-- 版本号：202607021200
+-- 1、更新时间：2026-07-02 12:00
+-- 2、更新内容
+--    新增airlbs.version()接口
+--    支持airlbs库文件版本号管理功能，版本号的格式为：yyyymmddhhmm，表示yyyy年mm月dd日hh时mm分发布的版本
+
 ```
 
 ## airlbs.request(param)
```

## api/libs/dhcam.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/libs/dhcam.md b/api/libs/dhcam.md
index fcd23e9e..4a467a88 100644
--- a/api/libs/dhcam.md
+++ b/api/libs/dhcam.md
@@ -11,6 +11,13 @@
         require "dhcam" -- 首先加载具体型号的摄像头功能模块（如大华）
         require "exremotecam" -- 然后加载exremotecam主模块
 
+-- 版本更新说明
+-- 版本号：202607021200
+-- 1、更新时间：2026-07-02 12:00
+-- 2、更新内容
+--    新增dhcam.version()接口
+--    支持dhcam库文件版本号管理功能，版本号的格式为：yyyymmddhhmm，表示yyyy年mm月dd日hh时mm分发布的版本
+
 ```
 
 ## split_string_by_pipe(input_str,return_type)
@@ -144,6 +151,8 @@ URL编码函数，用于将字符串转换为符合URL标准的编码格式
 |number|dahua_param.channel 摄像头通道号，默认为全局的DH_channel|
 |number|dahua_param.x OSD显示的X坐标，默认为0|
 |number|dahua_param.y OSD显示的Y坐标，默认为0|
+|string|dahua_param.username 摄像头登录用户名（可选，默认为"admin"）|
+|string|dahua_param.password 摄像头登录密码（可选，默认为"Air123456"）|
 
 **返回值**
 
@@ -169,6 +178,8 @@ URL编码函数，用于将字符串转换为符合URL标准的编码格式
 |string|dahua_param.host 摄像头/NVR的IP地址|
 |number|dahua_param.channel 摄像头通道号|
 |string|dahua_param.save_path 照片保存路径（可选，默认为"/sd/1.jpeg"）|
+|string|dahua_param.username 摄像头登录用户名（可选，默认为"admin"）|
+|string|dahua_param.password 摄像头登录密码（可选，默认为"Air123456"）|
 
 **返回值**
 
```

## api/libs/dhcpsrv.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/libs/dhcpsrv.md b/api/libs/dhcpsrv.md
index d264e7de..154f707f 100644
--- a/api/libs/dhcpsrv.md
+++ b/api/libs/dhcpsrv.md
@@ -5,6 +5,13 @@
 ```lua
 -- 参考dhcpsrv.create函数
 
+-- 版本更新说明
+-- 版本号：202607021200
+-- 1、更新时间：2026-07-02 12:00
+-- 2、更新内容
+--    新增dhcpsrv.version()接口
+--    支持dhcpsrv库文件版本号管理功能，版本号的格式为：yyyymmddhhmm，表示yyyy年mm月dd日hh时mm分发布的版本
+
 ```
 
 ## dhcpsrv.create(opts)
```

## api/libs/dnsproxy.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/libs/dnsproxy.md b/api/libs/dnsproxy.md
index 04ad2725..db5ca00a 100644
--- a/api/libs/dnsproxy.md
+++ b/api/libs/dnsproxy.md
@@ -5,6 +5,18 @@
 ```lua
 -- 具体用法请查阅demo
 
+-- 版本更新说明
+-- 版本号：202607100900
+-- 1、更新时间：2026-07-10 09:00
+-- 2、更新内容
+--    新增 dnsproxy.close() 接口，关闭所有 socket 并清空 DNS 请求映射表
+
+-- 版本号：202607021200
+-- 1、更新时间：2026-07-02 12:00
+-- 2、更新内容
+--    新增dnsproxy.version()接口
+--    支持dnsproxy库文件版本号管理功能，版本号的格式为：yyyymmddhhmm，表示yyyy年mm月dd日hh时mm分发布的版本
+
 ```
 
 ## dnsproxy.setup(adapter, main_adapter)
```

## api/libs/exaudio.md

- 状态：新增
- 提交：110223c0

```diff
diff --git a/api/libs/exaudio.md b/api/libs/exaudio.md
new file mode 100644
index 00000000..87441c40
--- /dev/null
+++ b/api/libs/exaudio.md
@@ -0,0 +1,57 @@
+# exaudio - exaudio扩展库
+
+**示例**
+
+```lua
+
+-- 版本更新说明
+-- 版本号：202607141800
+-- 1、更新时间：2026-07-14 18:00
+--    新增codec_voltage参数控制ES8311电平
+--    codec_voltage=1(默认3.3V)，codec_voltage=0(1.8V，适配Air8201等特殊板型)
+-- 版本号：202607081647
+-- 1、更新时间：2026-07-08 16:47
+--    移除exaudio.shutdown()，统一合并到exaudio.pm()中
+--    exaudio.pm()新增新音频框架支持
+--    新增exaudio.make_probe_id()函数，用于合成音频驱动ID
+--    新增Air700/Air1780系列模组检测
+-- 版本号：202607021200
+-- 1、更新时间：2026-07-02 12:00
+-- 2、更新内容
+--    新增exaudio.version()接口
+--    支持exaudio库文件版本号管理功能，版本号的格式为：yyyymmddhhmm，表示yyyy年mm月dd日hh时mm分发布的版本
+
+```
+
+## exaudio.parse_audio_info(file_path, codec_id)
+
+@description 从音频文件解析播放信息（采样率、位宽、声道数等）
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|string|file_path 音频文件路径|
+|number|codec_id 编解码器ID (0=PCM, 1=WAV, 2=AMR_NB, 3=AMR_WB, 5=MP3)|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|table|成功返回包含音频信息的table，失败返回nil|
+
+**例子**
+
+```lua
+local info = exaudio.parse_audio_info("/luadb/test.mp3", 5)
+if info then
+    log.info("采样率:", info.sample_rate)
+    log.info("位宽:", info.data_bits)
+    log.info("声道数:", info.channel_nums)
+end
+注意：此函数仅在audio_v2模式下可用
+
+```
+
+---
+
```

## api/libs/exgnss.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/libs/exgnss.md b/api/libs/exgnss.md
index 39697956..7a9eb623 100644
--- a/api/libs/exgnss.md
+++ b/api/libs/exgnss.md
@@ -116,6 +116,13 @@ end
 sys.subscribe("GNSS_STATE",gnss_state)
 
 
+-- 版本更新说明
+-- 版本号：202607021200
+-- 1、更新时间：2026-07-02 12:00
+-- 2、更新内容
+--    新增exgnss.version()接口
+--    支持exgnss库文件版本号管理功能，版本号的格式为：yyyymmddhhmm，表示yyyy年mm月dd日hh时mm分发布的版本
+
 ```
 
 ## exgnss.setup(opts)
```

## api/libs/exlcd.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/libs/exlcd.md b/api/libs/exlcd.md
index b70af81a..d44c8fec 100644
--- a/api/libs/exlcd.md
+++ b/api/libs/exlcd.md
@@ -17,6 +17,13 @@
 5、exlcd.wakeup()：屏幕唤醒
 6、exlcd.get_sleep()：休眠状态查询
 
+-- 版本更新说明
+-- 版本号：202607021200
+-- 1、更新时间：2026-07-02 12:00
+-- 2、更新内容
+--    新增exlcd.version()接口
+--    支持exlcd库文件版本号管理功能，版本号的格式为：yyyymmddhhmm，表示yyyy年mm月dd日hh时mm分发布的版本
+
 ```
 
 ## exlcd.init(param)
```

## api/libs/exmodbus.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/libs/exmodbus.md b/api/libs/exmodbus.md
index 3ae5a545..f8747c98 100644
--- a/api/libs/exmodbus.md
+++ b/api/libs/exmodbus.md
@@ -11,6 +11,13 @@
 5、modbus:on(callback)：从站注册回调接口，用于处理主站发起的请求（仅适用于 RTU、ASCII、TCP 从站模式）
 6、exmodbus.debug(enable)：设置 debug 开关，开启后会打印接收和发送的原始数据
 
+-- 版本更新说明
+-- 版本号：202607021200
+-- 1、更新时间：2026-07-02 12:00
+-- 2、更新内容
+--    新增exmodbus.version()接口
+--    支持exmodbus库文件版本号管理功能，版本号的格式为：yyyymmddhhmm，表示yyyy年mm月dd日hh时mm分发布的版本
+
 ```
 
 ## exmodbus.debug(enable)
```

## api/libs/exmtn.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/libs/exmtn.md b/api/libs/exmtn.md
index 4c54c88d..8ac3478d 100644
--- a/api/libs/exmtn.md
+++ b/api/libs/exmtn.md
@@ -6,6 +6,13 @@
 exmtn.init(1, 0)  -- 初始化，1个块，缓存写入
 exmtn.log("info", "tag", "message", 123)  -- 输出运维日志
 
+-- 版本更新说明
+-- 版本号：202607021200
+-- 1、更新时间：2026-07-02 12:00
+-- 2、更新内容
+--    新增exmtn.version()接口
+--    支持exmtn库文件版本号管理功能，版本号的格式为：yyyymmddhhmm，表示yyyy年mm月dd日hh时mm分发布的版本
+
 ```
 
 ## exmtn.init(blocks, write_way)
```

## api/libs/exnetif.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/libs/exnetif.md b/api/libs/exnetif.md
index aa39d87b..46663c62 100644
--- a/api/libs/exnetif.md
+++ b/api/libs/exnetif.md
@@ -3,12 +3,46 @@
 **示例**
 
 ```lua
-本文件的对外接口有5个：
+本文件的对外接口有9个：
 1、exnetif.set_priority_order(networkConfigs)：设置网络优先级顺序并初始化对应网络(需要在task中调用)
 2、exnetif.notify_status(cb_fnc)：设置网络状态变化回调函数
 3、exnetif.setproxy(adapter, main_adapter,other_configs)：配置网络代理实现多网融合(需要在task中调用)
 4、exnetif.check_network_status(interval),检测间隔时间ms(选填)，不填时只检测一次，填写后将根据间隔时间循环检测，会提高模块功耗
-5、exnetif.close(type, adapter)：关闭指定网卡,内核固件版本号需>=2020
+5、exnetif.close(type, adapter)：关闭网卡功能或多网融合,内核固件版本需为2026年1月后的固件
+6、exnetif.update_wifi(config)：运行时更新WiFi账号密码,用于引擎主机等需要动态获取WiFi凭证的场景
+7、exnetif.switch_upstream_wifi(config)：多网融合代理模式下切换上游WiFi，自动处理NAPT关闭/重开(需要在task中调用)
+8、exnetif.disable_upstream_autoreconnect()：禁用上游WiFi自动重连功能
+9、exnetif.version()：获取库文件版本信息
+
+-- 版本更新说明
+-- 版本号：202607141200
+-- 1、更新时间：2026-07-14 12:00
+-- 2、更新内容
+--    新增exnetif.switch_upstream_wifi(config)接口：多网融合代理模式下切换上游WiFi，封装NAPT关闭→断连→重连→NAPT恢复全流程
+--    新增exnetif.disable_upstream_autoreconnect()接口：禁用上游WiFi自动重连
+--    setproxy 增加 auto_reconnect 参数：建立代理时可选择启用上游WiFi异常掉线自动重连
+--    exnetif.close(true) 同步清理 wifi_config 字段
+
+-- 版本号：202607100900
+-- 1、更新时间：2026-07-10 09:00
+-- 2、更新内容
+--    exnetif.close(true)：完整实现关闭多网融合功能（停止 DHCP 服务器→关闭 DNS 代理→禁用 NAPT→停止代理网卡服务）
+--    exnetif.close(false, socket.LWIP_GP_GW)：支持关闭 airlink 4G 网卡（仅设置 DISCONNECTED 状态+apply_priority，无硬件操作）
+--    setproxy：保存 DHCP 服务器引用和代理网卡列表，支持多次 setproxy 后的全部清理
+--    修复 proxy_state 单值覆盖问题：多次 setproxy 的代理网卡改为数组累积，close(true) 遍历全部关闭
+
+-- 版本号：202607022100
+-- 1、更新时间：2026-07-02 21:00
+-- 2、更新内容
+--    新增exnetif.update_wifi(config)接口
+--    修复： 1601 多网融合设置以太网 airlink over uart 4g顺序后，以太网断开后 4g网络连不上问题，ip_lose_handle 网卡掉线时遗漏恢复 OPENED 网卡
+--    修复： 1601引擎主机的gpio设置与开发板不同，原airlink_wifi_hardware_init函数会导致引擎主机按键中断失效，airlink_wifi_hardware_init 支持 UART/SPI 双模式，目前改为了手动配置
+
+-- 版本号：202607021200
+-- 1、更新时间：2026-07-02 12:00
+-- 2、更新内容
+--    新增exnetif.version()接口
+--    支持exnetif库文件版本号管理功能，版本号的格式为：yyyymmddhhmm，表示yyyy年mm月dd日hh时mm分发布的版本
 
 ```
 
@@ -304,28 +338,94 @@ exnetif.set_priority_order({
 
 ---
 
-## exnetif.close(type,adapter)
+## exnetif.update_wifi(config)
 
-关闭网卡功能。(内核固件版本号需>=2020)
+运行时更新WiFi账号密码。用于如下场景：设备先通过4G/以太网上线获取WiFi凭证，再动态更新WiFi连接信息。
 
 **参数**
 
 |传入值类型|解释|
 |-|-|
-|param|type boolean 是否为多网融合|
-|param|adapter number 需要关闭的网卡|
+|table|config WiFi配置表|
 
 **返回值**
 
 |返回值类型|解释|
 |-|-|
-|boolean|操作结果|
+|boolean|成功返回true，失败返回false|
+
+**例子**
+
+```lua
+    -- 场景：设备通过4G上线后，从服务端获取WiFi账号密码，动态更新
+    exnetif.update_wifi({
+        ssid = "new_wifi_ssid",
+        password = "new_wifi_password",
+        bssid = "AABBCCDDEEFF"  -- 可选，指定BSSID
+    })
+    -- 如果WiFi之前未初始化（未在set_priority_order中配置），会自动初始化并加入优先级列表
+
+```
+
+---
+
+## exnetif.close(type,adapter)
+
+关闭网卡功能。(内核固件版本支持情况：Air8000模组对应V2022版本及以后版本，Air780EPM/EHM/EHV/EGH 模组对应V2024及以后版本，Air1601模组对应V1008版本固件)
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|param|type boolean 是否为多网融合(true=关闭多网融合, false=关闭单个网卡)|
+|param|adapter number 需要关闭的网卡，可选值: socket.LWIP_ETH/LWIP_USER1/LWIP_STA/LWIP_AP/LWIP_GP/LWIP_GP_GW|
+
+**返回值**
+
+无
+
+**例子**
+
+无
+
+---
+
+## exnetif.switch_upstream_wifi(config)
+
+切换代理模式下的上游WiFi网络。用于场景：多网融合（如ETH -> STA）运行时切换上游WiFi凭证。
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|table|config WiFi配置表|
+
+**返回值**
+
+无
+
+**例子**
+
+无
+
+---
+
+## exnetif.disable_upstream_autoreconnect()
+
+禁用上游WiFi自动重连功能
+
+**参数**
+
+无
+
+**返回值**
+
+无
 
 **例子**
 
 ```lua
-    exnetif.close(true) --关闭多网融合功能
-    exnetif.close(false,socket.LWIP_ETH)  --关闭优先级中的以太网网卡
+    exnetif.disable_upstream_autoreconnect()
 
 ```
 
```

## api/libs/exremotecam.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/libs/exremotecam.md b/api/libs/exremotecam.md
index 146cc506..4fcc62d6 100644
--- a/api/libs/exremotecam.md
+++ b/api/libs/exremotecam.md
@@ -24,14 +24,18 @@ local osd_param = {
     channel = 0,  -- 摄像头通道号
     text = "行1|行2|行3",  -- OSD文本内容，需用竖线分隔，格式如"1111|2222|3333|4444"
     x = 0,  -- 显示位置的X坐标
-    y = 2000  -- 显示位置的Y坐标
+    y = 2000,  -- 显示位置的Y坐标
+    username = "admin",  -- 摄像头登录用户名
+    password = "Air123456"  -- 摄像头登录密码
 }
 
 -- 拍照功能参数配置表
 local photo_param = {
     brand = "dhcam",  -- 摄像头品牌，当前仅支持"dhcam"(大华)
     host = "192.168.1.108",  -- 摄像头/NVR的IP地址
-    channel = 0  -- 摄像头通道号
+    channel = 0,  -- 摄像头通道号
+    username = "admin",  -- 摄像头登录用户名
+    password = "Air123456"  -- 摄像头登录密码
 }
 
 function camera_start()
@@ -50,6 +54,13 @@ end
 
 sys.taskInit(camera_start)
 
+-- 版本更新说明
+-- 版本号：202607021200
+-- 1、更新时间：2026-07-02 12:00
+-- 2、更新内容
+--    新增exremotecam.version()接口
+--    支持exremotecam库文件版本号管理功能，版本号的格式为：yyyymmddhhmm，表示yyyy年mm月dd日hh时mm分发布的版本
+
 ```
 
 ## exremotecam.osd(camera_param)
@@ -67,6 +78,8 @@ sys.taskInit(camera_start)
 |string|camera_param.text OSD文本内容，需用竖线分隔|
 |number|camera_param.x 显示位置的X坐标|
 |number|camera_param.y 显示位置的Y坐标|
+|string|camera_param.username 摄像头登录用户名（可选，默认为"admin"）|
+|string|camera_param.password 摄像头登录密码（可选，默认为"Air123456"）|
 
 **返回值**
 
@@ -93,6 +106,8 @@ sys.taskInit(camera_start)
 |string|camera_param.host 摄像头/NVR的IP地址|
 |number|camera_param.channel 摄像头通道号（主要用于NVR）|
 |string|camera_param.save_path 照片保存路径（可选，默认为"/sd/1.jpeg"）|
+|string|camera_param.username 摄像头登录用户名（可选，默认为"admin"）|
+|string|camera_param.password 摄像头登录密码（可选，默认为"Air123456"）|
 
 **返回值**
 
```

## api/libs/exremotefile.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/libs/exremotefile.md b/api/libs/exremotefile.md
index c8bdd90d..ab4f9e69 100644
--- a/api/libs/exremotefile.md
+++ b/api/libs/exremotefile.md
@@ -23,6 +23,13 @@ V1.0：
 
 2、exremotefile.close()：关闭远程文件管理系统，停止AP热点和关闭HTTP服务器（不卸载SD卡）
 
+-- 版本更新说明
+-- 版本号：202607021200
+-- 1、更新时间：2026-07-02 12:00
+-- 2、更新内容
+--    新增exremotefile.version()接口
+--    支持exremotefile库文件版本号管理功能，版本号的格式为：yyyymmddhhmm，表示yyyy年mm月dd日hh时mm分发布的版本
+
 ```
 
 ## exremotefile.open(ap_opts, sdcard_opts, server_opts)
```

## api/libs/exsip.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/libs/exsip.md b/api/libs/exsip.md
index 534d2aea..02095645 100644
--- a/api/libs/exsip.md
+++ b/api/libs/exsip.md
@@ -47,6 +47,13 @@ exsip.start()
 -- 挂断通话
 -- exsip.hangUp()
 
+-- 版本更新说明
+-- 版本号：202607021200
+-- 1、更新时间：2026-07-02 12:00
+-- 2、更新内容
+--    新增exsip.version()接口
+--    支持exsip库文件版本号管理功能，版本号的格式为：yyyymmddhhmm，表示yyyy年mm月dd日hh时mm分发布的版本
+
 ```
 
 ## exsip.init(config)
```

## api/libs/exsipproto.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/libs/exsipproto.md b/api/libs/exsipproto.md
index 3f186a35..9e35d413 100644
--- a/api/libs/exsipproto.md
+++ b/api/libs/exsipproto.md
@@ -19,6 +19,7 @@ local auth = proto.digest_auth({
     uri = "sip:example.com"
 })
 
+
 ```
 
 ## exsipproto.parse_headers(resp)
```

## api/libs/extp.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/libs/extp.md b/api/libs/extp.md
index 61bda55a..58c75d6c 100644
--- a/api/libs/extp.md
+++ b/api/libs/extp.md
@@ -23,6 +23,13 @@ SWIPE_UP、SWIPE_DOWN、SINGLE_TAP、LONG_PRESS
 
 所有触摸事件均通过sys.publish("BASE_TOUCH_EVENT", event_type, ...)发布
 
+-- 版本更新说明
+-- 版本号：202607021200
+-- 1、更新时间：2026-07-02 12:00
+-- 2、更新内容
+--    新增extp.version()接口
+--    支持extp库文件版本号管理功能，版本号的格式为：yyyymmddhhmm，表示yyyy年mm月dd日hh时mm分发布的版本
+
 ```
 
 ## extp.set_publish_enabled(msg_type, enabled)
```

## api/libs/exvib.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/libs/exvib.md b/api/libs/exvib.md
index 2818c9cc..27c6a137 100644
--- a/api/libs/exvib.md
+++ b/api/libs/exvib.md
@@ -108,6 +108,13 @@ end
 sys.taskInit(vib_fnc)
 
 
+-- 版本更新说明
+-- 版本号：202607021200
+-- 1、更新时间：2026-07-02 12:00
+-- 2、更新内容
+--    新增exvib.version()接口
+--    支持exvib库文件版本号管理功能，版本号的格式为：yyyymmddhhmm，表示yyyy年mm月dd日hh时mm分发布的版本
+
 ```
 
 ## exvib.read_xyz()
```

## api/libs/httpdns.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/libs/httpdns.md b/api/libs/httpdns.md
index c11f551e..ee4d37f0 100644
--- a/api/libs/httpdns.md
+++ b/api/libs/httpdns.md
@@ -11,6 +11,13 @@ log.info("httpdns", "air32.cn", ip)
 local ip = httpdns.tx("air32.cn")
 log.info("httpdns", "air32.cn", ip)
 
+-- 版本更新说明
+-- 版本号：202607021200
+-- 1、更新时间：2026-07-02 12:00
+-- 2、更新内容
+--    新增httpdns.version()接口
+--    支持httpdns库文件版本号管理功能，版本号的格式为：yyyymmddhhmm，表示yyyy年mm月dd日hh时mm分发布的版本
+
 ```
 
 ## httpdns.ali(domain_name, opts)
```

## api/libs/httpplus.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/libs/httpplus.md b/api/libs/httpplus.md
index ccaa65cd..bee5dd11 100644
--- a/api/libs/httpplus.md
+++ b/api/libs/httpplus.md
@@ -33,6 +33,13 @@
 -- 支持 文件下载到本地
 -- 支持 fota升级
 
+-- 版本更新说明
+-- 版本号：202607021200
+-- 1、更新时间：2026-07-02 12:00
+-- 2、更新内容
+--    新增httpplus.version()接口
+--    支持httpplus库文件版本号管理功能，版本号的格式为：yyyymmddhhmm，表示yyyy年mm月dd日hh时mm分发布的版本
+
 ```
 
 ## httpplus.request(opts)
```

## api/libs/index.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/libs/index.md b/api/libs/index.md
index b8eb30bd..11a0249e 100644
--- a/api/libs/index.md
+++ b/api/libs/index.md
@@ -9,6 +9,7 @@ airlbs
 dhcam
 dhcpsrv
 dnsproxy
+exaudio
 exgnss
 exlcd
 exmodbus
@@ -28,7 +29,6 @@ lbsLoc2
 libfota
 libfota2
 libnet
-netLed
 udpsrv
 xmodem
 ```
```

## api/libs/lbsLoc.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/libs/lbsLoc.md b/api/libs/lbsLoc.md
index cdf5ba36..7f94e7b9 100644
--- a/api/libs/lbsLoc.md
+++ b/api/libs/lbsLoc.md
@@ -48,6 +48,13 @@ sys.taskInit(function()
     end
 end)
 
+-- 版本更新说明
+-- 版本号：202607021200
+-- 1、更新时间：2026-07-02 12:00
+-- 2、更新内容
+--    新增lbsLoc.version()接口
+--    支持lbsLoc库文件版本号管理功能，版本号的格式为：yyyymmddhhmm，表示yyyy年mm月dd日hh时mm分发布的版本
+
 ```
 
 ## lbsLoc.request(cbFnc,reqAddr,timeout,productKey,host,port,reqTime,reqWifi)
```

## api/libs/lbsLoc2.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/libs/lbsLoc2.md b/api/libs/lbsLoc2.md
index 561e2fa6..28e7af9d 100644
--- a/api/libs/lbsLoc2.md
+++ b/api/libs/lbsLoc2.md
@@ -27,6 +27,13 @@ sys.taskInit(function()
     end
 end)
 
+-- 版本更新说明
+-- 版本号：202607021200
+-- 1、更新时间：2026-07-02 12:00
+-- 2、更新内容
+--    新增lbsLoc2.version()接口
+--    支持lbsLoc2库文件版本号管理功能，版本号的格式为：yyyymmddhhmm，表示yyyy年mm月dd日hh时mm分发布的版本
+
 ```
 
 ## lbsLoc2.request(timeout, host, port, reqTime)
```

## api/libs/libfota.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/libs/libfota.md b/api/libs/libfota.md
index 649fd608..4fb8d8ce 100644
--- a/api/libs/libfota.md
+++ b/api/libs/libfota.md
@@ -43,6 +43,13 @@ sys.timerLoopStart(libfota.request, 4*3600*1000, libfota_cb)
 -- 自建平台
 sys.timerLoopStart(libfota.request, 4*3600*1000, libfota_cb, "http://xxxxxx.com/xxx/upgrade?version=" .. _G.VERSION)
 
+-- 版本更新说明
+-- 版本号：202607021200
+-- 1、更新时间：2026-07-02 12:00
+-- 2、更新内容
+--    新增libfota.version()接口
+--    支持libfota库文件版本号管理功能，版本号的格式为：yyyymmddhhmm，表示yyyy年mm月dd日hh时mm分发布的版本
+
 ```
 
 ## libfota.request(cbFnc,ota_url,storge_location, len, param1,ota_port,libfota_timeout,server_cert, client_cert, client_key, client_password)
```

## api/libs/libfota2.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/libs/libfota2.md b/api/libs/libfota2.md
index d87df6e4..d3bdffa9 100644
--- a/api/libs/libfota2.md
+++ b/api/libs/libfota2.md
@@ -40,6 +40,13 @@ sys.timerLoopStart(libfota2.request, 4*3600*1000, libfota_cb)
 -- 自建平台
 sys.timerLoopStart(libfota2.request, 4*3600*1000, libfota_cb, opts)
 
+-- 版本更新说明
+-- 版本号：202607021200
+-- 1、更新时间：2026-07-02 12:00
+-- 2、更新内容
+--    新增libfota2.version()接口
+--    支持libfota2库文件版本号管理功能，版本号的格式为：yyyymmddhhmm，表示yyyy年mm月dd日hh时mm分发布的版本
+
 ```
 
 ## libfota2.request(cbFnc, opts)
```

## api/libs/netLed.md

- 状态：删除
- 提交：110223c0

```diff
diff --git a/api/libs/netLed.md b/api/libs/netLed.md
deleted file mode 100644
index a6e68b85..00000000
--- a/api/libs/netLed.md
+++ /dev/null
@@ -1,186 +0,0 @@
-# netLed - netLed 网络状态指示灯
-
-**示例**
-
-```lua
---注意:因使用了sys.wait()所有api需要在协程中使用
--- 用法实例
-local netLed = require ("netLed")
-
-local LEDA = gpio.setup(27,1,gpio.PULLUP) --LED引脚判断赋值结束
-sys.taskInit(function()
---呼吸灯
-sys.wait(5080)--延时5秒等待网络注册
-log.info("mobile.status()", mobile.status())
-  while true do
-        if mobile.status() == 1 then--已注册
-            sys.wait(688)
-            netLed.setupBreateLed(LEDA)
-        end
-   end
-end)
-
-```
-
-## netLed.setState
-
-更新网络指示灯表示的工作状态
-
-**参数**
-
-无
-
-**返回值**
-
-|返回值类型|解释|
-|-|-|
-|nil|无返回值|
-
-**例子**
-
-```lua
-netLed.setState()
-
-```
-
----
-
-## netLed.taskLed(ledPinSetFunc)
-
-网络指示灯模块的运行任务
-
-**参数**
-
-无
-
-**返回值**
-
-|返回值类型|解释|
-|-|-|
-|nil|无返回值|
-
-**例子**
-
-```lua
-local LEDA = gpio.setup(27,1,gpio.PULLUP) --LED引脚判断赋值结束
-netLed.taskLed(LEDA)
-
-```
-
----
-
-## netLed.taskLte(ledPinSetFunc)
-
-LTE指示灯模块的运行任务
-
-**参数**
-
-无
-
-**返回值**
-
-|返回值类型|解释|
-|-|-|
-|nil|无返回值|
-
-**例子**
-
-```lua
-local LEDA = gpio.setup(27,1,gpio.PULLUP) --LED引脚判断赋值结束
-netLed.taskLte(LEDA)
-
-```
-
----
-
-## netLed.setup(flag,ledpin,ltepin)
-
-配置网络指示灯和LTE指示灯并且立即执行配置后的动作
-
-**参数**
-
-|传入值类型|解释|
-|-|-|
-|bool|flag 是否打开网络指示灯和LTE指示灯功能,true为打开,false为关闭|
-|number|ledPin 控制网络指示灯闪烁的GPIO引脚,例如pio.P0_1表示GPIO1|
-|number|ltePin 控制LTE指示灯闪烁的GPIO引脚,例如pio.P0_4表示GPIO4|
-
-**返回值**
-
-|返回值类型|解释|
-|-|-|
-|nil|无返回值|
-
-**例子**
-
-```lua
-netLed.setup(true,27,0)
-
-```
-
----
-
-## netLed.setBlinkTime(state,on,off)
-
-配置某种工作状态下指示灯点亮和熄灭的时长（如果用户不配置,使用netLed.lua中ledBlinkTime配置的默认值）
-
-**参数**
-
-|传入值类型|解释|
-|-|-|
-|string|state 某种工作状态,仅支持"FLYMODE"、"SIMERR"、"IDLE"、"GSM"、"GPRS"、"SCK"|
-|number|on 指示灯点亮时长,单位毫秒,0xFFFF表示常亮,0表示常灭|
-|number|off 指示灯熄灭时长,单位毫秒,0xFFFF表示常灭,0表示常亮|
-
-**返回值**
-
-|返回值类型|解释|
-|-|-|
-|nil|无返回值 |
-
-**例子**
-
-```lua
-netLed.setBlinkTime(("FLYMODE",1000,500) --表示飞行模式工作状态下,指示灯闪烁规律为: 亮1秒,灭8.5秒
-
-```
-
----
-
-## netLed.setupBreateLed(ledPin)
-
-呼吸灯
-
-**参数**
-
-|传入值类型|解释|
-|-|-|
-|function|ledPin 呼吸灯的ledPin(1)用pins.setup注册返回的方法|
-
-**返回值**
-
-|返回值类型|解释|
-|-|-|
-|nil|无返回值|
-
-**例子**
-
-```lua
-local netLed = require ("netLed")
-local LEDA = gpio.setup(27,1,gpio.PULLUP) --LED引脚判断赋值结束
-sys.taskInit(function()
---呼吸灯
-sys.wait(5080)--延时5秒等待网络注册
-log.info("mobile.status()", mobile.status())
-  while true do
-        if mobile.status() == 1 then--已注册
-            sys.wait(688)
-            netLed.setupBreateLed(LEDA)
-        end
-   end
-end)
-
-```
-
----
-
```

## api/libs/udpsrv.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/libs/udpsrv.md b/api/libs/udpsrv.md
index 548422e9..3a483c98 100644
--- a/api/libs/udpsrv.md
+++ b/api/libs/udpsrv.md
@@ -6,6 +6,13 @@
 -- 具体用法请查
 阅demo
 
+-- 版本更新说明
+-- 版本号：202607021200
+-- 1、更新时间：2026-07-02 12:00
+-- 2、更新内容
+--    新增udpsrv.version()接口
+--    支持udpsrv库文件版本号管理功能，版本号的格式为：yyyymmddhhmm，表示yyyy年mm月dd日hh时mm分发布的版本
+
 ```
 
 ## udpsrv.create(port, topic, adapter)
```

## api/libs/xmodem.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/libs/xmodem.md b/api/libs/xmodem.md
index f7e4052f..ba00e22f 100644
--- a/api/libs/xmodem.md
+++ b/api/libs/xmodem.md
@@ -84,7 +84,12 @@ end
 --运行这个task的主函数xmodem_run
 sys.taskInit(xmodem_run, taskName,xmodem_run_cb)
 
-
+-- 版本更新说明
+-- 版本号：202607021200
+-- 1、更新时间：2026-07-02 12:00
+-- 2、更新内容
+--    新增xmodem.version()接口
+--    支持xmodem库文件版本号管理功能，版本号的格式为：yyyymmddhhmm，表示yyyy年mm月dd日hh时mm分发布的版本
 
 ```
 
```

## api/little_flash.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/little_flash.md b/api/little_flash.md
index 017a65c7..658e5f11 100644
--- a/api/little_flash.md
+++ b/api/little_flash.md
@@ -187,7 +187,7 @@ log.info("lf.getInfo",lf.getInfo(lf_device))
 
 ---
 
-## lf.mount(flash, mount_point, offset, maxsize)
+## lf.mount(flash, mount_point, offset, maxsize, opts)
 
 挂载 little_flash lfs文件系统
 
@@ -199,6 +199,7 @@ log.info("lf.getInfo",lf.getInfo(lf_device))
 |string|mount_point 挂载目录名|
 |int|起始偏移量,默认0|
 |int|总大小, 默认是整个flash|
+|table/string|opts 可选, 文件系统选择. nil/"lfs2"为默认; 可传"pgfs"/"tfs"或{fs="pgfs"}、{fs="tfs"}|
 
 **返回值**
 
@@ -215,3 +216,51 @@ log.info("lf.mount",lf.mount(little_flash_device,"/little_flash"))
 
 ---
 
+## lf.unmount(mount_point)
+
+取消挂载 little_flash 文件系统
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|string|mount_point 挂载目录名|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|bool|成功返回true|
+
+**例子**
+
+```lua
+log.info("lf.unmount", lf.unmount("/little_flash"))
+
+```
+
+---
+
+## lf.pgfsctl(cmd, value)
+
+PGFS runtime control helper
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|string|cmd lock_mode\|powercut_stage\|corrupt_latest_cp\|bad_block_once\|reset_runtime\|run_c_tests|
+|string/bool|value value for command|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|bool|success|
+
+**例子**
+
+无
+
+---
+
```

## api/mcu.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/mcu.md b/api/mcu.md
index 9c07b79f..b7b9163f 100644
--- a/api/mcu.md
+++ b/api/mcu.md
@@ -267,7 +267,7 @@ print("ticks", result, diff_tick)
 
 ## mcu.setXTAL(source_main, source_32k, delay)
 
-选择时钟源,当前仅air105支持
+选择时钟源,当前无模组支持
 
 **参数**
 
```

## api/miniz.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/miniz.md b/api/miniz.md
index 4b46b37e..bb76b999 100644
--- a/api/miniz.md
+++ b/api/miniz.md
@@ -106,7 +106,7 @@ end
 
 ---
 
-## miniz.unzip(zip_file_path, target_dir, debug)
+## miniz.unzip(zip_file_path, target_dir, debug, timeout_ms)
 
 解压ZIP文件到指定目录
 
@@ -117,6 +117,7 @@ end
 |string|zip_file_path ZIP文件的完整路径|
 |string|target_dir 目标解压目录的完整路径, 必须以 / 结尾|
 |boolean|debug 可选, 是否输出解压过程日志, 默认为false|
+|int|timeout_ms 可选, 整个unzip过程的超时时间(毫秒), 默认30000|
 
 **返回值**
 
```

## api/mobile.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/mobile.md b/api/mobile.md
index 69978373..50ba087c 100644
--- a/api/mobile.md
+++ b/api/mobile.md
@@ -146,6 +146,28 @@ log.info("simid", mobile.simid())
 
 ---
 
+## mobile.muidSet(muid)
+
+设置MUID
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|string|muid MUID字符串|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|int|0成功, -1失败|
+
+**例子**
+
+无
+
+---
+
 ## mobile.iccid(id)
 
 获取或设置ICCID
@@ -899,54 +921,248 @@ mobile.setBand(buff, 4) --设置使用的band一共4个，为3,5,8,40
 
 ---
 
-## mobile.nstOnOff(onoff, uart_id)
+## mobile.rfTestMode(uart_id, onoff)
+
+RF测试:进入/退出模式 (同 nstOnOff, 推荐用这个)
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|int|串口号,默认 VUART_0|
+|boolean|true 进入, false 退出|
+|return|nil|
+
+**返回值**
+
+无
+
+**例子**
+
+```lua
+mobile.rfTestMode(uart.VUART_0, true)
+mobile.rfTestMode(nil, false)
+
+```
+
+---
+
+## mobile.rfTestInput(data)
 
-RF测试开关和配置
+RF测试:喂入字节 (同 nstInput, 推荐用这个)
 
 **参数**
 
 |传入值类型|解释|
 |-|-|
-|boolean|true开启测试模式，false关闭|
-|int|串口号|
+|string|or zbuff 字节流; 传 nil 表示 flush|
+|return|nil|
+
+**返回值**
+
+无
+
+**例子**
+
+```lua
+mobile.rfTestInput(uart_data)
+mobile.rfTestInput(nil)
+
+```
+
+---
+
+## mobile.rfTestParam(key, value, is_set)
+
+RF测试:查询/设置 PC 端"模组"参数 (NPI 位 / 状态机 / 错误注入)
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|string|key  "rfCaliDone" / "rfNSTDone" / "rfCTDone" / "state" / "erfMode"|
+|int|value   读时忽略, 写时给值|
+|boolean|is_set true=写, false=读 (默认读)|
 
 **返回值**
 
 |返回值类型|解释|
 |-|-|
-|nil|无返回值|
+|int|读时返回值; 写时返回 0 成功 / -1 失败|
 
 **例子**
 
 ```lua
-mobile.nstOnOff(true, uart.VUART_0)    --打开测试模式，并且用虚拟串口发送结果
-mobile.nstOnOff(false) --关闭测试模式
+print(mobile.rfTestParam("state"))  -- 0
+mobile.rfTestParam("rfCaliDone", 1, true)
 
 ```
 
 ---
 
-## mobile.nstInput(data)
+## mobile.rfTestImei()
 
-RF测试数据输入
+RF测试:读 IMEI 字符串 (15 位 ASCII)
+
+**参数**
+
+无
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|string|15 位 IMEI, 失败返回 nil|
+
+**例子**
+
+```lua
+print(mobile.rfTestImei())  --> 864317081553409
+
+```
+
+---
+
+## mobile.rfTestImeiSet(imei)
+
+RF测试:写 IMEI 字符串 (15 位 ASCII)
 
 **参数**
 
 |传入值类型|解释|
 |-|-|
-|string|or zbuff 用户从串口获取的数据，注意，当获取完所有数据后，需要再传一个nil来作为传输结束|
+|string|imei 15 位 IMEI|
 
 **返回值**
 
 |返回值类型|解释|
 |-|-|
-|nil|无返回值|
+|int|0 成功, -1 长度错误|
+
+**例子**
+
+```lua
+mobile.rfTestImeiSet("864317081553409")
+
+```
+
+---
+
+## mobile.rfTestGmData()
+
+RF测试:读 Golden Unit 数据
+
+**参数**
+
+无
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|string|数据字符串, 失败返回 nil|
+
+**例子**
+
+```lua
+print(mobile.rfTestGmData())
+
+```
+
+---
+
+## mobile.rfTestGmDataSet(data)
+
+RF测试:写 Golden Unit 数据
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|string|data 数据字符串|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|int|0 成功, -1 失败|
+
+**例子**
+
+```lua
+mobile.rfTestGmDataSet("golden data")
+
+```
+
+---
+
+## mobile.rfTestNst(hex)
+
+RF测试: NST 校准/非信令指令同步处理
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|string|hex 输入的 hex 字符串, 如 "02040900..."|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|int|0 成功, -2 CRC 错误, -3 数据块索引错误, 其他错误|
+|string/nil|成功且有输出时返回响应字符串 (如 "MT0204..."), 否则 nil|
+
+**例子**
+
+```lua
+local rc, resp = mobile.rfTestNst("02040900010003000500080022002600270028002900000000000000000000000000000000000000000000000000000000000000000000000000000000000000000034126000076A")
+
+```
+
+---
+
+## mobile.rfTestVersion()
+
+RF测试:读取 RF/CP 版本及模块信息
+
+**参数**
+
+无
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|string|AT+ECVERSION? 响应体多行字符串,失败返回nil|
+
+**例子**
+
+```lua
+local info = mobile.rfTestVersion()
+
+```
+
+---
+
+## mobile.rfTestBandList()
+
+RF测试:读取支持的频段列表
+
+**参数**
+
+无
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|string|逗号分隔的频段列表,失败返回nil|
 
 **例子**
 
 ```lua
-mobile.nstInput(uart_data)
-mobile.nstInput(nil)
+local bands = mobile.rfTestBandList()
 
 ```
 
```

## api/natp.md

- 状态：删除
- 提交：110223c0

```diff
diff --git a/api/natp.md b/api/natp.md
deleted file mode 100644
index b150e92b..00000000
--- a/api/natp.md
+++ /dev/null
@@ -1,78 +0,0 @@
-# natp - 网络地址端口转换(开发中)
-
-**示例**
-
-```lua
--- 开发中, 请关注 https://github.com/wendal/xt804-spinet
-
-```
-
-## napt.init(adapter)
-
-初始化NAPT
-
-**参数**
-
-|传入值类型|解释|
-|-|-|
-|int|adapter 目标网卡索引, 默认是socket.LWIP_AP, 这里指内网|
-
-**返回值**
-
-|返回值类型|解释|
-|-|-|
-|nil|无返回值|
-
-**例子**
-
-无
-
----
-
-## napt.rebuild(buff, is_inet, adapter)
-
-重建MAC包
-
-**参数**
-
-|传入值类型|解释|
-|-|-|
-|userdata|待处理的MAC包,必须是zbuff对象|
-|bool|来源是不是内网|
-|int|目标网络适配器的索引, 例如socket.LWIP_GP|
-
-**返回值**
-
-|返回值类型|解释|
-|-|-|
-|bool|成功返回true,失败返回false|
-
-**例子**
-
-无
-
----
-
-## napt.check()
-
-检查和清理NAT表
-
-**参数**
-
-无
-
-**返回值**
-
-|返回值类型|解释|
-|-|-|
-|nil|无返回值|
-
-**例子**
-
-```lua
--- 两次check之间没有数据包的映射记录,会被清理
-
-```
-
----
-
```

## api/ndk.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/ndk.md b/api/ndk.md
index af574271..ebf9b47f 100644
--- a/api/ndk.md
+++ b/api/ndk.md
@@ -3,20 +3,30 @@
 **示例**
 
 ```lua
--- 载入一个RV32镜像并执行若干步
-local ctx, err = ndk.rv32i("/luadb/app.bin", 32 * 1024, 1024)
+-- 最小生命周期: create -> info -> setData -> exec -> getData -> stop/reset -> release
+local ctx, err = ndk.rv32i("/luadb/baremetal.bin", 32 * 1024, 1024)
 if not ctx then
     log.error("ndk", err)
     return
 end
-local ok, ret = ndk.exec(ctx, {steps = 100000, elapsed = 500})
-if ok then
-    log.info("ndk", "retval", ret)
+local info = ndk.info(ctx)
+log.info("ndk", "mem", info.mem, "exchange", info.exchange, "abi", info.abi_version, "features", info.features, "last_error", info.last_error)
+ndk.setData(ctx, "ping")
+local ok, ret, mcause, mtval = ndk.exec(ctx, {steps = 100000, elapsed = 500})
+if not ok then
+    log.error("ndk", ret, mcause, mtval)
+    ndk.stop(ctx, 1000)
+    return
 end
+log.info("ndk", "retval", ret, "data", ndk.getData(ctx, 16, 0))
+ndk.stop(ctx, 1000) -- 空闲态也可安全调用
+ndk.reset(ctx)
+ctx = nil
+collectgarbage("collect")
 
 ```
 
-## ndk.rv32i(path, mem_size, exchange_size)
+## ndk.rv32i(path, mem_size, exchange_size, opts)
 
 创建并加载一个RV32镜像
 
@@ -25,8 +35,9 @@ end
 |传入值类型|解释|
 |-|-|
 |string|path 镜像路径|
-|int|mem_size 可选，沙盒RAM大小，默认 LUAT_NDK_DEFAULT_RAM_SIZE|
-|int|exchange_size 可选，交换区大小，默认 LUAT_NDK_DEFAULT_EXCHANGE_SIZE|
+|int|mem_size 可选，沙盒RAM大小，默认 8 KiB，最大 512 KiB（LUAT_NDK_MAX_RAM_SIZE）|
+|int|exchange_size 可选，交换区大小，默认 LUAT_NDK_DEFAULT_EXCHANGE_SIZE，必须小于 mem_size|
+|table|opts 可选，目前支持 {isa="rv32ima"\|"rv32imf"}|
 
 **返回值**
 
@@ -98,14 +109,14 @@ end
 |传入值类型|解释|
 |-|-|
 |userdata|ctx ndk.rv32i 返回的上下文|
-|int\|table|opts 步数或表 {steps=步数, elapsed=每步时间us}，步数为0使用默认预算|
+|int\|table|opts 步数或表 {steps=步数, elapsed=每步时间us}，steps=0 表示不限步数（运行到 SYSCON 退出、ecall、trap 或 ndk.stop）|
 |int|elapsed_us 可选，opts为数字时的步时间us|
 
 **返回值**
 
 |返回值类型|解释|
 |-|-|
-|boolean,int|成功返回 true,retval；失败返回 false,err,mcause,mtval|
+|boolean,int|成功返回 true,retval；失败返回 false,err,mcause,mtval。运行中调用会返回 busy|
 
 **例子**
 
@@ -127,7 +138,7 @@ end
 
 |返回值类型|解释|
 |-|-|
-|boolean|成功返回 true，失败返回 false,err|
+|boolean|成功返回 true，失败返回 false,err。运行中/停止中调用会返回 busy|
 
 **例子**
 
@@ -144,14 +155,14 @@ end
 |传入值类型|解释|
 |-|-|
 |userdata|ctx ndk.rv32i 返回的上下文|
-|int\|table|opts 步数或表 {steps=步数, elapsed=每步时间us}|
+|int\|table|opts 步数或表 {steps=步数, elapsed=每步时间us}，steps=0 表示不限步数|
 |int|elapsed_us 可选，opts为数字时的步时间us|
 
 **返回值**
 
 |返回值类型|解释|
 |-|-|
-|int|线程ID，失败返回 nil,err|
+|int|线程ID（递增），失败返回 nil,err。运行中/停止中调用会返回 busy|
 
 **例子**
 
@@ -174,7 +185,7 @@ end
 
 |返回值类型|解释|
 |-|-|
-|boolean|成功返回 true，失败返回 false,err|
+|boolean|成功返回 true，失败返回 false,err。空闲态调用为幂等成功；wait_ms=0可用于非阻塞轮询|
 
 **例子**
 
@@ -196,7 +207,7 @@ end
 
 |返回值类型|解释|
 |-|-|
-|table|包含 mem/exchange/exchange_addr/image/running/mcause/mtval|
+|table|包含 mem/exchange/exchange_addr/image/running/mcause/mtval/abi_magic/abi_version/features/last_error/event_slots/isa/flen/fcsr/frm/fflags，便于判断生命周期状态和ABI能力|
 
 **例子**
 
```

## api/netdrv.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/netdrv.md b/api/netdrv.md
index b165c2de..23f6758e 100644
--- a/api/netdrv.md
+++ b/api/netdrv.md
@@ -11,6 +11,10 @@
 |netdrv.RESET_HARD|number|请求对网卡硬复位,当前仅支持CH390H|
 |netdrv.RESET_SOFT|number|请求对网卡软复位,当前仅支持CH390H|
 |netdrv.EVT_SOCKET|number|事件类型-socket事件|
+|netdrv.CH_HW|number|数据包通道-物理硬件 (HW RX = FROM_HW, send_raw target TO_HW)|
+|netdrv.CH_LWIP|number|数据包通道-LWIP协议栈 (send_raw target TO_LWIP, 未来 FROM_LWIP)|
+|netdrv.CH_NAPT|number|数据包通道-NAPT层 (send_raw target TO_NAPT, 未来 FROM_NAPT)|
+|netdrv.EVT_PKG|number|事件类型-数据包事件|
 
 
 ## netdrv.setup(id, tp, opts)
@@ -370,55 +374,24 @@ end)
 
 ---
 
-## netdrv.on(adapter_id, event_type, callback)
+## netdrv.send_raw(id, target, zbuff, len)
 
-订阅网络事件
+直接向 netdrv 链路投递原始数据包
 
 **参数**
 
 |传入值类型|解释|
 |-|-|
-|int|网络适配器的id|
-|int|事件总类型, 当前支持 netdrv.EVT_SOCKET|
-|function|回调函数 function(id, event, params)|
+|int|网络适配器编号|
+|int|投递目标 (target/dst):|
 
 **返回值**
 
-|返回值类型|解释|
-|-|-|
-|bool|成功与否,成功返回true,否则返回nil|
+无
 
 **例子**
 
-```lua
--- 订阅socket连接状态变化事件
-netdrv.on(socket.LWIP_ETH, netdrv.EVT_SOCKET, function(id, event, params)
-    -- id 是网络适配器id
-    -- event是事件id, 字符串类型, 
-        - create 创建socket对象
-        - release 释放socket对象
-        - connecting 正在连接, 域名解析成功后出现
-        - connected 连接成功, TCP三次握手成功后出现
-        - closed 连接关闭
-        - remote_close 远程关闭, 网络中断,或者服务器主动断开
-        - timeout dns解析超时,或者tcp连接超时
-        - error 错误,包括一切异常错误
-    -- params是参数表
-        - remote_ip 远端ip地址,未必存在
-        - remote_port 远端端口,未必存在
-        - online_ip 实际连接的ip地址,未必存在
-        - domain_name 远端域名,如果是通过域名连接的话, release时没有这个值, create时也没有
-    log.info("netdrv", "socket event", id, event, json.encode(params or {}))
-    if params then
-        -- params里会有remote_ip, remote_port等信息, 可按需获取
-        local remote_ip = params.remote_ip
-        local remote_port = params.remote_port
-        local domain_name = params.domain_name
-        log.info("netdrv", "socket event", "remote_ip", remote_ip, "remote_port", remote_port, "domain_name", domain_name)
-    end
-end)
-
-```
+无
 
 ---
 
```

## api/pm.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/pm.md b/api/pm.md
index 9aea06a4..04a166ef 100644
--- a/api/pm.md
+++ b/api/pm.md
@@ -194,7 +194,7 @@ local timer_id = pm.dtimerWkId()
 
 |返回值类型|解释|
 |-|-|
-|int|0-上电/复位开机, 1-RTC开机, 2-WakeupIn/Pad/IO开机, 3-未知原因(Wakeup/RTC皆有可能)开机,目前只有air101,air103会有这个返回值|
+|int|0-上电/复位开机, 1-RTC开机, 2-WakeupIn/Pad/IO开机, 3-未知原因(Wakeup/RTC皆有可能)开机|
 |int|0-普通开机(上电/复位),3-深睡眠开机,4-休眠开机|
 |int|复位开机详细原因：0-powerkey或者上电开机 1-充电或者AT指令下载完成后开机 2-闹钟开机 3-软件重启 4-未知原因 5-RESET键 6-异常重启 7-工具控制重启 8-内部看门狗重启 9-外部重启 10-充电开机|
 |int|WakeupPad唤醒情况下，具体是哪些pad唤醒，每个bit代表1个引脚，目前只有移芯平台有用，2026.1.15启用|
```

## api/socket.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/socket.md b/api/socket.md
index daaf4744..a9081ce7 100644
--- a/api/socket.md
+++ b/api/socket.md
@@ -23,7 +23,6 @@
 |socket.LWIP_STA|number|使用LWIP协议栈的WIFI STA，值为2|
 |socket.LWIP_AP|number|使用LWIP协议栈的WIFI AP，值为3|
 |socket.LWIP_GP|number|使用LWIP协议栈的移动蜂窝模块，值为1|
-|socket.USB|number|使用LWIP协议栈的USB网卡，值为6|
 |socket.LINK|number|LINK事件|
 |socket.ON_LINE|number|ON_LINE事件|
 |socket.EVENT|number|EVENT事件|
@@ -39,6 +38,7 @@
 |socket.LWIP_USER6|number|使用LWIP协议栈的自定义网卡6, 2025.1.12新增|
 |socket.LWIP_USER7|number|使用LWIP协议栈的自定义网卡7, 2025.1.12新增|
 |socket.LWIP_GP_GW|number|4G代理网关|
+|socket.LWIP_USB|number|LWIP-side USB netif (RNDIS/CDC-ECM)|
 
 
 ## socket.localIP(adapter)
```

## api/supported.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/supported.md b/api/supported.md
index 4b2ce792..dbba5064 100644
--- a/api/supported.md
+++ b/api/supported.md
@@ -30,6 +30,7 @@
 |[fota](fota.md)|`底层固件升级`|
 |[fskv](fskv.md)|`kv数据库,掉电不丢数据`|
 |[ftp](ftp.md)|`ftp 客户端 (服务器推荐使用vsftpd,其他暂不做支持)`|
+|[gbc](gbc.md)|`GBC模拟器`|
 |[gmssl](gmssl.md)|`国密算法(SM2/SM3/SM4)`|
 |[gpio](gpio.md)|`GPIO操作`|
 |[gtfont](gtfont.md)|`高通字库芯片`|
@@ -66,7 +67,6 @@
 |[mobile](mobile.md)|`蜂窝网络`|
 |[modbus](modbus.md)|`modbus主从协议栈协议`|
 |[mqtt](mqtt.md)|`mqtt客户端`|
-|[natp](natp.md)|`网络地址端口转换(开发中)`|
 |[ndk](ndk.md)|`在沙盒化的RV32环境中运行MiniRV32IMA镜像`|
 |[nes](nes.md)|`nes模拟器`|
 |[netdrv](netdrv.md)|`网络设备管理`|
@@ -104,7 +104,6 @@
 |[tp](tp.md)|`触摸库`|
 |[u8g2](u8g2.md)|`u8g2图形处理库`|
 |[uart](uart.md)|`串口操作库`|
-|[ulwip](ulwip.md)|`用户空间的lwip集成(开发中)`|
 |[usb](usb.md)|`usb操作库`|
 |[usbapp](usbapp.md)|`USB功能操作`|
 |[videoplayer](videoplayer.md)|`视频播放库`|
```

## api/touchkey.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/touchkey.md b/api/touchkey.md
index 8763a267..8fb52f63 100644
--- a/api/touchkey.md
+++ b/api/touchkey.md
@@ -8,7 +8,7 @@
 
 |传入值类型|解释|
 |-|-|
-|int|传感器id,请查阅硬件文档, 例如air101/air103支持 1~15, 例如PA7对应touch id=1|
+|int|传感器id,请查阅硬件文档|
 |int|扫描间隔,范围1 ~ 0x3F, 单位16ms,可选|
 |int|扫描窗口,范围2-7, 可选|
 |int|阀值, 范围0-127, 可选|
```

## api/tp.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/tp.md b/api/tp.md
index 2aadb8da..3ded5f10 100644
--- a/api/tp.md
+++ b/api/tp.md
@@ -79,3 +79,35 @@
 
 ---
 
+## tp.wakeup(tp_device)
+
+触摸休眠唤醒
+
+**参数**
+
+|传入值类型|解释|
+|-|-|
+|userdata|tp_device:触摸设备对象|
+
+**返回值**
+
+|返回值类型|解释|
+|-|-|
+|boolean|唤醒成功返回true,失败返回false|
+
+**例子**
+
+```lua
+    local function tp_callBack(tp_device, tp_data)
+        log.info("TP", tp_data[1].x, tp_data[1].y, tp_data[1].event)
+        sys.publish("TP", tp_device, tp_data)
+    end
+
+    tp_device = tp.init("gt911",{port=0,pin_rst = 22,pin_int = 23},tp_callBack)
+    tp.sleep(tp_device)
+    tp.wakeup(tp_device)
+
+```
+
+---
+
```

## api/u8g2.md

- 状态：修改
- 提交：110223c0

```diff
diff --git a/api/u8g2.md b/api/u8g2.md
index 49551688..12dbb0bd 100644
--- a/api/u8g2.md
+++ b/api/u8g2.md
@@ -13,6 +13,15 @@
 
 |常量|类型|解释|
 |-|-|-|
+|u8g2.flush_page|number|标准分页寻址刷新|
+|u8g2.flush_page_arg|number|分页命令后带页参数的刷新|
+|u8g2.flush_window_gray4|number|窗口寻址并将1bpp转换为4bpp灰阶|
+|u8g2.flush_window_2row_lut|number|双行查表打包窗口刷新|
+|u8g2.vertical_top|number|U8g2纵向字节布局|
+|u8g2.horizontal_right|number|U8g2横向字节布局|
+|u8g2.cad_001|number|CAD 001命令参数数据模式|
+|u8g2.cad_011|number|CAD 011命令参数数据模式|
+|u8g2.cad_100|number|CAD 100命令参数数据模式|
 |u8g2.DRAW_UPPER_RIGHT|number|上右|
 |u8g2.DRAW_UPPER_LEFT|number|上左|
 |u8g2.DRAW_LOWER_LEFT|number|下左|
@@ -58,6 +67,12 @@ u8g2显示屏初始化
 -- i2c_sda: 数值软件i2c时数据线的GPIO编号
 -- spi_id、spi_res、spi_dc、spi_cs: 数值,硬件spi的SPI编号,复位GPIO编号,DC线的GPIO编号, CS线的GPIO编号
 -- x_offset: 数值,X轴偏移量,默认按驱动走, 2023.11.10新增的配置项
+-- ic="custom"时第二个table必须包含width/height
+-- tile_w/tile_h: 可选,默认ceil(width/8)、ceil(height/8)
+-- flush_mode: 可选,默认u8g2.flush_page;另支持flush_page_arg、flush_window_gray4、flush_window_2row_lut
+-- hvline/cad_mode: 可选,默认值由flush_mode决定;不兼容的hvline会初始化失败
+-- flush_window_2row_lut还需要column_start,row_offset可选且默认0
+-- initcmd元素:0x0001xxxx延时、0x0002xx命令、0x0003xx数据
 
 -- 初始化硬件i2c的ssd1306
 u8g2.begin({ic = "ssd1306",direction = 0,mode="i2c_hw",i2c_id=0}) -- direction 可选0 90 180 270
```

## api/ulwip.md

- 状态：删除
- 提交：110223c0

```diff
diff --git a/api/ulwip.md b/api/ulwip.md
deleted file mode 100644
index aa406b90..00000000
--- a/api/ulwip.md
+++ /dev/null
@@ -1,257 +0,0 @@
-# ulwip - 用户空间的lwip集成(开发中)
-
-**示例**
-
-```lua
---[[
-注意: 本库处于开发中, 接口随时可能变化
-用户空间的LWIP集成, 用于支持lwip的netif的网络集成, 实现在lua代码中直接控制MAC包/IP包的收发
-
-总体数据路径如下
-
-lua代码 -> ulwip.input -> lwip(netif->input) -> lwip处理逻辑 -> luatos socket框架
-
-lua代码 <- ulwip回调函数 <- lwip(netif->low_level_output) <- lwip处理逻辑 <- luatos socket框架
-
-应用示例:
-1. Air601的wifi模块作为被控端, 通过UART/SPI收发MAC包, 实现Air780E/Air780EP集成wifi模块的功能
-2. 使用W5500/CH395/ENC28J60等以太网模块, 在用户lua代码中控制其mac包收发, 并集成到luatos socket框架中
-3. 通过蓝牙模块,集成lowpan6
-
--- 开发中, 请关注 https://github.com/wendal/xt804-spinet
-]]
-
-```
-
-## ulwip.setup(adapter_index, mac, output_lua_ref, opts)
-
-初始化lwip netif
-
-**参数**
-
-|传入值类型|解释|
-|-|-|
-|int|adapter_index 适配器编号|
-|string|mac 网卡mac地址|
-|function|output_lua_ref 回调函数, 参数为(adapter_index, data)|
-|table|额外参数, 例如 {mtu=1500, flags=(ulwip.FLAG_BROADCAST \| ulwip.FLAG_ETHARP)}|
-
-**返回值**
-
-|返回值类型|解释|
-|-|-|
-|boolean|成功与否|
-
-**例子**
-
-```lua
--- 初始化一个适配器, 并设置回调函数
-ulwip.setup(socket.LWIP_STA, string.fromHex("18fe34a27b69"), function(adapter_index, data)
-    log.info("ulwip", "output_lua_ref", adapter_index, data:toHex())
-end)
--- 注意, setup之后, netif的状态是down, 调用ulwip.updown(adapter_index, true)后, 才能正常收发数据
-
--- 额外参数配置table可选值
--- mtu, 默认1460
--- flags, 默认 ulwip.FLAG_BROADCAST | ulwip.FLAG_ETHARP | ulwip.FLAG_ETHERNET | ulwip.FLAG_IGMP | ulwip.FLAG_MLD6
--- zbuff_out 回调函数接受zbuff作为参数, 默认false
--- reverse 本地lwip设备,翻转调用逻辑, 默认false, 这个参数是为了拦截当前设备的硬件联网数据所设计的
-
-```
-
----
-
-## ulwip.updown(adapter_index, up)
-
-设置netif的状态
-
-**参数**
-
-|传入值类型|解释|
-|-|-|
-|int|adapter_index 适配器编号|
-|boolean|up true为up, false为down|
-
-**返回值**
-
-|返回值类型|解释|
-|-|-|
-|boolean|成功与否|
-
-**例子**
-
-```lua
--- 参考ulwip.setup
-
-```
-
----
-
-## ulwip.link(adapter_index, up)
-
-设置netif的物理链路状态
-
-**参数**
-
-|传入值类型|解释|
-|-|-|
-|int|adapter_index 适配器编号|
-|boolean|up true为up, false为down|
-
-**返回值**
-
-|返回值类型|解释|
-|-|-|
-|boolean|当前状态|
-
-**例子**
-
-```lua
--- 参考ulwip.setup
-
-```
-
----
-
-## ulwip.input(adapter_index, data, len, offset)
-
-往netif输入数据
-
-**参数**
-
-|传入值类型|解释|
-|-|-|
-|int|adapter_index 适配器编号|
-|string/userdata|data 输入的数据|
-|int|如果data是zbuff, len默认是zbuff的used, 对string无效|
-|int|如果data是zbuff, offset为数据起始位置, 默认是0, 对string无效|
-
-**返回值**
-
-|返回值类型|解释|
-|-|-|
-|boolean|成功与否|
-
-**例子**
-
-```lua
--- 参考ulwip.setup
-
-```
-
----
-
-## ulwip.dhcp(adapter_index, up)
-
-启动或关闭dhcp
-
-**参数**
-
-|传入值类型|解释|
-|-|-|
-|int|adapter_index 适配器编号|
-|boolean|up true为启动, false为关闭|
-
-**返回值**
-
-|返回值类型|解释|
-|-|-|
-|boolean|当前状态|
-
-**例子**
-
-```lua
--- 参考ulwip.setup
-
-```
-
----
-
-## ulwip.ip(adapter_index, ip, netmask, gw)
-
-设置或获取ip信息
-
-**参数**
-
-|传入值类型|解释|
-|-|-|
-|int|adapter_index 适配器编号|
-|string|ip IP地址, 仅获取时可以不填|
-|string|netmask 子网掩码, 仅获取时可以不填|
-|string|gw 网关地址, 仅获取时可以不填|
-
-**返回值**
-
-|返回值类型|解释|
-|-|-|
-|string|ip地址, 子网掩码, 网关地址|
-
-**例子**
-
-```lua
--- 获取现有值
-local ip, netmask, gw = ulwip.ip(socket.LWIP_STA)
--- 设置新值
-ulwip.ip(socket.LWIP_STA, "192.168.0.1", "255.255.255.0", "192.168.0.1")
-
-```
-
----
-
-## ulwip.reg(adapter_index)
-
-将netif注册到luatos socket中
-
-**参数**
-
-|传入值类型|解释|
-|-|-|
-|int|adapter_index 适配器编号|
-
-**返回值**
-
-|返回值类型|解释|
-|-|-|
-|boolean|成功与否|
-
-**例子**
-
-```lua
--- 参考ulwip.setup
-
-```
-
----
-
-## ulwip.xt804_xfer(spi_id, cs_pin, addr, zbuff, len, offset, auto_seek, auto_len)
-
-操作XT804进行SPI快速收发
-
-**参数**
-
-|传入值类型|解释|
-|-|-|
-|int|spi_id SPI的ID号|
-|int|cs_pin CS脚的GPIO号|
-|int|addr 寄存器地址|
-|zbuff|zbuff对象|
-|int|len 长度|
-|int|offset 偏移量, 默认buff:used()|
-|boolean|auto_seek 是否自动移动偏移量, 默认false|
-|int|auto_len 自动分片长度, 默认按寄存器自动选择|
-
-**返回值**
-
-|返回值类型|解释|
-|-|-|
-|nil|无返回值|
-
-**例子**
-
-```lua
--- 本函数属于辅助函数
-
-```
-
----
-
```

