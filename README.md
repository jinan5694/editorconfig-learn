## EditorConfig是什么？

EditorConfig可以帮助开发者在不同的编辑器和IDE之间定义和维护一致的代码风格。EditorConfig包含一个用于定义代码格式的文件和一批编辑器插件，这些插件可以让编辑器读取配置文件并依此格式化代码。

## EditorConfig的配置文件是怎样的？

以下是一个用于设置Python和JavaScript行尾和缩进风格的配置文件。

```
# http://editorconfig.org
root = true

[*]
indent_style = space
indent_size = 2
end_of_line = lf
charset = utf-8
insert_final_newline = true

[*.md]
trim_trailing_whitespace = false

```

## 在哪里存放配置文件

当打开一个文件时，EditorConfig插件会在打开文件的目录和其每一级父目录查找.editorconfig文件，直到有一个配置文件root=true。

EditorConfig配置文件从上往下读取，并且路径最近的文件最后被读取。匹配的配置属性按照属性应用在代码上，所以最接近代码文件的属性优先级最高。

Windows 用户：在资源管理器创建.editorconfig文件，可以先创建.editorconfig.文件，系统会自动重名为.editorconfig。

文件格式详情

EditorConfig文件使用INI格式（译注：请参考维基百科），目的是可以与Python ConfigParser Library兼容，但是允许在分段名（译注：原文是section names）中使用“and”。分段名是全局的文件路径，格式类似于gitignore。斜杠(/)作为路径分隔符，#或者;作为注释。注释应该单独占一行。EditorConfig文件使用UTF-8格式、CRLF或LF作为换行符。

## 通配符


通配符 | 说明
---|---
* | 匹配除/之外的任意字符串
** | 匹配任意字符串
? | 匹配任意单个字符
[name] | 匹配name字符
[!name] | 匹配非name字符
{s1,s3,s3} | 匹配任意给定的字符串（0.11.0起支持

## 支持的属性
> 注意：不是每种插件都支持所有的属性，具体可见Wiki。

key | value
---|---
indent_style | tab为hard-tabs，space为soft-tabs。
indent_size | 设置整数表示规定每级缩进的列数和soft-tabs的宽度（译注：空格数）。如果设定为tab，则会使用tab_width的值（如果已指定）。
tab_width | 设置整数用于指定替代tab的列数。默认值就是indent_size的值，一般无需指定。
end_of_line | 定义换行符，支持lf、cr和crlf。
charset | 编码格式，支持latin1、utf-8、utf-8-bom、utf-16be和utf-16le，不建议使用uft-8-bom。
trim_trailing_whitespace | 设为true表示会除去换行行首的任意空白字符，false反之。
insert_final_newline | 设为true表明使文件以一个空白行结尾，false反之。
root | 表明是最顶层的配置文件，发现设为true时，才会停止查找.editorconfig文件。


目前所有的属性名和属性值都是大小写不敏感的。编译时都会将其转为小写。通常，如果没有明确指定某个属性，则会使用编辑器的配置，而EditorConfig不会处理。

*推荐不要指定某些EditorConfig属性。比如，tab_width不需要特别指定，除非它与indent_size不同。同样的，当indent_style设为tab时，不需要配置indent_size，这样才方便阅读者使用他们习惯的缩进格式。另外，如果某些属性并没有规范化（比如end_of_line），就最好不要设置它。*

## 后言

可以看到，EditorConfig目前支持的属性非常少，且只局限于基本的文件缩进、换行等格式（当然这与其定位有关），虽然并不能满足团队里代码规范统一的要求，但是其简单易上手、跨编辑器且静默生效的特点，建议在项目中使用。
