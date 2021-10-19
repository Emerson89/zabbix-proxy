# Zabbix-proxy 
==============================

Requerimentos
------------
- ansible 2.9.6
- Suporte as distribuições baseadas em Debian e RedHat
- Testado no Ubuntu20, Rocky8 e Centos7 
- Banco de dados Sqlite e Mysql

Versão Zabbix
--------------
A definir no arquivo de playbook.yml de acordo com a versão do zabbix-server padrão 4.4 

## Inside variáveis DB MYSQL RHEL 8/ Ubuntu20 zabbix/vars/main.yml:
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
## Para Centos 7 utilize as variáveis
```
mysql_databases:
  - name: "{{ zabbix_proxy_dbname }}"
    login_password: "{{ mysql_root_password }}"
    encoding: utf8
    collation: utf8_bin
mysql_users:
  - login_password: "{{ mysql_root_password }}"
    name: "{{ zbx_database_user }}"
    password: "{{ zbx_database_password }}"
    priv: "{{ zabbix_proxy_dbname }}.*:ALL"
```
-----------------
Se você usa mysql, deve definir o nome de usuário, senha e host mysql para preparar o banco de dados zabbix, caso contrário, eles serão considerados como seu valor default (e, portanto, conectar-se ao banco de dados será considerado como conectar-se ao host local sem senha). as chaves: login_host login_user login_password
Existem 2 database_types que serão suportados: mysql e sqlite. Você precisará inserir as variáveis no playbook o banco de dados que deseja usar. Caso contrário seguirá o default que é SQlite3

Playbook Exemplo
----------------
```
---
- hosts: all
  vars:
    zabbix_server_ip: 'IP-ZABBIX-SERVER'
    zabbix_version: 4.4
    zabbix_proxy_database: mysql or sqlite3 
    zabbix_proxy_database_long: mysql or sqlite3
  roles:
    - zabbix
  become: yes
  
```
Arquivo de inventário
--------------
```
[zabbix]
xx.xx.xx.xx ansible_ssh_private_key_file=/Path-Dir/key.pem ansible_user=vagrant
```

Licença
-------
GPLv3
