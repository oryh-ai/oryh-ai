# 接入你的 Agent

一个人是通过自己的 AI agent 干活的。在那个 agent 能碰这个工作区之前，它需要两样东西：描述怎么做的技能，和一份属于它自己的凭据。两者都通过同一次引导拿到。

## 为什么不是复制粘贴一个 API key

`oryh-connect` 是唯一一个在登录之前就能用的 oryh 技能，而它**不携带任何凭据** —— 只带这个部署的地址，在你下载它的那一刻渲染进去。agent 装上它，打开一个授权页面，你在页面上登录并批准，之后 agent 才拿到属于它自己的、绑定这台设备的密钥，以及这把密钥所对应范围的技能包。

你和 agent 之间不传递任何东西，你也永远不会把密码输进 agent。你批准的是一台具体的设备，页面上写着它的名字，还有一个 agent 同时显示给你的短码。设计说明见[设备授权流程](https://github.com/AIE-enginehub/Oryh/blob/main/docs/device-flow.md)。

## 1. 下载引导技能

```bash
curl -O http://127.0.0.1:8080/api/v1/connect-skill
```

拿到的是 `oryh-connect.zip`。同一份下载在浏览器里也有：<http://127.0.0.1:8080/web/connect> —— 对不会敲 `curl` 的同事来说这条路更省事。

## 2. 解压到 agent 找技能的目录

| Agent 运行时 | 技能目录 |
|---|---|
| Claude Code | `~/.claude/skills` |
| Codex（应用、CLI、IDE） | `~/.agents/skills` |
| Copilot CLI | `~/.agents/skills` |
| Hermes | `~/.hermes/skills` |
| OpenClaw | `openclaw skills install ./oryh-connect --global` |

`oryh-connect` 每台机器只装一次，不带前缀。其他所有 oryh 技能都只属于一个雇主，并以它命名 —— 这就是为什么一个人可以在同一台笔记本上同时给两家公司干活。

## 3. 让 agent 连接

支持斜杠命令的运行时里输入 `/oryh-connect`；不支持的直接说人话就行 —— 「连接公司的 oryh」即可。

agent 会给出一个链接和一个八位短码。**你自己**在自己的浏览器里打开那个链接，用你的 oryh 账号登录，核对页面上的短码和设备名与 agent 显示的一致，然后批准。

即便 agent 跑在 SSH、WSL 或容器里，这个链接照样能用 —— 浏览器是你的，不是 agent 的。

## 4. agent 拿到了什么

批准之后，只此一次：一份设备凭据，和这份凭据对应范围的个人技能包。技能包是根据**你**持有的东西生成的 —— 你的角色能力，以及工作区定向发给你的技能 —— 所以两个同事用一模一样的笔记本连接，拿到的包也不一样。这不是要报的 bug，这正是设计目的。见[能力与技能](https://github.com/AIE-enginehub/Oryh/blob/main/docs/capabilities-skills-api.md)。

连接第二台设备不会让第一台失效。每台设备各持一把自己的密钥。

## 保持最新

- **技能会变。** 让 agent 同步一次；`oryh-skill-sync` 会检查本机为这家公司装的技能包是否还是最新，不是就重装。支持会话启动钩子的 agent 会自己做这件事。
- **某把密钥不灵了。** 任何 oryh 技能返回 `401 invalid API key` 就意味着要重连：再跑一次 `oryh-connect`。加入第二家雇主用的也是它。
- **地址不能挪用。** 技能包里带着签发它的那个部署的地址。从测试服务器下载的副本不应该指向生产 —— 各自下载一份新的。

## 下一步

[初始化工作区](workspace.md) —— 工作区现在还是空的。
