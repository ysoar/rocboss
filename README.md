
#根据 rocboss  v2.2.1 微论坛改版
## 主要新特性
- 新增全文索引支持(xunsearch)
- 新增积分提现功能
- 新增会员间积分转账功能
- 新增文章模块
- 新增明/暗两套主题，可自主切换
- 新增微信扫码登录模块
- 前端Webpack打包
- 优化系统结构
- 变更加密流程，提高安全性
- 解决2.2.0中存留的一些小BUG

## 安装须知

**环境要求**

1. PHP >= 5.4，MySQL >= 5.5
2. 部署Redis服务器以及对应的PHP Redis扩展
3. 部署[Xunsearch服务器][0](如果不启用可忽略该步骤)
4. 开启pdo_mysql扩展
5. 支持伪静态（建议使用Linux操作系统，**不支持虚拟主机**!）

**安装步骤**

1. 配置网站指向到 web/ 目录下

2. 导入 install.sql 数据库文件

3. 修改配置文件，**app/config/** 下的文件需要分别重命名为 _base.php,_othere.php,_database.php，然后根据注释修改配置。

4. 新建并设置 app/cache 目录777权限

5. 配置文件完全填写结束后，访问首页，管理员登陆后，可进入管理地址 : `你的网址/admin`， 默认管理员 `admin` 密码 `123123123`

6. 关于伪静态，apache环境直接使用 .htaccess 文件，nginx使用如下规则：
    ```
    location / {
        try_files $uri $uri/ /index.php;
    }
    ```

7. 由于使用[七牛云存储][1]，所以需要配置图片处理样式，分割符为“ - ”，必须配置，否则图片无法使用
    - - -
        名称： `800`
        处理接口： 自行控制水印等，宽度800
    - - -
        名称： `100x100`
        处理接口：`imageView2/1/w/100/h/100/q/100`
    - - -
        名称：`800.png`
        处理接口：自行控制水印等，宽度800
    - - -
        名称：`90x68.png`
        处理接口： `imageView2/1/w/90/h/68/q/100/format/png`
    - - -
        名称：`avatar.png`
        处理接口：`imageView2/1/w/100/h/100/q/100/format/png`

8. 针对启用xunsearch的用户，考虑到数据的一致性和老数据的同步，项目根目录下提供 console 脚本文件，项目根目录下执行 ``` ./console index/push-all ``` 命令即可全量推送数据到索引服务器，建议每天定时跑一次该脚本。

#### 附言

  [0]:http://www.xunsearch.com/
  [1]: https://portal.qiniu.com/signup?code=3lho3ffob4oya
