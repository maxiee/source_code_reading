处理两个事件：

- `SET_IS_DRAG_DISABLE`
- `SET_IS_MENU_OPEN`

都是布尔值，处理方法也很简单，跟新以下状态。代码如下：

```ts
!((/home/maxiee/Code/React-Desktop/src/store/slices/os/reducer.ts))
```

需要注意的是，osReducer 的类型是 osInitialState，定义在 `src/store/slices/os/state.ts`，代码如下：

```ts
!((/home/maxiee/Code/React-Desktop/src/store/slices/os/state.ts))
```

osInitialState 既定义了 osReducer 的类型，同时也指定了默认值。
