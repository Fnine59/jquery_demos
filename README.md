# jquery_demos
> 一些实用的html常用案例，全部基于jQuery框架

# 目录

* [checkall.html](#checkall)
* [dialog.html](#dialog)
* [menus.html](#menus)


<div id="checkall"></div>

## checkall.html

> checkall.html实现了一个简单的列表全选功能

项目功能：点击添加按钮可以添加新的行，新行内容是写死的。选择某几行点击删除按钮可以删除该行。

实现思路：
全选按钮应该考虑这样几个方面：
1. 添加新行的时候，该行的选中状态应该跟着全选按钮当前的状态走，如果此时全选按钮勾选了，则新添加的行也应当是被勾选的，因此在添加新行的时候要执行一个判断；
2. 考虑全选按钮控制下方所有按钮，全选按钮勾选则下方所有按钮勾选，全选按钮取消则下方所有按钮取消，因此可考虑代码为点击全选按钮的时候将全选按钮的checked属性值赋予下方所有按钮；
3. 考虑下方所有按钮整体控制全选按钮，即，如果下方所有按钮全部选中，则全选按钮选中；如果下方有一个按钮没有选中，则全选按钮不被选中。因此可以检测所有`index`值大于`0`的`checkbox`的点击事件（记得使用`on`函数因为文档中含有动态产生的控件），检测到了点击事件之后可以设立一个`flag`标志，此时使用`each`对选中的每一个`checkbox`进行循环判断，只要有一个`checkbox`没有被选中就改变`flag`的值为`false`，最终将这个值赋给全选按钮的`checked`属性。
4. 考虑删除按钮，删除按钮只要使用`:checked`选择器选择被选中的多选框，并找到这些多选框的祖先元素中的`tr`元素，并删除即可。

优化思路： 添加的新行应当由用户来手动填写；多选框以及按钮的样式可以进一步优化；

<div id="dialog"></div>

## dialog.html

> dialog.html简单的实现了一个带有遮罩层的弹出框

实现思路：
遮罩层使用一个`position`属性值为`fixed`的占满页面的div，并且为该div指定了无法选中的样式，保证了在不能穿透div点击的基础上，也能够控制该层div之下的文本不会被选中。其中对话框的div指定了`position`为`fixed`，这代表就算页面具有滚动条，该对话框也不会跟随页面滚动，如果需要对话框跟随页面滚动个的话将`position`的值改为`absolute`即可。

优化思路：可以对样式进行细致的优化，并最终抽象成为一个插件，该插件应当由用户提供的数据有：对话框标题文本，对话框内容（可能为一段html代码），对话框按钮个数（1-2个）及文本等。并且要灵活的控制对话框的位置。

<div id="menus"></div>

## menus.html

> menus.html实现了一个简单的风琴菜单效果

实现思路：主要使用了jQuery中的`slideToggle`函数，点击某一个父菜单项时对它之下的子菜单项使用`slideToggle`函数，对其他的子菜单项使用`slideUp`函数，这样保证了其他显示的子菜单被收回，而其他没有显示的子菜单则不发生任何变化。