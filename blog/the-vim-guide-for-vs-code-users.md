---
layout: post
date: 2020-09-29
title: 写给 VS Code 用户的 Vim 入坑指南
featured: true
---

现实当中使用 Vim 来写前端的人是少之又少，大多数人基本上都是使用 VSCode。但作为「编辑器之神」，不管使不使用 Vim 进行编码，学习 Vim 的编辑模式都是有好处的。

本文会从最基本的使用和配置开始介绍作为前端工程师怎么从零到一到开始使用 Vim。当然，我也不期望因为一篇文章而让广大的 VSCode 用户转用 Vim，所以最后会介绍如何在 VSCode 中使用 Vim 插件进行更高效的编码。

## 基本使用

### 模式

与一般的编辑器最大的不同是，在 Vim 中有 4 种编辑模式，分别是：普通模式、插入模式、可视模式和命令行模式。使用 Vim 进行编辑就需要熟练的在各个模式之间进行切换。

![四种编辑模式](https://ahonn-me.oss-cn-beijing.aliyuncs.com/images/wAUpUM.png)

#### 普通模式

一般情况下每次进入编辑器的时候默认为普通模式，此时可以使用 `h/j/k/l` 来对光标进行移动。

普通模式下我们的输入会被当作是一个命令，而命令是可以指定次数的。例如我们想要向下移动 10 行。我们可以在普通模式下连续按 10 次 j（类似于在普通编辑器中连续按 10 次向下键），除此之外我们也可以直接输入 10j。

##### 移动光标

在 Vim 中为了提高输入效率而区分编辑模式，因此我们可以在尽量少的移动手指的情况下来进行光标的移动。以下是一些在普通模式下常用的用于移动光标的命令:

- `h/j/k/l`：分别代表着向左，下，上，右的方向移动
- `^/$`：跳到行首/行尾
- `w/b`：跳到下一个单词头/跳到上一个单词头
- `f{char}/F{char}`：跳到下一个字符为 char 的位置/跳到上一个字符为 char 的位置

`h/j/k/l` 等同于一般情况下的上下左右键，能够在不移出键盘主区域的情况下移动光标。一种简单的记忆方式是左右两边的 `h/l` 代表左右移动，而食指在键盘的默认位置 `j`即为向下，反之 `k` 为向上。

如果你也是快捷键小能手的话，大概率也会使用 `ctrl + a` 或者 `ctrl + e` 来跳到行首或者行尾。 在 Vim 的普通模式下我们可以使用 `^/$` 来进行这个操作，如果你熟悉正则表达式的话可以发现其实 `^` 就是表示行首的意思，而 `$` 是行尾的意思。

我们这个时候已经能够上下左右移动光标和跳转到行首行尾了。你可能会问，如果我只想移动两个单词的位置的话该怎么办？这时候我们就可以使用 `w/b` 来移动到下一个单词或者上一个单词的单词头了。如上所提到的，在普通模式下命令是可以指定字数的，所以我们可以通过 `2w` 来移动两个单词的位置。

![使用 ^/$ 与 w/b 快速移动光标](https://ahonn-me.oss-cn-beijing.aliyuncs.com/images/gyKgUn.png)

这时候又有了另外的一个疑惑，我们在移动光标的时候总不能还在脑子里面算一下还有几个单词的位置吧？就算连续的按 w 来到达我们想要到的地方也有点蠢，所以在 Vim 中，我们还能够使用 `f{char}/F{char}` 来向前/向后搜索某个字符，然后跳过去。

因此，我们也可以通过 `f{char}/F{char}` 来操作光标跳转到上图的位置：

![使用 f{char}/F{char} 跳转到指定字符](https://ahonn-me.oss-cn-beijing.aliyuncs.com/images/Pddwc3.png)

通过以上的各种跳转方式可以满足绝大多数跳转的场景，熟练使用之后基本上就不要再通过鼠标去移动光标了。

#### 插入模式

插入模式其实大家都很熟悉，一般的编辑器默认的状态就是 Vim 中的插入模式。在插入模式我们能够进行插入字符、换行等操作。

当然，在这个模式里面也可以通过方向键移动光标，假如忽略其他的模式的话，完全可以把 Vim 当成普通的编辑器进行使用。但这样的话就失去了学 Vim 的意义了，Vim 最值得学习的就是通过切换编辑模式来进行快速的移动/输入/选择。

在 [Vim 实用技巧](https://book.douban.com/subject/26967597/) 中是这样描述 Vim 中的普通模式的：

> 画家在休息时不会把画笔放在画布上。对 Vim 而言也是这样，普通模式就是 Vim 的自然放松状态，其名字已经寓示了这一点。

> 谁说一定要切换到插入模式才行？我们可以重新调整已有代码的格式，复制它们，移动其位置，或是删除它们。在普通模式中，我们有众多的工具可以利用。

所以当我们使用 Vim 的时候，只有想要输入点什么内容的时候才会进入插入模式。那么我们如何从普通模式进入插入模式呢？

从普通模式进入插入模式有许多中方式：

- `i`：在光标的前面进行插入
- `a`：在光标的后面进行插入
- `o`：在光标所在行后面插入新一行

![进入插入模式](https://ahonn-me.oss-cn-beijing.aliyuncs.com/images/diLxcP.png)

##### 变种命令

除此之外，我们还可以使用变种的 `I/A/O` 来使用不同的插入姿势。`I` 与 `i` 都是在前面进行插入，而不同的是 `I` 是在行首进行插入，操作有点类似与使用 `^` 将光标移动到行首之后在通过 `i` 进入插入模式。相似的 `A` 是在行尾进行输入，约等于 `$a`。

使用`o`在光标所在行的后面插入新一行进行插入，那么如何在光标所在行的前面插入新一行呢？我们可以使用 `O` 来做类似 `k` 向上移一行然后 `o` 的操作。

简单来说，可以这样去记忆：

- `I` == `^i`
- `A` == `$a`
- `O` == `ko`

那么如何在插入模式中切换到普通模式呢？答案是 `Esc` 或者 `ctrl + [`。我们在任何模式当中都可以通过这两种方式来切换回普通模式。所以一般的流程是普通模式中移动光标或者执行命令，然后在需要插入代码的位置切换到插入模式进行编辑，编辑完成之后再切换回普通模式。就像是画家思考完成之后拿起画布画，然后再放下画笔继续思考，以此往复。

如果你能够练习到熟练的切换普通模式与插入模式的话，会发现在输入效率上会有所提升。虽然这可能需要经历一段阵痛期，一但形成肌肉记忆之后就可以不需要回忆那个命令是自己想要的操作了。这一点上跟从全拼输入法切换到双拼输入法的时候的感觉类似。习惯了通过切换模式 + 命令的方式移动光标进行输入后，移动鼠标去点击的动作就会显得非常的不自然。

#### 可视模式

细心的你可能会发现，到目前为止我们只提到了如何在普通模式下进入插入模式进行编辑操作。没有提到如何在普通模式下面进行删除操作。

虽然你也可以在插入模式里通过删除键进行删除，但此时只能够删除光标前的字符。显然，我们总不能每次都切换到普通模式后移动光标，再进入插入模式进行删除操作。插入模式，最大的职责就是进行字符的插入。

所以，我们可以在普通模式中移动光标，然后通过 `x` 这个命令来删除对应的字符，并且通过 `d` 来删除指定范围的内容。

以下是命令 `d` 的常用用法：

- `dd`：删除当前光标所在的行
- `diw`：删除当前光标所在的单词
- `dt{char}`：从当前位置删除到某个字符前为止

一般情况下我们会使用 `dd` 来删除一整行，但是真实的情况是我们可能不想一整行都删除，这时候你可以会想要进入插入模式使用鼠标选中某一点要删除的内容然后按删除键。这有笨拙，我们有更方便的做法。

在普通模式里面我们可以使用 `v` 进入可视模式，在可视模式中允许我们通过普通模式中移动光标的方式来选中某一段内容进行操作。使用的 `v` 命令是进入以字符为单位的可视模式，此外我们还有以行为单位的可视模式的命令 `V` 以及以列为单位的可视模式命令 `ctrl + v`。这里我们主要讨论 以字符为单位的可视模式 `v`，另外可视模式的区别请自行了解。

##### 剪切、复制与粘贴

当我们在普通模式中按 `v` 的时候，会把当前光标为主作为选区的起点，然后我们可以通过 `h/j/k/l/w/b` 等进行光标的移动，确定选区的终点。

![在可视模式中进行选择](https://ahonn-me.oss-cn-beijing.aliyuncs.com/images/lNuHSh.png)

在选择了要操作的范围之后我们就可以使用 `d` 命令来进行删除。使用 `d` 命令进行操作的时候实际上进行的是我们熟悉的「剪切」操作，我们可以通过另外的一个命令 `p` 在普通模式下进行粘贴操作。

与 `d` 命令类似的还有复制命令 `y`，我们可以通过 `yy` 来复制一行内容。同样的，也可以进入可视模式之后选定指定的内容进行复制，然后回到普通模式进行 `p` 粘贴操作。

##### 文本对象

讲到这里就不得不说 Vim 非常有特色的文本对象（text object）了。文本对象能够让我们不移动光标的情况下来操作一定区域内的内容。

上面提到的 `diw` 删除当前光标所在的单词的命令中就使用到了文本对象，我们可以把这一整个命令拆解为 `d` + `iw`。这里的 `iw` 即为文本对象，指的是当前单词的意思。

我常用的其他文本对象:

- `aw`：当前单词以及空格
- `i(`：括号内的内容
- `a(`：括号以及括号内的内容

其中，`i(` 和 `a（` 中的括号可以换成任何成对的符号，例如 `i[`、`i{`、`i"` 等，表示删除成对的符号范围的内容。

既然 `d` 命令后面可以跟着文本对象，那么同理 `y` 命令进行复制的时候也是可以跟着文本对象来指定复制的区域内容的。例如我们可以在普通模式下通过`yiw`来复制光标下的单词：

![复制文本对象](https://ahonn-me.oss-cn-beijing.aliyuncs.com/images/593bq4.png)

类似的，我们还能够快速的复制任何成对符号中的内容，这在复制代码中的字符串时非常的有用。通过文本对象我们可以无需进入可视模式而进行一些简单的操作。关于文本对象的内容非常的多，这里由于篇幅原因就不详细介绍了，有兴趣的小伙伴可以自行去了解。

#### 命令模式

在普通模式中我们输入 `:` 会进入命令模式，在命令模式中我们可以使用与 shell 下的命令行类似的命令，比如我们退出 Vim 编辑器需要使用的 `:qa` 命令。

这里指介绍下我最常使用的命令：

- `:q!`：强制退出
- `:w`、`:wa`：保持当前文件/保存所有文件
- `:s/old/new/g`：将字符串 `old` 替换为 `new`

命令模式下[支持非常多的命令](http://vimdoc.sourceforge.net/htmldoc/vimindex.html#ex-cmd-index)，但一般来说我们不需要进入命令模式就可以完成我们的编辑操作了，并且把需要经常使用的命令模式下的命令映射到某一个快捷键当中来进行使用。

### 快捷键

例如我们可以把上面的字符串的命令映射到某一个快捷键上，在 `~/.vimrc` 文件中添加如下内容：

```vim
nnoremap <C-f> :s/
```

然后在命令模式中重新载入我们的 vim 配置：`:source $MYVIMRC`。之后我们就可以通过 `ctrl + f` 这个快捷键来进入命令模式，并且自动的为你输入 `:s/`，我们只需要在后面输入对应的替换的正则表达式就可以了。

这里的 `nnoremap` 表示的意思是普通模式下的非递归映射，此外我们还有 `inoremap`，`vnoremap` 等表示在不同模式下的非递归映射。

所以到底什么是非递归映射（noremap）？这里我们需要先介绍下递归映射，如果我们有如下的配置：

```vim
map a b
map c a
```

那么就相对于是 `map c b`，即快捷键的映射会被其他的映射所影响。而如果是非递归映射的话：

```vim
noremap a b
noremap c a
```

当我们按下 c 的时候会直接映射到 a 而不会继续映射到 c。一般情况下我们使用 `noremap` 即可。对于`map` 以及 `noremap` 的详细的介绍可以查看这篇文章：[vim 的几种模式和按键映射](http://haoxiang.org/2011/09/vim-modes-and-mappin/)。

另外，在 Vim 中还有 `Leader` 键的概念，它有点像是我们按快捷键的时候的 `ctrl` 或者 `cmd`。但不同的是我们不需要按住它。例如我们可以为普通模式下的某个插件的功能或者命令添加如下快捷键：

```vim
nnoremap <Leader>j 2j
```

这样我们就可以先按 `Leader` 键，然后在按 `j` 来映射到 `2j` 上。 日常情况下我们会把安装的插件按照自己喜欢的组合方式配置快捷键，这个时候就会经常使用到 `Leader` 键。

`Leader` 键在默认的情况下是 `,`，即我们上面的设置的快捷键是 `,j` 映射到 `2j`。此外我们可以通过如下配置将 `Leader` 键修改为其他的按键，我的习惯是把 `Leader` 键设置为空格。

```vim
let g:mapleader = "\<Space>"
```

喜欢使用 Vim 的其中一个原因其实也跟快捷键有关，在 Vim 中我们可以相对自由的设置自己喜欢的快捷键，而不会像其他编辑器一样有诸多限制，并且容易跟现有的默认快捷键产生冲突。

### 宏

Vim 中提供了「宏」来方便进行一系列的操作，简单来说就是在开始前开启宏的录制，然后进行一顿操作后停止宏的录制。这样会把我们的操作都保存到寄存器中，执行宏的时候会从寄存器上取出来进行回放操作。

一般情况下我会通过 `qq` 来开启宏录制，把相关的操作录制到名为 `q` 的寄存器上（第一个 `q` 表示开始宏的录制，第二个 `q` 表示寄存器）。再按一次 `q` 将会停止宏的录制。

例如我们要给 10 行的文字添加相同的前缀和后缀，我们可以开始宏的录制后进行以下操作：`I`、`prefix`、`Esc`、`A`、`suffix`、`Esc`、`j`对第一行进行操作，然后按 `q` 停止宏的录制。最后我们通过 `@q` 来回放存放在寄存器 q 中的操作来对第二行生效。

![宏的录制和回放](https://ahonn-me.oss-cn-beijing.aliyuncs.com/images/89gI2Y.gif)

那么剩下的 8 行难道要按 8 次 `@q` 来进行回放吗？显然，宏跟命令一样都适用在前面加执行次数的规则，因此我们可以通过 `8@q` 来完成剩下的工作：

![多次回放宏](https://ahonn-me.oss-cn-beijing.aliyuncs.com/images/qwpvT1.gif)

这种通过录制和回放宏来执行重复机械式的操作非常有用，我经常会使用宏来处理枚举，JSON 或者对象的转换上。

宏作为 Vim 中的意大利炮非常的强大，这里只做了最基本的时候介绍，关于宏还有非常多的使用技巧，有机会的话再写另一篇文章进行介绍。

## 简单配置

目前到这里我们已经学会了如何使用 Vim 进行最基本的光标移动、输入、删除和快捷键映射等。但是对于一个什么配置都没有的 Vim 编辑器来说实在是太简陋了。因此我们需要对 Vim 进行简单的配置。

默认情况下，我们可以在 `~/.vimrc` 中添加我们自己的个性化配置（如果不存在这个文件需要自行创建）。

### 显示相对行号

```vim
set number
set relativenumber
```

通过 `set number` 可以显示当前光标所在行的行号，而 `set relativenumber` 将显示相对光标所在行的行数，方便我们执行类似 `10j`，`4dd` 之类对行进行的操作。

![当前行号与相对行号](https://ahonn-me.oss-cn-beijing.aliyuncs.com/images/TmK9Ua.png)

### 缩进设置

在普通模式下，我们可以通过 `>>` 或者 `<<` 来调整缩进，有点类似与普通的编辑器中的 `tab` 与 `shift + tab`。但每一次都按两下 `>` 来进行缩进显得非常的繁琐，因此我们可以添加如下快捷键映射：

```vim
nnoremap < <<
nnoremap > >>
```

这样我们就可以在普通模式下愉快的使用 `>` 和 `<` 缩进了！

说到缩进那么就免不了提到用空格还是用 Tab 了。理想的情况下我是不希望我一直按空格的，但是我又不希望使用 Tab 来进行缩进，所以我会添加如下配置：

```vim
set shiftwidth=2
set tabstop=2
set autoindent
set smarttab
set expandtab
```

这里的意思是我们使用 2 个空格来进行缩进，不管是在普通模式还是在插入模式中按 `>` 或者 `Tab` 进行缩进都使用空格。如果想了解 Vim 缩进设置推荐看这篇文章：[Vim 缩进有关的设置总结](https://www.kawabangga.com/posts/2817)

### 更好的光标跳转

如果你和我一样，觉得使用 `^` 或者 `$` 来跳转到行首和行尾很别扭的话，可以像我一样考虑添加相关的快捷键映射：

    noremap H ^
    noremap L $
    noremap J G
    noremap K gg

这里额外的添加了两条映射，目的是让我们大写的 `H/J/K/L` 更加符合直觉：我们可以通过 `J` 或者 `K` 来到达文件的开头和结尾，通过 `H` 和 `L` 来到达当前行的行首和行尾。简单来说，它就是光标移动的放大版。

## 在 VS Code 中使用

按照一般的套路，这里我们会接着讨论如何给 Vim 添加配置以及插件，使得 Vim 更加好用。但绝大多数的人在读了这篇文章之后也不会有换编辑器的想法，因此我们这里会聊聊如何在现有的编辑器中更好的使用 Vim 模式进行编辑，这里我们主要介绍如何在 VS Code 中使用。

在 VS Code 中使用 Vim 模式进行编辑可以通过两个插件来实现，分别是：

- [VSCodeVim/Vim](https://marketplace.visualstudio.com/items?itemName=vscodevim.vim)
- [asvetliakov/vscode-neovim](https://marketplace.visualstudio.com/items?itemName=asvetliakov.vscode-neovim)

### VSCodeVim/Vim

说到 VS Code 上的 Vim 插件就必须要提 VSCodeVim/Vim 了。该插件在 VS Code 中模拟了 Vim 中的模式切换以及基本的命令。但比较可惜的是我们不能复用前面所提到的 .vimrc 配置文件，我们需要在 `settings.json` 里通过 JSON 的方式来进行设置，添加快捷键等。

```json
{
  "vim.insertModeKeyBindings": [
    {
      "before": ["j", "j"],
      "after": ["<Esc>"]
    }
  ],
  "vim.normalModeKeyBindingsNonRecursive": [
    {
      "before": ["H"],
      "after": ["^"]
    },
    {
      "before": ["L"],
      "commands": ["$"]
    }
  ]
}
```

除此之外如果我们要通过快捷键来调用 VS Code 中的插件的话也是同样的需要在 `settings.json` 进行配置。

```json
{
  "vim.normalModeKeyBindings": [
    {
      "before": [":"],
      "commands": ["workbench.action.showCommands"]
    }
  ]
}
```

作为 Vim 用户的我是不喜欢这种方式的，我更加希望通过 .vimrc 来复用原先的配置，无缝的切换到 VS Code 中。而 VSCodeVim/Vim 需要重新写配置，并且配置的过程过于复杂，所以我很快就放弃了这个插件。

但如果是作为 VS Code 用户想在 VS Code 中慢慢开始使用 Vim 的编辑模式的话，不失为一个好的入门插件。

### asvetliakov/vscode-neovim

由于 VSCodeVim/Vim 插件配置比较繁琐，并且使用起来也稍微有点卡。我放弃 Vim 插件在 VS Code 中使用了一段时间，然后我发现了 vscode-neovim 这个插件。

vscode-neovim 插件集成了 neovim 与 VS Code，完美的满足了我的需求，它能够读取现有的 Vim 配置并且使用起来非常的顺滑。

只需要在 Vim 的配置中通过 `if !exists('g:vscode')` 将不需要的 Vim 插件剔除就可以直接使用了。与 neovim 集成的好处就是我们既可以使用部分 Vim 插件又可以使用 VS Code 插件。当然，这也提高了门槛，该插件依赖 neovim 0.5.0+ 以上的版本。对于刚入门 Vim 的同学来说安装的步骤过于复杂，这里就不向 Vim 新手推荐了。

熟悉 neovim 的同学感兴趣可以试试。或者查看我在 vscode-neovim 中[使用的 Vim 配置](https://github.com/ahonn/dotfiles/tree/master/vim/vscode)。

## 最后

虽然本文已经非常的长了，但是依然对于 Vim 中的快速分屏与切换以及其他非常有用的功能或者技巧没有进行介绍。这里强烈的建议感兴趣的小伙伴看 [简明 Vim 练级攻略](https://coolshell.cn/articles/5426.html) 或者 [Vim 实用技巧](https://book.douban.com/subject/25869486/) 这本书来进一步的了解。

如果是面向 VS Code 用户的话，本篇文章到这里就结束了。原本是打算继续写 Vim 中相关的一些好用的插件推荐的，但考虑到阅读本文的同学可能大部分对 Vim 比较陌生，因此就没有继续再写。如果你感兴趣的话欢迎留言，后面可以专门写一篇。

最后，不管看完文章的你是开始使用 Vim 编辑模式还是重新审视目前的输入习惯，希望大家都能够有所收获。

## 参考

- [Vim 实用技巧](https://book.douban.com/subject/25869486/)
- [简明 Vim 练级攻略| | 酷壳- CoolShell](https://coolshell.cn/articles/5426.html)
- [Vim Awesome](http://vimawesome.com/)
- [Vim documentation: index](http://vimdoc.sourceforge.net/htmldoc/vimindex.html)
- [Learn Vimscript the Hard Way](https://learnvimscriptthehardway.stevelosh.com/)
- [vim 的几种模式和按键映射](http://haoxiang.org/2011/09/vim-modes-and-mappin/)
- [Vim 缩进有关的设置总结](https://www.kawabangga.com/posts/2817)
