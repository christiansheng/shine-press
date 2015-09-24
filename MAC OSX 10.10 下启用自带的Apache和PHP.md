Mac 系统自带Apache和PHP，只要你开启即可使用
<!--more-->

1. 修改Apache配置文件
--------
sudo vim /etc/apache2/httpd.conf。

取消注释掉下面两行
<pre class="lang:default decode:true ">LoadModule rewrite_module libexec/apache2/mod_rewrite.so
LoadModule php5_module libexec/apache2/libphp5.so
</pre>
注释掉221行的#Require all denied
<pre class="nums:false lang:default decode:true ">212 #ServerName www.example.com:80
213
214 #
215 # Deny access to the entirety of your server's filesystem. You must
216 # explicitly permit access to web content directories in other
217 # &lt;Directory&gt; blocks below.
218 #
219 &lt;Directory /&gt;
220     AllowOverride none
221 #    Require all denied
222 &lt;/Directory&gt;
</pre>
另外取消499行的注释，使apache的vhost设置生效
<pre class="nums:false lang:default decode:true ">498 # Virtual hosts
499 Include /private/etc/apache2/extra/httpd-vhosts.conf
500
501 # Local access to the Apache HTTP Server Manual
502 #Include /private/etc/apache2/extra/httpd-manual.conf</pre>
2. 添加虚拟域名
--------
vim /etc/apache2/extra/httpd-vhosts.conf
添加如下内容（sheng 是我的用户名，christiansheng.com 是自己添加的虚拟域名）
<pre class="lang:default decode:true ">&lt;VirtualHost *:80&gt;
      DocumentRoot "/Users/sheng/site/christiansheng.com"
      ServerName christiansheng.com
      &lt;Directory "/Users/sheng/site/christiansheng.com"&gt;
          Options FollowSymLinks
          AllowOverride All
          Require all granted
      &lt;/Directory&gt;
&lt;/VirtualHost&gt;
</pre>
重启apeche使修改生效
<pre class="lang:zsh decode:true ">sudo apachectl start
</pre>
3. 修改本机的host设置
--------
vim /etc/hosts
添加一行
<pre class="lang:default decode:true ">127.0.0.1   christiansheng.com
</pre>
4. 测试
--------
在/Users/sheng/site/christiansheng.com/ 新建一个index.php 文件

可以写入如下内容。(MAC OSX 10.10的PHP 版本在5.4以上，不知道为什么短标签默认不能用)
<pre class="lang:php decode:true ">&lt;?php
    echo "hello php";
?&gt;</pre>
打开浏览器
输入 christiansheng.com
如果出现 hello php，表明OK
Have fun!

本文由 **Christian Sheng** 写于 **2015-07-21**。转载请注明出处: <a href="http://www.christiansheng.com" target="_blank">**希恩印象** www.christiansheng.com</a>。
