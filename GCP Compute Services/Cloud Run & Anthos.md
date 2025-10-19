# 🚀 Cloud Run

**Cloud Run** es el servicio de computación **Serverless** (*Sin servidor*) de Google Cloud que te permite ejecutar **contenedores sin estado** (*Stateless Containers*) mediante peticiones web (HTTP). Permite pasar de contenedores a producción en cuestión de segundos.

### ✨ Características Clave

* **Serverless Totalmente Gestionado:**
    * Cero gestión de infraestructura (*Zero Infrastructure Management*).
    * No hay que gestionar **Kubernetes *clusters*** (a diferencia de GKE).
* **Basado en Estándares:** Está basado en el estándar abierto **Knative**, lo que asegura portabilidad y facilita el cambio entre entornos *Serverless*.
* **Flujo de Trabajo del Despliegue:** Se elige la aplicación a desplegar, ya sea seleccionando una **imagen de contenedor** (*Container Image*) de **Artifact Registry** o generándola a partir de un **repositorio de código fuente** (*Source Repository*).
    * **Nota:** Una vez creado, **no se puede cambiar el nombre del servicio** ni la **región** de Cloud Run.

### 💰 Configuración y Costos

* **Asignación de CPU:** Se puede configurar el modelo de cobro y asignación de recursos:
    * **CPU solo durante el procesamiento de solicitudes:** (Modelo por defecto) La CPU se asigna solo mientras se procesa una petición. **Se cobra por invocación.** Ideal para un modelo *Pay-per-use*.
    * **CPU siempre asignada:** La CPU está disponible todo el tiempo, incluso sin peticiones. Necesario para tareas en segundo plano o *background tasks*.
* **Pago por Uso (`Pay-per-use`):** Solo se cobra por los recursos consumidos: CPU, Memoria (*Memory*), Peticiones (*Requests*) y *Networking*.
* **Auto-Scaling (Autoescalado) a Cero:** Se puede llegar a tener **cero instancias** (*Scale-to-Zero*) cuando no hay tráfico. Esto es **cost-effective** (rentable) y es la estadística genial (*The Key Metric for Serverless*).
    * **Latency Penalty (Penalización de Latencia):** Si llega una petición y no hay instancias, el sistema experimenta un **cold start** (arranque en frío) mientras se lanza el contenedor, lo que añade latencia al tiempo de respuesta. Para evitarlo, se pueden configurar **instancias mínimas** (*Min Instances*).

### 🛡️ Red y Seguridad

* **Configuración de Ingreso de Tráfico (`Traffic Ingress`):**
    * **Allow all traffic:** Tráfico público de Internet.
    * **Allow internal traffic and traffic from Cloud Load Balancing:** Tráfico de la red interna de GCP y peticiones que pasan por un Balanceador de Carga.
    * **Allow internal traffic only:** Solo el tráfico originado dentro de tu red VPC (*Virtual Private Cloud*) o de otros servicios de GCP.
* **Autenticación:** Se puede solicitar **autenticación** (*Authentication*) (vía IAM o cuentas de servicio) para restringir el acceso al servicio.

### 🛠️ Ecosistema y Desarrollo

* **Experiencia de Desarrolladores *End-to-End*:** No se limita a lenguajes, binarios ni dependencias, gracias al uso de contenedores.
* **Portabilidad:** Fácil portabilidad gracias a la contenedorización (*Containerization*).
* **Integración con Servicios:** Se integra con **Cloud Code**, **Cloud Build**, **Cloud Monitoring** y **Cloud Logging**.

---

# 🏛️ Anthos

**Anthos** es una plataforma de aplicación *open-source* (*código abierto*) que permite a las organizaciones modernizar sus aplicaciones, gestionar *clusters* de **Kubernetes** en **cualquier lugar** y aplicar políticas de seguridad y configuración de manera uniforme.

### 🌐 Funcionalidad Clave

* **Gestión Híbrida y Multi-Nube:** Permite correr y gestionar **Clusters de Kubernetes** de forma consistente en:
    * **Cloud** (Google Cloud).
    * **Multi-Cloud** (Otras nubes, como AWS o Azure).
    * **On-Premise** (Centros de datos locales).
* **Objetivo:** Ofrecer una **plataforma única** de desarrollo y operación, sin importar dónde se ejecute la carga de trabajo.

### 📦 Cloud Run for Anthos

* **Definición:** Es una implementación de Cloud Run que permite desplegar tus cargas de trabajo de contenedores usando la misma experiencia **Serverless** (*Sin servidor*) **dentro de tus clusters de Anthos** (ya sea en GCP o *On-Premise*).
* **Beneficio:** Combina la facilidad de uso y el escalado a cero de Cloud Run con el control y la flexibilidad de tener un *cluster* de Kubernetes donde tú elijas.