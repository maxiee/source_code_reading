```c
struct buffer
{
  union vectorlike_header header;

  // 缓冲区的名称。
  Lisp_Object name_;

  /* The last name of this buffer before it was renamed or killed.  */
  Lisp_Object last_name_;

  // 与缓冲区关联的文件名，如果没有关联文件则为 nil。
  Lisp_Object filename_;

  // 用于扩展相对文件名的目录。
  Lisp_Object directory_;

  // 指示缓冲区是否已备份。
  Lisp_Object backed_up_;

  // 上次读取或保存文件时的长度。
  Lisp_Object save_length_;

  // 自动保存缓冲区内容时使用的文件名。
  Lisp_Object auto_save_file_name_;

  // 指示缓冲区是否为只读。
  Lisp_Object read_only_;

  // 表示缓冲区中的标记（mark）位置。
  Lisp_Object mark_;

  // 存储缓冲区的局部变量的关联列表。
  Lisp_Object local_var_alist_;

  // 缓冲区的主模式。
  Lisp_Object major_mode_;

  // 缓冲区启用的次要模式列表。
  Lisp_Object local_minor_modes_;

  /* Pretty name of major mode (e.g., "Lisp"). */
  Lisp_Object mode_name_;

  /* Mode line element that controls format of mode line.  */
  Lisp_Object mode_line_format_;

  /* Analogous to mode_line_format for the line displayed at the top
     of windows.  Nil means don't display that line.  */
  Lisp_Object header_line_format_;

  /* Analogous to mode_line_format for the line displayed at the top
     of windows.  Nil means don't display that line.  */
  Lisp_Object tab_line_format_;

  // 缓冲区的局部键绑定。
  Lisp_Object keymap_;

  /* This buffer's local abbrev table.  */
  Lisp_Object abbrev_table_;

  // 缓冲区的语法表。
  Lisp_Object syntax_table_;

  // 缓冲区的类别表。
  Lisp_Object category_table_;

  // 各种缓冲区局部变量，如 `tab_width_`、`fill_column_` 等。
  Lisp_Object tab_width_;
  Lisp_Object fill_column_;
  Lisp_Object left_margin_;

  /* Function to call when insert space past fill column.  */
  Lisp_Object auto_fill_function_;

  // 大小写转换表
  /* Case table for case-conversion in this buffer.
     This char-table maps each char into its lower-case version.  */
  Lisp_Object downcase_table_;

  /* Char-table mapping each char to its upper-case version.  */
  Lisp_Object upcase_table_;

  /* Char-table for conversion for case-folding search.  */
  Lisp_Object case_canon_table_;

  /* Char-table of equivalences for case-folding search.  */
  Lisp_Object case_eqv_table_;

  // 显示相关的属性，如 `truncate_lines_`、`word_wrap_`、`ctl_arrow_` 等。
  /* Non-nil means do not display continuation lines.  */
  Lisp_Object truncate_lines_;

  /* Non-nil means to use word wrapping when displaying continuation lines.  */
  Lisp_Object word_wrap_;

  /* Non-nil means display ctl chars with uparrow.  */
  Lisp_Object ctl_arrow_;

  /* Non-nil means reorder bidirectional text for display in the
     visual order.  */
  Lisp_Object bidi_display_reordering_;

  /* If non-nil, specifies which direction of text to force in all the
     paragraphs of the buffer.  Nil means determine paragraph
     direction dynamically for each paragraph.  */
  Lisp_Object bidi_paragraph_direction_;

  /* If non-nil, a regular expression for bidi paragraph separator.  */
  Lisp_Object bidi_paragraph_separate_re_;

  /* If non-nil, a regular expression for bidi paragraph start.  */
  Lisp_Object bidi_paragraph_start_re_;

  /* Non-nil means do selective display;
     see doc string in syms_of_buffer (buffer.c) for details.  */
  Lisp_Object selective_display_;

  /* Non-nil means show ... at end of line followed by invisible lines.  */
  Lisp_Object selective_display_ellipses_;

  /* t if "self-insertion" should overwrite; `binary' if it should also
     overwrite newlines and tabs - for editing executables and the like.  */
  Lisp_Object overwrite_mode_;

  /* Non-nil means abbrev mode is on.  Expand abbrevs automatically.  */
  Lisp_Object abbrev_mode_;

  /* Display table to use for text in this buffer.  */
  Lisp_Object display_table_;

  /* t means the mark and region are currently active.  */
  Lisp_Object mark_active_;

  /* Non-nil means the buffer contents are regarded as multi-byte
     form of characters, not a binary code.  */
  Lisp_Object enable_multibyte_characters_;

  /* Coding system to be used for encoding the buffer contents on
     saving.  */
  Lisp_Object buffer_file_coding_system_;

  /* List of symbols naming the file format used for visited file.  */
  Lisp_Object file_format_;

  /* List of symbols naming the file format used for auto-save file.  */
  Lisp_Object auto_save_file_format_;

  /* True if the newline position cache, width run cache and BIDI paragraph
     cache are enabled.  See search.c, indent.c and bidi.c for details.  */
  Lisp_Object cache_long_scans_;

  /* If the width run cache is enabled, this table contains the
     character widths width_run_cache (see above) assumes.  When we
     do a thorough redisplay, we compare this against the buffer's
     current display table to see whether the display table has
     affected the widths of any characters.  If it has, we
     invalidate the width run cache, and re-initialize width_table.  */
  Lisp_Object width_table_;

  // `pt_marker_`、`begv_marker_`、`zv_marker_`：间接缓冲区中用于记录 PT、BEGV 和 ZV 的标记。

  /* In an indirect buffer, or a buffer that is the base of an
     indirect buffer, this holds a marker that records
     PT for this buffer when the buffer is not current.  */
  Lisp_Object pt_marker_;

  /* In an indirect buffer, or a buffer that is the base of an
     indirect buffer, this holds a marker that records
     BEGV for this buffer when the buffer is not current.  */
  Lisp_Object begv_marker_;

  /* In an indirect buffer, or a buffer that is the base of an
     indirect buffer, this holds a marker that records
     ZV for this buffer when the buffer is not current.  */
  Lisp_Object zv_marker_;

  /* This holds the point value before the last scroll operation.
     Explicitly setting point sets this to nil.  */
  Lisp_Object point_before_scroll_;

  /* Truename of the visited file, or nil.  */
  Lisp_Object file_truename_;

  /* Invisibility spec of this buffer.
     t => any non-nil `invisible' property means invisible.
     A list => `invisible' property means invisible
     if it is memq in that list.  */
  Lisp_Object invisibility_spec_;

  /* This is the last window that was selected with this buffer in it,
     or nil if that window no longer displays this buffer.  */
  Lisp_Object last_selected_window_;

  /* Incremented each time the buffer is displayed in a window.  */
  Lisp_Object display_count_;

  /* Widths of left and right marginal areas for windows displaying
     this buffer.  */
  Lisp_Object left_margin_cols_;
  Lisp_Object right_margin_cols_;

  /* Widths of left and right fringe areas for windows displaying
     this buffer.  */
  Lisp_Object left_fringe_width_;
  Lisp_Object right_fringe_width_;

  /* Non-nil means fringes are drawn outside display margins;
     othersize draw them between margin areas and text.  */
  Lisp_Object fringes_outside_margins_;

  /* Width, height and types of scroll bar areas for windows displaying
     this buffer.  */
  Lisp_Object scroll_bar_width_;
  Lisp_Object scroll_bar_height_;
  Lisp_Object vertical_scroll_bar_type_;
  Lisp_Object horizontal_scroll_bar_type_;

  /* Non-nil means indicate lines not displaying text (in a style
     like vi).  */
  Lisp_Object indicate_empty_lines_;

  /* Non-nil means indicate buffer boundaries and scrolling.  */
  Lisp_Object indicate_buffer_boundaries_;

  /* Logical to physical fringe bitmap mappings.  */
  Lisp_Object fringe_indicator_alist_;

  /* Logical to physical cursor bitmap mappings.  */
  Lisp_Object fringe_cursor_alist_;

  /* Time stamp updated each time this buffer is displayed in a window.  */
  Lisp_Object display_time_;

  /* If scrolling the display because point is below the bottom of a
     window showing this buffer, try to choose a window start so
     that point ends up this number of lines from the top of the
     window.  Nil means that scrolling method isn't used.  */
  Lisp_Object scroll_up_aggressively_;

  /* If scrolling the display because point is above the top of a
     window showing this buffer, try to choose a window start so
     that point ends up this number of lines from the bottom of the
     window.  Nil means that scrolling method isn't used.  */
  Lisp_Object scroll_down_aggressively_;

  /* Desired cursor type in this buffer.  See the doc string of
     per-buffer variable `cursor-type'.  */
  Lisp_Object cursor_type_;

  /* An integer > 0 means put that number of pixels below text lines
     in the display of this buffer.  */
  Lisp_Object extra_line_spacing_;

