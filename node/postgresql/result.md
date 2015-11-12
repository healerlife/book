# 负载解决方案

1. 修改 /etc/odoo-server.conf 中的db_maxconn

2. 修改 /var/lib/pgsql/9.2/data/postgresql.conf 中的 max_connections = 200

3. 总结：所有openerp服务器中的db_maxconn总和需要小于postgresql.conf中的max_connections。