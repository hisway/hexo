title: Sublime Text
date: 2014-03-24 12:02:58
categories: 开发工具
tags: tool
---
##下载安装
<http://www.sublimetext.com>
##插件
- [Package Control](https://sublime.wbond.net)

可通过此插件来安装安装其他插件

安装方法：快捷键ctrl+` 或者 View > Show Console 菜单打开控制器

sublime text 3 复制以下安装

	import urllib.request,os,hashlib; h = '7183a2d3e96f11eeadd761d777e62404' + 'e330c659d4bb41d3bdf022e94cab3cd0'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)

 sublime text 2 复制以下安装

 	import urllib2,os,hashlib; h = '7183a2d3e96f11eeadd761d777e62404' + 'e330c659d4bb41d3bdf022e94cab3cd0'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); os.makedirs( ipp ) if not os.path.exists(ipp) else None; urllib2.install_opener( urllib2.build_opener( urllib2.ProxyHandler()) ); by = urllib2.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); open( os.path.join( ipp, pf), 'wb' ).write(by) if dh == h else None; print('Error validating download (got %s instead of %s), please try manual install' % (dh, h) if dh != h else 'Please restart Sublime Text to finish installation')


安装完成之后，我们摁下“shift + ctrl + p”呼出面板，输入cp选命令执行即可
<!--more-->
- Emmet

 Zen Coding 的升级版，由 Zen Coding 的原作者进行开发，Emmet 可以快速的编写 HTML 和 CSS 以及实现其他的功能。例子：
 
 #page>div.logo+ul#navigation>li*5>a{Item $}
 
在打开的 HTML 文件中输入以上，敲击一下 TAB 键，你就会发现这行指令变成了下面的 HTML 结构：

	<div id="page">
    	<div class="logo"></div>
    	<ul id="navigation">
        	<li><a href="">Item 1</a></li>
        	<li><a href="">Item 2</a></li>
        	<li><a href="">Item 3</a></li>
        	<li><a href="">Item 4</a></li>
        	<li><a href="">Item 5</a></li>
    	</ul>
	</div>

经常用到 html:xt 来快速生成html基础结构

	<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
	<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en">
	<head>
		<meta http-equiv="Content-Type" content="text/html;charset=UTF-8">
		<title>Document</title>
	</head>
	<body>
		
	</body>
	</html>

使用方法：<http://docs.emmet.io/cheat-sheet/>