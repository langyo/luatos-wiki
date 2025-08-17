# exnetif - exnetif 控制网络优先级（以太网->WIFI->4G）根据优先级选择上网的网卡。简化开启多网融合的操作，4G作为数据出口给WIFI,以太网设备上网，以太网作为数据出口给WIFI,Air8000上网，WIFI作为数据出口给Air8000,以太网上网。

**示例**

```lua
本文件的对外接口有4个：
1、exnetif.set_priority_order(networkConfigs)：设置网络优先级顺序并初始化对应网络(需要在task中调用)
2、exnetif.notify_status(cb_fnc)：设置网络状态变化回调函数
3、exnetif.setproxy(adapter, main_adapter,other_configs)：配置网络代理实现多网融合(需要在task中调用)
4、exnetif.check_network_status(interval),检测间隔时间ms(选填)，不填时只检测一次，填写后将根据间隔时间循环检测，会提高模块功耗

```

## exnetif.set_priority_order(new_priority)

设置网络优先级，相应网卡获取到ip且网络正常视为网卡可用，丢失ip视为网卡不可用.(需要在task中调用)

**参数**

|传入值类型|解释|
|-|-|
|table|网络优先级列表,优先级从高到低对应table中的第一个参数到最后一个参数|

**返回值**

|返回值类型|解释|
|-|-|
|boolean|成功返回true，失败返回false|

**例子**

```lua
exnetif.set_priority_order({
    { -- 最高优先级网络
        WIFI = { -- WiFi配置
            ssid = "your_ssid",       -- WiFi名称(string)
            password = "your_pwd",    -- WiFi密码(string)
            local_network_mode = true,-- 局域网模式(选填参数)，设置为true时，exnetif会自动将ping_ip设置为网卡的网关ip。
                                      -- 用户不需要传入ping_ip参数，即使传入了，也无效。
                                      -- 这个模式的使用场景，仅适用于局域网环境；可以访问外网时，不要使用
            ping_ip = "112.125.89.8", -- 连通性检测IP(选填参数),默认使用httpdns获取baidu.com的ip作为判断条件，
                                      -- 注：如果填写ip，则ping通作为判断网络是否可用的条件，
                                      -- 所以需要根据网络环境填写内网或者外网ip,
                                      -- 填写外网ip的话要保证外网ip始终可用，
                                      -- 填写局域网ip的话要确保相应ip固定且能够被ping通
            ping_time = 10000         -- 填写ping_ip且未ping通时的检测间隔(ms, 可选，默认为10秒)
                                      -- 定时ping将会影响模块功耗，使用低功耗模式的话可以适当延迟间隔时间
        }
    },
    { -- 次优先级网络
        ETHERNET = { -- 以太网配置
            pwrpin = 140,             -- 供电使能引脚(number)
            local_network_mode = true,-- 局域网模式(选填参数)，设置为true时，exnetif会自动将ping_ip设置为网卡的网关ip。
                                      -- 用户不需要传入ping_ip参数，即使传入了，也无效。
                                      -- 这个模式的使用场景，仅适用于局域网环境；可以访问外网时，不要使用
            ping_ip = "112.125.89.8", -- 连通性检测IP(选填参数),默认使用httpdns获取baidu.com的ip作为判断条件，
                                      -- 注：如果填写ip，则ping通作为判断网络是否可用的条件，
                                      -- 所以需要根据网络环境填写内网或者外网ip,
                                      -- 填写外网ip的话要保证外网ip始终可用，
                                      -- 填写局域网ip的话要确保相应ip固定且能够被ping通
            ping_time = 10000         -- 填写ping_ip且未ping通时的检测间隔(ms, 可选,默认为10秒)
                                      -- 定时ping将会影响模块功耗，使用低功耗模式的话可以适当延迟间隔时间
            tp = netdrv.CH390         -- 网卡芯片型号(选填参数)，仅spi方式外挂以太网时需要填写。
            opts = { spi = 1, cs = 12 }   -- 外挂方式,需要额外的参数(选填参数)，仅spi方式外挂以太网时需要填写。
        }
    },
    { -- 最低优先级网络
        LWIP_GP = true  -- 启用4G网络
    }
})

```

---

