EDM是Email Direct Marketing的缩写，又称运营邮件，并不是页面重构师都做过，虽然也只是个简单的HTML，但其中却包含着很多让人无可奈何的地方，因为桌面和移动端渲染电子邮件大约有很多种不同的组合方式！

HTML邮件内容虽然也是HTML，但是事与愿违，因为安全原因，各大邮箱服务商及邮件客户端都会对邮件内容进行一定程度上的处理，所以展示的效果和你平时写的可能不一样。

特别是Outlook，它支持的标签和属性少得可怜，所以只要兼容了OutLook，其他邮箱客户端基本都不会有什么问题。如果你的工作中有需要制作运营邮件，下面的建议将非常有用。

## 什么是运营邮件？
是指承载推广信息投递到邮箱的邮件，显示在邮箱中的页面，受到邮箱环境影响，在视觉、代码和兼容性都会受到限制。   

![image](http://cimg1.fenqile.com/ibanner/M00/00/B9/wicJAFju-AeACeJSAAAeE0Me2o0616.png)
## 运营邮件的阅读环境

环境 | 软件
---|---
智能手机 | 系统自带邮箱、QQ邮箱、网易邮箱大师、Inbox Email、...
电脑PC | Foxmail、Outlook、网易邮箱大师、网易邮箱大师、WPS邮箱、139邮箱、Gmail、Inbox Email、...

## 运营邮件的限制
出于安全问题，邮件页面禁止嵌入flash文件、不支持任何动态程序、不支持JS等 交互代码、不支持读取外部页面iframe标签； 不支持内外部样式表（只支持内联样式）；否则会引起意外的错误，例如文字乱码等；

## 运营邮件设计标准
![image](http://cimg1.fenqile.com/ibanner/M00/00/B8/wycJAFjvHE6AM_ITAAF0KUzOncs661.png)

注意项 | 说明
---|---
邮件尺寸 | 宽度720像素，高度根据内容适应
邮件标志 | 左上角区域放置公司logo
设计区域 | 设计师自由发挥
版本信息区域| 版权信息及一些其他公用信息

## 运营邮件重构制作基本规则

#### 1、HTML<!DOCTYPE>声明
删除我们平时写HTM页面的第一段代码说明：<!DOCTYPE html>
，邮件以<html>开始，以</html>为结尾

#### 2、编码
邮件的必须指定一种字符编码，否则会造成乱码；

```
<meta http-equiv="Content-Type" content="text/html;charset=gb2312" />
```
#### 3、布局使用 table
老式的table布局是最好的选择。这就意味着HTML邮件中几乎只有这几个元素：table、 tr 、td、 span、img、a 。

而且并不是所有邮箱都支持 colspan、rowspan 属性，所以所有布局都需要使用 table 嵌套解决。

使用表格布局导致的最直接的问题就是会产生多余的空白像素，所以要养成习惯给每个 table 都加上边框 border ，单元格内边距 cellpadding ，单元格间距 cellspacing ，边框合并属性 border-collapse 这些属性：


```
<table border="0" cellpadding="0" cellspacing="0" style="border-collapse: collapse;">
    
</table>
```

#### 4、使用内联样式
与普通 HTML 页面开发一样，HTML 邮件依旧离不开 CSS，HTML 邮件并不支持外部的 style 文件，head 标签有可能被删除，所以不要在 head 标签内写 style 标签。

那么在 body 内写 style 标签是不是就保险了呢？然并卵！典型的就是 Gmail 邮箱，会把 HTML 邮件内所有 style 标签删除，这就意味着只有內联样式是可靠的样式信息。

#### 5、能用属性就不要用样式
比如在 OutLook 中，图片使用样式来设置宽高是无效的：

```
<img style="width: 60px; height: 60px;" alt="说明" src="*.png" />
```
正确的写法：
```
<img width="60px" height="60px" alt="说明" src="*.png" />
```
常用的属性有：

```
width
height
bgcolor
align
valign
```


#### 6、所有样式单独指定
在HTML邮件中，继承规则依旧有效，但是大部分邮件都无法完整继承样式，邮箱的默认样式也会对邮件产生一些影响,因此每个标签单独指定样式是必须的，尽可能不要依赖继承，即使它十分地繁琐。

#### 7、背景图片
style 内容里面 background 可以设置 color ，但是 image 会被过滤，但是有一个元素属性，也叫 background ，里面可以定义一个图片路径。

```
<td background="*.png">
    
</td>
```

#### 8、字体
在 HTML 邮件中， font-family 只支持系统字体，不支持自定义字体，也不支持 font 简写， color 尽可能也不要使用简写：

```
font: 12px / 16px “微软雅黑”, Arial, sans-serif; 
color: #eee;
```
正确的写法：

```
font-size: 12px; 
line-height: 16px; 
font-family: “微软雅黑”,Arial, sans-serif; 
color: #eeeeee;
```

#### 9、图片和Alt属性
图片一定要指定高度和宽度，width 和 height 属性一定要加上单位！

在有些邮箱里，图片不是默认加载的，往往加载前需要用户的许可。那么高宽的指定可以使邮件在没有图片撑出样子前也能保持良好的大小结构，加上 alt 属性可以提示图片的内容让用户选择是否下载它们。
