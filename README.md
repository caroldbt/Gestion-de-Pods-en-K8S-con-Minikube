
# Configuración y Gestión de un Pod en Minikube
Este documento proporciona una guía paso a paso para reiniciar Minikube, crear un pod, verificar su estado, reenviar puertos y editar archivos dentro del pod.

## Requisitos
Minikube instalado
Kubectl instalado
Editor de texto (por ejemplo, Notepad)
## Pasos
1. Eliminar Minikube y Reiniciar
Primero, eliminamos Minikube y purgamos todos los datos:
```
minikube delete --purge
```
Luego, reiniciamos Minikube:
```
minikube start
```
2. Crear el Pod
Abrimos un editor de texto (en este caso, Notepad) para crear el archivo de definición del pod:
```
notepad pod-definition.yaml
```
Pegamos el contenido del archivo pod-definition.yaml en Notepad y guardamos el archivo. Luego, aplicamos la configuración para crear el pod:
```
kubectl apply -f .\pod-definition.yaml
```
3. Verificar el Estado del Pod
Verificamos el estado del pod para asegurarnos de que se ha creado correctamente:
```
kubectl get pods
```
4. Reenviar un Puerto del Pod a la Máquina Local
Reenviamos un puerto del pod a la máquina local para poder acceder a los servicios que corren en el pod:
```
kubectl port-forward my-pod 80:80
```
5. Acceder al Pod y Editar Archivos
Accedemos al pod usando kubectl exec para poder ejecutar comandos dentro del pod:
```
kubectl exec -it my-pod -- /bin/bash
```
Navegamos al directorio donde se encuentran los archivos HTML:
```
cd /usr/share/nginx/html/
ls -la
```
Actualizamos el paquete de listas de fuentes:
```
apt-get update
```
Instalamos el editor de texto nano para editar archivos:
```
apt-get install nano -y
```
Finalmente, editamos el archivo index.html:
```
nano index.html
```
## Archivo de Definición del Pod
A continuación, se muestra un ejemplo de contenido que podrías tener en pod-definition.yaml:
```
yaml
Copiar código
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
    - name: nginx
      image: nginx:latest
      ports:
        - containerPort: 80
```
Este archivo define un pod llamado my-pod que ejecuta un contenedor con la imagen de nginx en el puerto 80.

