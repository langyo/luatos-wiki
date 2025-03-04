# ftp - ftp 客户端

## ftp.login(adapter,ip_addr,port,username,password)



FTP客户端

**参数**

|传入值类型|解释|
|-|-|
|int|适配器序号, 只能是socket.ETH0, socket.STA, socket.AP,如果不填,会选择平台自带的方式,然后是最后一个注册的适配器|
|string|ip_addr 地址|
|string|port 端口,默认21|
|string|username 用户名|
|string|password 密码|
|bool/table|是否为ssl加密连接,默认不加密,true为无证书最简单的加密，table为有证书的加密 <br>server_cert 服务器ca证书数据 <br>client_cert 客户端ca证书数据 <br>client_key 客户端私钥加密数据 <br>client_password 客户端私钥口令数据|

**返回值**

|返回值类型|解释|
|-|-|
|bool/string|成功返回true 失败返回string|

**例子**

```lua
ftp_login = ftp.login(nil,"xxx")

```

---

## ftp.command(cmd)



FTP命令

**参数**

|传入值类型|解释|
|-|-|
|string|cmd 命令 目前支持:NOOP SYST TYPE PWD MKD CWD CDUP RMD DELE LIST|

**返回值**

|返回值类型|解释|
|-|-|
|string|成功返回true 失败返回string|

**例子**

```lua
    // 空操作，防止连接断掉
    print(ftp.command("NOOP").wait())
    // 报告远程系统的操作系统类型
    print(ftp.command("SYST").wait())
    // 指定文件类型
    print(ftp.command("TYPE I").wait())
    // 显示当前工作目录名
    print(ftp.command("PWD").wait())
    // 创建目录
    print(ftp.command("MKD QWER").wait())
    // 改变当前工作目录
    print(ftp.command("CWD /QWER").wait())
    // 返回上一层目录
    print(ftp.command("CDUP").wait())
    // 删除目录
    print(ftp.command("RMD QWER").wait())
    // 获取当前工作目录下的文件名列表
    print(ftp.command("LIST").wait())
    // 删除文件
    print(ftp.command("DELE /1/12222.txt").wait())

```

---

## ftp.pull(local_name,remote_name)



FTP文件下载

**参数**

|传入值类型|解释|
|-|-|
|string|local_name 本地文件|
|string|remote_name 服务器文件|

**返回值**

|返回值类型|解释|
|-|-|
|bool/string|成功返回true 失败返回string|

**例子**

```lua
ftp.pull("/1222.txt","/1222.txt").wait()

```

---

## ftp.push(local_name,remote_name)



FTP文件上传

**参数**

|传入值类型|解释|
|-|-|
|string|local_name 本地文件|
|string|remote_name 服务器文件|

**返回值**

|返回值类型|解释|
|-|-|
|bool/string|成功返回true 失败返回string|

**例子**

```lua
ftp.push("/1222.txt","/1222.txt").wait()

```

---

## ftp.close()



FTP客户端关闭

**参数**

无

**返回值**

|返回值类型|解释|
|-|-|
|bool/string|成功返回true 失败返回string|

**例子**

```lua
ftp.close().wait()

```

---

## ftp.debug(onoff)



配置是否打开debug信息

**参数**

|传入值类型|解释|
|-|-|
|boolean|是否打开debug开关|

**返回值**

|返回值类型|解释|
|-|-|
|nil|无返回值|

**例子**

无

---

