# Primeras pruebas con el clúster.

Comenzaremos levantando el entorno de minikube.

`minikube start`{{execute}}

Una vez arrancado vamos a ver los detalles del clúster que hemos creado mediante *kubectl cluster-info*:

`kubectl cluster-info`{{execute}}

Para ver los nodos que tenemos levantados:

`kubectl get nodes`{{execute}}

Este comando muestra todos los nodos que se pueden utilizar para hospedar nuestras aplicaciones. Ahora solo tenemos un nodo y podemos ver que su estado es *"Ready"* para recibir nuestras aplicaciones.

