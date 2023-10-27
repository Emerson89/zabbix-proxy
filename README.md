# Instalação Zabbix-proxy usando ansible 
==============================

Requerimentos
------------
- ansible 2.9.6
- Testado no Ubuntu20, Rocky8, Almalinux8 e Centos7 
- Banco de dados Sqlite e Mysql

Versão Zabbix
--------------
A definir no arquivo de playbook.yml de acordo com a versão do zabbix-server padrão 4.4 

## Principais Variáveis

| Nome | Descrição | Default | 
|------|-----------|---------|
| zabbix_version | Versão zabbix-server | 4.4|
| zabbix_server_database_long | Tipo de database[mysql/sqlite3] | sqlite3
| zabbix_server_database | Tipo de database[mysql/sqlite3] | sqlite3
| zabbix_server_ip | ip zabbix-server | 127.0.0.1

```
mysql_databases:
  - name: "{{ zabbix_proxy_dbname }}"
    login_password: "{{ mysql_root_pass }}"
    encoding: utf8
    collation: utf8_bin
mysql_users:
  - login_password: "{{ mysql_root_pass }}"
    name: "{{ zbx_database_user }}"
    password: "{{ mysql_zabbix_pass.stdout }}"
    priv: "{{ zabbix_proxy_dbname }}.*:ALL"
mysql_root_users:
  - login_user: root
    login_password: "" 
    name: "{{ mysql_root_username }}"
    password: "{{ mysql_root_pass }}"
    host: "{{ zbx_user_privileges }}"
    priv: "*.*:ALL,GRANT"
```
Importante
-----------------
Existem 2 database_types que serão suportados: mysql e sqlite. Você precisará inserir as variáveis no playbook ou em extra-vars o banco de dados que deseja usar. Caso contrário seguirá o default que é o SQlite3

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
