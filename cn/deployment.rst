部署
##########

一旦你的应用完成了, 或者你想要部署它了.
为了发布CakePHP应用, 还有一些事要做.

Check your security
===================

If you're throwing your application out into the wild, it's a good idea to make
sure it doesn't have any leaks. Check the :doc:`/core-libraries/components/security-component` to guard against
CSRF attacks, form field tampering, and others. Doing :doc:`/models/data-validation`, and/or 
:doc:`/core-utility-libraries/sanitize` is also a great idea, for protecting your
database and also against XSS attacks. Check that only your ``webroot`` directory 
is publicly visible, and that your secrets (such as your app salt, and
any security keys) are private and unique as well!

Set document root
=================

Setting the document root correctly on your application is an important step to
keeping your code secure and your application safer. CakePHP applications
should have the document root set to the application's ``app/webroot``.  This
makes the application and configuration files inaccessible through a URL.
Setting the document root is different for different webservers.  See the
:doc:`/installation/url-rewriting` documentation for webserver specific
information.

In all cases you will want to set the virtual host/domain's document to be
``app/webroot/``. This removes the possibility of files outside of the webroot
directory being executed.

修改 core.php
===============

修改 core.php, 尤其是 ``debug`` 的值非常重要.
修改为 debug = 0 来禁止大部分开发用的特性不能暴露到网络上.
禁用调式会有以下改变:

* 禁用 :php:func:`pr()` 和 :php:func:`debug()` 调试信息.
* CakePHP核心的缓存会默认设置刷新周期为999天, 而开发模式中是每10刷新.
* 视图错误提示信息减少, 并会使用通用的错误信息代替.
* 错误不会被显示出来.
* 禁用异常的栈追踪.

除了上述内容, 许多插件和应用扩展也使用 ``debug`` 来控制自身的行为.

提高应用的性能
======================================

Since handling static assets, such as images, JavaScript and CSS files of plugins,
through the Dispatcher is incredibly inefficient, it is strongly recommended to symlink
them for production. For example like this::

    ln -s app/Plugin/YourPlugin/webroot/css/yourplugin.css app/webroot/css/yourplugin.css

.. meta::
    :title lang=en: Deployment
    :keywords lang=en: stack traces,application extensions,set document,installation documentation,development features,generic error,document root,func,debug,caches,error messages,configuration files,webroot,deployment,cakephp,applications