## exnetif.notify_status(cb_fnc)

设置网络状态变化回调函数。触发条件：网卡切换或者所有网卡都断网。回调函数的输入参数: 1. 当有可用网络的时候，返回当前使用网卡、网卡id；2. 当没有可用网络的时候，返回 nil、-1 。

**参数**

|传入值类型|解释|
|-|-|
|function|回调函数|

**返回值**

无

**例子**

```lua
    exnetif.notify_status(function(net_type,adapter)
    log.info("可以使用优先级更高的网络:", net_type,adapter)
    end)

```

---

## exnetif.setproxy(adapter, main_adapter,other_configs)

设置多网融合模式，例如4G作为数据出口给WIFI或以太网设备上网(需要在task中调用)

**参数**

|传入值类型|解释|
|-|-|
|adapter|需要使用网络的网卡，例如socket.LWIP_ETH|
|adapter|提供网络的网卡，例如socket.LWIP_GP|
|table|其他设置参数(选填参数)，|

**返回值**

无

**例子**

```lua
    --典型应用：
    -- 4G作为出口供WiFi和以太网设备上网
    exnetif.setproxy(socket.LWIP_AP, socket.LWIP_GP, {
        ssid = "Hotspot",                -- WiFi名称(string)，网卡包含wifi时填写
        password = "password123",        -- WiFi密码(string)，网卡包含wifi时填写
        adapter_addr = "192.168.5.1",    -- adapter网卡的ip地址(选填),需要自定义ip和网关ip时填写
        adapter_gw= { 192, 168, 5, 1 },   -- adapter网卡的网关地址(选填),需要自定义ip和网关ip时填写
        ap_opts={                        -- AP模式下配置项(选填参数)
        hidden = false,                  -- 是否隐藏SSID, 默认false,不隐藏
        max_conn = 4 },                  -- 最大客户端数量, 默认4
        channel=6                        -- AP建立的通道, 默认6
    })
    exnetif.setproxy(socket.LWIP_ETH, socket.LWIP_GP, {
        tp = netdrv.CH390,               -- 网卡芯片型号(选填参数)，仅spi方式外挂以太网时需要填写。
        opts = { spi = 1, cs = 12},      -- 外挂方式,需要额外的参数(选填参数)，仅spi方式外挂以太网时需要填写。
        ethpower_en = 140,               -- 以太网模块的pwrpin引脚(gpio编号)
        adapter_addr = "192.168.5.1",    -- adapter网卡的ip地址(选填),需要自定义ip和网关ip时填写
        adapter_gw= { 192, 168, 5, 1 },   -- adapter网卡的网关地址(选填),需要自定义ip和网关ip时填写
    })
    -- 以太网作为出口供WiFi设备上网
    exnetif.setproxy(socket.LWIP_AP, socket.LWIP_ETH, {
        ssid = "Hotspot",                -- WiFi名称(string)，网卡包含wifi时填写
        password = "password123",        -- WiFi密码(string)，网卡包含wifi时填写
        tp = netdrv.CH390,               -- 网卡芯片型号(选填参数)，仅spi方式外挂以太网时需要填写。
        opts = { spi = 1, cs = 12},      -- 外挂方式,需要额外的参数(选填参数)，仅spi方式外挂以太网时需要填写。
        ethpower_en = 140,               -- 以太网模块的pwrpin引脚(gpio编号)
    })
    -- 4G作为出口供以太网设备上网
    exnetif.setproxy(socket.LWIP_ETH, socket.LWIP_GP, {
        tp = netdrv.CH390,               -- 网卡芯片型号(选填参数)，仅spi方式外挂以太网时需要填写。
        opts = { spi = 1, cs = 12},      -- 外挂方式,需要额外的参数(选填参数)，仅spi方式外挂以太网时需要填写。
        ethpower_en = 140,               -- 以太网模块的pwrpin引脚(gpio编号)
    })

```

---

## exnetif.check_network_status(interval),

对正常状态的网卡进行ping测试

**参数**

|传入值类型|解释|
|-|-|
|int|检测间隔时间ms(选填)，不填时只检测一次，填写后将根据间隔时间循环检测，会提高模块功耗|

**返回值**

无

**例子**

无

---

