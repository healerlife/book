# saas化——安装过程

1. 安装依赖程序

	<pre>pip install simplejson<br/>pip install oauthlib<br/>pip install requests --upgrade<br/></pre>

2. 修改 /etc/init.d/odod-server

	>--db-filter 采用^%h$ （必须的）
	>修改已有数据库名称使用ALTER DATABASE name RENAME TO "new_name"

3. 在openerp根目录执行以下代码,实现数据库名称可带.号

	<pre>sed -i 's/matches="[^"]*"//g' addons/web/static/src/xml/base.xml</pre>

4. 修改 /etc/hosts 映射文件
	
	>如果你在本地测试记得这一步骤

5. 下载saas模块

	<pre>https://github.com/yelizariev/odoo-saas-tools 下载至openerp根目录下的addons目录</pre>

	>注释saas_portal_start\views\website.xml里的id="theme"和id="assets_frontend"

6. 访问www.example.com（主控制系统）
	<pre>安装saas_portal 和 saas_portal_* 模块</pre>

7. 访问server.example.com（服务系统）
	<pre>安装saas_server</pre>

8. 配置服务系统
	<pre>进入(?)/About 进入开发模式<br/>进入 Settings/Users/OAuth Providers 编辑Saas<br/>http://odoo.local/oauth2/auth和http://odoo.local/oauth2/tokeninfo，将odoo.local修改成www.example.com(注：如果不是80端口记得带上端口)<br/>body——显示在登录页的文本提示，可改成XX授权登录<br/>拷贝一下Client ID 下个步骤会使用到</pre>

9. 配置主控制系统
	<pre>进入SaaS/SaaS/Servers<br/>点击新建<br/>database name设置server.example.com,Database UUID设置上个操作拷贝的Client ID，并设置端口<br/>点击保存</pre>

10. 创建计划

	<pre>点击新建<br/>设置名称 例如：CRM套餐<br/>saas server选择server.example.com<br/>temlpate 选择新建 temlpate1.example.com<br/>db Names写temlpate1.example.com<br/>设置过期时间（注，可多安装一个过期自动删除过期数据库的模块）<br/>选择模块<br/>点击保存<br/>点击 Create Template DB<br/>点击Sync server  同步服务</pre>

11. 准备模块数据库

	<pre>点击Log in to template DB<br/>登录后安装与上面套餐设定一致的模块<br/>可在修改其他需要的配置，例如可创建用户<br/>进入Settings/Users/Users 设置administrator权限 Access Rights</pre>

12. 创建客户端
	
	<pre>进入SaaS/Saas/Plans<br/>设置数据库名称client1.example.com<br/>点击创建<br/>结束后点击Sync server<br/>进入SaaS/SaaS/Client 选择对应的客户端<br/>click [Configure] -> open Parameters tab -> add parameter "Max Users", set Value 2 -> Execute -> Close -> Log in</pre>

13. 到此结束，往后可制作更多模版数据库实现saas快速创建