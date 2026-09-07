# 运维

## 备份

**数据库就是全部状态。** 没有别的要备 —— 没有上传目录、没有独立搜索索引、API 容器里也没有藏着的状态。

```bash
docker compose exec -T db pg_dump -U ofbiz -d oryh > oryh-$(date +%F).sql
```

恢复到一个空库：

```bash
docker compose exec -T db psql -U ofbiz -d oryh < oryh-2026-08-29.sql
```

每次升级前做一份。在真正需要之前，先试一次恢复。

## 升级

```bash
git pull
docker compose up -d --build
```

迁移在启动时执行且是幂等的，所以同版本重启是空操作。升级后的第一次启动，盯一下 API 日志：

```bash
docker compose logs -f api
```

`ensure_standalone_tenant` 每次启动都会跑，并报告工作区已存在。**这一行是正常的** —— 它意味着引导脚本正确地拒绝了去动一个正在用的工作区。

## 邮件

在你配好 SMTP 之前，`ORYH_EMAIL_BACKEND=console` 会把外发邮件打印到 API 日志而不是发出去。应付几封邀请是够用的：

```bash
docker compose logs api | grep -A6 "\oryh email\"
```

切到 SMTP 之前，先设 `ORYH_BASE_URL`。安全链接 —— 邀请、密码重置 —— 在没有声明规范源的情况下会拒绝发送，因为一个「按请求碰巧从哪个地址进来」拼出来的链接，不是能寄给人的东西。

## 无人值守的流程驱动（可选）

默认关闭。它用**你自己的** agent 运行时和**你自己的**模型密钥来驱动队列；系统不替你提供任何一样。

```bash
docker compose --profile flow-runner up -d
```

它需要你提供两个文件：一个凭据文件，装工作区 id 和一把服务密钥（首次启动那把就行）；一个 provider 文件，装你的模型凭据。两者都以只读挂载，模型密钥每次运行时重新读取，并且只传给 agent 子进程。

先把 `ORYH_RUNNER_PI_BINARY` 留空，用桩适配器观察它的行为，再决定要不要花模型调用。**没有装任何流程技能时不存在订阅，所以它会一直空转** —— 那是预期中的静止状态，不是故障。

## 排障

**某个服务不 healthy。**

```bash
docker compose ps
docker compose logs api
docker compose logs gateway
```

API 自己的健康端点是 `/healthz`，网关的是 `/_health`。

**控制台打开了但什么都不work。** 通常是 API 还在跑迁移，或者迁移失败了。`docker compose logs api` 会说是哪一种。

**邮件里的链接指向错误的主机。** 设 `ORYH_BASE_URL` 然后重启 API。

**agent 收到 `401 invalid API key`。** 凭据没了或被停用了。用 `oryh-connect` 重连；在 *访问凭证* 里查这把密钥的状态。

**agent 装的是另一个部署的技能。** 技能包里带着签发它的部署地址。从你真正要用的那个部署下载 `oryh-connect`，重新连接。

**某个技能谁也没触达。** 技能页面对「定向到具名人员但一个都没指定」的技能显示 **定向 · 无人**。指定人。**仅托管代理** 是另一回事：审批流技能出厂就是这样，不用管。

**端口被占了。** 设 `ORYH_CONSOLE_PORT` 然后重启。

## 删除

```bash
docker compose down            # 停止；数据卷保留
docker compose down -v         # 停止，并永久删除数据库
```

第二条不可恢复。没有软删除，也没有第二份副本。

## 反馈问题

Bug 和安全报告提到公开仓库 —— 见那里的 `SECURITY.md`。附上你所在的版本和相关的 `docker compose logs` 输出；**不要贴 API 密钥**。
