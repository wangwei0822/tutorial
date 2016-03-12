Markdown语法简要说明
==============================================

Here is an overview of the markdown syntax. Feel free to save this document and use it for reference later.

> You can always learn the syntax by pressing the "raw" button in the top right.  
> 你总是可以点击右上角"raw"按钮看原始代码来学习。
  
A few tricks to start with:

- Put a blank line in between to start a new paragraph
	- 空行是段落的分隔（*这里是二级项目列表*）
- If you want a line break, end your line with `two spaces` 
	- 如果你想换行，以***两个空格***来结束一行，这是实体引用&reg;

Paragraph
==========

One or more consecutive lines of text separated by one or more blank lines.
 
This is another paragraph.

And another!

Section Headings
================

There are two ways to do headers in Markdown.  

You can underline text to make the two top-level headers:

Header 1
========

Header 2
---------

The number of `=` or `-` signs doesn't matter; you can get away with just one.  But using enough to underline the text makes your titles look better in plain text.

You can also use hash marks for all six levels of HTML headers:

# Header 1 #
## Header 2 ##
### Header 3 ###
#### Header 4 ####
##### Header 5 #####
###### Header 6 ######
----
# 一级标题#
## 二级标题##
### 三级标题###
#### 四级标题（后面的#可以省略）
###### 六级标题######
----
The closing `#` characters are optional.  
  

Phrase Emphasis  
================


*This is italicized*, and so is _this_.  

**This is bold**, and so is __this__.

You can use ***italics and bold together*** if you ___have to___.



Horizontal Rules
================

You can insert a horizontal rule by putting three or more hyphens on a line by themselves:

---


Blockquotes
===========

Blockquotes are indented:

> The syntax is based on the way email programs
> usually do quotations. You don't need to hard-wrap
> the paragraphs in your blockquotes, but it looks much nicer if you do.  Depends how lazy you feel.
> Looks good!



Lists
=====

A bulleted list:

- You can use a minus sign for a bullet
+ Or plus sign
* Or an asterisk

A numbered list:

1. Numbered lists are easy
2. Markdown keeps track of the numbers for you
7. So this will be item 3.

Links
=====

Here's an inline link to [Google](http://www.google.com/).

这是[版本服务器的网址](http://git.gf.com.cn/)。

You can write bare URLs or email addresses by enclosing them in angle brackets:

> Markdown项目主页 <http://daringfireball.net/projects/markdown/>  
> 我的email地址: <frankxdwang@163.com>

这是到[本项目主页][1]的链接附注形式。

[1]: http://git.gf.com.cn/frank/git-tutorial/ "git-tutorial"


Images
======

图片引入演示，和制定外部链接类似:

![Valid XHTML](http://w3.org/Icons/valid-xhtml10)
![图片ALT信息](http://weibo.yunzhijie.com/scripture/images/joinus.gif)

The word in square brackets is the alt text, which gets displayed if the browser can't show the image.  Be sure to include meaningful alt text for blind users' screen-reader software.


Special sections (Notes, Tips, etc.)
===================================

To make a special section, indent four spaces:

    NOTE: This is some other cool stuff we can do with Markdown PRO! 
	       Of course, it can be a paragraph inside a note.
	       
    重要声明：这是很重要的
    
    function justForTest(url){
    	if(url && url.length > 0) {
    		console.log(url);
    	}
    	else return;
    	
    }


Use backticks to create a special formatted section inline. (The backtick key is in the upper left corner of most keyboards)

This is `really` expensive item, lots of `$`.  `重要提示，真的很重要`


表格演示
====================

	这样很好，一般这里用于贴程序代码！
	原来是这样啊，用Tab或四个空格开头即可！

或者是```这样？```

___TODO! TODO!___


* Outer pipes on tables are optional
* Colon used for alignment (right versus left)


&copy; 演示一下特殊字符的转义表示.