#ifdef HAVE_TREE_SITTER
  /* A list of tree-sitter parsers for this buffer.  */
  Lisp_Object ts_parser_list_;
#endif

  /* What type of text conversion the input method should apply to
     this buffer.  */
  Lisp_Object text_conversion_style_;

  /* Cursor type to display in non-selected windows.
     t means to use hollow box cursor.
     See `cursor-type' for other values.  */
  Lisp_Object cursor_in_non_selected_windows_;

  /* No more Lisp_Object beyond cursor_in_non_selected_windows_.
     Except undo_list, which is handled specially in Fgarbage_collect.  */

  // 存储缓冲区内容的坐标的结构体。
  struct buffer_text own_text;

  // 指向用于缓冲区的 `struct buffer_text` 的指针。
  struct buffer_text *text;

  /* Char position of point in buffer.  */
  ptrdiff_t pt;

  /* Byte position of point in buffer.  */
  ptrdiff_t pt_byte;

  /* Char position of beginning of accessible range.  */
  ptrdiff_t begv;

  /* Byte position of beginning of accessible range.  */
  ptrdiff_t begv_byte;

  /* Char position of end of accessible range.  */
  ptrdiff_t zv;

  /* Byte position of end of accessible range.  */
  ptrdiff_t zv_byte;

  // 对于间接缓冲区，指向其基础缓冲区。
  struct buffer *base_buffer;

  // 间接缓冲区的数量。
  int indirections;

  // 显示缓冲区的窗口数量。
  int window_count;

  /* A non-zero value in slot IDX means that per-buffer variable
     with index IDX has a local value in this buffer.  The index IDX
     for a buffer-local variable is stored in that variable's slot
     in buffer_local_flags as a Lisp integer.  If the index is -1,
     this means the variable is always local in all buffers.  */
  char local_flags[MAX_PER_BUFFER_VARS];

  // 访问文件的修改时间。
  struct timespec modtime;

  /* Size of the file when modtime was set.  This is used to detect the
     case where the file grew while we were reading it, so the modtime
     is still the same (since it's rounded up to seconds) but we're actually
     not up-to-date.  -1 means the size is unknown.  Only meaningful if
     modtime is actually set.  */
  off_t modtime_size;

  // 上次自动保存时的 `modiff` 值。
  modiff_count auto_save_modified;

  /* The value of text->modiff at the last display error.
     Redisplay of this buffer is inhibited until it changes again.  */
  modiff_count display_error_modiff;

  /* The time at which we detected a failure to auto-save,
     Or 0 if we didn't have a failure.  */
  time_t auto_save_failure_time;

  // 上次显示缓冲区时的起始位置。
  ptrdiff_t last_window_start;

  // 用于优化的缓存结构体。
  /* If the long line scan cache is enabled (i.e. the buffer-local
     variable cache-long-scans is non-nil), newline_cache points to
     the newline cache, and width_run_cache points to the width run
     cache.

     The newline cache records which stretches of the buffer are
     known *not* to contain newlines, so that they can be skipped
     quickly when we search for newlines.

     The width run cache records which stretches of the buffer are
     known to contain characters whose widths are all the same.  If
     the width run cache maps a character to a value > 0, that value is
     the character's width; if it maps a character to zero, we don't
     know what its width is.  This allows compute_motion to process
     such regions very quickly, using algebra instead of inspecting
     each character.   See also width_table, below.

     The latter cache is used to speedup bidi_find_paragraph_start.  */
  struct region_cache *newline_cache;
  struct region_cache *width_run_cache;
  struct region_cache *bidi_paragraph_cache;

  /* Non-zero means disable redisplay optimizations when rebuilding the glyph
     matrices (but not when redrawing).  */
  bool_bf prevent_redisplay_optimizations_p : 1;

  /* Non-zero whenever the narrowing is changed in this buffer.  */
  bool_bf clip_changed : 1;

  /* Non-zero for internal or temporary buffers that don't need to
     run hooks kill-buffer-hook, kill-buffer-query-functions, and
     buffer-list-update-hook.  This is used in coding.c to avoid
     slowing down en/decoding when a lot of these hooks are
     defined, as well as by with-temp-buffer, for example.  */
  bool_bf inhibit_buffer_hooks : 1;

  /* Non-zero when the buffer contains long lines and specific
     display optimizations must be used.  */
  bool_bf long_line_optimizations_p : 1;

  // 存储缓冲区中叠加层（overlay）的区间树。
  struct itree_tree *overlays;

  // 缓冲区的撤销信息列表。
  Lisp_Object undo_list_;
};
```