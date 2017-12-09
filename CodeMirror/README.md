
## 使用 CodeMirror 打造属于自己的在线代码编辑器

![mark](http://ohfk1r827.bkt.clouddn.com/blog/171209/bA6g59gGB5.jpg-1)

### 前提

写这个的目的是因为之前项目里用到过 CodeMirror，觉得作为一款在线代码编辑器还是不错，也看到过有些网站用到过在线代码编辑，当然我不知道他们是用什么做的，这里我把公司项目里用到的那部分抽出来，单独写篇博客，并把抽出来的那部分代码提交到 GitHub 去（），以防日后可能会再次用到（没准毕业设计里可能用的到）。
<!-- more -->
### 简单介绍

CodeMirror 是一款在线的支持语法高亮的代码编辑器。官网： [http://codemirror.net/](http://codemirror.net/)

可能光看官网，第一眼觉得那些在线编辑器有点**丑**，反正第一眼给我的感觉就是这样子，但是经过自己的细调，也能打造出一款精美的在线代码编辑器。

官网可以把它下载下来。

下载后，解压开得到的文件夹中，lib 下是放的是核心库和核心 css，mode 下放的是各种支持语言的语法定义，theme 目录下是支持的主题样式。一般在开发中，添加 lib 下的引用和 mode 下的引用就够了。

![mark](http://ohfk1r827.bkt.clouddn.com/blog/171209/cJHjjadJ9E.png)

### 如何使用

下面两个是使用 Code Mirror 必须引入的：

```html
<link rel="stylesheet" href="codemirror-5.31.0/lib/codemirror.css"/>
<script src="codemirror-5.31.0/lib/codemirror.js"></script>
```

接下来要引用的就是在 mode 目录下编辑器中要编辑的语言对应的 js 文件，这里以 Groovy 为例：

```html
<!--groovy代码高亮-->
<script src="codemirror-5.31.0/mode/groovy/groovy.js"></script>
```

如果你想让 Java 代码也支持代码高亮，则需要引入我从网上下载下来的 clike.js（我已经放到我的 GitHub 去了）

```html
<!--Java代码高亮必须引入-->
<script src="codemirror-5.31.0/clike.js"></script>
```

引用的文件用于支持对应语言的语法高亮。

然后前面说了第一次进入 Code Mirror 官网，觉得那些编辑器比较丑，那可能是主题比较丑，我这里推荐一款还不错的主题，只需按照如下引入即可：

```html
<!--引入css文件，用以支持主题-->
<link rel="stylesheet" href="codemirror-5.31.0/theme/dracula.css"/>
```

如果你还想让你的编辑器支持代码行折叠，请按照如下进行操作：

```html
<!--支持代码折叠-->
<link rel="stylesheet" href="codemirror-5.31.0/addon/fold/foldgutter.css"/>
<script src="codemirror-5.31.0/addon/fold/foldcode.js"></script>
<script src="codemirror-5.31.0/addon/fold/foldgutter.js"></script>
<script src="codemirror-5.31.0/addon/fold/brace-fold.js"></script>
<script src="codemirror-5.31.0/addon/fold/comment-fold.js"></script>
```

是不是这样引入就好了呢，当然不是啦

### 创建编辑器

在实际项目中，一般都不会直接把 body 整个内容作为编辑器的容器。而最常用的，是使用 textarea。这里我在 <body> 里使用个 textarea，

```html
<!-- begin code -->
<textarea class="form-control" id="code" name="code"></textarea>
<!-- end code-->
```

接下来就是创建编辑器了。

```javascript
//根据DOM元素的id构造出一个编辑器
var editor = CodeMirror.fromTextArea(document.getElementById("code"), {
});
```

是不是有点单调？

没错，我还可以在里面给他设置些属性：（充分利用我一开始引入的那些文件）

```javascript
mode: "text/groovy",    //实现groovy代码高亮
mode: "text/x-java", //实现Java代码高亮
lineNumbers: true,	//显示行号
theme: "dracula",	//设置主题
lineWrapping: true,	//代码折叠
foldGutter: true,
gutters: ["CodeMirror-linenumbers", "CodeMirror-foldgutter"],
matchBrackets: true,	//括号匹配
//readOnly: true,        //只读
```

如果需要查看更多属性，可以去官网查找，目前我只用到这些属性！

**下面也列举些吧：**

**indentUnit: integer**
缩进单位，值为空格数，默认为2 。

**smartIndent: boolean**
自动缩进，设置是否根据上下文自动缩进（和上一行相同的缩进量）。默认为true。

**tabSize: integer**
tab字符的宽度，默认为4 。

**indentWithTabs: boolean**
在缩进时，是否需要把 n*tab宽度个空格替换成n个tab字符，默认为false 。

**electricChars: boolean**
在输入可能改变当前的缩进时，是否重新缩进，默认为true （仅在mode支持缩进时有效）。

**specialChars: RegExp**
需要被占位符(placeholder)替换的特殊字符的正则表达式。最常用的是非打印字符。默认为：/[\u0000-\u0019\u00ad\u200b-\u200f\u2028\u2029\ufeff]/。

**specialCharPlaceholder: function(char) → Element**
这是一个接收由specialChars选项指定的字符作为参数的函数，此函数会产生一个用来显示指定字符的DOM节点。默认情况下，显示一个红点（•），这个红点有一个带有前面特殊字符编码的提示框。

**rtlMoveVisually: boolean**
Determines whether horizontal cursor movement through right-to-left (Arabic, Hebrew) text is visual (pressing the left arrow moves the cursor left) or logical (pressing the left arrow moves to the next lower index in the string, which is visually right in right-to-left text). The default is false on Windows, and true on other platforms.（这段完全不晓得搞啥子鬼）

**keyMap: string**
配置快捷键。默认值为default，即 codemorrir.js 内部定义。其它在[key map](http://codemirror.net/keymap/)目录下。

**extraKeys: object**
给编辑器绑定与前面keyMap配置不同的快捷键。

**lineWrapping: boolean**
在长行时文字是换行(wrap)还是滚动(scroll)，默认为滚动(scroll)。

**lineNumbers: boolean**
是否在编辑器左侧显示行号。

**firstLineNumber: integer**
行号从哪个数开始计数，默认为1 。

**lineNumberFormatter: function(line: integer) → string**
使用一个函数设置行号。

**gutters: array<string>**
用来添加额外的gutter（在行号gutter前或代替行号gutter）。值应该是CSS名称数组，每一项定义了用于绘制gutter背景的宽度（还有可选的背景）。为了能明确设置行号gutter的位置（默认在所有其它gutter的右边），也可以包含CodeMirror-linenumbers类。类名是用于传给setGutterMarker的键名(keys)。

**fixedGutter: boolean**
设置gutter跟随编辑器内容水平滚动（false）还是固定在左侧（true或默认）。

**scrollbarStyle: string**
设置滚动条。默认为”native”，显示原生的滚动条。核心库还提供了”null”样式，此样式会完全隐藏滚动条。Addons可以设置更多的滚动条模式。

**coverGutterNextToScrollbar: boolean**
当fixedGutter启用，并且存在水平滚动条时，在滚动条最左侧默认会显示gutter，当此项设置为true时，gutter会被带有CodeMirror-gutter-filler类的元素遮挡。
**inputStyle: string**
选择CodeMirror处理输入和焦点的方式。核心库定义了textarea和contenteditable输入模式。在移动浏览器上，默认是contenteditable，在桌面浏览器上，默认是textarea。在contenteditable模式下对IME和屏幕阅读器支持更好。

**readOnly: boolean|string**
编辑器是否只读。如果设置为预设的值 “nocursor”，那么除了设置只读外，编辑区域还不能获得焦点。

**showCursorWhenSelecting: boolean**
在选择时是否显示光标，默认为false。

**lineWiseCopyCut: boolean**
启用时，如果在复制或剪切时没有选择文本，那么就会自动操作光标所在的整行。

**undoDepth: integer**
最大撤消次数，默认为200（包括选中内容改变事件） 。

**historyEventDelay: integer**
在输入或删除时引发历史事件前的毫秒数。

**tabindex: integer**
编辑器的tabindex。

**autofocus: boolean**
是否在初始化时自动获取焦点。默认情况是关闭的。但是，在使用textarea并且没有明确指定值的时候会被自动设置为true。

**dragDrop: boolean**
是否允许拖放，默认为true。

**allowDropFileTypes: array<string>**
默认为null。当设置此项时，只接收包含在此数组内的文件类型拖入编辑器。文件类型为MIME名称。

**cursorBlinkRate: number**
光标闪动的间隔，单位为毫秒。默认为530。当设置为0时，会禁用光标闪动。负数会隐藏光标。

**cursorScrollMargin: number**
当光标靠近可视区域边界时，光标距离上方和下方的距离。默认为0 。

**cursorHeight: number**
光标高度。默认为1，也就是撑满行高。对一些字体，设置0.85看起来会更好。

**resetSelectionOnContextMenu: boolean**
设置在选择文本外点击打开上下文菜单时，是否将光标移动到点击处。默认为true。

**workTime, workDelay: number**
通过一个假的后台线程高亮 workTime 时长，然后使用 timeout 休息 workDelay 时长。默认为200和300 。（完全不懂这个功能是在说啥）

**pollInterval: number**
指明CodeMirror向对应的textarea滚动（写数据）的速度（获得焦点时）。大多数的输入都是通过事件捕获，但是有的输入法（如IME）在某些浏览器上并不会生成事件，所以使用数据滚动。默认为100毫秒。

**flattenSpans: boolean**
默认情况下，CodeMirror会将使用相同class的两个span合并成一个。通过设置此项为false禁用此功能。

**addModeClass: boolean**
当启用时（默认禁用），会给每个标记添加额外的表示生成标记的mode的以cm-m开头的CSS样式类。例如，XML mode产生的标记，会添加cm-m-xml类。

**maxHighlightLength: number**
当需要高亮很长的行时，为了保持响应性能，当到达某些位置时，编辑器会直接将其他行设置为纯文本(plain text)。默认为10000，可以设置为Infinity来关闭此功能。

**viewportMargin: integer**
指定当前滚动到视图中内容上方和下方要渲染的行数。这会影响到滚动时要更新的行数。通常情况下应该使用默认值10。可以设置值为Infinity始终渲染整个文档。注意：这样设置在处理大文档时会影响性能。

---

如果你要设置代码框的大小该怎么做呢？

```javascript
editor.setSize('800px', '950px');     //设置代码框的长宽
```

另外，如果你想给代码框赋值，该怎么办呢？

```javascript
editor.setValue("");    //给代码框赋值
editor.getValue();    //获取代码框的值
```

如果你再想在其他地方设置新的属性，可以像下面这样写：

```javascript
editor.setOption("readOnly", true);	//类似这种
```

### 总结

上面就大概讲了下 Code Mirror 怎么使用，那么我们来看看效果吧

![mark](http://ohfk1r827.bkt.clouddn.com/blog/171209/C1303F6F9A.png-1)

我自我感觉还是可以的哈！

里面所有涉及的代码在 GitHub 里可以下载：[https://github.com/zhisheng17/CoderBlog/tree/master/CodeMirror](https://github.com/zhisheng17/CoderBlog/tree/master/CodeMirror)

文章原创，转载务必请注明原创地址：[http://www.54tianzhisheng.cn/2017/12/09/CodeMirror/](http://www.54tianzhisheng.cn/2017/12/09/CodeMirror/)

### 最后

fuck  无脑的推酷爬虫，竟然把我所有文章最后的原创链接都给去掉了，这是我现在想到的一种对策方法。任何其他形式的转载，也必须把我文章所有内容加上，不得做任何修改，否则请别转载了！