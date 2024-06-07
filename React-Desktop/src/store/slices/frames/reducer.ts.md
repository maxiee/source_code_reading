`src/store/slices/frames/reducer.ts`，这是一个用于进行窗口管理的 Redux Toolkit Reducer，我想请你帮我分析该 Reducer 中对每个 Actions 的处理逻辑。

这个 Reducer 的作用是根据不同的 action type 对窗口状态进行相应的更新,包括添加窗口、删除窗口、更新窗口可见性、调整窗口层级、更新窗口尺寸和位置等操作。每个 action 的处理逻辑都是通过遍历窗口数组,找到目标窗口并进行相应的属性更新,然后返回新的窗口数组和状态对象。

## `ADD_FRAME` 添加窗口

- 通过 `getFrameMaxId` 获取当前最大的窗口 ID,并将其加 1 作为新窗口的 ID。
- 通过 `getMaxZindex` 获取当前最大的 zIndex,并将其加 1 作为新窗口的 zIndex。
- 通过 `getApplicationTypeByFileType` 根据文件类型获取对应的应用类型。
- 创建一个新的 `FrameType` 对象,设置其各项属性。
- 将新窗口对象添加到 `state.elements` 数组中,返回新的 state。

```ts
case ADD_FRAME:
  const id = getFrameMaxId(state.elements) + 1;
  const zIndex = getMaxZindex(state.elements) + 1;
  const type = getApplicationTypeByFileType(action.payload.file.type);

  const newFrame: FrameType = {
    id,
    type,
    fileId: action.payload.file.id,
    zIndex,
    hidden: false,
    width: "100%",
    height: "100vh",
    top: 0,
    left: 0,
    viewState: FrameViewStateEnum.Fullscreen,
  };

  return {
    ...state,
    elements: [...state.elements, newFrame],
  };
```

## `DELETE_FRAME` 删除窗口

- 遍历 `state.elements` 数组,将 ID 不等于要删除的窗口 ID 的元素添加到新数组 `elements` 中。
- 返回更新后的 state,其中 `elements` 为过滤后的窗口数组。

```ts
case DELETE_FRAME:
  elements = [];

  for (let element of state.elements) {
    if (element.id !== action.payload.frameId) {
      elements.push(element);
    }
  }

  return {
    ...state,
    elements: [...elements],
  };
```

## `UPDATE_FRAME_VISIBILITY` 更新可见性

- 遍历 `state.elements` 数组,对于 ID 等于要更新的窗口 ID 的元素,将其 `hidden` 属性==取反==,其他元素不变,将结果添加到新数组 `elements` 中。
- 返回更新后的 state,其中 `elements` 为更新后的窗口数组。

```ts
case UPDATE_FRAME_VISIBILITY:
  elements = [];
  for (let el of state.elements) {
    if (el.id === action.payload.frameId) {
      elements.push({ ...el, hidden: !el.hidden });
    } else {
      elements.push(el);
    }
  }

  return {
    ...state,
    elements,
  };
```

## `UPDATE_Z_INDEX` 层级置顶

   - 获取当前窗口数量作为最大 zIndex。
   - 找到要更新 zIndex 的窗口对象 `frame`。
   - 遍历 `state.elements` 数组,对于每个元素:
     - 如果是 `frame`,将其 zIndex 设为最大值。
     - 如果 zIndex 大于 `frame` 的 zIndex,将其减 1。
     - 将更新后的元素添加到新数组 `elements` 中。
   - 返回更新后的 state,其中 `elements` 为更新后的窗口数组。

```ts
case UPDATE_Z_INDEX:
  const maxZ = state.elements.length;
  const frame = state.elements.filter(
    (el) => el.id === action.payload.frameId
  )[0];

  if (!frame) {
    return state;
  }

  elements = [];
  for (let el of state.elements) {
    let newZ = el.zIndex;

    if (el.id === frame.id) {
      newZ = maxZ;
    }

    if (el.zIndex > frame.zIndex) {
      newZ = newZ - 1;
    }

    elements.push({ ...el, zIndex: newZ });
  }

  return { ...state, elements };
```

## `UPDATE_WIDTH` 更新窗口宽度

- 根据 action 中的 `width` 计算新的宽度字符串 `newWidth`。
- 遍历 `state.elements` 数组,对于 ID 等于要更新的窗口 ID 的元素,将其 `width` 属性更新为 `newWidth`,其他元素不变,将结果添加到新数组 `elements` 中。
- 返回更新后的 state,其中 `elements` 为更新后的窗口数组。

```ts
case UPDATE_WIDTH:
  const newWidth = `${action.payload.width}%`;
  elements = [];

  for (let frame of state.elements) {
    if (frame.id === action.payload.frameId) {
      elements.push({ ...frame, width: newWidth });
    } else {
      elements.push({ ...frame });
    }
  }
  return { ...state, elements };
```

## `UPDATE_HEIGHT`更新高度

- 根据 action 中的 `height` 计算新的高度字符串 `newHeight`。
- 遍历 `state.elements` 数组,对于 ID 等于要更新的窗口 ID 的元素,将其 `height` 属性更新为 `newHeight`,其他元素不变,将结果添加到新数组 `elements` 中。
- 返回更新后的 state,其中 `elements` 为更新后的窗口数组。


## `UPDATE_TOP`

   - 从 action 中获取新的 `top` 值。
   - 遍历 `state.elements` 数组,对于 ID 等于要更新的窗口 ID 的元素,将其 `top` 属性更新为新值,其他元素不变,将结果添加到新数组 `elements` 中。
   - 返回更新后的 state,其中 `elements` 为更新后的窗口数组。

## `UPDATE_LEFT`

   - 从 action 中获取新的 `left` 值。
   - 遍历 `state.elements` 数组,对于 ID 等于要更新的窗口 ID 的元素,将其 `left` 属性更新为新值,其他元素不变,将结果添加到新数组 `elements` 中。
   - 返回更新后的 state,其中 `elements` 为更新后的窗口数组。

##  `UPDATE_VIEW_STATE`

- 遍历 `state.elements` 数组,对于 ID 等于要更新的窗口 ID 的元素,将其 `viewState` 属性更新为 action 中的新值,其他元素不变,将结果添加到新数组 `elements` 中。
- 返回更新后的 state,其中 `elements` 为更新后的窗口数组。

##  `default`:

- 对于未匹配到的 action type,直接返回当前的 state,不做任何修改。

