# Conociendo nuestro clúster.

> Un clúster es una colección de recursos de cómputo, almacenamiento y redes que Kubernetes usa para ejecutar las diversas cargas de trabajo que componen su sistema.



Comenzaremos levantando el entorno de minikube.

`minikube start`{{execute}}

Una vez arrancado vamos a ver los detalles del clúster que hemos creado mediante *kubectl cluster-info*:

`kubectl cluster-info`{{execute}}

Una forma sencilla de tener un diagnóstico del estado del clúster es usar:

`kubectl get componentstatuses`{{execute}}

Deberemos obtener algo parecido a esta salida:

```bash
$ kubectl get componentstatuses
NAME                 STATUS    MESSAGE             ERROR
controller-manager   Healthy   ok
scheduler            Healthy   ok
etcd-0               Healthy   {"health":"true"}
```

Podemos ver aquí los componentes que conforman el clúster de Kubernetes. 

- **controller-manageres**  Es el responsable de ejecutar varios controladores que regulan el comportamiento en el clúster; por ejemplo, garantizar que todas las réplicas de un servicio estén disponibles y en buen estado.
- **scheduleres** responsable de colocar diferentes Pods en diferentes nodos en el clúster. 
- **etcd** Es el almacenamiento para el clúster donde se almacenan todos los objetos API.



## Nodos

> Un nodo es un único host. Puede ser una máquina física o virtual. Su trabajo es ejecutar pods, que son la unidad mínima de procesamiento de Kubernetes. Cada nodo de Kubernetes ejecuta varios componentes de Kubernetes, como pueden ser  *kubelet* y *kube proxy*. Los nodos son gestionados por el nodo master. 

Para ver los nodos que tenemos levantados:

`kubectl get nodes`{{execute}}

Este comando muestra todos los nodos que se pueden utilizar para hospedar nuestras aplicaciones. Ahora solo tenemos un nodo y podemos ver que su estado es *"Ready"* para recibir nuestras aplicaciones.

Podemos usar *"kubectl describe"* para obtener información específica del nodo. Obtendremos información referente a:

- Información básica del nodo. (Sistema Operativo, procesador)
- Información sobre el funcionamiento.
- Información sobre la capacidad de la máquina.
- Información sobre el software del nodo.
- Información sobre los Pods que se están ejecutando.

`kubectl describe nodes minikube`{{execute}}



