这些是 Redux 的 action creators。在 Redux 中，actions 是发送数据到 store 的唯一途径。你可以把它们想象成描述发生了什么的对象。这些对象由一个 type 和一个 payload 组成。

```ts
// 删除窗口
export const deleteFrame = (frameId: number) => ({
  type: DELETE_FRAME,
  payload: { frameId },
});

// 创建窗口
export const addFrame = (file: FileType) => ({
  type: ADD_FRAME,
  payload: { file },
});

// 窗口可见性
export const updateFrameVisiblity = (frameId: number) => ({
  type: UPDATE_FRAME_VISIBILITY,
  payload: { frameId },
});

// 更新 z-index
export const updateZindex = (frameId: number) => ({
  type: UPDATE_Z_INDEX,
  payload: { frameId },
});

// 更新宽度
export const updateWidth = (frameId: number, newWidth: number) => ({
  type: UPDATE_WIDTH,
  payload: { frameId, width: newWidth },
});

// 更新高度
export const updateHeight = (frameId: number, newHeight: number) => ({
  type: UPDATE_HEIGHT,
  payload: { frameId, height: newHeight },
});

// 更新纵向位置
export const updateTop = (frameId: number, newTop: number) => ({
  type: UPDATE_TOP,
  payload: { frameId, top: newTop },
});

// 更新横向位置
export const updateLeft = (frameId: number, newLeft: number) => ({
  type: UPDATE_LEFT,
  payload: { frameId, left: newLeft },
});

// 更新视图状态
export const updateViewState = (
  frameId: number,
  newState: FrameViewStateEnum
) => ({
  type: UPDATE_VIEW_STATE,
  payload: { frameId, viewState: newState },
});

```