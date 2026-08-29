# 日常使用

日常没人开控制台。人对自己的 agent 说话，agent 用工作区发给它的技能去做。这一页讲那是什么样子，按角色分。

下面列的是当前公开版本随附的技能。**你手上那份到底有哪些，以仓库里的 `skills/` 目录为准** —— 这个列表在版本之间会增加。

## 每个人

| 你要什么 | 技能 |
|---|---|
| 「我有什么要办的？」 | `oryh-my-work` |
| 「周四把 B 会议室订了」 | `oryh-resource-booking` |
| 「我这个月发了多少？」 | `oryh-payslip` |
| 「连接一下」/「我的密钥不好使了」 | `oryh-connect` |
| 让已装技能保持最新 | `oryh-skill-sync` |

最值得先教给人的是 `oryh-my-work`。它从服务端自己的队列回答「我该做什么」—— 什么在等他审批、他提交的什么被退回来了、什么快到期了。支持会话启动钩子的 agent 会在会话开始时自动跑，于是人是被告知的，而不用先想起来问。

## 提交自己的单据

下面每一个都对应一种单据，站在填单人的立场：起草、修改、查询、提交。

| 单据 | 技能 |
|---|---|
| 工时 | `oryh-timesheet-submit` |
| 报销（会读发票/小票） | `oryh-expense-submit` |
| 请假，以及背后的余额 | `oryh-leave-submit` |
| 采购申请 | `oryh-purchase-submit` |
| 销售报价单 | `oryh-quotation-submit` |
| 销售订单 | `oryh-order-submit` |

输入就是平常说话。「周一到周三做 Globex 对接，每天八小时，周四在面试」就是一张工时单。agent 把它变成字段，然后**把结果读回给你** —— 读回来这一半才是关键，因为结构化的结果是 agent 的理解，只有本人能确认那是不是他的意思。

## 审批

| 你要什么 | 技能 |
|---|---|
| 对一份单据审批、驳回或退回 | `oryh-approve` |
| 告诉相关人「有东西动了」 | `approval-notifier` |

`oryh-approve` 一个技能覆盖所有单据类型 —— 工时、报销和采购申请的审批方式是一样的，因为审批本来就是同一个动作。不一样的是路由，而路由是你的工作区写的一份文档，不是谁画的一张流程图。

**路由本身不随公开版本发布。** 托管服务维护它自己的一套审批流程技能；自托管部署要么用 `oryh-skill-author` 写自己的，要么直接审批。想让它无人值守地跑，可选的 flow runner 会用**你自己的** agent 运行时和模型密钥来驱动队列 —— 见[运维](operations.md)。

## 采购与库存

| 你要什么 | 技能 |
|---|---|
| 下采购单、维护、按单收货 | `oryh-purchase-order` |
| 入库、出库、盘点、调整 | `oryh-inventory` |

## 财务

| 你要什么 | 技能 |
|---|---|
| 给客户开票、登记收款、核销 | `oryh-receivables` |
| 登记供应商开来的票、与采购单核对、付款 | `oryh-payables` |
| 客户预存款与挂账额度 | `oryh-billing-account` |

核销是一本账，不是一个状态字段 —— 一张发票不会因为谁把它设成「已付」就付了，它付了是因为有付款被匹配上去。原因见[发票、收付款与核销](https://github.com/AIE-enginehub/Oryh/blob/main/docs/receivables-payables.md)和[账户余额](https://github.com/AIE-enginehub/Oryh/blob/main/docs/billing-accounts.md)。

## 人事与薪酬

| 你要什么 | 技能 |
|---|---|
| 设定或调整某人的薪酬条款 | `oryh-payroll` |
| 看工资 —— 自己的，或持有 `payroll.read` 时看一批 | `oryh-payslip` |

工资是「读也是权限」最锋利的例子：`oryh-payslip` 不需要任何额外授权就能让人看自己的工资条，而看一整批只对工作区明确指定的人开放。见[薪酬](https://github.com/AIE-enginehub/Oryh/blob/main/docs/payroll.md)。

## 管理员

| 你要什么 | 技能 |
|---|---|
| 「让谢婷能下采购单」 | `oryh-access-admin` |
| 起草、发布、修订、废止一条公司制度 | `oryh-policy` |
| 导入和维护主数据 | `oryh-master-data` |
| 把一句流程要求变成工作区配置 | `oryh-skill-author` |
| 从旧系统批量导入历史 | `oryh-data-migration` |
| 记录或查询任何工作区自定义对象 | `oryh-business-object` |
| 汇总一批对象 —— 「这周的现场勘查单」 | `oryh-business-object-summary` |

## 改变它的行为

公司口中的「我们的流程」在这里大部分是文字，所以改它通常是对 agent 说一句话，而不是立一个项目：

> 「报我的待办时只列标题和到期日，不要展开关联记录。」

> 「批过的报销直接付。我们不开报销发票。」

> 「审批后的发票状态叫「已批准」，不叫「已开具」。」

这三句落在三个不同的旋钮上 —— 技能的 calibration、工作流定义、生命周期状态机 —— 管理员的 agent 知道是哪一个。三者都立刻对所有人生效，不分叉、不发版。agent 在下一次会话时接上变更，并且是被告知发生了什么变化，而不是被悄悄重新指令。

**文字的边界在哪：** calibration 不能扩大一个技能被允许做的事。权限、状态迁移、核销算术和操作人归属由服务端强制执行，不管指令里怎么写。自然语言决定「怎么做」，它从不决定「允许做什么」。

## 下一步

[管理控制台](administration.md) —— 逐个页面。
