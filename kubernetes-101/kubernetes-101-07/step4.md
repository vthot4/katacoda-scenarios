# Establecer un namespace por defecto.

Podemos indicar en un determinado contexto (un contexto determina el cluter y el usuario que podemos utilizar) un namespace, de tal manera que cuando utilicemos dicho contexto se va a utilizar el namespace indicado, y no será necesario indicarlo con la opción -n. Para ello es necesario determinar el contexto en el que estamos trabajando:

`kubectl config current-context`{{execute}}

Para modificar el contexto actual:

`kubectl config set-context kubernetes-admin@kubernetes --namespace=produccion`{{execute}}

`kubectl config current-context`{{execute}}

