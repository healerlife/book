# openerp——安装过程

1. 更新系统

	<pre>apt-get update</pre>

2. 安装依赖程序

    <pre>apt-get install -y --no-install-recommends git openssh-client vim curl ca-certificates libldap2-dev python-dev libxslt-dev libsasl2-dev libjpeg-dev libpq-dev gcc g++ python2.7 make</pre>

3. 安装python工具包

	<pre>curl -o get-pip.py https://bootstrap.pypa.io/get-pip.py<br/>python2.7 get-pip.py</pre>

4. openerp源码包-使用gihub

	<pre>git clone https://github.com/odoo/odoo.git</pre>

5. 安装openerp需要的python依赖

	<pre>pip install -r requirements.txt</pre>

6. 添加odoo用户（openerp也可以，自由选择）

	<pre>groupadd odoo<br/>useradd -g odoo odoo</pre>

7. 添加openerp配置文件
	<pre>vi /etc/odoo-server.conf<br/>chown odoo: /etc/odoo-server.conf<br/>chmod 640 /etc/odoo-server.conf</pre>
	> [内容下载地址](https://github.com/odoo/odoo/tree/9.0/debian "openerp配置文件")


