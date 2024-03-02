# Домашнее задание к занятию 2 «Работа с Playbook»
## Описание
```
Playbook устанавливает и производит настройки конфигураций сервисов: Clichouse и Vector, на Linux дистрибутивах, с пакетным менеджером YUM.
Версии дистрибутивов четко определены в "group_vars"
```
## Задача 1
```
Дописать playbook: установка и настройка vector
```
```yaml
- name: Install Vector
  hosts: vector
  handlers:
    - name: Start Vector service
      become: true
      ansible.builtin.service:
        name: vector
        state: restarted

  tasks:
    - name: Get Vector distrib
      ansible.builtin.get_url:
        url: "https://packages.timber.io/vector/latest/vector-{{ vector_version }}.x86_64.rpm"
        dest: "./vector-{{ vector_version }}.rpm"

    - name: Install Vector packages
      become: true
      ansible.builtin.yum:
        name: vector-{{ vector_version }}.rpm
      notify: Start Vector service

    - name: Creates directory
      become: true
      file:
        path: /var/lib/vector/local_logs
        state: directory
        owner: "{{ ansible_user_id }}"
        group: "{{ ansible_user_gid }}"
        mode: 0644

    - name: Config template
      become: true
      ansible.builtin.template:
        src: "vector.yml.j2"
        dest: "/etc/vector/vector.yaml"
        mode: "0755"
      notify: Start Vector service
```
## Задача 2
```
Запустить `ansible-lint site.yml и справить ошибки
```
![1](https://github.com/RziankinS/devops-netology/blob/ee912497f08a605c2d373644cd943525561f488d/screen/ansible-lint.png)
## Задача 3
```
Запустить playbook с флагом `--check`
```
![2](https://github.com/RziankinS/devops-netology/blob/main/screen/ansible-playbook%20--check.png)
## Задача 4
```
Запустить playbook с флагом `--diff`
```
```yaml
sergei@L540:~/ansible$ ansible-playbook playbook/site.yml -i /home/sergei/ansible/playbook/inventory/prod.yml --diff

PLAY [Install Clickhouse] **********************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************************************
ok: [clickhouse-01]

TASK [Get clickhouse distrib] ******************************************************************************************************************
ok: [clickhouse-01] => (item=clickhouse-client)
ok: [clickhouse-01] => (item=clickhouse-server)
ok: [clickhouse-01] => (item=clickhouse-common-static)

TASK [Install clickhouse packages] *************************************************************************************************************
ok: [clickhouse-01]

TASK [Flush handlers] **************************************************************************************************************************

TASK [Create database] *************************************************************************************************************************
ok: [clickhouse-01]

PLAY [Install Vector] **************************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************************************
ok: [vector-01]

TASK [Get Vector distrib] **********************************************************************************************************************
ok: [vector-01]

TASK [Install Vector packages] *****************************************************************************************************************
ok: [vector-01]

TASK [Creates directory] ***********************************************************************************************************************
ok: [vector-01]

TASK [Config template] *************************************************************************************************************************
ok: [vector-01]

PLAY RECAP *************************************************************************************************************************************
clickhouse-01              : ok=4    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
vector-01                  : ok=5    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

sergei@L540:~/ansible$ ssh sergei@158.160.8.144
[sergei@test ~]$ uptime -p
up 23 minutes
[sergei@test ~]$ vector -V
vector 0.36.0 (x86_64-unknown-linux-gnu a5e48bb 2024-02-13 14:43:11.911392615)
[sergei@test ~]$ logout
Connection to 158.160.8.144 closed.
sergei@L540:~/ansible$ ansible-playbook playbook/site.yml -i /home/sergei/ansible/playbook/inventory/prod.yml --diff

PLAY [Install Clickhouse] **********************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************************************
ok: [clickhouse-01]

TASK [Get clickhouse distrib] ******************************************************************************************************************
ok: [clickhouse-01] => (item=clickhouse-client)
ok: [clickhouse-01] => (item=clickhouse-server)
ok: [clickhouse-01] => (item=clickhouse-common-static)

TASK [Install clickhouse packages] *************************************************************************************************************
ok: [clickhouse-01]

TASK [Flush handlers] **************************************************************************************************************************

TASK [Create database] *************************************************************************************************************************
ok: [clickhouse-01]

PLAY [Install Vector] **************************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************************************
ok: [vector-01]

TASK [Get Vector distrib] **********************************************************************************************************************
ok: [vector-01]

TASK [Install Vector packages] *****************************************************************************************************************
ok: [vector-01]

TASK [Creates directory] ***********************************************************************************************************************
ok: [vector-01]

TASK [Config template] *************************************************************************************************************************
ok: [vector-01]

PLAY RECAP *************************************************************************************************************************************
clickhouse-01              : ok=4    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
vector-01                  : ok=5    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

sergei@L540:~/ansible$ ssh sergei@158.160.8.144
[sergei@test ~]$ uptime -p
up 25 minutes
[sergei@test ~]$ vector -V
vector 0.36.0 (x86_64-unknown-linux-gnu a5e48bb 2024-02-13 14:43:11.911392615)
[sergei@test ~]$ logout
Connection to 158.160.8.144 closed.
```
