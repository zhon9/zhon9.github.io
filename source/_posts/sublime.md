---
title: sublime note
date: 2018-11-06 14:18:12
tags: sublime
---
### Shortcut
1. 搜索文件：ctrl+p 输入文件名
2. 搜索函数/方法：ctrl+p 输入`“文件名@方法名”` 如 User@show
3. 跳转到指定行：ctrl+p 输入`文件名:行号`,只输入: 时在当前文件跳转
4. 查找当前文件方法：ctrl+r
5. 返回/前进编辑位置：Alt + -、Alt + Shift + -
6. 切换标签页：Ctrl + PgUp、Ctrl + PgDn
7. 选中单词：Ctrl + D 连续按会选中页面中所有单词，以实现批量编辑
8. 以单词为单位快速移动光标：Ctrl + ←、Ctrl + →
9. 选中当前行：Ctrl + L
10. 跳转到第几行：Ctrl+G
11. 跳转到对应括号：Ctrl+M
12. 开关侧栏：Ctrl+K+B
13. 选中当前括号内容，重复可选着括号本身：Ctrl+Shift+M
14. 注释当前html标签块：Ctrl+Shift+/
15. 专注编写模式：Shift+F11
16. 分屏显示：Alt+Shift+数字
17. Ctrl+Enter 在下一行插入新行。举个栗子：即使光标不在行尾，也能快速向下插入一行。
18. Ctrl+Shift+Enter 在上一行插入新行。举个栗子：即使光标不在行首，也能快速向上插入一行。
19. Ctrl+Shift+[ 选中代码，按下快捷键，折叠代码。
20. Ctrl+Shift+] 选中代码，按下快捷键，展开代码。

---
### Plugins
- A File Icon
Sublime Text File-Specific Icons for Improved Visual Grepping
- AdvancedNewFIle
File creation plugin for Sublime Text 2 and Sublime Text 3.
- BracketHighlighter
Bracket and tag highlighter for Sublime Text 
- DocBlockr
Simplifies writing DocBlock comments in Javascript, PHP, CoffeeScript, Actionscript, C & C++
- Emmet
Emmet for Sublime Text
- Package Control
A full-featured package manager
- Side Bra
Duplicate files and copy paths from the Side Bar in Sublime Text 3
- Babel
Syntax definitions for ES6 JavaScript with React JSX extensions.
- HTML-CSS-JS Prettify
HTML, CSS, JavaScript, JSON, React/JSX and Vue code formatter for Sublime Text 2 and 3 via node.js
- SublimeCodeIntel
Full-featured code intelligence and smart autocomplete engine
- SublimeREPL
SublimeREPL - run an interpreter inside ST2 (Clojure, CoffeeScript, F#, Groovy, Haskell, Lua, MozRepl, NodeJS, Python + virtualenv, R, Ruby, Scala...)
- Auto​File​Name
Sublime Text plugin that autocompletes filenames
- Compare Side-By-Side
This package adds a simple side-by-side comparison tool to Sublime Text 2 and 3.
- Material Theme
Material Theme, the most epic theme for Sublime Text 3 by Mattia Astorino
- SublimeLinter
- SublimeLinter-php
This linter plugin for SublimeLinter provides an interface to php -l. It will be used with files that have the “PHP”, “HTML”, or “HTML 5” syntax.
- ConvertToUTF8
A Sublime Text 2 & 3 plugin for editing and saving files encoded in GBK, BIG5, EUC-KR, EUC-JP, Shift_JIS, etc.
- Laravel 5 Artisan
Laravel 5 Artisan Commands for Sublime Text 3
- SideBarEnhancements
Enhancements to Sublime Text sidebar. Files and folders.
- Git
Plugin for some git integration into sublime text
- GitGutter
A Sublime Text 2/3 plugin to see git diff in gutter

---

### Setting
```json
{
	"font_size": 13,
	"ignored_packages":
	[
		"Vintage"
	],
    "save_on_focus_lost": true,
	"theme": "Default.sublime-theme",
	"word_wrap": true,
    
    // material theme
    "font_options":["gray_antialias", "subpixel_antialias"],
    "always_show_minimap_viewport": true,
    "bold_folder_labels": true,
    "indent_guide_options":
    [
        "draw_normal",
        "draw_active"
    ],
    "line_padding_bottom": 3,
    "line_padding_top": 3,
    "material_theme_accent_red": true,
    "material_theme_big_fileicons": true,
    "material_theme_disable_folder_animation": true,
    "material_theme_disable_tree_indicator": true,
    "overlay_scroll_bars": "enabled",
}

```

### Key Bingdings
```json
[
	//格式化代码,single_line参数删除时，格式化只影响当前光标所在行
	{"keys": ["ctrl+alt+l"], "command": "reindent" ,"args": {"single_line": false}},
    
	//emmet
	{
    "keys": ["tab"],
    "command": "expand_abbreviation_by_tab",

    // put comma-separated syntax selectors for which 
    // you want to expandEmmet abbreviations into "operand" key 
    // instead of SCOPE_SELECTOR.
    // Examples: source.js, text.html - source
    "context": [{
            "operand": "source.js",
            "operator": "equal",
            "match_all": true,
            "key": "selector"
        },

        // run only if there's no selected text
        {
            "match_all": true,
            "key": "selection_empty"
        },

        // don't work if there are active tabstops
        {
            "operator": "equal",
            "operand": false,
            "match_all": true,
            "key": "has_next_field"
        },

        // don't work if completion popup is visible and you
        // want to insert completion with Tab. If you want to
        // expand Emmet with Tab even if popup is visible -- 
        // remove this section
        {
            "operand": false,
            "operator": "equal",
            "match_all": true,
            "key": "auto_complete_visible"
        }, {
            "match_all": true,
            "key": "is_abbreviation"
        }
    ]
	},

    //sublimerepl
    { "keys": ["f5"], "caption": "SublimeREPL:Python", 
                      "command": "run_existing_window_command", "args":
                      {
                           "id": "repl_python_run",
                           "file": "config/Python/Main.sublime-menu"
                      } 
    }
]


```