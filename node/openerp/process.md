# openerp——安装过程

1. 更新系统

	<pre>apt-get update</pre>

2. 安装依赖程序

    <pre>apt-get install -y --no-install-recommends git openssh-client vim curl ca-certificates libldap2-dev python-dev libxslt-dev libsasl2-dev libjpeg-dev libpq-dev gcc g++ python2.7 make</pre>

3. 安装python工具包

	<pre>curl -o get-pip.py https://bootstrap.pypa.io/get-pip.py<br/>python2.7 get-pip.py</pre>

4. openerp源码包-使用gihub

	<pre>
		git clone https://github.com/odoo/odoo.git<br/>
		cd odoo<br/>
		chmod 755 odoo-server
	</pre>

5. 安装openerp需要的python依赖,进入git clone后的根目录

	<pre>pip install -r requirements.txt</pre>

6. 添加odoo用户（openerp也可以，自由选择）

	<pre>groupadd odoo<br/>useradd -g odoo odoo</pre>

7. 添加openerp配置文件

	<pre>vi /etc/odoo-server.conf<br/>chown odoo: /etc/odoo-server.conf<br/>chmod 755 /etc/odoo-server.conf</pre>
	> [odoo-server.conf样本下载地址](https://github.com/odoo/odoo/blob/9.0/debian/openerp-server.conf "openerp配置文件")

8. 添加开机启动代码

	<pre>
		vi /etc/init.d/odoo-server<br/>
		chmod 755 /etc/init.d/odoo-server<br/>
		chown root: /etc/init.d/odoo-server
	</pre>
	> [odoo-server样本下载地址](https://github.com/odoo/odoo/blob/9.0/debian/init "odoo-server开机启动文件")

	注：DAEMON=git clone根目录的openerp-server，其他配置参数按照实际安装的情况修改

9. 添加openerp日志目录

	<pre>
		mkdir /var/log/odoo<br/>
		chown odoo:root /var/log/odoo
	</pre>

10. 安装nodejs——源码方式

	<pre>
		curl -o node-v4.2.1.tar.gz https://nodejs.org/dist/v4.2.1/node-v4.2.1.tar.gz<br/>
		tar zxvf node-v4.2.1.tar.gz<br/>
		cd node-v4.2.1<br/>
		./configure<br/>
		make && make install<br/>
		npm install -g less less-plugin-clean-css<br/>
	</pre>

11. 开机启动openerp服务——docker方式，其他可用init.d
	
	<pre>
		vi /etc/bash.bashrc<br/>
		添加 service odoo-server start
	</pre>

12. 安装wkhtmltopdf

	<pre>
		curl -o xxx.deb http://xxxx.deb
		dpkg -i xxx.deb
	</pre>
	> [wkhtmltopdf下载地址](ttp://wkhtmltopdf.org/downloads.html "wkhtmltopdf")
	
13. 安装中文字体
	
	<pre>
		apt-get install ttf-wqy-zenhei<br/>
		apt-get -f install<br/>
		apt-get install ttf-wqy-zenhei
	</pre>

14. 附件存数据库

	进入开发模式，在系统参数中添加以下键值对,在网上有许多其他的方式，但是那都是旧版本的，以下版本才是真实靠谱的。
	<pre>ir_attachment.location=db</pre>

15. 修改时区
	
	<pre>dpkg-reconfigure tzdata</pre>

16. 重启系统

	<pre>reboot</pre>