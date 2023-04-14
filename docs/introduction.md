## Introduction

This wiki was designed to help new developers out when it comes to coding in lua. The tutorials are focused around scripting in CS:GO using the aimware lua api.

If you're completely new to programming or scripting I recommend you check out the [official Lua documentation](https://www.lua.org/pil/contents.html) first. The examples section is a good place to learn too. All code blocks contain comments that make it much easier to understand what the code does.

## Code editors and preparation

You can write code using any text editor, but here are my personal recommendations:

* Notepad++ - fast and simple code editor that supports lots of languages
* Visual Studio Code - more advanced code editor that has addons like snippets (automatic code completion) and error checking (language server)

#
Other text editors will work too, but I highly advise against any of these:

* Built-in Lua editor - after V5.1 the editor was heavily improved, but it still can't compare with proper code editors
* Notepad, MS Word, Google Docs (or any similar editors not made for coding) - general lack of features (line numbers, syntax highlighting, automatic indenting etc.)

???+ warning "Avoiding encoding errors"
	To avoid any unnecessary errors and issues, please select the UTF-8 text encoding in your code editor's settings.
	
???+ note "Testing out code examples"
	To test code examples from the Lua basics page you can use this [online Lua interpreter](https://rextester.com/l/lua_online_compiler). Simply copy the code and paste it into the text editor on the website. You can also play around and try to write some of your own code. Note that it does not support the aimware Lua API.