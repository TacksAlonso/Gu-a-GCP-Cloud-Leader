# ⚙️ Servicios Gestionados (`Managed Services`)

## ☁️ Modelos de Servicios en la Nube

Los modelos de servicio definen la división de responsabilidades entre el proveedor de la nube (Google) y el usuario (tú).

### IaaS (Infrastructure as a Service)

* **Definición:** El usuario alquila la infraestructura base (hardware virtual).
* **Usuario es Responsable de (Alta Responsabilidad):**
    * Código de la aplicación y *runtime*.
    * Configuración y parches del **Sistema Operativo (OS) invitado**.
    * Configuración de la seguridad de red (firewalls).
    * Gestión de la disponibilidad, autoescalado y balanceo de cargas.
* **Proveedor es Responsable de (Baja Responsabilidad):**
    * Infraestructura física (hardware).
    * Conectividad y *networking* de la infraestructura.
    * La plataforma base para crear VMs (Compute Engine).

### PaaS (Platform as a Service)

* **Definición:** El proveedor ofrece un entorno de desarrollo y despliegue listo para usar.
* **Proveedor es Responsable de (Media Responsabilidad):**
    * OS (actualizaciones y parches).
    * *Runtime* de la aplicación (Java, Python, etc.).
    * Autoescalado, disponibilidad y balanceo de cargas.
    * **Ejemplo GCP:** Google **App Engine**.
* **Usuario es Responsable de (Media Responsabilidad):**
    * Código y lógica de la aplicación.
    * Configuración específica de la aplicación.
* **Variantes de PaaS:**
    * FaaS (Function as a Service): Cloud Functions.
    * CaaS (Container as a Service): Google Kubernetes Engine (GKE), Cloud Run.
    * Bases de Datos Gestionadas: Cloud SQL (Relacionales), Firestore/Bigtable (NoSQL).
    * Servicios de Mensajería: Cloud Pub/Sub.

### SaaS (Software as a Service)

* **Definición:** Se ofrece software listo para usar a través de una suscripción. El usuario solo se preocupa por la configuración de la aplicación.
* **Proveedor es Responsable de (Máxima Responsabilidad):**
    * OS, *runtime*, código de la aplicación.
    * Autoescalado, disponibilidad y balanceo de cargas.
    * Mantenimiento completo de la aplicación.
* **Ejemplos:** Gmail, Google Workspace (Office tools), Calendarios, CRM, ERP.
* **Usuario es Responsable de (Mínima Responsabilidad):**
    * **Uso** y **configuración** de la aplicación.
    * Gestión de usuarios y políticas de acceso.

---

## ⚡ Serverless

* **Concepto:** Una forma de computación en la que el desarrollador **no gestiona la infraestructura** (VMs, OS, escalado), solo el código.
    * **No significa "sin servidores"**, sino que el servidor es gestionado por el proveedor.
* **Características Clave:**
    * **No hay gestión de infraestructura** (Compute Engine o *clusters*).
    * **Escalado Flexible y Automático:** Responde a la demanda, pudiendo escalar a cero.
    * **Alta Disponibilidad Automatizada.**
    * **Pago por Uso:** Se paga por las peticiones, la duración del código ejecutado y los recursos consumidos, **no por el número de servidores** en funcionamiento.
* **Servicios Serverless en GCP:** Google **Cloud Functions**, Google **Cloud Run**.

---

## 📦 Contenedores y Orquestación

### Evolución a Microservicios

* Las arquitecturas modernas migran de aplicaciones **monolíticas** a **microservicios** por su **flexibilidad**, **desacoplamiento** y la posibilidad de usar múltiples lenguajes de programación.
* El aumento de microservicios incrementa la **complejidad de despliegue**.

### Contenedores (Docker)

* **Qué es:** Un paquete ejecutable que contiene **todo** lo necesario para correr un microservicio: código, *runtime*, librerías y dependencias.
* **Ventajas:**
    * **Ligeros:** Son mucho más rápidos y ligeros que las VMs porque **no incluyen un OS invitado completo**.
    * **Aislamiento:** Están aislados entre sí. Un fallo en uno no afecta a los otros.
    * **Portabilidad:** Se ejecutan de forma consistente en entornos locales, de prueba y de nube.

### Orquestación de Contenedores (Kubernetes)

* **Propósito:** Gestionar, escalar, comunicar y desplegar grandes cantidades de contenedores de forma eficiente.
* **Kubernetes (Código Abierto):**
    * **Auto Escalado:** Ajusta el número de contenedores según la demanda.
    * **Service Discovery:** Permite a los microservicios encontrarse dinámicamente sin necesidad de direcciones fijas.
    * **Balanceo de Carga:** Distribuye el tráfico entre las instancias del microservicio.
    * **Auto Sanación (`Self-Healing`):** Reemplaza automáticamente los contenedores fallidos con instancias sanas.
    * **Despliegues sin Interrupción (`Zero Downtime Deployments`):** Permite actualizar el código sin afectar al servicio.
* **Servicios GCP:**
    * **Google Kubernetes Engine (GKE):** Servicio gestionado de Kubernetes. Requiere configuración avanzada de *clusters*.
    * **Cloud Run:** Servicio **Serverless** para ejecutar contenedores. **No necesita un *cluster*** de Kubernetes.

---

## 🤝 Modelo de Responsabilidad Compartida

La seguridad en la nube es una responsabilidad compartida entre Google y el cliente.

* **Google (Proveedor) es Responsable de (Security *of* the Cloud):**
    * **Infraestructura Física:** Hardware, *networking*.
    * **Base de la Nube:** Almacenamiento + Cifrado, *Audit Logging*, *Hardened Kernel* (Sistema Operativo del host).
* **Cliente (Usuario) es Responsable de (Security *in* the Cloud):** Varía según el modelo de servicio.

| Servicio | Responsabilidades del Cliente |
| :--- | :--- |
| **SaaS** | Contenido, Políticas de Acceso, Uso del servicio. |
| **PaaS** | *Responsabilidades SaaS* + Código de la Aplicación, Configuración de Despliegue, Seguridad de la Aplicación Web. |
| **IaaS** | *Responsabilidades PaaS* + **Sistema Operativo Invitado**, Parches del OS, Seguridad de Red (Firewalls), Operaciones. |

---

## 🎯 Servicios de Computación de GCP

| Servicio | Detalles | Categoría |
| :--- | :--- | :--- |
| **Compute Engine** | VMs de alto rendimiento y propósito general que escalan globalmente. | IaaS |
| **Google Kubernetes Engine (GKE)** | Orquesta microservicios en contenedores con Kubernetes. Necesita configuración y monitoreo del *cluster*. | CaaS |
| **App Engine** | Plataforma completamente gestionada para construir aplicaciones escalables. | PaaS (o Serverless para el entorno *Standard*) |
| **Cloud Functions** | Aplicaciones impulsadas por eventos usando funciones simples y de un solo propósito. | FaaS, Serverless |
| **Cloud Run** | Desarrollar y desplegar aplicaciones en contenedores altamente escalables **sin la necesidad de un *cluster***. | CaaS, Serverless |