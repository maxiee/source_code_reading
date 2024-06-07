slices 有一个规范化的目录结构：

- 模块名
	- actions.ts：定义 Action
	- constants.ts：定义 Action 常量名称
	- reducer.ts：更新状态
	- selectors.ts：从总状态中选出本模块状态
	- state.ts：初始化状态