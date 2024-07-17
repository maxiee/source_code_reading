## MainWindow

初始化和 UI 设置:

- 在**init**方法中初始化 UI 组件,包括菜单栏、工具栏、状态栏等。
- 创建 QWebEngineView 作为主要的阅读界面。
- 设置缓存路径和加载上次阅读位置。

Cookie 管理:

- save_cookie 方法保存从 QWebEngineView 获取的 cookie。
- dump_cookies 方法将 cookie 保存到文件。
- load_cookies 方法从文件加载 cookie 并应用到 QWebEngineView。

书架和笔记管理:

- download_shelf 方法获取用户的书架信息。
- init_model 方法初始化列表和表格视图来显示书籍。
- get_note 和 get_hot_note 方法获取指定书籍的笔记和热门笔记。
- download_notes 方法批量下载所有书籍的笔记。

界面切换:

- toggle_mode 方法在阅读模式和笔记模式之间切换。
- view_library 和 view_shelf 方法加载书城和书架页面。

事件处理:

- on_listView_clicked 和 on_tableView_clicked 处理书籍选择。
- on_curBook_changed 更新当前选中书籍的笔记显示。

文件操作:

- save_note 方法保存当前笔记到文件。
- open_notes 方法打开保存的笔记文件。

其他功能:

- update_lastpage 方法记录最后阅读位置。
- resizeEvent 方法处理窗口大小变化。

核心业务逻辑主要包括:

1. 通过 WebEngine 加载微信读书网页,实现阅读功能。
2. 管理和同步用户的书架信息。
3. 获取、显示和保存书籍笔记。
4. 在阅读界面和笔记管理界面之间切换。
5. 保存阅读进度和用户登录状态(通过 cookie)。
