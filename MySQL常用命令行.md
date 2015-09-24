虽然有 MySQL-workbench 那样好用的图形化工具， 但基本的命令行技能还是必须要掌握的.
<!--more-->

说明：

sheng为我常用的username

123456为我的演示password

bookstore是演示的数据库名

books是演示的数据表名

----------

删除&amp;新建 数据库
-------------

最简单的就是删除和新建一个数据库．

**删除:**
<pre class="tab-convert:true lang:default decode:true ">shell&gt; mysql -usheng -p    #进入MySQL命令行模式
mysql&gt; DROP DATABASE bookstore;
</pre>
**新建:**
<pre class="tab-convert:true lang:default decode:true ">shell&gt; mysql -usheng -p    #进入MySQL命令行模式
mysql&gt; CREATE DATABASE bookstore DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
</pre>
备份&amp;还原 数据库
-------------

备份十分简单，使用mysqldump命令，还原的话需要保证数据库存在．

**备份:**
<pre class="lang:default decode:true ">shell&gt;  mysqldump -usheng -p bookstore &gt; bookstore.sql
</pre>
**还原:**
<pre class="lang:default decode:true">shell&gt;  mysql -usheng -p bookstore &lt; bookstore.sql
</pre>
如果提示locktable错误：则mysqldump 加上 --skip-lock-tables 选项

新建用户和授权
-------------

在下面的命令中 username(sheng/root)和host(localhost/ip-address)可以用(%)来通配, db(bookstore)和table(books)可以用(*)来通配.

**新建:**
<pre class="tab-convert:true lang:default decode:true ">shell&gt; mysql -usheng -p    #进入MySQL命令行模式
mysql&gt; CREATE USER sheng@localhost IDENTIFIED BY 123456;
</pre>
**授权:**
<pre class="tab-convert:true lang:default decode:true ">shell&gt; mysql -uroot -p    #进入MySQL命令行模式
mysql&gt; GRANT ALL PRIVILEGES ON bookstore.books TO sheng@localhost IDENTIFIED BY 123456 WITH GRANT OPTION;
</pre>
本文由 **Christian Sheng** 写于 **2015-09-13**。转载请注明出处: <a href="http://www.christiansheng.com" target="_blank">**希恩印象** www.christiansheng.com</a>。
