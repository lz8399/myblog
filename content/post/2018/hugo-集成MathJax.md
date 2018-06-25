+++
title= "hugo-集成MathJax"
date= "2018-06-22T00:51:40+08:00"
categories= ["Web"]
tags= ["Hugo", "Blog", "集成MathJax"]
mathjax= ["ture"]
+++

keywords：hugo、MathJax、公式、数学表达式

##### 步骤

1，在theme\layouts\partials\目录下新建一个文件，命名为 `mathjax_support.html`，内容为：

	<script type="text/javascript" async
	  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.4/MathJax.js?config=TeX-MML-AM_CHTML">
	</script>
	<script type="text/x-mathjax-config">
	MathJax.Hub.Config({
	  tex2jax: {
		inlineMath: [['$','$'], ['\\(','\\)']],
		displayMath: [['$$','$$'], ['\[','\]']],
		processEscapes: true,
		processEnvironments: true,
		skipTags: ['script', 'noscript', 'style', 'textarea', 'pre','code'],
		TeX: { equationNumbers: { autoNumber: "AMS" },
			 extensions: ["AMSmath.js", "AMSsymbols.js"] }
	  }
	});
	</script>
	
2，在`header.html`的\</header>之前或者`footer.html`的\</footer>之前添加：

	{{ if .Params.mathjax}}{{ partial "mathjax_support.html" . }}{{ end }}
	
3，在MD文件的头部追加`mathjax : ture`：

	---
	title : "hugo-集成MathJax"
	date : "2018-06-22T00:51:40+08:00"
	mathjax : ture
	---
	
如果是新语法，则追加`mathjax= ["ture"]`：

	+++
	title= "hugo-集成MathJax"
	date= "2018-06-22T00:51:40+08:00"
	mathjax= ["ture"]
	+++

##### 测试

格式：

	$ 公式表达式 $
	
或者

	$$ 
	公式表达式 
	$$
	
前者靠左显示，后者居中显示


示例：

	$\sqrt{3x-1}+(1+x)^2$
	
$\sqrt{3x-1}+(1+x)^2$
	

	$$
	\sqrt{3x-1}+(1+x)^2
	$$

$$
\sqrt{3x-1}+(1+x)^2
$$
	
	
***
`对的那条路，往往不是最好走的。`