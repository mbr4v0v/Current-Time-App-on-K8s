Deployment.yaml

Descripción General
El archivo deployment.yaml define la configuración del Deployment de Kubernetes, que gestiona cómo se despliegan los pods de la aplicación Time Server en el clúster.
Estructura del deployment.yaml
yamlCopyapiVersion: apps/v1
kind: Deployment
metadata:
  name: timer-server
spec:
  replicas: 2
  selector:
    matchLabels:
      app: timer-server
  template:
    metadata:
      labels:
        app: timer-server
    spec:
      containers:
      - name: timer-server
        image: mbravov/timer-server:latest
        ports:
        - containerPort: 5000

Explicación Línea por Línea

apiVersion: apps/v1 - Especifica la versión de la API de Kubernetes a utilizar
kind: Deployment - Define que este recurso es un Deployment
metadata: - Sección para metadatos del recurso
  name: timer-server - Nombre del Deployment
spec: - Especificaciones del Deployment
  replicas: 2 - Configura 2 réplicas (pods) para alta disponibilidad
  selector: - Define cómo el Deployment identifica los pods que debe gestionar
    matchLabels: - Selector basado en etiquetas
      app: timer-server - La etiqueta específica para seleccionar pods
  template: - Plantilla para crear nuevos pods
    metadata: - Metadatos para los pods
      labels: - Etiquetas para los pods
        app: timer-server - Etiqueta que coincide con el selector
    spec: - Especificaciones para los pods
      containers: - Lista de contenedores en cada pod
      - name: timer-server - Nombre del contenedor
        image: mbravov/timer-server:latest - Imagen del contenedor a utilizar
        ports: - Puertos expuestos por el contenedor
        - containerPort: 5000 - Puerto 5000 expuesto por el contenedor


Características Principales

Alta disponibilidad: Mantiene 2 réplicas activas para garantizar que el servicio siempre esté disponible
Etiquetas: Utiliza etiquetas para organizar y seleccionar recursos
Imagen de contenedor: Usa la imagen mbravov/timer-server:latest
Exposición de puertos: Configura el puerto 5000 para la aplicación Flask


Posibles Mejoras

Añadir solicitudes y límites de recursos (CPU/memoria)
Configurar sondas de salud (readiness/liveness probes)
Implementar estrategias de actualización (RollingUpdate)
Usar una versión específica de la imagen en lugar de :latest
Añadir configuración de volúmenes si fuera necesario
