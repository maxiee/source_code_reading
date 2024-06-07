`FileType`：这是一个类型，定义了一个“文件”的属性。这个文件有一个ID，一个名字，一个类型（由`FileTypeEnum`定义），一个内容（字符串），一个父级（字符串），以及一个选中标志。

```tsx
export type FileType = {
  id: number;
  name: string;
  type: FileTypeEnum;
  content: string;
  parent: string;
  selected: boolean;
};
```