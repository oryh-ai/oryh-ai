# 首次启动

## 第一次启动时发生了什么

API 容器在对外服务之前，会跑一条固定的链：

```text
alembic upgrade head          # 建库或升级表结构
bootstrap_db_roles.py         # 建立/刷新受限的运行时角色
sync_tenant_defaults.py       # 装入预置的默认配置
ensure_standalone_tenant.py   # 创建那一个工作区 —— 仅当一个都不存在时
```

对你有意义的是最后一步。standalone 部署有且只有一个工作区，所以没有注册流程要走：第一次启动直接创建公司、它的第一位管理员，以及一个用于接入 agent 的服务密钥，然后把三样都打印出来。

它**只打印一次**，就在创建它们的那次启动，之后再也不打。判断依据故意做得很钝 —— 只要已经存在任何工作区，脚本就说一声然后退出，不碰它。它不会在每次重启时去「修正」一个正在用的工作区。

## 取凭据

它们落在 `api` 服务的日志里，在上百行迁移输出之后：

```bash
docker compose logs api | grep -A6 "standalone workspace created"
```

```text
================================================================
  oryh standalone workspace created
  company:   某某公司
  console:   sign in as admin@example.com
  password:  8Kd2mQ-xR4vT9wL   (generated — change it after first sign-in)
  agent key: oryh_sk_...       (service key for connecting agents)
  This is printed ONCE. Store it now.
================================================================
```

`password:` 这一行**只在密码是自动生成时才出现**。如果是你自己通过 `ORYH_STANDALONE_ADMIN_PASSWORD` 设的，系统认为设它的人已经知道，不会回显。

**现在就把这两行存进你们放密钥的地方。** agent key 是这个工作区的服务凭据，password 是你的管理员登录口令。

## 登录

打开 <http://127.0.0.1:8080/>（或你配的 `ORYH_BASE_URL`），用管理员身份登录。如果密码是自动生成的，立刻改掉。

你会看到一个空工作区：没有员工、没有客户、没有单据。这是对的。控制台是用来管理工作区的 —— 干活本身发生在 agent 里，那是[下一步](connect-agent.md)。

## 如果凭据丢了

没有第二次打印，重跑脚本也没用：工作区已经存在，它会直接退出。怎么救取决于你手上还剩什么。

**你知道管理员邮箱。** 用控制台的密码重置。在默认的 `ORYH_EMAIL_BACKEND=console` 下，这封重置邮件哪儿也没发 —— 它连同链接一起被打印到 API 日志里：

```bash
docker compose logs api | grep -A6 "\oryh email\"
```

打开里面的链接，设一个新密码。

**你需要一个新的 agent 密钥。** 在控制台的 **访问凭证** 里签发一个，不需要把首次启动那把找回来。见[管理控制台](administration.md)。

**什么都没有，而且工作区本来就是空的。** 在还没有真实数据的时候重来一次很便宜 —— 但要清楚它到底销毁了什么：

```bash
docker compose down -v      # -v 会永久删除数据库卷
docker compose up -d
```

对已经装了你在意的记录的部署，永远不要执行这条。

## 下一步

[接入你的 Agent](connect-agent.md)。
