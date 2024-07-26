# Troubleshooting

### 1. Установить приложение по команде:
```shell
kubectl apply -f https://raw.githubusercontent.com/netology-code/kuber-homeworks/main/3.5/files/task.yaml
```
- [x] Установка прошла успешно, добавлено два namespace: web; data
![1](https://github.com/RziankinS/devops-netology/blob/a46fbb4d7f713ef194f728189a3dbd60a15f6bde/screen/1.15/1.png)
---
### 2. Выявить проблему и описать.
- [x] Смотрим логи пода, видим ошибку подклчючения по dns-имени:
![2](https://github.com/RziankinS/devops-netology/blob/a46fbb4d7f713ef194f728189a3dbd60a15f6bde/screen/1.15/2.png)
---
### 3. Исправить проблему, описать, что сделано.
- [x] Подключаемся к контейнеру, проверяем подключение к auth-db - получаем тайм-аут. Проверяем по ip-адресу - подключение проходит
![3](https://github.com/RziankinS/devops-netology/blob/a46fbb4d7f713ef194f728189a3dbd60a15f6bde/screen/1.15/3.png)
---
- [x] Через команду nslookup получаем корректное dns-имя; проверяем подключение по указому имени - успешно:
![4](https://github.com/RziankinS/devops-netology/blob/a46fbb4d7f713ef194f728189a3dbd60a15f6bde/screen/1.15/4.png)
---
- [x] Дописываем строку в манифесте: ~~while true; do curl auth-db; sleep 5; done~~ > ***while true; do curl auth-db.data.svc.cluster.local; sleep 5; done***
---
### 4. Продемонстрировать, что проблема решена.

- [x] Обновляем deployment и проверяем, что подключение проходит успешно:
![5](https://github.com/RziankinS/devops-netology/blob/a46fbb4d7f713ef194f728189a3dbd60a15f6bde/screen/1.15/5.png)
---
