这个文件定义了一个名为`App`的函数组件。是整个应用的根组件。

整个布局由两个组件构成：

- Desktop 组件：桌面
- MenuBar 组件：菜单栏

```tsx
import { MenuBar } from "./components/MenuBar";
import { Desktop } from "./components/Desktop";

// 函数组件
function App() {
  return (
    <div className="App">
      <Desktop />
      <MenuBar />
    </div>
  );
}

export default App;
```