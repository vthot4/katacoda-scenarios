# Primer despliegue en Kubernetes.

Intro

Conceptos





Creamos un deployment que iniciará un POD con nginx

`kubectl run --image=nginx nginx-app --port=80 --env="DOMAIN=cluster"`{{execute}}

Revisamos el pod que acabamos de crear

`kubectl get pods`{{execute}}

También podemos ver el deployment que se ha creado:

`kubectl get deployment`{{execute}}

Exponemos el puerto a través de un servicio

`kubectl expose deployment nginx-app --port=80 --name=nginx-http`{{execute}}

Revisamos el servicio que acabamos de crear

`kubectl get services`{{execute}}

`kubectl get svc`{{execute}}

Podemos ver toda la información a la vez:

`kubectl get po,svc,deploy`{{execute}}

Comprobamos que el servicio está expuesto:

$ curl 10.99.211.105:80



kubectl describe pod nginx-app-658666f5d-nxrv7



kubectl exec nginx-app-658666f5d-nxrv7 -- cat /etc/hostname

kubectl exec nginx-app-658666f5d-nxrv7 -- cat /etc/nginx/nginx.conf



kubectl logs -f nginx-app-658666f5d-nxrv7



Podemos escalar el deployment de la siguiente forma:

`kubectl get pods`{{execute}}

`kubectl scale deployment --replicas 3 nginx-app`{{execute}}

`kubectl get pods`{{execute}}

`kubectl scale deployment --replicas 10 nginx-app`{{execute}}

`kubectl get pods`{{execute}}

`kubectl scale deployment --replicas 1 nginx-app`{{execute}}

`kubectl get pods`{{execute}}



Exponemos los pods a internet

`kubectl expose deployment nginx-app --port=80 --type=LoadBalancer`{{execute}}

`kubectl get services`{{execute}}

mostrar el acceso a nginx



Borrar el entorno desplegado:

`kubectl delete deployment nginx-app`{{execute}}





