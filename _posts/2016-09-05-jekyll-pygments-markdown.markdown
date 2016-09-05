---
layout:     post
title:      "大巧不工--pygments的使用与配置"
subtitle:   "pygments-markdown"
date:       2016/9/5 16:46:46
author:     "roc"
header-img: "img/post-bg-js-module.jpg"
tags:
  - jekyll
---



## 前言

> 让工作更有效率

虽然有一些急于求成，但是依然咬牙把jekyll咬下来了，其实按部就班和匆忙上阵各有各的好处，看人
也看事，具体问题具体分析才能活的睿智从容。

## 正文

本文主要目的是记录今天的学习成果-[pygments](http://pygments.org/)Python实现的highlight
。有人可能就问了，一个高亮能学一天你也是够拼的。没错，我想说的是即使是有众多文献和强大的stackoverflow加持，也是学了一天。又有人问了，不是插件只讲使用么，为什么要学这么多？这个问题留给大家自己思考:)

首先确定了高亮需求后，在官网发现如下资源
> Code snippet highlightingPermalink

> Jekyll has built in support for syntax highlighting of over 60 languages thanks to Rouge. Rouge is the default highlighter in Jekyll 3 and above. To use it in Jekyll 2, set highlighter to rouge and ensure the rouge gem is installed properly.

> Alternatively, you can use Pygments to highlight your code snippets. To use Pygments, you must have Python installed on your system, have the pygments.rb gem installed and set highlighter to pygments in your site’s configuration file. Pygments supports over 100 languages

一段来自官网的例子：ruby的代码高亮

{ % highlight ruby % }

def foo

   puts 'foo'

end

{ % endhighlight % }

{% highlight ruby %}
def foo
  puts 'foo'
end
{% endhighlight %}

随即开始更新jekyll gem install jekyll(默认是3.3.1版本)，一连串惊天的阴谋就从这里开始了
：更新后语法不兼容
- && 首当其冲，&&要写成and
- \{\% 里面的 变量不能再写成\{\{\}\}形式，而是直接引用\%\}，不过还好中途有很多warning可以调试。

全部fix后，高亮的第一步就是修改config，highlight选项，jekyll其实是默认提供了highlight的，但是我比较喜欢monokai的风格，所以被迫折腾pygments，这也是本文的重点。

官网给出了明确说明，jekyll3自带rough可以使用，只要配置
```js
highlight:rough
```
既可，其实后面我就是在这么干的。
为了安装pygments首先还是应该安装python吧。python安装还好，最新版windows即可，pip貌似是一个包管理工具，但是目前没有深入研究，
```bash
pip install pygments
```
安装了pygments之后,就要记住一条命令

```bash
pygmentize -f html -a .highlight -S default > pygments.css
```
生成的css用文件引入就可以使用了。

然后就是解决配置里面的解析器，由于每次上传redcarpet都会导致GITHUB发邮件给我，神烦，于是乎我就改用了支持的highlight:true，和karmdown解析器

配置如下：

```yml
highlighter: rouge
markdown: kramdown
kramdown:
  input: GFM   
```

## 参考文献
1.[http://jekyll-windows.juthilo.com/3-syntax-highlighting/](http://jekyll-windows.juthilo.com/3-syntax-highlighting/)

2.[http://jerryzou.com/posts/usePygments/](http://jerryzou.com/posts/usePygments/)
