# Запуск приложений в K8S

### Задание 1. Создать Deployment и обеспечить доступ к репликам приложения из другого Pod
- [x] 1. Создать Deployment приложения, состоящего из двух контейнеров — nginx и multitool:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 1
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.25.4
        ports:
          - containerPort: 80
      - name: multitool
        image: wbitt/network-multitool
        ports:
          - containerPort: 8080
```
![1](https://github.com/RziankinS/devops-netology/blob/75cc408609f30c3083513fbce9e670daecbd148a/screen/1.3/1.1.png)  

- [x] 1.1. Решить возникшую ошибку: добавляем в Deployment
```yaml
        env: 
          - name: HTTP_PORT
            value: "81"
```
![2](https://github.com/RziankinS/devops-netology/blob/75cc408609f30c3083513fbce9e670daecbd148a/screen/1.3/2.png)

- [x] 2. Увеличить количество реплик работающего приложения до 2:

![3](https://github.com/RziankinS/devops-netology/blob/75cc408609f30c3083513fbce9e670daecbd148a/screen/1.3/3.png)

- [x] 3. Создать Service, который обеспечит доступ до реплик приложений:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: deploy-service
  namespace: netology
spec:
  selector:
    app: nginx
  ports:
    - protocol: TCP
      name: nginx
      port: 80
      targetPort: 80
    - protocol: TCP
      name: multitool
      port: 8080
      targetPort: 8080
```
- [x] 4. Создать отдельный Pod с приложением multitool и проверить доступ через `curl`:

```yaml
apiVersion: v1
kind: Pod
metadata:
   name: multitool
   namespace: netology
spec:
   containers:
     - name: multitool
       image: wbitt/network-multitool
       ports:
        - containerPort: 8080
```

![4](https://github.com/RziankinS/devops-netology/blob/8917eb705708c0d626b58afaefeed0472d43549b/screen/1.3/5.png)

### Задание 2. Создать Deployment и обеспечить старт основного контейнера при выполнении условий

- [x] 1. Создать Deployment приложения nginx и обеспечить старт контейнера только после того, как будет запущен сервис этого приложения.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-init
  namespace: netology
spec:
  selector:
    matchLabels:
      app: nginx-init
  replicas: 1
  template:
    metadata:
      labels:
        app: nginx-init
    spec:
      containers:
      - name: nginx
        image: nginx:1.25.4
      initContainers:
      - name: wait-for-service
        image: busybox
        command: ['sh', '-c', "until nslookup svc-nginx-init.$(cat /var/run/secrets/kubernetes.io/serviceaccount/namespace).svc.cluster.local; do echo waiting for service; sleep 2; done;"]
```

![5](https://github.com/RziankinS/devops-netology/blob/8917eb705708c0d626b58afaefeed0472d43549b/screen/1.3/6.png)

- [x] 2. Создать и запустить Service. Убедиться, что Init запустился
```yaml
apiVersion: v1
kind: Service
metadata:
  name: svc-nginx-init
  namespace: netology
spec:
  ports:
    - name: nginx-init
      port: 80
  selector:
    app: nginx-init
```
![6](https://github.com/RziankinS/devops-netology/blob/9975c5d8ec64a3fc2c1ae90ca28e343d5102bf26/screen/1.3/7.png)
