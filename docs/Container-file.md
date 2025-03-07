Documentación del Containerfile
Descripción General
El Containerfile define cómo construir la imagen de contenedor para la aplicación Time Server. 
Utiliza una imagen base de Python 3.9 y configura todo lo necesario para ejecutar la aplicación Flask.

Estructura del Containerfile:

dockerfileCopy# Containerfile
FROM python:3.9-slim
WORKDIR /app
COPY . /app
RUN pip install flask
CMD ["python", "app.py"]
Explicación Línea por Línea

- FROM python:3.9-slim - Utiliza la imagen oficial de Python 3.9 en su versión "slim", que es más pequeña que la imagen completa
- WORKDIR /app - Establece el directorio de trabajo dentro del contenedor como /app
- COPY . /app - Copia todos los archivos del directorio actual al directorio /app en el contenedor
- RUN pip install flask - Instala el framework Flask utilizando pip
- CMD ["python", "app.py"] - Define el comando que se ejecutará cuando el contenedor se inicie

Buenas Prácticas Implementadas:

Imagen base ligera: Utiliza la variante "slim" para reducir el tamaño de la imagen
Dependencias mínimas: Solo instala Flask, que es la única dependencia necesaria
Comando explícito: Define claramente cómo iniciar la aplicación

Posibles Mejoras

Añadir un archivo requirements.txt y usar pip install -r requirements.txt para gestionar dependencias
Implementar un usuario no-root para ejecutar la aplicación
Utilizar multi-stage builds para reducir aún más el tamaño de la imagen
Añadir etiquetas (LABEL) para metadatos como versión, mantenedor, etc.
