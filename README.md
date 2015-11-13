###  Clutch.io  使用说明
***
#### Prerequisites (以Linux例)
***
- **Python 2.7 or Greater** (里面有用libimport模块,这个模块从Python2.7开始成为标准模块,当然也可在2.6上配置,但比较复杂)
- **PostgreSQL && Psycopg2**
- **libevent 2.0.20 + **
- **S3 Account **(for hybrid native/html application framework ONLY,如果不使用混合框架也需要安装或者修改clutchrpc文件下面的相关python文件将相关代码去掉,这样就不用安装)
- **Django**(Web端使用的此框架)
- **Gunicorn**(AB测试服务端主要使用此来并发处理请求)
- **其他Python模块,例如Gevent,simplejson,pytz...**(这个可以先不安装,运行时发现没有某某模块的错误就去安装)
> **注意:** 安装软件的时候最好到官网上去按照步骤安装,官网一般会给出不同派系系统的安装方法,一般Ubuntu用apt(有时需要兼容模式安装)和easy_install就能搞定,Centos一般用yum install 和rpm源码编译安装

###Installing and Running Clutch.io
***

Before you get started, make sure all of the prerequisites are installed and
that PostgreSQL is running.  Now we need to create a Clutch user and database:

    createuser -s clutch

    createdb -E utf8 --owner=clutch clutch

Next we need to install Clutch:

    easy_install clutchserver

Now we will generate a configuration file used to setup ports and such:

    clutch-config > conf.py

You can check the configuration defaults provided by clutch-config and decide
whether they are right for your setup.  For most people, the defaults should be
just fine.  When you're ready, let's start up the server:

    clutch-all conf.py

That's it, you're now running Clutch.io!  Visit http://127.0.0.1:8000/ to see
it in action.
> **注意:** 
> - 如果运行起来读写数据库时出错(例如用户不合法,没权限等),一般要 **/etc/postgresql/x.x/main/pg_hba.conf
 
	local   all             all                                     trust
	host    all             all             127.0.0.1/32            trust

并到/etc/init.d/postgresql reload 使配置生效
> - 要在clutch下面目录去运行而不是在bin里面,即./bin/clutch-all ./bin/conf.py,否则会因为路径出错 
> - 其他的问题我也忘了,Google应该就没问题了
