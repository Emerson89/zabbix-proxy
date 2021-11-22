# Zabbix-proxy 
==============================

[![Build Status](https://app.travis-ci.com/Emerson89/zabbix-proxy.svg?branch=master)](https://app.travis-ci.com/Emerson89/zabbix-proxy)

Requerimentos
------------
- ansible 2.9.6
- Suporte as distribuições baseadas em Debian e RedHat
- Testado no Ubuntu20, Rocky8 e Centos7 
- Banco de dados Sqlite e Mysql

Versão Zabbix
--------------
A definir no arquivo de playbook.yml de acordo com a versão do zabbix-server padrão 4.4 

## Inside variáveis DB MYSQL RHEL 8 zabbix/vars/main.yml:
```
mysql_databases:
  - name: "{{ zabbix_proxy_dbname }}"
    encoding: utf8
    collation: utf8_bin
mysql_users:
  - name: "{{ zbx_database_user }}"
    password: "{{ mysql_zabbix_pass.stdout }}"
    priv: "{{ zabbix_proxy_dbname }}.*:ALL"
```
## Para Centos 7 utilize as variáveis
```
mysql_databases:
  - name: "{{ zabbix_proxy_dbname }}"
    login_password: "{{ mysql_root_pass.stdout }}"
    encoding: utf8
    collation: utf8_bin
mysql_users:
  - login_password: "{{ mysql_root_pass.stdout }}"
    name: "{{ zbx_database_user }}"
    password: "{{ mysql_zabbix_pass.stdout }}"
    priv: "{{ zabbix_proxy_dbname }}.*:ALL"
```
## Para Ubuntu20 utilize as variáveis
```
mysql_databases:
  - name: "{{ zabbix_proxy_dbname }}"
    login_password: "{{ mysql_root_pass.stdout }}"
    encoding: utf8
    collation: utf8_bin
mysql_users:
  - login_password: "{{ mysql_root_pass.stdout }}"
    name: "{{ zbx_database_user }}"
    password: "{{ mysql_zabbix_pass.stdout }}"
    priv: "{{ zabbix_proxy_dbname }}.*:ALL"
    login_unix_socket: /var/run/mysqld/mysqld.sock 
```
Importante
-----------------
Existem 2 database_types que serão suportados: mysql e sqlite. Você precisará inserir as variáveis no playbook o banco de dados que deseja usar. Caso contrário seguirá o default que é o SQlite3

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
