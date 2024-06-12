`buffer_text` 结构体，用于描述一个缓冲区的文本内容。这个结构体在间接缓冲区（indirect buffers）和它们的基础缓冲区（base buffer）之间共享。下面是每个字段的解释：

```c
struct buffer_text
  {
    // 这是指向缓冲区内容的实际地址。
    // 如果定义了 `REL_ALLOC`，那么当块被重新定位（例如，当调用 `malloc` 时）这个地址可能会改变。
    // 因此，不要将指向缓冲区文本的指针传递给调用 `malloc` 的函数。
    unsigned char *beg;

    // 表示缓冲区中间隙位置
    ptrdiff_t gpt;
    // 表示缓冲区结束的字符位置
    ptrdiff_t z;
    // 表示缓冲区中间隙字节位置
    ptrdiff_t gpt_byte;
    // 表示缓冲区结束的字节位置
    ptrdiff_t z_byte;
    // 表示缓冲区间隙的大小。
    ptrdiff_t gap_size;
    // 计数缓冲区的修改事件。
    // 每次修改事件发生时，它会以对数方式增加，除此之外，它不会改变。
    modiff_count modiff;
    // 在每次字符更改事件发生时被修改。
    // 每次这样的事件发生时，它都会被设置为 `modiff`，除此之外，它不会改变。
    modiff_count chars_modiff;
    // 表示上次访问或保存文件时 `modiff` 的值。
    modiff_count save_modiff;
    // 计数对覆盖层的修改。
    modiff_count overlay_modiff;
    // 每次为这个缓冲区调用 `compact_buffer` 时，都会将其设置为 `modiff`。
    modiff_count compact;
    // 上次完成的重绘以来 GPT - BEG 最小值
    ptrdiff_t beg_unchanged;
	// 上次完成的重绘以来 Z - GPT 最小值
    ptrdiff_t end_unchanged;
	// 表示上次完成的重绘时的 MODIFF
	// 如果匹配 MODIFF，beg_unchanged 就不包含有用的信息。
    modiff_count unchanged_modified;
	// 表示上次完成的重绘时的 BUF_OVERLAY_MODIFF
	// 如果匹配 BUF_OVERLAY_MODIFF，end_unchanged 就不包含有用的信息。
    modiff_count overlay_unchanged_modified;

    // 表示缓冲区文本的属性。
    INTERVAL intervals;

    // 表示引用这个缓冲区的标记。
    // 这实际上是一个标记，它的 `chain` 中的连续元素是引用这个缓冲区的其他标记。
    // 这是一个单链无序列表，这意味着将一个标记添加到列表中以及在缓冲区内移动一个标记都非常便宜。
    struct Lisp_Marker *markers;

    // 这个字段通常为假。在 `decode_coding_gap` 中临时为真，以防止 `Fgarbage_collect` 缩小间隙并丢失尚未解码的字节。
    bool_bf inhibit_shrinking : 1;

    // 如果需要重新显示，则此字段为真。
    bool_bf redisplay : 1;
  };
```

