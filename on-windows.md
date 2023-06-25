# 在Windows上使用webDAV

适用于在局域网中跨设备传输文件这样的场景

首先感谢源仓库[hacdias/webdav](https://github.com/hacdias/webdav)

# 安装

请新开一个浏览器窗口去下载页 [Releases page](https://github.com/hacdias/webdav/releases)

下载并解压好文件

一般下载`amd64`的版本

**在同级目录下创建**`config.yaml`

```yaml
# 启动配置
address: 0.0.0.0
# 请自行设定监听端口,示例5599端口
# 请确认防火墙放行该端口
port: 5599
# 启用授权
auth: true
# 禁用TLS时使用http，启用时使用https
tls: false
cert: cert.pem
key: key.pem
# URL前缀，建议使用默认
prefix: /
debug: false

# 默认用户设置 (will be merged)
scope: .
modify: true
rules: []

# CORS configuration
# 跨域设置
cors:
  enabled: true
  credentials: true
  allowed_headers:
    - Depth
  allowed_hosts:
    - http://localhost:8080
  allowed_methods:
    - GET
  exposed_headers:
    - Content-Length
    - Content-Range

# 用户自定义配置
users:
# 账户名与密码(请不要对字符串值打引号)
  - username: admin
    password: admin
# 访问地址，绝对路径
    scope: E:\torrent
# 是否拥有修改文件权限
    modify: true
```

# 注意事项

1. 防火墙放行对应的端口
2. 共享的文件夹放行权限（推荐属性-安全-编辑-添加-输入everyone-检查名称-确定-勾选完全控制-确定）
3. 配置文件中的值**不要**加引号

# 启动

使用**CMD**

`start .\webdav.exe`

## 创建启动脚本

`startup.bat`

```bat
@echo off
start .\webdav.exe
```

