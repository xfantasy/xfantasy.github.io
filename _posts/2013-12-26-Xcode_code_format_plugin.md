---
	layout: index
	title: 在Xcode中使用Uncrustify格式化代码
---

*Notice: 本文仅针对Mac环境*

XCode自带非常简单的代码格式化功能，位于`Editor\Structure\Re-indent`，快捷键`Control+I`，但这个功能非常弱，只能对代码行首位置做非常简单的对齐，很明显，我们需要更强大的格式化功能。

对于我来说，我希望能有以下功能：

- 可定制格式化风格
- 可以去掉多余的空格、可以加入必要的空格
- 支持多种对齐风格
- 批处理多个文件
- 能处理注释
- 能处理宏语句

昨晚在家尝试好久，最终找到最佳组合如下：

- [Uncrustify](http://uncrustify.sourceforge.net/): 一个C语系通用的格式化命令行工具，功能非常强大，但比较蛋疼的格式化风格文件需要手工配置
- [BBUncrustifyPlugin](https://github.com/benoitsan/BBUncrustifyPlugin-Xcode): Xcode插件，在编辑菜单下生成菜单，点击即可调用Uncurstify格式化代码
- [UncrustifyX](https://github.com/ryanmaxwell/UncrustifyX) Uncrustify配置文件修改工具，不是那么强大，但里面的说明很丰富全面

## 配置过程

### 安装Uncrustify

- 源码安装方式：去Sourceforge [下载](http://sourceforge.net/projects/uncrustify/files/) 源码编译安装，最新版本是0.6，下载过来后又有两种安装方式：命令行或者Xcode编译，见压缩包中的README文件
<pre launage="bash">
// 命令行安装方式
$: ./configure
$: make
$: sudo cp ~/src/uncrustify /usr/bin/
</pre>
- 使用包管理工具自动安装，如homebrew，只需要一句: `brew install uncrustify`
- 使用1方式安装完成后，在`解压目录/src/`下有名为 uncrustify.cfg 的文件，拷贝到桌面待用
	
### 安装`BBUncrustifyPlugin`Xcode插件
	
- 到[Github](https://github.com/benoitsan/BBUncrustifyPlugin-Xcode)下在源码
- 用Xcode打开文件包目录的Xcode工程文件，按下`Cmd + B`编译即可
- 重新启动Xcode后，会在`Edit`菜单下生成四个菜单，分别是：
	- Uncrustify selected files
	- Uncrustify actived file
	- Uncrustify selected lines
	- Open with UncurstifyX
- 到这一步，你已经可以使用菜单功能格式化文件了，非常强大有木有。比Xcode厉害一万倍有木有

### 使用UncrustifyX自定义格式化风格

Uncrustify是支持自定义风格的，虽然我们没办法像appCode里的格式配置一样做到图形化，鼠标点点就搞定，但用了UncrustifyX后，你会好过那么一点点。

- 首先去[github](https://github.com/ryanmaxwell/UncrustifyX/releases)下载最新的release版本，并拷贝到/Applications目录下
- 打开UncrustifyX后，点击import导入我们在第一步生成的配置文件
- 按照你自己的要求修改之
- 拷贝uncrustify.cfg文件到 `~/.uncrustify/uncrustify.cfg`
- 搞定之!!!

#### 一些我修改过的配置项
<pre>
comment width 				: 指定注释最大宽度
code width 					: 代码行最大宽度，超过自动折行
mod_add_long_function_closebrace_comment : 方法超过指定行数后，在方法结束大括号后自动加入内容为方法名称的注释
mod_sort_include 			: 对 #import 内容自动按字母顺序排序
nl_brace_else 				: else是否另起一行
nl_after_func_body 			: 方法起始位置大括号是否另起一行
</pre>

我将我修改过的文件放了一份在Github上，你可以直接[下载之](https://raw.github.com/xfantasy/dotfiles/master/uncrustify.cfg)
