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

7. Oтдельная ветка `feature/add_reply` в репозитории, новый метод для класса Welcomer: содержащий слово `hunter`;Дополнение теста для нового метода на поиск слова `hunter` в новой реплике.

![9](https://github.com/RziankinS/devops-netology/blob/40393b05a8995d6ab7194d0c63da272a948c9883/screen/ci-05/%D0%BD%D0%BE%D0%B2%D0%B0%D1%8F%20%D0%B2%D0%B5%D1%82%D0%BA%D0%B0%20%D0%B8%20welkomer.png)
![10](https://github.com/RziankinS/devops-netology/blob/40393b05a8995d6ab7194d0c63da272a948c9883/screen/ci-05/welkomertest.png)

15. Сделайте push всех изменений в новую ветку репозитория.
16. Убедитесь, что сборка самостоятельно запустилась, тесты прошли успешно.
17. Внесите изменения из произвольной ветки `feature/add_reply` в `master` через `Merge`.
18. Убедитесь, что нет собранного артефакта в сборке по ветке `master`.
19. Настройте конфигурацию так, чтобы она собирала `.jar` в артефакты сборки.
20. Проведите повторную сборку мастера, убедитесь, что сбора прошла успешно и артефакты собраны.
21. Проверьте, что конфигурация в репозитории содержит все настройки конфигурации из teamcity.
22. В ответе пришлите ссылку на репозиторий.

---

### Как оформить решение задания

Выполненное домашнее задание пришлите в виде ссылки на .md-файл в вашем репозитории.

---
