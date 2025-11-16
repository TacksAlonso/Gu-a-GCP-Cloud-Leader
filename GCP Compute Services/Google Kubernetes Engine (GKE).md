# ☸️ Google Kubernetes Engine (GKE)

## Kubernetes

**Kubernetes** (K8s) es la solución de **Orquestador** (*Orchestrator*) de contenedores más popular y de código abierto (*Open-Source*).

### 📄 Conceptos Clave

* **Cluster (Clúster):** Un **cluster** es un conjunto de máquinas (VMs) que se agrupan para trabajar como un único sistema. Se compone de un **Control Plane** (Plano de control, el cerebro del clúster) y **Worker Nodes** (Nodos trabajadores) que ejecutan los contenedores.
* **Worker Node (Nodo Trabajador):** Las VMs en el *cluster* donde se ejecuta la carga de trabajo (contenedores).
* **Pod (Cápsula):** La unidad de despliegue más pequeña en Kubernetes. Un **Pod** representa una instancia de la aplicación y contiene uno o más contenedores que se ejecutan de forma conjunta en el mismo nodo.

### ✨ Características del Orquestador

* **Auto Scaling (Autoescalado):** Ajusta automáticamente el número de *Pods* o *Nodes* según la demanda.
* **Service Discovery (Descubrimiento de Servicios):** Permite a los *Pods* encontrarse y comunicarse entre sí de forma dinámica.
* **Load Balancing (Balanceo de Carga):** Distribuye el tráfico de red entre múltiples *Pods*.
* **Self-Healing (Auto-sanación):** Monitorea la salud de los *Pods* y nodos; si uno falla, lo reemplaza o lo reinicia automáticamente.
* **Zero Downtime Deployments (Despliegues sin Interrupción):** Permite actualizar la aplicación sin afectar la disponibilidad del servicio.

---

## ☁️ Google Kubernetes Engine (GKE)

**GKE** es el **Servicio Gestionado** (*Managed Service*) de Google que permite desplegar, gestionar y escalar aplicaciones en contenedores utilizando Kubernetes.

* **Gestión Reducida:** Minimiza las operaciones de **Auto-Repair** (reparar nodos fallidos) y **Auto-Upgrade** (usa siempre la última versión de K8s).
* **Sistema Operativo Optimizado:** Utiliza **Container-Optimized OS (COS)**, un OS ligero y seguro creado por Google para ejecutar contenedores.
* **Almacenamiento:** Permite provisionar **Persistent Disks** (Discos Persistentes) y **Local SSDs** con los *Worker Nodes*.

### 🤝 Tipos de GKE

| Tipo | Gestión del Cluster | Responsabilidad del Cliente | Casos de Uso |
| :--- | :--- | :--- | :--- |
| **Standard (Estándar)** | **Parcialmente Delegada.** (GCP gestiona el *Control Plane*, el cliente gestiona los *Worker Nodes*: escalado, parches). | Cliente asume la **propiedad completa** del *cluster* y la gestión del *Node*. | Control total y personalización profunda. |
| **Autopilot** | **Completamente Delegada.** (GKE gestiona el *Control Plane* y escala automáticamente los *Worker Nodes*). | Cliente solo se preocupa por la aplicación (*Pods*). Experiencia **sin intervención** (*hands-off*). | Reducción de costos operacionales y enfoque total en el desarrollo. |

### 🚀 Relación entre Pods y Cluster

* **Pods (Unidad de Despliegue/Aplicación):** Aumentar *Pods* (escalado horizontal) incrementa la capacidad de la aplicación para manejar más tráfico o carga, utilizando los recursos **libres** del *Node* existente.
* **Cluster/Nodes (Unidad de Infraestructura/Recurso):** Aumentar *Nodes* (escalado del clúster) aumenta los recursos totales disponibles (CPU, RAM) para que se puedan programar **más Pods** en general.

> **Relación:** El **Horizontal Pod Autoscaling (HPA)** escala los *Pods*. Si los *Nodes* se quedan sin recursos para los nuevos *Pods*, el **Cluster Autoscaler** añade automáticamente nuevos *Nodes* al *Cluster* para satisfacer la demanda.

