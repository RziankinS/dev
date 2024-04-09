# Домашнее задание к занятию 9 «Процессы CI/CD»

## SonarQube

1. Версия sonar-scanner
    ![1](https://github.com/RziankinS/devops-netology/blob/367ac492d740c0c0c36a785aba3d3af43456c650/screen/sonar%20--version.png)
2. Запуск анализатора
    ![2](https://github.com/RziankinS/devops-netology/blob/367ac492d740c0c0c36a785aba3d3af43456c650/screen/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%20%D0%BE%D1%82%202024-04-09%2016-30-51.png)

## Nexus

1. Загрузка артефактов с GAV-параметрами в репозиторий `maven-public`:
    ![3](https://github.com/RziankinS/devops-netology/blob/367ac492d740c0c0c36a785aba3d3af43456c650/screen/maven-releases.png) 
2. 
3. 
4. В ответе пришлите файл `maven-metadata.xml` для этого артефекта.

### Знакомство с Maven

### Подготовка к выполнению

1. 
2. 
3. 
4. 
5. 

### Основная часть

1. Поменяйте в `pom.xml` блок с зависимостями под ваш артефакт из первого пункта задания для Nexus (java с версией 8_282).
2. Запустите команду `mvn package` в директории с `pom.xml`, ожидайте успешного окончания.
3. Проверьте директорию `~/.m2/repository/`, найдите ваш артефакт.
4. В ответе пришлите исправленный файл `pom.xml`.

---