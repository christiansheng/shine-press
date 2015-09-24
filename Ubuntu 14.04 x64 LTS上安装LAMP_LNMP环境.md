LAMP on Ubuntu.14.04
--------
<pre class="lang:zsh decode:true ">sudo  apt-get update

sudo apt-get  install apache2

sudo apt-get install php5

sudo apt-get install mysql-server-5.6 # default is 5.5

sudo apt-get install php5-mysql

sudo apt-get install php5-gd curl libcurl3 libcurl3-dev php5-curl

sudo apt-get install php-pear  php5-dev 

sudo apt-get install libpcre3 libpcre3-dev

sudo apt-get install libapache2-mod-php5 php5-mcrypt php5-memcache  php5-xdebug php-apc

sudo pecl install mongo oauth

sudo service mysql restart

sudo service apache2 restart
</pre>
LNMP on Ubuntu.14.04
-------- 
<pre class="lang:zsh decode:true " >
sudo apt-get install mysql-server mysql-client 

sudo apt-get install nginx

sudo apt-get install php5-fpm

sudo apt-get install php5-mysql php5-curl php5-gd php5-intl 

sudo apt-get install php-pear php5-imagick php5-imap php5-mcrypt php5-memcache php5-ming php5-ps php5-pspell php5-recode php5-snmp php5-sqlite php5-tidy php5-xmlrpc php5-xsl php5-xcache

sudo apt-get install libmcrypt-dev mcrypt php5-dev memcached

sudo service php5-fpm restart

sudo service nginx restart
</pre> 

配置Nginx
Nginx的配置文件默认在/etc/nginx/nginx.conf，下面是在此配置文件上的修改部分。
在nginx.conf中默认包含/etc/nginx/sites-enabled/下面的default文件，你可以在该配置文件中修改，
或者如果是虚机的话，也可以在该文件夹下创建一个配置文件，加入下面的配置信息。
 
<pre class="lang:yaml decode:true " >
server {
        listen 80 default_server;
        listen [::]:80 default_server ipv6only=on;

        root /usr/share/nginx/html;
        index index.html index.htm index.php;

        # Make site accessible from http://localhost/
        server_name localhost;

        location / {
                # First attempt to serve request as file, then
                # as directory, then fall back to displaying a 404.
                try_files $uri $uri/ =404;
                # Uncomment to enable naxsi on this location
                # include /etc/nginx/naxsi.rules
        }

        location ~ \.php$ {
                fastcgi_split_path_info ^(.+\.php)(/.+)$;
                # NOTE: You should have "cgi.fix_pathinfo = 0;" in php.ini
        
        #       # With php5-cgi alone:
        #       fastcgi_pass 127.0.0.1:9000;
        #       # With php5-fpm:
                fastcgi_pass unix:/var/run/php5-fpm.sock;
                fastcgi_index index.php;
                include fastcgi_params;
        } 
}
</pre> 

