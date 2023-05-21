# D3.4-Practice-Kubernetes

Описание
Итоговое задание модуля базируется на предыдущих заданиях в юнитах.

Вам предлагается:

  - создать сущность Deployment c тремя репликами веб-сервера;
  - добавить к нему сервис;
  - интегрировать его внутрь конфигурации с помощью ConfigMap;
  - добавить секрет для создания basic auth аутентификации в nginx.

Задание
1. Создать Deployment со свойствами ниже:
  - образ — nginx:1.21.1-alpine;
  - имя — nginx-sf;
  - количество реплик — 3.

2. Создать конфигурационный файл для нашего приложения и поместить его в наш Pod со следующими свойствами:
  - путь до файла в Pod’е — /etc/nginx/nginx.conf;
  - содержимое файла:
    user nginx;
    worker_processes  1;
    events {
      worker_connections  10240;
    }
    http {
      server {
          listen       80;
          server_name  localhost;
          location / {
            root   /usr/share/nginx/html;
            index  index.html index.htm;
        }
      }
    } 

3. Создать service для того, чтобы можно было обращаться к любому из Pod’ов по единому имени:
  - имя сервиса sf-webserver;
  - внешний порт — 80.

4. Создать секрет со следующими данными:
  - имя секрета — auth_basic;
  - ключ объекта в секрете — user1;
  - значение объекта в секрете user1 — password1;

5. Подключить в наш контейнер эти секреты. Обновить конфиг nginx таким образом, чтобы подключенные секреты использовались для авторизации для доступа к странице по умолчанию в nginx.


Запускаем создание сущностей из всех yaml файлов, находящихся в рабочем каталоге:
  - kubectl apply -f ./

И смотрим результат развёртывания и состояние кластера:
  - kubectl get all
  - kubectl get secrets
  - kubectl get nodes
  - minikube status -p multinode-demo

![Screenshot_1](https://github.com/MikhailRyzhkin/D3.4-Practice-Kubernetes/assets/69116076/1cb443f8-4070-4a89-b77d-4a3180d6546f)

