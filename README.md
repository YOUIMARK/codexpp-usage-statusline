# 用量状态栏

在 Codex 输入框下方显示输出速度、当前轮 Token 用量、缓存命中率和上下文占用。点击状态项可展开明细。

## 安装

将本目录中的 `codexpp.json`、`main.js`、`statusline.js` 和 `LICENSE` 放入：

```text
%APPDATA%\Codex++\user_scripts\usage-statusline\
```

在 Codex++ 管理器的「拓展」页启用「用量状态栏」；若页面未更新，执行「热重载拓展」。此拓展沿用官方相同 ID，请不要与官方版本同时安装。

## 显示内容

- 状态栏显示解码速度、当前轮总 Token 与缓存命中率、上下文占用百分比、本对话总耗时。
- 总耗时把已记录的各轮用时逐轮取整到秒后相加，不计轮次之间的空闲时间。点击可查看已计时的轮数。
- 点击速度项查看首 token 延迟及吞吐指标；点击 Token 项查看缓存命中、未缓存输入、缓存读取和输出；点击上下文项查看已用 Token 与模型窗口。
- Token 明细统计最近一轮的 rollout 事件；上下文数值使用 Codex 报告的 `total_tokens` 和 `context_window`。当前公开数据不包含系统提示词、工具定义与对话消息的可靠分项，因此不展示猜测的分类明细。

## 设计与来源

信息层级参考 DeepSeek Harness 的紧凑状态行与浅色明细面板；没有复制其代码或品牌素材。DSH 的 `StatsPills.tsx` 基于 React、`createPortal`、DSH 私有设计 token 和 `sessionStats` 投影，不能直接加载进 Codex++ 的脚本拓展。此拓展沿用 Codex++ 插槽，以原生 DOM/CSS 重做交互。

DSH 的会话统计还依赖其完整会话日志投影；Codex++ 当前公开路由没有可核实的工具耗时/会话墙钟总时长，所以本拓展不伪造这些数值，只展示本地接口确实提供的指标。

取数与会话兼容逻辑修改自 Codex++ 官方「用量状态栏」：

<https://github.com/BigPizzaV3/CodexPlusPlus/tree/main/assets/extensions/usage-statusline>

DSH 对应 UI 源码：[StatsPills.tsx](https://github.com/deepseek-ai/deepseek-harness/blob/master/packages/client/ui-chat/src/client/chat/StatsPills.tsx) 和 [stat-dialog.module.css](https://github.com/deepseek-ai/deepseek-harness/blob/master/packages/client/ui-chat/src/client/chat/stat-dialog.module.css)。相关 DSH 仓库及会话统计包使用 MIT；本拓展没有复制这些代码。

官方 Codex++ 代码依 AGPL-3.0 授权，完整许可见本目录 `LICENSE`。本地修改版本继续按相同许可证发布。
