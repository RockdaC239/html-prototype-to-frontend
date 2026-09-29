# HTML 原型转前端页面

将已有 HTML、CSS、JavaScript 原型迁移到 React、Vue 等前端框架或现有组件体系的 Codex skill。目标是在真实应用中保留任务要求的视觉、交互、数据语义和输出。

## 为什么使用

原型有源码时，直接迁移结构与样式通常比仅凭截图重画更省试错。转换仍会遇到宿主样式覆盖、根节点尺寸变化、浏览器默认样式及动态数据不一致，因此需要在真实入口校验。本 skill 提供转换、诊断和验收步骤；未经验证不能声称“像素级还原”。

浏览器验证使用 `ego-browser`，完成后关闭本次打开的标签页；不使用 Playwright。

## 文件

- [SKILL.md](SKILL.md)：框架无关的迁移流程。
- [references/parity.md](references/parity.md)：视觉、状态、数据和宿主集成的检查方法。
- [references/react.md](references/react.md)：目标为 React 时的 JSX、状态和副作用迁移要点。

## 使用

向 Codex 提供原型路径、目标项目路径、实际访问入口和迁移范围，然后调用 `$html-prototype-to-frontend`。例如：

> 用 `$html-prototype-to-frontend` 将 `prototype/admin.html` 迁移到现有 Vue 管理端。保留默认页、筛选和详情弹窗，最终在 Dashboard 宿主入口校验。

没有确定接口契约时，应说明哪些数据仅作本地演示；skill 不会凭原型猜测后端接口。

## 安装

将仓库克隆到 Codex 全局 skills 目录：

```bash
git clone https://github.com/RockdaC239/html-prototype-to-frontend.git ~/.codex/skills/html-prototype-to-frontend
```

如果通过 `rocc-matrix` 管理技能，以 `rocc-matrix/skills/html-prototype-to-frontend` 为维护源，并使用矩阵同步脚本更新全局副本。
