安装
############

CakePHP的安装简单有快捷.
最小的依赖就是一个web服务器和一份Cake的拷贝, 就这么多!
虽然本手册主要针对如何在Apache(因为它很常用)上配置Cake,但你也可以把Cake配置在大部分web服务器上运行, 例如LightHTTPD 或者 微软 IIS.

需求
============

-  HTTP服务器. 例如: Apache. 推荐打开mod\_rewrite, 但不是必须.
-  PHP 5.2.8 或更高.

从技术角度来讲数据引擎不是必须的, 但是我们可以想到大部分应用都会用到. CakePHP 支持多种数据存储引擎:

-  MySQL (4 或更高)
-  PostgreSQL
-  Microsoft SQL Server
-  SQLite

.. note::

    内建数据引擎驱动需要 PDO. 需要确保相应的 PDO 扩展已经安装并可用.

协议
=======

CakePHP在MIT协议下发布. 这意味着你可以在保留完整的版权协议下自由修改,分发,重新发布源代码. 
你也可以自由把CakePHP整合到商业软件或者闭源软件中.

下载CakePHP
===================

有两种主要方式来获取一份最新的CakePHP.
你可以从CakePHP主站上下载存档版本(zip/tar.gz/tar.bz2), 或者从git源中取出一份.

要下载CakePHP的最新主要发布版.
访问 `http://cakephp.org <http://cakephp.org>`_ 然后点击 "Download Now" 链接.

所有CakePHP的当前发布版本也托管在 `Github <http://github.com/cakephp/cakephp>`_.
Github 托管着CakePHP本身和许多CakePHP的插件.
CakePHP 的可用版本可以在
`Github tags <https://github.com/cakephp/cakephp/tags>`_ 找到.

你也可以获取最新的代码, 这些代码包含了最新的缺陷修复和最新的改进.
通过从github克隆的方式来获取
`Github`_ repository::

    git clone git://github.com/cakephp/cakephp.git


权限
===========

CakePHP 使用 ``app/tmp`` 目录来做很多操作. 例如:模型描述, 缓存的视图, 会话信息.
因此, 请保证cake 安装下的 ``app/tmp`` 目录以及其子目录对运行web服务器的用户可写.

设置
=====

安装 CakePHP 可以简单的直接将其放到服务器的文档根目录下, 或者按照你需要的方式灵活的配置.
这里会将阐述三种CakePHP的主要安装方式: development, production, 和 advanced.

-  Development: 简单配置, URL 可能会包含CakePHP的安装目录名, 安全性略低.
-  Production: 需要能配置web服务器的根目录, URL清晰, 非常安全.
-  Advanced: 通过一些配置, 可以让你将CakePHP的目录分别放置到文件系统的不同位置, 也可以让很多CakePHP应用共享一个CakePHP核心库目录.

开发
===========

A development installation is the fastest method to setup Cake.
This example will help you install a CakePHP application and make
it available at http://www.example.com/cake\_2\_0/. We assume for
the purposes of this example that your document root is set to
``/var/www/html``.

Unpack the contents of the Cake archive into ``/var/www/html``. You now
have a folder in your document root named after the release you've
downloaded (e.g. cake\_2.0.0). Rename this folder to cake\_2\_0.
Your development setup will look like this on the file system::

    /var/www/html/
        cake_2_0/
            app/
            lib/
            plugins/
            vendors/
            .htaccess
            index.php
            README

If your web server is configured correctly, you should now find
your Cake application accessible at
http://www.example.com/cake\_2\_0/.

Using one CakePHP checkout for multiple applications
----------------------------------------------------

If you are developing a number of applications, it often makes sense to have
them share the same CakePHP core checkout. There are a few ways in which you can
accomplish this.  Often the easiest is to use PHP's ``include_path``. To start
off, clone CakePHP into a directory.  For this example, we'll use
``~/projects``::

    git clone git://github.com/cakephp/cakephp.git ~/projects/cakephp

This will clone CakePHP into your ``~/projects`` directory.  If you don't want
to use git, you can download a zipball and the remaining steps will be the
same.  Next you'll have to locate and modify your ``php.ini``.  On \*nix systems
this is often in ``/etc/php.ini``, but using ``php -i`` and looking for 'Loaded
Configuration File'.  Once you've found the correct ini file, modify the
``include_path`` configuration to include ``~/projects/cakephp/lib``.  An
example would look like::

    include_path = .:/home/mark/projects/cakephp/lib:/usr/local/php/lib/php

After restarting your webserver, you should see the changes reflected in
``phpinfo()``.

.. note::

    如果使用的Windows, 需要用 : 代替 ; 做include路径分割符

当你配置好 ``include_path`` 后, 你的应用现在可以自动找到CakePHP了.

产品
==========

A production installation is a more flexible way to setup Cake.
Using this method allows an entire domain to act as a single
CakePHP application. This example will help you install Cake
anywhere on your filesystem and make it available at
http://www.example.com. Note that this installation may require the
rights to change the ``DocumentRoot`` on Apache webservers.

Unpack the contents of the Cake archive into a directory of your
choosing. For the purposes of this example, we assume you choose to
install Cake into /cake\_install. Your production setup will look
like this on the filesystem::

    /cake_install/
        app/
            webroot/ (this directory is set as the ``DocumentRoot``
             directive)
        lib/
        plugins/
        vendors/
        .htaccess
        index.php
        README

Developers using Apache should set the ``DocumentRoot`` directive
for the domain to::

    DocumentRoot /cake_install/app/webroot

If your web server is configured correctly, you should now find
your Cake application accessible at http://www.example.com.

高级安装和URL重写
=======================================

.. toctree::

    installation/advanced-installation
    installation/url-rewriting

Fire It Up
==========

好了, 让我们看看CakePHP.
你需要根据你的配置将你的浏览器指向 http://example.com/ 或者 http://example.com/cake\_install/.
现在CakePHP的默认主也将会展现在你眼前, 并且会有消息告诉你当前数据库连接的状况.

恭喜! 你已经可以准备开始 :doc:`创建你的第一个CakePHP应用 </getting-started>`.

没有正常工作? 如果你遇到了时区相关的PHP错误,请参考 ``app/Config/core.php``::

   /**
    * Uncomment this line and correct your server timezone to fix 
    * any date & time related errors.
    */
       date_default_timezone_set('UTC');


.. meta::
    :title lang=cn: 安装
    :keywords lang=cn: apache mod rewrite,microsoft sql server,tar bz2,tmp directory,database storage,archive copy,tar gz,source application,current releases,web servers,microsoft iis,copyright notices,database engine,bug fixes,lighthttpd,repository,enhancements,source code,cakephp,incorporate
