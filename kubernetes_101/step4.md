# PODS 101. Ficheros yaml.

Nota: Como el curso es un poco largo, es posible que el entorno se nos reinicie, por lo que recomiendo es reiniciar el lab y volver a este paso. 

`git clone https://github.com/vthot4/kubernetes_101_lab.git`{{execute}}

`cd kubernetes_101_lab/`{{execute}}

`chmod +x environment.sh`{{execute}}

`./environment.sh`{{execute}}

`cd`{{execute}}

Comprobamos que todo esta correcto:

`minikube status`{{execute}}



## Introducción

Hasta ahora hemos estado hablando de cómo trabajar con Kubernetes exclusivamente desde la línea de comando, pero esa una es una buena forma para entornos productivos y es más recomendable es uso de ficheros **Yaml** *(Another Markup Language)*.  Es un formato basado en texto legible por humanos para especificar información de tipo de configuración. El uso de este tipo de ficheros para las definiciones de K8 le brinda una serie de ventajas, que incluyen:

- **Convivencia**. Evitamos tener comandos con parámetros inmanejables. 
- **Mantenimiento.** Los archivos se pueden agregar a nuestro gestor de código, con lo que conseguimos todos los beneficios que nos proporciona este tipo de gestión.
- **Flexibilidad.** Permitirá crear estructuras mucho más complejas y sencillas de entender.

Yaml es un subconjunto de JSON, lo que significa que cualquier archivo JSON válido también es un archivo Yaml válido.  No es habitual que nos encontremos ficheros en JSON, pero podría ser posible. 

El mundo de Yaml es amplio, pero para el universo de Kubernetes nos bastará con conocer **List** y **Maps**. No quiere decir que no podamos hacer cosas más complejas, pero estas dos serán la base.

**Mapas Yaml** Los mapas nos permiten asociar pares de nombre-valor, cosa que nos viene muy bien para definir configuraciones. Un ejemplo sencillo:

```yaml
---
apiVersion: v1
Kind: Pod
```

También podemos especificar estructuras un poco más complicadas, creando una clave que se asigne a otro mapa, en lugar de una cadena, como en el siguiente ejemplo:

```yaml
---
apiVersion: v1
kind: Pod
metadata:
	name: webserver
	labels:
		app: web
```

En este caso, tenemos una clave, metadatos, que tiene como valor un mapa con 2 claves más, name y labels.  El procesador Yaml sabe cómo se relacionan las piezas usando el sangrado de líneas. Se suelen usar   dos espacios, pero la cantidad de espacios no es relevante mientras que siempre usemos la misma regla.

**Listas Yaml** Las listas de YAML son literalmente una secuencia de objetos. Por ejemplo:

```yaml
args:
	- sleep
	- "1000"
	- message
	- "Bring back Firefly"
```

por su puesto, los miembros de una lista pueden ser también mapas:

```yaml
---
apiVersion: v1
kind: Pod
metadata:
  name: webserver
  labels:
    app: web
spec:
  containers:
    - name: front-end
      image: nginx
      ports:
        - containerPort: 80
    - name: rss-reader
      image: nginx
      ports:
        - containerPort: 90
```

Como podemos ver aquí, tenemos una lista de contenedores "objetos", cada uno de los cuales consiste en un nombre, una imagen y una lista de puertos. Cada elemento de la lista debajo de los puertos es en sí mismo un mapa que enumera el containerPort y su valor.



## Crear un Pod usando Yaml.

vamos a levantar el mismo Pod que hemos usado en los ejemplos anteriores pero vamos a usar un yaml. Vamos a ver como podemos lanzar un pod o un deployment y los matices que presentan las diferentes opciones de despliegue.

El primer Yaml que vamos a usar es este:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: webserver
  labels:
    zone: prod
    version: v1
spec:
  containers:
   - name: nginx   
     image: nginx
```

Podemos crear el fichero o usar el que hemos bajado en repo del inicio del documento. Podemos verlo:

`cat kubernetes_101_lab/pod/lab1/nginx.yaml`{{execute}}

Explicamos algunas de las partes del fichero:

- **apiVersion.** Indicamos la versión que necesitamos.
- **kind.** Es donde indicamos el tipo de componente que queremos crear.
- **metadata.** Nos sirve para poner determinadas características al Pod. Más adelante veremos la utilidad de los labels.
- **spec.** Lugar donde definimos las especificaciones del Pod. Por ejemplo el nombre de la imagen que vamos a usar.

Existen numerosas etiquetas que no vamos a ver, pero que nos podemos ir encontrando en ejemplos y en la documentación.

Para crear nuestro primer Pod con un fichero *"yaml"* usaremos el modificador **create** de kubectl:

`kubectl create -f kubernetes_101_lab/pod/lab1/nginx.yaml`{{execute}}

Comprobamos que el Pod se ha creado correctamente:

`kubectl get pods`{{execute}}

`kubectl get deploy`{{execute}} 

Comprobamos que hemos creado un Pod y no un despliegue.



## Generando el yaml de un Pod en ejecución.

Algunas veces no disponemos de los yaml que han usado para desplegar el Pod que se encuentra en ejecución. Aunque no es una práctica que deberías permitir en nuestros entornos, podemos obtener de forma sencilla la configuración del Pod. Para ello:

`kubectl get pod webserver -o yaml`{{execute}}

Lo mas interesante es redireccionar esta salida a un fichero:

`kubectl get pod webserver -o yaml >> webserver.yml`{{execute}}

Vamos a hacer una pequeña prueba a ver si podemos recuperar el Pod desde el fichero que acabamos de crear. Primero borraremos el Pod y pasaremos a crearlo desde el fichero *"webserver.yaml":

`kubectl delete pod webserver`{{execute}}

`kubectl get pods`{{execute}}

`kubectl create -f webserver.yml`{{execute}}

`kubectl get pods`{{execute}}

Para terminar borramos el Pod:

`kubectl delete pod webserver`{{execute}}

