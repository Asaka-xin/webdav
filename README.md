> 本仓库将用中文帮助你搭建自定义的WebDAV

# webdav

**感谢源仓库作者**

[前往源仓库](https://github.com/hacdias/webdav)

一份中文指南，主要针对`Windows`平台与`Linux`平台

此为`Linux`上的部署指南，[前往查看Windows上的配置](./on-windows.md)

# 安装

如果你希望使用`Docker`来安装，那么你可以使用源仓库中的`Dockerfile`来自行构建镜像

请新开一个浏览器窗口去下载页 [Releases page](https://github.com/hacdias/webdav/releases)

下载并解压好文件

# 配置

请注意文件操作权限

我推荐在`webdav`的同级目录创建配置文件`./config.yaml`

以下是来自源仓库的配置模板

```yaml
# 启动配置
address: 0.0.0.0
# 请自行设定监听端口,示例5599端口
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
    scope: /share/01
# 是否拥有修改文件权限
    modify: true
# 另一个用户的配置
  - username: encrypted
    password: "{bcrypt}$2y$10$zEP6oofmXFeHaeMfBNLnP.DO8m.H.Mwhd24/TOX2MWLxAExXi4qgi"
# 读取环境变量
  - username: "{env}ENV_USERNAME"
    password: "{env}ENV_PASSWORD"
    
  - username: basic
    password: basic
    modify:   false
    rules:
      - regex: false
        allow: false
        path: /some/file
      - path: /public/access/
        modify: true
```

使用`./webdav -h`获得更多帮助提示

# 支持Systemd

支持`systemd` 查看详情 [webdav.service.example](/webdav.service.example).

# 在Alist中使用

驱动选择`webdav`

> URL:http://username@host:port
>
> username:
>
> password:
>
> 示例填写(admin/admin)你在其它地方可能会需要手动填写URL
>
> URL:http://admin@192.168.1.23:5599

# 启动

`./webdav`优先读取`./config.yaml`配置文件

可选的启动方式`./webdav -c config的地址` 查看更多`./webdav -h`
