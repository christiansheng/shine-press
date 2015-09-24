1、设置git的user name和email
如果是第一次在本机上使用git的话，需要设置git user的name和email
<!--more-->


 
<pre class="lang:zsh decode:true " >
shell&gt; git config --global user.name  "Christian Sheng"
shell&gt; git config --global user.email "christian.leo.sheng@gmail.com"
</pre> 

注：不喜欢 --global 选项的话可以用 --local

2、生成密钥
 
<pre class="lang:zsh decode:true " >
# run below command to get id_rsa and id_rsa.pu
shell&gt; ssh-keygen -t rsa -C "christian.leo.sheng@gmail.com"
</pre> 



3、添加密钥到ssh-agent

ssh-agent是一种控制用来保存公钥身份验证所使用的私钥的程序， 可以看成是一个密钥管理器，
运行ssh-agent以后，使用ssh-add将私钥交给ssh-agent保管，其他程序需要身份验证的时候可以
将验证申请交给ssh-agent来完成整个认证过程。

 
<pre class="lang:zsh decode:true " >
# start the ssh-agent in the background
shell&gt; eval "$(ssh-agent -s)"

# add new generated SSH key to ssh-agent。
shell&gt; ssh-add ~/.ssh/id_rsa
</pre> 


4、登陆Git服务器添加 ssh 
登陆Git服务器(如github, gitlab等) 把id_rsa.pub文件里的内容复制进去

本文由 **Christian Sheng** 写于 **2014-07-29**。转载请注明出处: <a href="http://www.christiansheng.com" target="_blank">**希恩印象** www.christiansheng.com</a>。
