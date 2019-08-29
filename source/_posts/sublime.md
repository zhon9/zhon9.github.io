---
title: sublime plugins
date: 2018-11-06 14:18:12
tags: sublime
---
sublime 插件
<!-- more -->
### A File Icon
Sublime Text File-Specific Icons for Improved Visual Grepping
### AdvancedNewFIle
File creation plugin for Sublime Text 2 and Sublime Text 3.
### BracketHighlighter
Bracket and tag highlighter for Sublime Text 
### DocBlockr
Simplifies writing DocBlock comments in Javascript, PHP, CoffeeScript, Actionscript, C & C++
### Emmet
Emmet for Sublime Text
### Package Control
A full-featured package manager
### Side Bra
Duplicate files and copy paths from the Side Bar in Sublime Text 3
### Babel
Syntax definitions for ES6 JavaScript with React JSX extensions.
### HTML-CSS-JS Prettify
HTML, CSS, JavaScript, JSON, React/JSX and Vue code formatter for Sublime Text 2 and 3 via node.js
### SublimeCodeIntel
Full-featured code intelligence and smart autocomplete engine
### SublimeREPL
SublimeREPL - run an interpreter inside ST2 (Clojure, CoffeeScript, F#, Groovy, Haskell, Lua, MozRepl, NodeJS, Python + virtualenv, R, Ruby, Scala...)
### Auto​File​Name
Sublime Text plugin that autocompletes filenames
### Compare Side-By-Side

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
	"word_wrap": true
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