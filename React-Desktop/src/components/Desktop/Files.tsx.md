这个 Files 组件主要用于展示桌面上的文件。

上所述,这个 Files 组件的实现原理如下:

- 从 Redux store 获取文件信息
- 过滤出桌面文件,并保存在组件状态中
- 遍历桌面文件,对每个文件渲染一个 File 组件
- 使用样式组件定义容器样式

这种实现方式的优点是:

- 使用 Redux 管理全局状态,使组件可以方便地访问需要的数据
- 使用 useSelector 和 useEffect 保持组件状态与 Redux store 同步
- 将文件的渲染委托给单独的 File 组件,使 Files 组件保持简洁
- 使用 styled-components 定义样式,使组件的结构和样式分离


`src/components/Desktop/Files.tsx`：

1. 首先,通过 useSelector 这个 Redux 的 hook,从 Redux store 中获取所有的文件信息,这个信息存储在 files 变量中。selectFiles 是一个 selector 函数,用于从 Redux store 中提取需要的数据。

2. 然后,使用 useState 这个 React 的 hook 定义了一个状态变量 desktopFiles,初始值为一个空数组。这个变量用于存储属于桌面的文件。

3. 接下来,使用 useEffect 这个 hook,在组件渲染后以及 files.elements 发生变化时执行一个副作用。这个副作用的作用是从所有的文件中过滤出父级为 "Desktop" 的文件,并更新 desktopFiles 状态。这样,desktopFiles 就始终保持与 Redux store 中的桌面文件同步。

4. 最后,在组件的渲染部分,使用 FilesStyle 这个样式组件作为容器,然后遍历 desktopFiles 数组,对于每一个文件,渲染一个 File 组件。File 组件接收文件信息作为 prop。

```tsx
export const Files = () => {
  const files = useSelector(selectFiles);

  const [desktopFiles, setDesktopFiles] = useState([] as FileType[]);

  useEffect(() => {
    setDesktopFiles(
      files.elements.filter((element) => element.parent === "Desktop")
    );
  }, [files.elements]);

  return (
    <FilesStyle>
      {desktopFiles?.map((element) => (
        <File
          key={`file-desktop-${element.name}-${element.id}`}
          file={element}
        />
      ))}
    </FilesStyle>
  );
};
```

其中，使用到了一个 Style 组件 FilesStyle，位于 `src/components/Desktop/style.tsx`，代码实现如下：

这里使用了 styled-components 库来定义样式组件。FilesStyle 定义了桌面文件容器的样式,它使用绝对定位,距离顶部 40px,距离左侧 20px。

```tsx
export const FilesStyle = styled.div`
  position: absolute;
  top: 40px;
  left: 20px;
`;
```