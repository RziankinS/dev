# Домашнее задание "Использование Ansible"
## Описание
```
Playbook устанавливает и производит настройки конфигураций сервисов: Clichouse, Vector, Lighthouse, Nginx на Linux дистрибутивах, с пакетным менеджером YUM.
Версии дистрибутивов определены в "group_vars"
```
## Задача
```
Дописать playbook: установка настройка LightHouse и Nginx
```
```yaml
- name: Install nginx
  hosts: lighthouse
  handlers:
    - name: Start Nginx
      become: true
      ansible.builtin.command: nginx
    - name: Restart Nginx Service
      become: true
      ansible.builtin.service:
        name: nginx
        state: restarted
  tasks:
    - name: NGINX | Install epel-release
      become: true
      ansible.builtin.yum:
        name: epel-release
        state: present
    - name: Install nginx
      become: true
      ansible.builtin.yum:
        name: nginx
        state: present
      notify: start nginx service
    - name: NGINX config
      become: true
      ansible.builtin.template:
        src: nginx.j2
        dest: /etc/nginx/nginx.conf
        mode: "0644"
      notify: Reload-nginx

- name: Install lighthouse
  hosts: lighthouse
  handlers:
    - name: Reload-nginx
      become: true
      command: nginx -s reload
    - name: Restart nginx service
      become: true
      ansible.builtin.service:
        name: nginx
        state: restarted
  pre_tasks:
    - name: lighthouse git
      become: true
      ansible.builtin.yum:
        name: git
        state: present
  tasks:
    - name: Lighthouse | Copy from git
      git:
        repo: "{{ lighthouse_vcs }}"
        version: master
        dest: "{{ lighthouse_dir }}"
    - name: Lighthouse config
      become: true
      ansible.builtin.template:
        src: lighthouse.j2
        dest: /etc/nginx/conf.d/defult.conf
        mode: "0644"
      notify: Reload-nginx
```
## Задача
```
Запустить `ansible-lint site.yml и справить ошибки
```
![1](https://github.com/RziankinS/devops-netology/blob/main/screen/lint.png)
```
Запустить playbook с флагом `--check`
```
![2](https://github.com/RziankinS/devops-netology/blob/main/screen/check.png)
## Задача
```
Запустить playbook с флагом `--diff`
```
```yaml
sergei@L540:~/ansible$ ansible-playbook playbook/site.yml -i /home/sergei/ansible/playbook/inventory/prod.yml --diff

PLAY [Install Clickhouse] *********************************************************************************************************************************

TASK [Gathering Facts] ************************************************************************************************************************************
ok: [clickhouse-01]

TASK [Get clickhouse distrib] *****************************************************************************************************************************
ok: [clickhouse-01] => (item=clickhouse-client)
ok: [clickhouse-01] => (item=clickhouse-server)
ok: [clickhouse-01] => (item=clickhouse-common-static)

TASK [Install clickhouse packages] ************************************************************************************************************************
ok: [clickhouse-01]

TASK [Flush handlers] *************************************************************************************************************************************

TASK [Create database] ************************************************************************************************************************************
ok: [clickhouse-01]

PLAY [Install Vector] *************************************************************************************************************************************

TASK [Gathering Facts] ************************************************************************************************************************************
ok: [vector-01]

TASK [Get Vector distrib] *********************************************************************************************************************************
ok: [vector-01]

TASK [Install Vector packages] ****************************************************************************************************************************
ok: [vector-01]

TASK [Creates directory] **********************************************************************************************************************************
ok: [vector-01]

TASK [Config template] ************************************************************************************************************************************
ok: [vector-01]

PLAY [Install nginx] **************************************************************************************************************************************

TASK [Gathering Facts] ************************************************************************************************************************************
ok: [lighthouse-01]

TASK [NGINX | Install epel-release] ***********************************************************************************************************************
ok: [lighthouse-01]

TASK [Install nginx] **************************************************************************************************************************************
ok: [lighthouse-01]

TASK [NGINX config] ***************************************************************************************************************************************
ok: [lighthouse-01]

PLAY [Install lighthouse] *********************************************************************************************************************************

TASK [Gathering Facts] ************************************************************************************************************************************
ok: [lighthouse-01]

TASK [lighthouse git] *************************************************************************************************************************************
ok: [lighthouse-01]

TASK [Lighthouse | Copy from git] *************************************************************************************************************************
ok: [lighthouse-01]

TASK [Lighthouse config] **********************************************************************************************************************************
ok: [lighthouse-01]

PLAY RECAP ************************************************************************************************************************************************
clickhouse-01              : ok=4    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
lighthouse-01              : ok=8    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
vector-01                  : ok=5    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

sergei@L540:~/ansible$ ansible-playbook playbook/site.yml -i /home/sergei/ansible/playbook/inventory/prod.yml --diff

PLAY [Install Clickhouse] *********************************************************************************************************************************

TASK [Gathering Facts] ************************************************************************************************************************************
ok: [clickhouse-01]

TASK [Get clickhouse distrib] *****************************************************************************************************************************
ok: [clickhouse-01] => (item=clickhouse-client)
ok: [clickhouse-01] => (item=clickhouse-server)
ok: [clickhouse-01] => (item=clickhouse-common-static)

TASK [Install clickhouse packages] ************************************************************************************************************************
ok: [clickhouse-01]

TASK [Flush handlers] *************************************************************************************************************************************

TASK [Create database] ************************************************************************************************************************************
ok: [clickhouse-01]

PLAY [Install Vector] *************************************************************************************************************************************

TASK [Gathering Facts] ************************************************************************************************************************************
ok: [vector-01]

TASK [Get Vector distrib] *********************************************************************************************************************************
ok: [vector-01]

TASK [Install Vector packages] ****************************************************************************************************************************
ok: [vector-01]

TASK [Creates directory] **********************************************************************************************************************************
ok: [vector-01]

TASK [Config template] ************************************************************************************************************************************
ok: [vector-01]

PLAY [Install nginx] **************************************************************************************************************************************

TASK [Gathering Facts] ************************************************************************************************************************************
ok: [lighthouse-01]

TASK [NGINX | Install epel-release] ***********************************************************************************************************************
ok: [lighthouse-01]

TASK [Install nginx] **************************************************************************************************************************************
ok: [lighthouse-01]

TASK [NGINX config] ***************************************************************************************************************************************
ok: [lighthouse-01]

PLAY [Install lighthouse] *********************************************************************************************************************************

TASK [Gathering Facts] ************************************************************************************************************************************
ok: [lighthouse-01]

TASK [lighthouse git] *************************************************************************************************************************************
ok: [lighthouse-01]

TASK [Lighthouse | Copy from git] *************************************************************************************************************************
ok: [lighthouse-01]

TASK [Lighthouse config] **********************************************************************************************************************************
ok: [lighthouse-01]

PLAY RECAP ************************************************************************************************************************************************
clickhouse-01              : ok=4    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
lighthouse-01              : ok=8    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
vector-01                  : ok=5    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0  
```
