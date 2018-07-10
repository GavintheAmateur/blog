---
layout: post
title: "Struts2 ValueStack取值顺序实验"
date:       2017-03-10
author:     "Gavin"
header-img: ""
categories:
	-Java
tags:
    - Struts2
    - ValueStack
---

今天学ValueStack取值时有点迷糊，于是写了如下测试：<br/>
Action类里的动作方法：
<pre><code>
public String execute() {
		ActionContext context = ActionContext.getContext();
		ValueStack vs = context.getValueStack();
		vs.push(new Teacher("AAAA",66));
		vs.push(new Teacher("BBBB",77));
		vs.push(new Teacher("CCCC",88));
		vs.push(new Teacher("DDDD",99));
		vs.push(new Student("A1",22));
		vs.push(new Student("A2",33));
		vs.push(new Student("A3",44));
		vs.push(new Student("A4",55));
		return SUCCESS;
	}
</code></pre>
JSP页面：

<pre><code> 
  	s:property value="[2].name"
</code></pre>
(为了markdown显示问题去掉了html，body，尖括号等，就留了这个struts标签内容)

这样当value="[2].name时，页面显示的是A2;当我将JSP页面的OGNL表达式改为`property value="[2].nickname"`时，输出变为了DDDD。

当value里时[2].name时页面是A2很好理解，因为ValueStack是一个栈，遵循先进后出的顺序，[2]对应的就是倒数第三个元素，也就是student A2。但是当改为[2].nickname之后为甚么是teacher DDDD（第5个元素）了呢？一开始我以为这是因为struts只在有nickname属性的元素（也就是teacher）中找，后来发现不对：要是这样，那应该是teacher BBBB啊。后来想通了：Struts是拿着这个[2]下标在栈中所有元素里找的，只是它数到第三个是发现是个student，没有nickname属性，于是接着往下数，直到数到第一个有nickname属性的元素，也就是teacher DDDD。为了验证我的想法，我保持nickname不变，将目录编号从0变到7，结果发现开始都显示的是DDDD,当编号改到5时开始显示CCCC，正常对应顺序了。假设成立。

<font color=red size=3>
总结：OGNL表达式中用索引编号取ValueStack中元素属性值时，如果Struts在指定编号位置找不到有对应属性的元素，将往下继续查询直到有这个属性的元素为止。另外注意Stack元素的顺序是先进后出，从后面数起。
</font>

*********************************
第一次发技术日志，有点小激动 (*^__^*)
