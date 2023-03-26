## Задача 1
```
Запуск playbook на окружении из test.yml; значение, которое имеет факт "some_fact":
```
![1](https://github.com/RziankinS/devops-netology/blob/main/screen/1.png)
## Задача 2
```
Замена значений в файле с переменными (group_vars):
```
![2](https://github.com/RziankinS/devops-netology/blob/main/screen/2.png)
## Задача 3
```
docker run --name ubuntu -d pycontribs/ubuntu sleep 65000000
docker run --name centos7 -d pycontribs/centos:7 sleep 65000000
```
## Задача 4
```
Запуск playbook на окружении из prod.yml; значения some_fact для каждого из managed host:
```
![3](https://github.com/RziankinS/devops-netology/blob/main/screen/3.png)
## Задача 5; 6
```
Добавление фактов в group_vars так, чтобы для some_fact получились значения: для deb — deb default fact, для el — el default fact
Запуск paybook
```
![4](https://github.com/RziankinS/devops-netology/blob/main/screen/4.png)
## Задача 7; 8
```
ansible-vault и проверка рработоспособности

```
![5](https://github.com/RziankinS/devops-netology/blob/main/screen/5.png)

![6](https://github.com/RziankinS/devops-netology/blob/main/screen/6.png)
## Задача 9
```
ansible-doc -t connection -l

plugin: local
```
## Задача 10; 11
![7](https://github.com/RziankinS/devops-netology/blob/main/screen/7.png)

