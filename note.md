[TOC]
## 打印信息
帮助`:help echo`和`:help echom`
执行:`:echo "output string echo"` 和`echom "output string echom"`
**不同:**
`echo`输出的信息不能通过`:messages`命令查看，通过`echom`输出的信息，通过`:messages`命令能查看到。

## 设置选项
vim拥有很多选项可以设置以改变展现方式。
主要有两种方式:布尔选项(值为on或off)和键值选项.
### 布尔选项
设置行号可见:`:set number`
设置行号不可见:`:set nonumber`
所有的布尔选项都是这种配置方法:`:set <name>`打开选项，`set no<name>`关闭选项.
### 切换布尔选项
可以切换布尔选项值，即从开启切为关闭或从关闭切为开启:
`:set number!`
### 查看选项当前值
可以使用`?`符号向vim获取一个选项的当前值:`:set number?`会获取到行号当前的显示状态.
### 键值选项
```
:set numberwidth=10
:set numberwidth?
```
## 基本映射
`:map -x`将光标置于文本中的某处，按下`-`就相当于按了`x`.
`:map <space> viw` 光标移动到一个单词上，按下空格键，Vim将高亮选中整个单词.
`:map <c-d> dd` 在键盘上按下`Ctrl+d`将执行`dd`命令。
### 注释
`:map <space> viw" Select world`

## 模式映射
可以使用`nmap`,`vmap`,`imap`命令分布指定映射仅在normal,visual,insert模式有效。

## 精确映射
|递归映射|非递归映射|
|--------|----------|
|nmap|noremap/nnoremap|
|imap|inoremap|
|vmap|vnoremap|
**注意:最好在任何时候都使用非递归映射** 

## Leaders
`:let mapleader="-"`设置前缀
`:noremap <leader>d dd`
### Local Learder
`:let maplocalleader="\\"` 只对那些只对某类文件(如Python文件，HTML文件)而设置对映射。
**注意:**上面设置使用的是\\而不是\,因为在vim中\是转义字符。
### 不退出vim的情况下编辑.vimrc并保存设置
打开.vimrc
`nnoremap <leader>ev :vsplit $MYVIMRC<cr>`
保存.vimrc
`nnoremap <leader>sv :source $MYVIMRC<cr>`

## Abbreviations
vim有个称为`abbreviations`的特性，与映射类似，但是它用于insert, replace,command模式。
```
:iabbrev adn and
```
上面的命令作用是在insert模式下，输入adn+空格后会自动替换为and.
## 给单词添加双引号
```
nnoremap <leader>" viw<esc>a"<esc>hbi"<esc>lel
```
## 设置mapping不可用
```
"设置esc不可用
inoremap <esc> <nop>
```
## 本地设置
local-options
setlocal
map-local
## 自动命令
这个命令可以让执行`:edit file_name`命令的时候直接创建一个文件,正常情况下`:edit`命令打开一个文件
如果文件不存在的话不会立刻创建，只有填入内容并保存后才会创建文件。
```
autocmd BufNewFile * :write
```
下面的命令跟上面的命令不一样，下面的命令只对txt文件有效，对其他文件无效。
```
autocmd BufNewFile *.txt :write
```
针对js文件自动缩进
```
autocmd BufNewFile *.js :normal gg=G
```
## 多个事件
可以创建一个绑定多个事件的自动命令，这些事件使用逗号分开。
```
autocmd BufNewFile,BufRead *.html :normal gg=G 
```
## FileType事件
```
autocmd FileType javascript nnoremap <buffer> <localleader>c I//<esc>
autocmd FileType python nnoremap <buffer> <localleader>c I#<esc>
```
help autocmd-events
```
autocmd FileType python :iabbrev <buffer> iff if:<left>
autocmd FileType javascript :iabbrev <buffer> iff if ()<left>
```
