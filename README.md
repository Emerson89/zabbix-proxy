Zabbix-proxy 
=========

Requerimentos
------------
- ansible 2.9.6
- Suporte as distribuições baseadas em Debian e RedHat
- Testado no Ubuntu20 e Rocky8 
- Banco de dados Sqlite e Mysql

Versão Zabbix
--------------
A definir no arquivo de playbook.yml de acordo com a versão do zabbix-server padrão 5.0 

## Inside variáveis DB zabbix/vars/main.yml:
```
mysql_databases:
  - name: "{{ zabbix_proxy_dbname }}"
    encoding: utf8
    collation: utf8_bin
mysql_users:
  - name: "{{ zbx_database_user }}"
    password: "{{ zbx_database_password }}"
    priv: "{{ zabbix_proxy_dbname }}.*:ALL"
```
```
  zabbix_proxy_database: mysql 
  zabbix_proxy_database_long: mysql 
  # zabbix_proxy_database: sqlite3 
  # zabbix_proxy_database_long: sqlite3
```
Existem 2 database_types que serão suportados: mysql e sqlite. Você precisará comentar ou descomentar o banco de dados que deseja usar. No exemplo acima, o banco de dados mysql é usado. Se você quiser usar o sqlite3, descomente as 2 linhas do sqlite3 e comente as 2 linhas do mysql.

Se você usa mysql, deve definir o nome de usuário, senha e host mysql para preparar o banco de dados zabbix, caso contrário, eles serão considerados como seu valor padrão (e, portanto, conectar-se ao banco de dados será considerado como conectar-se ao host local sem senha). as chaves estão abaixo: zabbix_proxy_mysql_login_host zabbix_proxy_mysql_login_user zabbix_proxy_mysql_login_password

Arquivo de inventário hosts
--------------
```
[zabbix]
xx.xx.xx.xx ansible_ssh_private_key_file=/Path-Dir/key.pem ansible_user=vagrant
```

Playbook Exemplo
----------------
```
---
- hosts: all
  vars:
    zabbix_server_ip: '192.168.33.11'
    zabbix_version: 5.0
  roles:
    - zabbix
  become: yes
  
```
Licença
-------

BSD
