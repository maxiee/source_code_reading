`FrameType`：这是一个类型，定义了一个“框架”的属性。这个框架有一个ID，一个类型（由`FrameAppTypeEnum`定义），一个文件ID，一个隐藏标志，宽度和高度（字符串），顶部和左侧的位置（数字），一个z-index（用于CSS堆叠顺序），以及一个视图状态（由`FrameViewStateEnum`定义）。

```tsx
export type FrameType = {
  id: number;
  type: FrameAppTypeEnum;
  fileId: number;
  hidden: boolean;
  width: string;
  height: string;
  top: number;
  left: number;
  zIndex: number;
  viewState: FrameViewStateEnum;
};
```