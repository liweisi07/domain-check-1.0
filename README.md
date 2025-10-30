# domain-check
这是一个简洁高效的域名可视化展示面板，基于Cloudflare Workers构建。它提供了一个直观的界面，让用户能够一目了然地查看他们域名的状态、注册商、注册日期、过期日期和使用进度，并可在到期前通过TG机器人向用户推送通知。
项目基于yutian81的项目<https://github.com/yutian81/domain-check>进行完善，增加了密码登录

**DEMO**：<https://domains.yutian81.top>  

## 2025-02-26 更新：增加了密码登录校验，将DOMAINS参数改为变量绑定方式配置，不再使用GitHub的json文件方式
- 创建一个KV命令空间：名称SECRET_KV
- 在 workers 或 pages 的设置里，绑定 kv 空间，变量名为`SECRET_KV`（不能修改），绑定上一步中新建的 kv 空间（SECRET_KV）
- 在cf的存储和数据库-->KV --> 点开SECRET_KV，在KV对中，新增一对数据，key（密钥）名password，value（值）为你想要设置的密码。

## 2024-11-11 更新：每天只进行一次 TG 通知
- 创建一个KV命令空间：名称随意，假设为`DOMAINS_TG_KV`
- 在 workers 或 pages 的设置里，绑定 kv 空间，变量名为`DOMAINS_TG_KV`（不能修改），绑定上一步中新建的 kv 空间

## 部署方法

**worker 部署**

在cf中创建一个workers，复制`_worker.js`中的代码到workers中，点击保存并部署。

## 变量设置
| 变量名 | 填写示例 | 说明 | 是否必填 | 
| ------ | ------- | ------ | ------ |
| SITENAME | 我的域名监控 | 自定义站点名称，默认为`域名监控` | 否 |
| DOMAINS | 具体见下面示例 | 你自己的json文件 | 是 |
| TGID | 652***4200 | TG机器人ID，不需要通知可不填 | 否 |
| TGTOKEN | 60947***43:BBCrcWzLb000000vdtt0jy000000-uKM7p8 | TG机器人TOKEN，不需要通知可不填 | 否 |
| DAYS | 7 | 提前几天发送TG提醒，必须是整数，默认为`7` | 否 |
## 域名信息json文件格式
**示例**
```
[
  { "domain": "883344.best", "registrationDate": "2024-06-16", "expirationDate": "2025-07-15", "system": "SpaceShip", "systemURL": "https://www.spaceship.com/zh" },
  { "domain": "711911.xyz", "registrationDate": "2024-04-16", "expirationDate": "2029-04-15", "system": "SpaceShip", "systemURL": "https://www.spaceship.com/zh" },
  { "domain": "hello.xyz", "registrationDate": "2024-07-17", "expirationDate": "2025-07-16", "system": "SpaceShip", "systemURL": "https://www.spaceship.com/zh" }
]
```

## 致谢
[ypq123456789](https://github.com/ypq123456789/domainkeeper)
