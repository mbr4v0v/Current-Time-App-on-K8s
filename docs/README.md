
Time Server
Un servicio simple que proporciona la hora actual, implementado como microservicio en Kubernetes utilizando Flask.
Estructura del Proyecto

time-server/
├── app.py
├── Containerfile
├── deployment.yaml
├── service.yaml
├── README.md
├── LICENSE
├── docs/
│   ├── containerfile.md
│   ├── deployment.md
│   ├── service.md
│   └── images/
│       ├── architecture.png
│       └── sequence.png
└── .gitignore


app.py - Aplicación Flask que sirve la hora actual
Containerfile - Definición para construir la imagen del contenedor
deployment.yaml - Configuración del Deployment de Kubernetes
service.yaml - Configuración del Service de Kubernetes

Descripción de la Aplicación
La aplicación es un servidor web simple desarrollado con Flask que expone un único endpoint:

/ - Devuelve la hora actual en formato YYYY-MM-DD HH:MM:SS

Arquitectura
Este proyecto implementa un servicio básico para proporcionar la hora actual mediante una API web simple. La aplicación está contenerizada y desplegada en Kubernetes con las siguientes características:

Deployment: Configura 2 réplicas (pods) para alta disponibilidad
Service: Expone la aplicación como un NodePort en el puerto 30008
Contenedor: Basado en Python 3.9 slim, ejecuta la aplicación Flask

Requisitos

Python 3.9 o superior
Flask
Docker o Podman
Kubernetes cluster o Minikube
kubectl

Instalación
Construir la imagen de contenedor
podman build -t mbravov/timer-server:latest -f Containerfile .
o con Docker
$ docker build -t mbravov/timer-server:latest -f Containerfile .
Subir la imagen al registro de contenedores
$ podman push mbravov/timer-server:latest
o con Docker : $docker push mbravov/timer-server:latest

Desplegar en Kubernetes
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml

Uso:
Una vez desplegado, puedes acceder al servicio utilizando el NodePort configurado (30008): curl http://<node-ip>:30008/
O desde dentro del clúster: $ curl http://timer-server-service/

El servidor responderá con un mensaje como:
Current Time: 2025-03-07 16:25:30

Desarrollo
Para ejecutar la aplicación localmente durante el desarrollo:
Instalar dependencias: $ pip install flask

# Ejecutar la aplicación de forma normal
$ python app.py

La aplicación estará disponible en http://localhost:5000/

Pero dentro del clúster Kubernetes el procedimiento es :


Licencia
MIT
