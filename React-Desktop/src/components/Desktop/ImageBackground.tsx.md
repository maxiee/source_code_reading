`ImageBackground.tsx` 文件定义了一个背景图片组件,它使用了 `style.tsx` 中定义的样式化组件来设置背景图片的样式。当点击背景时,会触发 Redux 的 action 来重置文件选择状态。这个组件的作用是为桌面提供一个可点击的背景图片,并在点击时重置文件选择状态。

`src/components/Desktop/ImageBackground.tsx` 代码如下：

- `useDispatch` 和 `resetSelection`: 这些是来自 Redux 的 hooks 和 action,用于在点击背景时重置文件选择状态。

- `draggable={false}`: 禁止拖拽背景图片。

```tsx
export const ImageBackground = () => {
  const dispatch = useDispatch();

  return (
    <ImageBackgroundStyle
      draggable={false}
      onClick={() => dispatch(resetSelection())}
      src={BGHD}
    />
  );
};
```

其中用到了 `ImageBackgroundStyle`，位于 `src/components/Desktop/style.tsx`，其代码实现如下：

`ImageBackgroundStyle` 组件定义了背景图片的样式:

- `position: absolute;`: 使用绝对定位。
- `top: 0;` 和 `left: 0;`: 将图片放置在左上角。
- `width: 100%;` 和 `height: 100%;`: 使图片填充整个容器。
- `object-fit: cover;`: 使图片保持原有比例并填充整个容器,超出部分会被裁剪。

```tsx
export const ImageBackgroundStyle = styled.img`
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
`;
```

