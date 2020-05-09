# Kubernetes 101

En este pequeño laboratorio vamos a ver los conceptos básicos de Kubernetes. Para ello vamos a utilizar **minikube**, una herramienta que nos permite desplegar un clúster de Kubernetes con un único nodo en una máquina virtual. 

Para evitar problemas con la instalación, hemos optado que estuviera instalado. Si queremos ver cual es el procedimiento de instalación en los diferentes entornos podemos recurrir a:

> https://kubernetes.io/es/docs/tasks/tools/install-minikube/

Para instalarlo en un entorno Linux, deberemos instalar previamente un hypervisor como  [KVM](http://www.linux-kvm.org/) o [Virtualvox](https://www.virtualbox.org/wiki/Downloads) y el interfaz de línea de comando de kubernetes: [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) .  Una vez cumplidos estos requisitos podemos realizar la instalación de Minikube con:

``` bash
$ curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && chmod +x minikube 

$ sudo cp minikube /usr/local/bin && rm minikube
```

Minikube presenta las siguientes características:

- DNS
- NodePorts
- ConfigMAps and Secrets.
- Dashboards.
- Container Runtime: Docker, CRI-O, and containerd.
- Enabling CNI(Container Network Interface).
- Ingress.



## Empezamos a jugar con minikube.

Lo primero que tenemos que hacer es comprobar que minikube esta instalado y funciona correctamente:

`minikube version`{{execute}}

Podemos ver todos las posibilidades que nos ofrece:

`minikube `{{execute}}

Comprobado que minikube esta instalado y operativo, vamos a levantar el clúster mono-nodo:

`minikube start `{{execute}}

Si todo ha ido bien, deberíamos tener funcionando un clúster kubernetes en nuestra máquina. Minikube ha levantado una máquina virtual sobre el hypervisor donde ejecuta el clúster.

  ![Introduction to Minikube](./images/minikube-architecture.jpg )