# Actividad-24-cc3s2
Actividad 24 del curso de Desarrollo de Software CC3S2

En esta actividad, veremos cómo podemos pasar de un solo host Docker a un grupo de máquinas
### Introducción a la clustering de servidores
- Un clúster es un conjunto de computadoras conectadas que se gestionan juntos y funcionan de tal manera que es equivalente a usar un solo sistema.

- Mientras que los nodos se encargan de ejecutar las aplicaciones, el maestro es el responsable de delegar las tareas, del proceso de orquestación, el descubrimiento de servicios, equilibrio de carga y detección de fallas de nodos

### Introducción a Kubernetes
Kubernetes es un sistema de administración de clústeres de código abierto. Entre sus principales características, tenemos a los siguientes:
- Equilibrio de contenedores
- Equilibrio de carga de tráfico
- Escalamiento horizontal dinámico
- Recuperación de fallas
- Actualizaciones continuas
- Orquestación de almacenamiento
- Detección de servicios
- Ejecutar en todas partes

 ### Instalación de Kubernetes
 Al igual que Docker, Kubernetes también cuenta con un cliente (kubectl) y un servidor.
 
 ### Cliente de Kubernetes
 El cliente de kubernetes, llamado kubectl, es una aplicación de línea de comandos que te permite realizar operaciones en el clúster de kubernetes.
 Para verificar si se ha instalado correctamente se puede ejecutar el sgte comando:
 ![Alt text](https://raw.githubusercontent.com/ricardoolivaresventura/Actividad-24-cc3s2/main/kubernetes-version.PNG "")
 
#### Servidor de Kubernetes
Hay varias formas de configurar un servidor de Kubernetes, pero si somos completamente nuevos en Kubernetes, entonces se recomienda comenzar desde un entorno local

#### Entorno local
Existen algunas herramientas que pueden simplificar su configuración de desarrollo local. Repasamos las opciones que tiene (Docker desktop, kind y minikube)

- En mi caso, yo estoy en Windows y tengo instalado Docker Desktop, por lo tanto, bastará con habilitada la casilla Kubernetes en la interfaz de usuario
 ![Alt text](https://raw.githubusercontent.com/ricardoolivaresventura/Actividad-24-cc3s2/main/enable-kubernetes.PNG "")
- Luego, podemos ver que kubernetes está corriendo
 ![Alt text](https://raw.githubusercontent.com/ricardoolivaresventura/Actividad-24-cc3s2/main/kubernetes-running.PNG "")
 
 #### Verificación de la configuración de Kubernetes
- Independientemente de la instalación de kubernetes que hayamos elegido, deberíamos poder ver la información del clúster con el comando kubectl cluster-info
![Alt text](https://raw.githubusercontent.com/ricardoolivaresventura/Actividad-24-cc3s2/main/kubernetes-running-2.PNG "")
 
### Uso de Kubernetes
Haremos uso de la imagen de Docker que creamos en actividades anteriores, "calculador"
 
### Implementación de una aplicación
- Para iniciar un contenedor Docker en Kubernetes, debemos preparar una configuración de implementación como un archivo YAML
![Alt text](https://raw.githubusercontent.com/ricardoolivaresventura/Actividad-24-cc3s2/main/deployment2.PNG "")

- En esta configuración de YAML, hemos definido lo sgte:
1. Hemos definido un recurso de Kubernetes del tipo Deployment de la versión de la API de
Kubernetes apps/v1.
2. El nombre de implementación único es calculador-deployment.
3. Hemos definido que debe haber exactamente 3 Pods iguales creados.
4. selector define cómo Deployment encuentra Pods para administrar, en este caso, solo por la
etiqueta.
5. template define la especificación para cada Pod creado.
6. Cada Pod está etiquetado con la aplicación: calculador.
7. Cada Pod contiene un contenedor Docker llamado calculador.
8. Se creó un contenedor Docker a partir de la imagen llamado checha/calculador.
9. El Pod expone el puerto del contenedor 8080.

- Para instalar la implementación debemos ejecutar el sgte comand "kubectl apply -f deployment.yaml"
![Alt text](https://raw.githubusercontent.com/ricardoolivaresventura/Actividad-24-cc3s2/main/install-deployment.PNG "")
- Podemos verificar que se hayan creado los tres Pods, cada uno en un contenedor Docker, con el sgte comando:
![Alt text](https://raw.githubusercontent.com/ricardoolivaresventura/Actividad-24-cc3s2/main/get-pods.PNG "")

### Implementación de un servicio de Kubernetes
