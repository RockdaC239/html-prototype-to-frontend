# React 迁移参考

仅在目标项目使用 React 时读取。以原型现有 HTML/CSS/JavaScript 为准，把 DOM 更新改为 React 状态和渲染；不要把整页放进 `dangerouslySetInnerHTML`，否则事件和状态仍在框架之外。

## HTML 与 JSX

| 原型写法 | React 对应做法 | 易遗漏点 |
| --- | --- | --- |
| `class`、`for` | `className`、`htmlFor` | 标签与输入框的关联 |
| 内联 `style="..."` | `style={{ ... }}` 或沿用 CSS class | 数值单位和 CSS 变量名 |
| `onclick`、`addEventListener` | `onClick={handler}` 等 | 不要在每次渲染后重复绑定 |
| `innerHTML`/`textContent` 更新 | state/props 驱动 JSX | 图表、过滤与列表要同源 |
| 手动修改 `value`/`checked` | `value`/`checked` 加 `onChange` | 初始值与取消回滚 |
| SVG 属性 | JSX 支持的属性名与大小写 | 保留 `viewBox`、坐标与裁切 |

按原型区块划分组件；有复用、独立状态或清晰职责时再拆子组件。静态装饰留在 JSX/CSS，交互元素使用有语义且能用键盘操作的控件。

## 状态和派生数据

- 将原型全局变量和手动 DOM 切换映射到 props、局部 `useState` 或项目已有状态库。状态放在所有使用者的最小共同父级。
- 过滤结果、计数和展示文本若能从现有 state/props 算出，直接计算；代价明显时再用 `useMemo`。避免存第二份同步困难的派生状态。
- 可取消的弹窗编辑要区分已保存值和草稿：打开时初始化草稿，取消时丢弃，保存成功后才更新已保存值。加载和错误也应有可观察 UI。
- 列表 `key` 用稳定实体 ID；筛选或排序后仍指向同一记录，不用数组位置或显示名称。

例如，将原型中靠添加 class 切换的 Tab 改为状态驱动：

```jsx
function Tabs({ tabs, initialTab }) {
  const [activeTab, setActiveTab] = React.useState(initialTab);

  return <div className="prototype-tabs" role="tablist">
    {tabs.map((tab) => <button
      key={tab.id}
      type="button"
      role="tab"
      aria-selected={activeTab === tab.id}
      className={activeTab === tab.id ? 'tab is-active' : 'tab'}
      onClick={() => setActiveTab(tab.id)}
    >{tab.label}</button>)}
  </div>;
}
```

此例仅表达 Tab 头部状态；实际页面还要按项目的无障碍约定连接 Tab 与面板。若原型标签原本是 `span`，检查 `button` 的边框、背景、字体、padding、行高与焦点态，否则尺寸会偏。

## 副作用、数据和宿主

- `useEffect` 用于订阅、定时器、外部图表实例和数据请求等外部同步；清理监听器与定时器，并处理过期请求结果。普通 CSS class、筛选与格式化无需 effect。
- 接口字段只按已确认契约映射。原型静态数据可作开发 fixture，但不得覆盖正式数据；图表、详情与导出使用一致的数据范围。
- 将原型 `body/:root` 样式限定到 React 页面根；检查宿主对 `button`、`table`、`svg` 的全局规则。先确认挂载点、路由及远程模块入口可用。
- 用 React 实际渲染的元素检查矩形、计算样式和交互状态，最后通过目标项目的真实宿主入口复验。