### 📈 Horizontal Pod Autoscaling (HPA)

**Horizontal Pod Autoscaling (HPA)** es un componente de Kubernetes que ajusta automáticamente el número de réplicas de *Pods* (*Deployment*) basándose en métricas observadas, como la utilización de CPU promedio o métricas personalizadas. Esto mantiene estable el rendimiento de la aplicación.

---

## 🛠️ Comandos Esenciales de GKE y Kubernetes

### Diferencia entre `gcloud` y `kubectl`

* **`gcloud`:** Interactúa con los **servicios de GCP** (crear/eliminar GKE *Cluster*, configurar proyectos).
* **`kubectl`:** Interactúa **dentro** del *cluster* de Kubernetes (desplegar *Pods*, *Services*).

### Comandos Comunes

| Comando | Tipo | Acción | Parámetros y Notas |
| :--- | :--- | :--- | :--- |
| `gcloud config set project` | `gcloud` | Configura el proyecto activo por defecto. | `[ID_DEL_PROYECTO]` |
| `gcloud container clusters create` | `gcloud` | Crea un nuevo **Cluster** de GKE. | `--zone [ZONA]`, `--num-nodes [N]` |
| `gcloud container clusters list` | `gcloud` | Lista los **Clusters** de GKE. | - |
| `gcloud container clusters get-credentials` | `gcloud` | **Configura `kubectl`** para conectarse al *Cluster* especificado. (Obligatorio antes de usar `kubectl`). | `[NOMBRE] --zone [ZONA]` |
| `gcloud container clusters resize` | `gcloud` | Cambia manualmente el número de **Nodes** en un *Cluster* (escalado manual del *Cluster*). | `[NOMBRE] --num-nodes=[N]` |
| `gcloud container clusters delete` | `gcloud` | Elimina un **Cluster** de GKE. | - |
| `kubectl create deployment` | `kubectl` | Crea un **Deployment** (Despliegue) de la aplicación. | `[NOMBRE] --image=[IMAGEN]` |
| `kubectl get deployment` | `kubectl` | Muestra el estado de los **Deployments** en el *Cluster*. | - |
| `kubectl expose deployment` | `kubectl` | Crea un **Service** (Servicio) para exponer el *Deployment* al tráfico (interna o externamente). | `--type=[LoadBalancer/NodePort/ClusterIP] --port=[PUERTO]` |
| `kubectl get services` | `kubectl` | Muestra los **Services** creados. | Muestra la IP pública del *LoadBalancer* si aplica. |
| `kubectl get services --watch` | `kubectl` | Muestra el estado del *Service* y lo **actualiza** automáticamente (útil para esperar la IP del *LoadBalancer*). | - |
| `kubectl scale deployment` | `kubectl` | Cambia el número de **réplicas de Pods** manualmente. | `--replicas=[N]` |
| `kubectl autoscale deployment` | `kubectl` | Crea un objeto **HPA** para autoescalar los *Pods*. | `--max=[N] --cpu-percent=[%]` |
| `kubectl get hpa` | `kubectl` | Muestra el estado de los objetos **Horizontal Pod Autoscaler**. | - |
| `kubectl delete [TIPO]` | `kubectl` | Elimina un recurso específico (`deployment`, `service`, `pod`). | `[TIPO] [NOMBRE]` |
| `curl [IP]:[PUERTO]/[RUTA]` | Shell | Comando de prueba para verificar la respuesta de la aplicación desplegada. | - |
| `gcloud container clusters resize my-cluster --node-pool default-pool --num-nodes=2 --zone=us-central1-c` | `gcloud` | Ejemplo de escalado manual del número de nodos en un *Node Pool* específico. | - |
| `kubectl autoscale deployment hello-world-rest-api --max=4 --cpu-percent=70` | `kubectl` | Ejemplo de creación de **HPA** para escalar hasta 4 réplicas con un objetivo de CPU del 70%. | - |
