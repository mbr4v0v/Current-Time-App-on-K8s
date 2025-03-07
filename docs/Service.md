Service.yaml

Descripción General
El archivo service.yaml define el Servicio de Kubernetes que expone la aplicación Time Server dentro y fuera del clúster, actuando como punto de entrada estable para los pods.
Estructura del service.yaml
yamlCopyapiVersion: v1
kind: Service
metadata:
  name: timer-server-service
spec:
  type: NodePort
  selector:
    app: timer-server
  ports:
  - protocol: TCP
    port: 80
    targetPort: 5000
    nodePort: 30008
Explicación Línea por Línea

apiVersion: v1 - Especifica la versión de la API de Kubernetes a utilizar
kind: Service - Define que este recurso es un Service
metadata: - Sección para metadatos del recurso
  name: timer-server-service - Nombre del Servicio
spec: - Especificaciones del Servicio
  type: NodePort - Tipo de servicio que expone el puerto en cada nodo del clúster
  selector: - Define qué pods serán seleccionados por este servicio
    app: timer-server - Selecciona los pods con la etiqueta app: timer-server
  ports: - Configuración de puertos
  - protocol: TCP - Protocolo utilizado (TCP)
    port: 80 - Puerto expuesto por el servicio (interno al clúster)
    targetPort: 5000 - Puerto del contenedor al que se redirige el tráfico
    nodePort: 30008 - Puerto expuesto externamente en cada nodo del clúster

Características Principales

Tipo NodePort: Expone el servicio en un puerto específico (30008) en todos los nodos del clúster
Mapeo de puertos: Traduce el puerto 80 (estándar HTTP) al puerto 5000 de la aplicación Flask
Selector de pods: Dirige el tráfico solo a los pods con la etiqueta app: timer-server

Uso
El servicio puede ser accedido de dos formas:

Desde fuera del clúster:
Copyhttp://<CUALQUIER-IP-DE-NODO>:30008/

Desde dentro del clúster:
Copyhttp://timer-server-service/
o
Copyhttp://timer-server-service.default.svc.cluster.local/


Posibles Mejoras

Considerar usar LoadBalancer en entornos cloud
Implementar Ingress para gestión de tráfico HTTP/HTTPS más avanzada
Añadir anotaciones para configuraciones específicas del proveedor
Configurar múltiples puertos si la aplicación lo requiriera
