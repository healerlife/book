# openerp——安装过程

- 更新系统
	<code>apt-get update</code>

- 安装依赖程序 
    <code>apt-get install -y --no-install-recommends git openssh-client vim curl ca-certificates libldap2-dev python-dev libxslt-dev libsasl2-dev libjpeg-dev libpq-dev gcc g++ python2.7 make</code>

- 安装python工具包
	<code>curl -o get-pip.py https://bootstrap.pypa.io/get-pip.py<br/>python2.7 get-pip.py</code>

- openerp源码包-使用gihub
	<code>git clone https://github.com/odoo/odoo.git</code>
	