# Reto 3 - Bootcamp DevOps

<img width="1195" height="611" alt="image" src="https://github.com/user-attachments/assets/4052474f-3650-4670-a186-3193964c8ff8" />


## Archivo del reto

El enunciado del reto se encuentra en: 
[Proyecto del BootCamp DevOps - Fase3 .pdf](https://github.com/user-attachments/files/23762673/Proyecto.del.BootCamp.DevOps.-.Fase.3.3.pdf)


Este repositorio contiene la **solución propuesta para el Reto #3** del Bootcamp de DevOps. A continuación se detalla la estructura y los componentes implementados.

Para la construcción de la infraestructura de AWS (VPC, subnets y NAT Gateway), se utilizó como referencia y punto de partida el siguiente repositorio:  
[aws-basic-infrastructure](https://github.com/braybaut/aws-basic-infrastructure)  
---

## Estructura del repositorio

- `microblog/`  
  Contiene el **Dockerfile** utilizado para construir la imagen de la aplicación del blog. Esta imagen fue subida a **ECR (AWS Elastic Container Registry)** para ser utilizada en los despliegues.

- `postgres-deployment.yaml`  
  Deployment de la base de datos PostgreSQL, configurada con **una sola réplica** para evitar problemas de concurrencia con el volumen persistente.

- `postgres-service.yaml`  
  Service que expone la base de datos dentro del cluster.

- `app-deployment.yaml`  
  Deployment de la aplicación del blog, configurada con **2 réplicas** para garantizar alta disponibilidad.

- `app-service.yaml`  
  Service que expone la aplicación dentro del cluster.

- `namespace.yml`  
  Archivo para la creación del namespace utilizado en todos los recursos (`microblog`).

- `ingress_app.yml`  
  Configuración del **Ingress** para exponer la aplicación a través de un Load Balancer.

- `lb-controller/`  
  Contiene todos los archivos YAML relacionados con la configuración del **Load Balancer** para la aplicación.

- `ebs-controller/`  
  Contiene los archivos YAML de **PersistentVolume (PV) y PersistentVolumeClaim (PVC)** para asegurar la **persistencia de datos** de la base de datos y la aplicación.

---

## Notas importantes

- La base de datos PostgreSQL utiliza un **volumen persistente EBS**, garantizando que los datos no se pierdan aunque el pod se reinicie o reprograme.
- La aplicación del blog está desplegada con **réplicas múltiples** para garantizar disponibilidad.
- Todos los controladores (LB y EBS) están separados en sus respectivas carpetas para facilitar la organización y mantenimiento de los recursos.

---
## Uso

1. Crear el namespace:

```bash
kubectl apply -f namespace.yml
kubectl apply -f ebs-controller/
kubectl apply -f postgres-deployment.yaml
kubectl apply -f postgres-service.yaml
kubectl apply -f app-deployment.yaml
kubectl apply -f app-service.yaml
kubectl apply -f app-deployment.yaml
kubectl apply -f app-service.yaml
```

## Documentacion de apoyo para instalar controladores lb y ebs

- https://docs.aws.amazon.com/eks/latest/userguide/lbc-manifest.html 
- https://docs.aws.amazon.com/eks/latest/userguide/ebs-csi.html




