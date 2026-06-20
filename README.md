balancer
========

Ansible Role para instalação e configuração do **Nginx como Load Balancer**
(proxy reverso) distribuindo tráfego HTTP entre dois servidores web de backend.

Suporta as famílias **Debian/Ubuntu** e **RedHat/CentOS**.

Requirements
------------

- Ansible >= 2.9
- Acesso `root`/`become` nos hosts de destino

Role Variables
--------------

Definidas em `defaults/main.yml` e sobrescrevíveis no playbook:

| Variável      | Padrão                              | Descrição                              |
|---------------|-------------------------------------|----------------------------------------|
| `balancer`    | `127.0.0.1`                         | IP em que o Nginx escuta na porta 80   |
| `server_name` | `www.exemplo.com.br exemplo.com.br` | `server_name` do virtual host          |
| `webserver01` | `172.16.0.201`                      | Primeiro backend do upstream `cluster` |
| `webserver02` | `172.16.0.202`                      | Segundo backend do upstream `cluster`  |

Dependencies
------------

Nenhuma.

Example Playbook
----------------

```yaml
- hosts: balancers
  become: true
  roles:
    - role: balancer
      balancer: 172.16.0.200
      server_name: "www.meusite.com.br meusite.com.br"
      webserver01: 10.0.0.11
      webserver02: 10.0.0.12
```

Testing
-------

Há testes com Test Kitchen + Docker + serverspec:

```bash
kitchen test
```

License
-------

GPLv3

Author Information
------------------

dotfob
