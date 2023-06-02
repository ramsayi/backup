---
title: Hexo中文实现打字机效果
copyright: false
tags:
  - Hexo
  - 博客
categories:
  - 建站博客
abbrlink: 70c2fc3d
date: 2021-08-22 20:37:26
---

花里胡哨的打字机效果

## 简单版本

效果如下：

<script src="https://cdn.jsdelivr.net/gh/Justlovesmile/CDN/js/typed.js"></script>

<strong id="typedjs1"></strong>

<script>
var typed = new Typed("#typedjs1", {
  strings: ['满堂花醉三千客，一剑霜寒十四州。'],
  startDelay: 0,
  typeSpeed: 200,
  backSpeed: 100,
  loop: true,
  showCursor: true,
  shuffle: false
});
</script>


```html
<script src="https://cdn.jsdelivr.net/gh/Justlovesmile/CDN/js/typed.js"></script>

<strong id="typedjs1"></strong>

<script>
var typed = new Typed("#typedjs1", {
  strings: ['醒亦念卿，梦亦念卿','频繁记录，只因生活和你太值得❤'],
  startDelay: 0,
  typeSpeed: 200,
  backSpeed: 100,
  loop: true,
  showCursor: true,
  shuffle: false
});
</script>
```

## 花里胡哨的版本：

效果如下：

<p><strong id="colortap1"></strong></p>
<script>
var colortap = function (r) {
	function t() {return b[Math.floor(Math.random() * b.length)]}  
	function e() {return String.fromCharCode(94 * Math.random() + 33)}
	function n(r) {
		for(var n=document.createDocumentFragment(),i=0;r>i;i++){
			var l=document.createElement("span");
			l.textContent=e(),l.style.color=t(),n.appendChild(l)
		}
		return n;
	}
	function i() {
		var t = o[c.skillI];
		c.step ? c.step-- : (c.step = g, c.prefixP < l.length ? (c.prefixP >= 0 && (c.text += l[c.prefixP]), c.prefixP++) : "forward" === c.direction ? c.skillP < t.length ? (c.text += t[c.skillP], c.skillP++) : c.delay ? c.delay-- : (c.direction = "backward", c.delay = a) : c.skillP > 0 ? (c.text = c.text.slice(0, -1), c.skillP--) : (c.skillI = (c.skillI + 1) % o.length, c.direction = "forward")), 
		r.textContent = c.text,
		r.appendChild(n(c.prefixP < l.length ? Math.min(s, s + c.prefixP) : Math.min(s, t.length - c.skillP))),
		setTimeout(i, d)
	}
	var l = "",
	o = ["醒亦念卿，梦亦念卿","频繁记录，只因生活和你太值得","孜孜不倦，认真且怂"].map(function (r) {return r + ""}),
	a = 2,g = 1,s = 5,d = 75,
	b = ["rgb(110,64,170)", "rgb(150,61,179)", "rgb(191,60,175)", "rgb(228,65,157)", "rgb(254,75,131)", "rgb(255,94,99)", "rgb(255,120,71)", "rgb(251,150,51)", "rgb(226,183,47)", "rgb(198,214,60)", "rgb(175,240,91)", "rgb(127,246,88)", "rgb(82,246,103)", "rgb(48,239,130)", "rgb(29,223,163)", "rgb(26,199,194)", "rgb(35,171,216)", "rgb(54,140,225)", "rgb(76,110,219)", "rgb(96,84,200)"],
	c = {text: "",prefixP: -s,skillI: 0,skillP: 0,direction: "forward",delay: a,step: g};i()
};
colortap(document.getElementById('colortap1'));
</script>

```html
<p><strong id="colortap1"></strong></p>
<script>
var colortap = function (r) {
	function t() {return b[Math.floor(Math.random() * b.length)]}  
	function e() {return String.fromCharCode(94 * Math.random() + 33)}
	function n(r) {
		for(var n=document.createDocumentFragment(),i=0;r>i;i++){
			var l=document.createElement("span");
			l.textContent=e(),l.style.color=t(),n.appendChild(l)
		}
		return n;
	}
	function i() {
		var t = o[c.skillI];
		c.step ? c.step-- : (c.step = g, c.prefixP < l.length ? (c.prefixP >= 0 && (c.text += l[c.prefixP]), c.prefixP++) : "forward" === c.direction ? c.skillP < t.length ? (c.text += t[c.skillP], c.skillP++) : c.delay ? c.delay-- : (c.direction = "backward", c.delay = a) : c.skillP > 0 ? (c.text = c.text.slice(0, -1), c.skillP--) : (c.skillI = (c.skillI + 1) % o.length, c.direction = "forward")), 
		r.textContent = c.text,
		r.appendChild(n(c.prefixP < l.length ? Math.min(s, s + c.prefixP) : Math.min(s, t.length - c.skillP))),
		setTimeout(i, d)
	}
	var l = "",
	o = ["醒亦念卿，梦亦念卿","频繁记录，只因生活和你太值得","孜孜不倦，认真且怂"].map(function (r) {return r + ""}),
	a = 2,g = 1,s = 5,d = 75,
	b = ["rgb(110,64,170)", "rgb(150,61,179)", "rgb(191,60,175)", "rgb(228,65,157)", "rgb(254,75,131)", "rgb(255,94,99)", "rgb(255,120,71)", "rgb(251,150,51)", "rgb(226,183,47)", "rgb(198,214,60)", "rgb(175,240,91)", "rgb(127,246,88)", "rgb(82,246,103)", "rgb(48,239,130)", "rgb(29,223,163)", "rgb(26,199,194)", "rgb(35,171,216)", "rgb(54,140,225)", "rgb(76,110,219)", "rgb(96,84,200)"],
	c = {text: "",prefixP: -s,skillI: 0,skillP: 0,direction: "forward",delay: a,step: g};i()
};
colortap(document.getElementById('colortap1'));
</script>
```

> 作者: Justlovesmile
> 链接: https://blog.justlovesmile.top/posts/7e7ef81c.html
> 来源: Justlovesmile's BLOG
> 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
