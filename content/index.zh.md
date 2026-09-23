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
10. [商品名字对不上，先别让 Agent 猜](writing/10-when-product-names-dont-match-dont-guess.md)
11. [给了通用对象，Agent 却绕开了已有的业务结构](writing/11-custom-objects-bypassed-the-business-model.md)
12. [合同摘要写得很好，原文在哪里？](writing/12-the-contract-summary-looks-good-where-is-the-original.md)
13. [算出缺料，不等于应该下采购单](writing/13-a-material-shortage-is-not-a-purchase-decision.md)
14. [银行扣了一笔钱，系统里却有十张付款单](writing/14-one-bank-debit-ten-payment-records.md)
15. [“还剩几天假”，为什么不是一个字段？](writing/15-why-days-of-leave-left-isnt-a-field.md)
16. [货被占了，和货已经出库，是两件事](writing/16-reserved-stock-hasnt-left-the-warehouse.md)
17. [把客户标成“经销商”，然后呢？](writing/17-we-marked-a-customer-as-a-dealer-what-happens-next.md)
18. [定制化，为什么不能就是用户的一段话？](writing/18-customization-starts-with-a-sentence.md)
19. [电商订单来了，改规则，还是改软件？](writing/19-a-new-order-channel-doesnt-need-a-new-workflow-engine.md)
20. [只是加一句规则，原来的规矩怎么没了？](writing/20-add-one-rule-dont-replace-the-rest.md)

系列之外：

- [AI 时代的 ERP，得重写，不是加个 Agent](writing/ai-era-erp-needs-a-rewrite.md)
- [ERP/CRM 正在“隐身”](writing/ai-native-erp-crm-market.md)
- [本体建好的那天，它就开始过期](writing/an-ontology-ages-from-the-day-its-built.md)
- [别再神化本体论](writing/facts-before-relationship-labels.md)
- [面向对象都没玩明白，怎么敢把企业交给本体？](writing/if-we-cant-get-objects-right-why-build-ontology.md)
- [本体论不是企业 AI 的地基](writing/ontology-is-not-the-foundation-of-enterprise-ai.md)

## 设计说明

建模背后的推理 —— 能力与 Skill、设备授权流程，以及每个业务对象各一篇 ——
随代码发布，不放在这个站上：仓库里的
[`docs/`](https://github.com/AIE-enginehub/Oryh/tree/main/docs)。
任何一个运行中的部署，API 文档在 `/redoc`。
