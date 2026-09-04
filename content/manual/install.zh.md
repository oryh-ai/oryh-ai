# 安装部署

## 需要什么

- **Docker**，带 Compose v2（`docker compose`，不是 `docker-compose`）。
- **约 2 GB 内存**，四个服务够用。
- 一个能访问到端口的机器 —— 默认 `8080`。

没别的了。Postgres、API、控制台、网关全部来自 compose 文件；不需要另外准备数据库、不需要配应用服务器，也不需要装 Node 或 Python 工具链。

## 跑起来

```bash
git clone https://github.com/AIE-enginehub/Oryh.git
cd Oryh
docker compose up -d --build
```

首次构建要几分钟，因为 API 和控制台镜像是从源码构建的。之后启动时会自动跑数据库迁移。

启动之后：

```bash
docker compose ps
```

四个服务都应当是 healthy。

| 服务 | 是什么 |
|---|---|
| `db` | Postgres 16。系统的全部状态都在这里。 |
| `api` | FastAPI 应用。启动时跑迁移。 |
| `console` | 静态的浏览器控制台。 |
| `gateway` | nginx。唯一对外暴露端口的服务。 |

然后打开 <http://127.0.0.1:8080/> —— 但**先别急着登录**。先读[首次启动](first-boot.md)，因为你需要的凭据在刚才启动的过程中已经打进日志里了。

## 配置

配置放在 compose 文件旁边的 `.env` 里。每一项都有能用的默认值，所以试用性质的部署完全可以不写 `.env`。`.env.example` 列了全集，下面这些是真实部署会用到的。

### 对外地址

```bash
ORYH_CONSOLE_PORT=8080          # 网关对外暴露的端口
ORYH_BASE_URL=https://oryh.example.com
```

`ORYH_BASE_URL` 是规范的浏览器访问源。如果只是通过 IP 走明文 HTTP 自己试用，就别设 —— 链接和来源校验会跟着每个请求进来的地址走，这在试用阶段正合适。一旦这台机器不只有你能访问，就应该设上：它会被渲染进技能包、邀请链接和密码重置链接，而且 **SMTP 在没有它的情况下会拒绝发送安全链接**。

### 第一个工作区

只在创建工作区的那一次启动时被读取，之后永远失效。

```bash
ORYH_STANDALONE_COMPANY_NAME=某某公司
ORYH_STANDALONE_ADMIN_EMAIL=admin@example.com
ORYH_STANDALONE_ADMIN_PASSWORD=            # 留空则自动生成
```

留空是更好的默认：自动生成的密码只打印一次，也就不可能被提交到任何地方。见[首次启动](first-boot.md)。

### 邮件

```bash
ORYH_EMAIL_BACKEND=console      # standalone 的默认值
```

`console` 会把所有外发邮件 —— 邀请、密码重置 —— **打印到 `api` 服务的日志**里，而不是真的发出去。这是刻意的：一台新装的机器没有邮件中继，而邀请必须仍然能从 `docker compose logs` 里拿到。等你有中继了再切成真发：

```bash
ORYH_EMAIL_BACKEND=smtp
ORYH_SMTP_HOST=smtp.example.com
ORYH_SMTP_PORT=465
ORYH_SMTP_SECURITY=tls
ORYH_SMTP_USER=service@example.com
ORYH_SMTP_PASSWORD=...
ORYH_SMTP_FROM=service@example.com
```

如果中继是按出口 IP 认证的，`ORYH_SMTP_USER` 和 `ORYH_SMTP_PASSWORD` 可以不填。`ORYH_BASE_URL` 不行 —— 见上。

### 数据库口令

```bash
ORYH_APP_DB_PASSWORD=change-me
```

API 运行时以受限的 `oryh_app` 角色连接，行级安全因此生效；迁移则用属主角色。在这个部署装进真实数据之前，把它改成你自己的值。

## 下一步

[首次启动](first-boot.md) —— 凭据在哪，以及拿它做什么。
