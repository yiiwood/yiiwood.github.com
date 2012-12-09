---
layout: post
title: "Octopress Blog 配置"
date: 2012-10-01 19:32
comments: true
categories: [ Octopress ]
---
##一、本地环境配置##
1、安装[Git](http://code.google.com/p/msysgit/downloads/list)。

2、安装[Ruby](http://rubyforge.org/frs/download.php/75127/rubyinstaller-1.9.2-p290.exe)，加入环境变量。

3、安装[Devkit](https://github.com/downloads/oneclick/rubyinstaller/DevKit-tdm-32-4.5.2-20111229-1559-sfx.exe)，首先解压，然后用如下CMD命令安装：

{% codeblock %}
cd DevKit
ruby dk.rb init
ruby dk.rb install
{% endcodeblock %}

4、安装[python](http://www.activestate.com/activepython/downloads)。

5、下载Octopress，执行下面的git命令：

{% codeblock %}
git clone git://github.com/imathis/octopress.git  octopress
{% endcodeblock %}

6、加入中文UTF-8编码支持，Windows环境变量配置如下：

{% codeblock %}
LANG=zh_CN.UTF-8
LC_ALL=zh_CN.UTF-8
{% endcodeblock %}

7、更新源，执行如下CMD命令：

{% codeblock %}
gem sources -a http://ruby.taobao.org/
gem sources -r http://rubygems.org/
{% endcodeblock %}

8、安装Octopress，执行CMD命令：

{% codeblock %}
cd octopress
gem install bundler
bundle install
{% endcodeblock %}

<!-- more -->

##二、建立Github项目##

登录[Github](https://github.com/)，新建一个命名为 username.github.com 的Repo。

##三、发布Octopress到Github##

1、执行CMD命令，按照提示输入Repo地址（git@github.com:username/username.github.com）：

{% codeblock %}
cd octopress
rake setup_github_pages
{% endcodeblock %}

2、发布，git命令（#号后面是注释）：

{% codeblock %}
rake install      #安装主题
rake generate     #生成静态页面
rake preview      #本地预览
rake deploy       #发布到Github
{% endcodeblock %}

本地预览地址[http://localhost:4000/](http://localhost:4000/)。

3、源文件发布到source分支下面，git命令：

{% codeblock %}
git add .
git commit -m “your message”
git push origin source
{% endcodeblock %}

4、更新博客后，执行`rake generate`、`rake deploy` 。

##四、一些Markdown语法##

1、代码块

（1）在每行代码前面空Tab键：

{% codeblock %}
/*每行前空Tab*/
	int main()
	{
		int i;
		i = 0;
		return 0;
	}
{% endcodeblock %}

效果：

	int main()
	{
		int i;
		i = 0;
		return 0;
	}

（2）用codeblock和endcodeblock作为代码块的开头和结尾，效果：

{% codeblock %}
int main()
{
	printf("Hello World\n");
}
{% endcodeblock %}

2、引用块

代码：

{% codeblock %}
> This is the first level of quoting.
>
> > This is nested blockquote
>
> Back to the first level.
{% endcodeblock %}

效果：

> This is the first level of quoting.
>
> > This is nested blockquote
>
> Back to the first level.

##五、加入Latex支持##

1、首先安装`kramdown`包：

{% codeblock %}
gem install kramdown
{% endcodeblock %}

再把下面的代码添加到`source/_includes/custom/head.html`文件中:

{% gist 3938526   head_add.html %}

修改`_config.yml`

{% codeblock %}
markdown: kramdown  #rdiscount
{% endcodeblock %}

2、例子

插入代码：

{% codeblock %}
$$
\begin{align*}
  & \phi(x,y) = \phi \left(\sum_{i=1}^n x_ie_i, \sum_{j=1}^n y_je_j \right)
  = \sum_{i=1}^n \sum_{j=1}^n x_i y_j \phi(e_i, e_j) = \\
  & (x_1, \ldots, x_n) \left( \begin{array}{ccc}
      \phi(e_1, e_1) & \cdots & \phi(e_1, e_n) \\
      \vdots & \ddots & \vdots \\
      \phi(e_n, e_1) & \cdots & \phi(e_n, e_n)
    \end{array} \right)
  \left( \begin{array}{c}
      y_1 \\
      \vdots \\
      y_n
    \end{array} \right)
\end{align*}
$$
{% endcodeblock %}

效果：

$$
\begin{align*}
  & \phi(x,y) = \phi \left(\sum_{i=1}^n x_ie_i, \sum_{j=1}^n y_je_j \right)
  = \sum_{i=1}^n \sum_{j=1}^n x_i y_j \phi(e_i, e_j) = \\
  & (x_1, \ldots, x_n) \left( \begin{array}{ccc}
      \phi(e_1, e_1) & \cdots & \phi(e_1, e_n) \\
      \vdots & \ddots & \vdots \\
      \phi(e_n, e_1) & \cdots & \phi(e_n, e_n)
    \end{array} \right)
  \left( \begin{array}{c}
      y_1 \\
      \vdots \\
      y_n
    \end{array} \right)
\end{align*}
$$

单行代码：`$\exp(-\frac{x^2}{2})$`，效果：$\exp(-\frac{x^2}{2})$




