# ORYH

ORYH 是一个 AI 原生的 OA/BPM 平台。业务逻辑不在服务端 —— 它在 agent 代表某个人
加载的 Skill 里，而服务端记录真正发生了什么。

## 自己把它跑起来

**[使用手册](manual/index.md)** 覆盖自托管产品的完整链路：[安装部署](manual/install.md)、
[取走首次启动只打印一次的凭据](manual/first-boot.md)、[接入 agent](manual/connect-agent.md)、
[把公司的记录装进去](manual/workspace.md)、以及[长期运维](manual/operations.md)。

```bash
git clone https://github.com/AIE-enginehub/Oryh.git
cd Oryh
docker compose up -d --build
```

开源内核以 Apache-2.0 发布于
[AIE-enginehub/Oryh](https://github.com/AIE-enginehub/Oryh)。

## 文章

《当 Agent 开始操作企业：ORYH 的设计探索》—— 关于它从哪儿来、为什么长成这样。

1. [从一张工时单开始](writing/01-it-started-with-a-timesheet.md)
2. [如果用 ERP 的主要是 Agent，软件要怎么写？](writing/02-when-agents-use-erp.md)
3. [软件负责记录，Agent 负责逻辑](writing/03-software-records-agents-decide.md)
4. [公司的规则，为什么不该是一堆 `if`](writing/04-why-rules-should-not-be-if-statements.md)
5. [审批走到哪了，不一定是一个状态](writing/05-workflow-position-is-not-a-status.md)
6. [Agent 会掉线，事情不能跟着丢](writing/06-an-agent-can-disappear-the-work-cant.md)
7. [为什么还需要一个 Flow Runner](writing/07-why-we-need-a-flow-runner.md)
8. [这一步，到底是谁做的？](writing/08-who-actually-took-this-step.md)
9. [接口有了，Agent 为什么还是会用错？](writing/09-the-api-exists-why-does-the-agent-still-get-it-wrong.md)

另有一篇谈这个品类往哪儿走：
[ERP/CRM 正在“隐身”](writing/ai-native-erp-crm-market.md)。

## 设计说明

建模背后的推理 —— 能力与 Skill、设备授权流程，以及每个业务对象各一篇 ——
随代码发布，不放在这个站上：仓库里的
[`docs/`](https://github.com/AIE-enginehub/Oryh/tree/main/docs)。
任何一个运行中的部署，API 文档在 `/redoc`。
