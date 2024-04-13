# Teamcity
## Подготовка к выполнению
В Yandex Cloud созданы два новых инстансов на основе образа `jetbrains/teamcity-server` и вм для Nexus:

![1](https://github.com/RziankinS/devops-netology/blob/40393b05a8995d6ab7194d0c63da272a948c9883/screen/ci-05/create%20vm.png)

Первоначальные настройки выполены, агент авторизован,fork репозитория example-teamcity выполнен.

## Основная часть

1. Новый проект в teamcity на основе fork:

![2](https://github.com/RziankinS/devops-netology/blob/40393b05a8995d6ab7194d0c63da272a948c9883/screen/ci-05/1.%D0%BF%D1%80%D0%BE%D0%B5%D0%BA%D1%82.png)
 
2. Autodetect конфигурации:

![3](https://github.com/RziankinS/devops-netology/blob/40393b05a8995d6ab7194d0c63da272a948c9883/screen/ci-05/2.png)

3. Запуск первой сборки master:

![4](https://github.com/RziankinS/devops-netology/blob/40393b05a8995d6ab7194d0c63da272a948c9883/screen/ci-05/3.png)

![5](https://github.com/RziankinS/devops-netology/blob/40393b05a8995d6ab7194d0c63da272a948c9883/screen/ci-05/4.png)

4. Изменить условия сборки: если на`mvn clean deploy`, и импорт settings.xml:

![6](https://github.com/RziankinS/devops-netology/blob/40393b05a8995d6ab7194d0c63da272a948c9883/screen/ci-05/settings%26clean%20deploy.png)

5. Aртефакт в nexus:

![7](https://github.com/RziankinS/devops-netology/blob/40393b05a8995d6ab7194d0c63da272a948c9883/screen/ci-05/%D0%B0%D1%80%D1%82%D0%B5%D1%84%D0%B0%D0%BA%D1%82%20%D0%BD%D0%B5%D0%BA%D1%81%D1%83%D1%81.png)

6. Миграция `build configuration` в репозиторий:

![8](https://github.com/RziankinS/devops-netology/blob/40393b05a8995d6ab7194d0c63da272a948c9883/screen/ci-05/18.%D0%BF%D0%BE%D0%B2%D1%82%D0%BE%D1%80%D0%BD%D1%8B%D0%B9%20%D0%B1%D0%B8%D0%BB%D0%B4%20%D0%BA%D0%BE%D0%BD%D1%84%D0%B8%D0%B3.png)

7. Oтдельная ветка `feature/add_reply` в репозитории; новый метод для класса Welcomer: содержащий слово `hunter`; Дополнение теста для нового метода на поиск слова `hunter` в новой реплике:

![9](https://github.com/RziankinS/devops-netology/blob/40393b05a8995d6ab7194d0c63da272a948c9883/screen/ci-05/%D0%BD%D0%BE%D0%B2%D0%B0%D1%8F%20%D0%B2%D0%B5%D1%82%D0%BA%D0%B0%20%D0%B8%20welkomer.png)
![10](https://github.com/RziankinS/devops-netology/blob/40393b05a8995d6ab7194d0c63da272a948c9883/screen/ci-05/welkomertest.png)

8. Запуск сборки из ветки feature/add_reply:

![11](https://github.com/RziankinS/devops-netology/blob/40393b05a8995d6ab7194d0c63da272a948c9883/screen/ci-05/%D1%81%D0%B1%D0%BE%D1%80%D0%BA%D0%B0%20%D0%BD%D0%B0%20%D0%B2%D0%B5%D1%82%D0%BA%D0%B5%20feature.png) 
![12](https://github.com/RziankinS/devops-netology/blob/40393b05a8995d6ab7194d0c63da272a948c9883/screen/ci-05/%D0%B0%D1%80%D1%82%D0%B5%D1%84%D0%B0%D0%BA%D0%B0%D1%82%20%D0%BD%D0%B0%20%D0%B2%D0%B5%D1%82%D0%BA%D0%B5%20feature.png)

9. Внес изменения из ветки `feature/add_reply` в `master` через `Merge`; Убедиться, что нет собранного артефакта в сборке по ветке `master`:
![13](https://github.com/RziankinS/devops-netology/blob/40393b05a8995d6ab7194d0c63da272a948c9883/screen/ci-05/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%20%D0%BE%D1%82%202024-04-13%2018-03-22.png)

20. Провеcти повторную сборку мастера, убедиться, что сборка прошла успешно и артефакты собраны:
![14](https://github.com/RziankinS/devops-netology/blob/40393b05a8995d6ab7194d0c63da272a948c9883/screen/ci-05/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%20%D0%BE%D1%82%202024-04-13%2018-22-59.png)   
![15](https://github.com/RziankinS/devops-netology/blob/40393b05a8995d6ab7194d0c63da272a948c9883/screen/ci-05/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%20%D0%BE%D1%82%202024-04-13%2018-23-20.png)

---

---
