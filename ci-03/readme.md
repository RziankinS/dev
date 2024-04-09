# Процессы CI/CD

## SonarQube

1. Версия sonar-scanner
   
    ![1](https://github.com/RziankinS/devops-netology/blob/367ac492d740c0c0c36a785aba3d3af43456c650/screen/sonar%20--version.png)
   
2. Запуск анализатора
   
    ![2](https://github.com/RziankinS/devops-netology/blob/367ac492d740c0c0c36a785aba3d3af43456c650/screen/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%20%D0%BE%D1%82%202024-04-09%2016-30-51.png)

## Nexus

1. Загрузка артефактов с GAV-параметрами в репозиторий `maven-public`:

    ![3](https://github.com/RziankinS/devops-netology/blob/367ac492d740c0c0c36a785aba3d3af43456c650/screen/maven-releases.png)
   
2. файл `maven-metadata.xml` для этого артефекта:
   
    [`maven-metadata.xml`](https://github.com/RziankinS/dev/blob/4ef5357f3ac4e43095858dafc29c78e6850fcf28/ci-03/maven-metadata.xml)


## Maven

1. Версия mvn

  ![4](https://github.com/RziankinS/devops-netology/blob/1b59c32bf4eb7de53332e81cbc12fda61c5900b3/screen/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%20%D0%BE%D1%82%202024-04-09%2023-32-37.png)

2. mvn package:
   
  ![5](https://github.com/RziankinS/devops-netology/blob/1b59c32bf4eb7de53332e81cbc12fda61c5900b3/screen/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%20%D0%BE%D1%82%202024-04-09%2022-47-31.png)

3. Исправленный pom.xml:
   
   [pom.xml](https://github.com/RziankinS/dev/blob/0ede32c99cc98d50d49e96b5938616a49d939954/ci-03/pom.xml)  
 
---
