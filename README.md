Zabbix-proxy 
=========

Requerimentos
------------
- Nenhum
- Suporte as distribuições baseadas em Debian e RedHat
- Testado no Ubuntu20 e Rocky8 
- Banco de dados Sqlite

Versão Zabbix
--------------
A definir no arquivo de playbook.yml de acordo com a versão do zabbix-server padrão 5.0 

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
