# 🚀 App Engine

**App Engine** fue uno de los primeros servicios ofrecidos por GCP (lanzado en 2008) y es una de las maneras más sencillas de desplegar y escalar aplicaciones en Google Cloud.

* Es una plataforma **PaaS (Platform as a Service)** y un servicio **Serverless (Sin servidor)**.
* Proporciona una gestión *end-to-end* (de extremo a extremo) de las aplicaciones.
* **Menor Responsabilidad** para el usuario (menos gestión de infraestructura).
* **Menor Flexibilidad** comparado con Compute Engine o GKE.

### 💰 Facturación

* **No hay cargos por el uso de App Engine** en sí (el servicio de plataforma).
* **Sí hay cargos por el aprovisionamiento de recursos** (VMs subyacentes, almacenamiento, *networking*, etc.) que tu aplicación utiliza. El costo se basa en las horas de instancia, el tráfico y otros recursos que consume tu aplicación.

### ✨ Funcionalidades Clave (`Key Features`)

* **Automatic Load Balancing & Auto Scaling (Balanceo de Carga Automático y Autoescalado):** Escala automáticamente la aplicación según la demanda de tráfico.
* **Managed Platform Updates & Application Health Monitoring (Actualizaciones de Plataforma Gestionadas y Monitoreo de Salud de la Aplicación):** Google gestiona el OS y la plataforma de ejecución.
* **Application Versioning (Versionado de Aplicaciones):** Permite tener múltiples versiones del mismo código ejecutándose.
* **Traffic Splitting (División de Tráfico):** Permite dirigir porcentajes del tráfico entrante a diferentes versiones (útil para pruebas A/B o despliegues *Canary*).

---

## 🌎 Entornos de App Engine (`App Engine Environments`)

App Engine ofrece dos entornos principales, que difieren en el nivel de gestión y flexibilidad:

### ⚙️ App Engine Standard (Estándar)

* Las aplicaciones se ejecutan en entornos **aislados y securizados** dentro de *sandboxes*.
* **Aislamiento Completo del OS/Disco:** Solo debes proporcionar tu código y configuración; Google se encarga del OS y la infraestructura.
* **Escalado a Cero:** Las instancias se pueden reducir a **cero** cuando no hay tráfico (lo que ahorra costos).
* **Soporte de Runtimes:**
    * **V1:** Para versiones antiguas de: Java, Python, PHP, Go. **NO soporta .NET.**
    * **V2 (Recomendado):** Para versiones más recientes de: Java, Python, PHP, Go, Node.js, Ruby y **.NET**.
        * **Compatibilidad .NET:** Soporte para **.NET Core 3.1**, **.NET 6** y **.NET 7**. Las versiones más recientes como **.NET 8** y **.NET 9** generalmente se adoptan primero en el entorno Flexible o Cloud Run debido a las limitaciones del entorno Standard.

### 🛠️ App Engine Flexible (Flexible)

* Las aplicaciones se ejecutan dentro de **contenedores Docker personalizados**.
* **Uso de Máquinas Virtuales de Compute Engine (VMs) (Aclaración):** El entorno Flexible utiliza instancias de **VM de Compute Engine** detrás de escena para ejecutar tus contenedores. La diferencia es que Google **gestiona** estas VMs (parches, monitoreo) por ti; tú solo ves el entorno de App Engine, no las VMs directamente.
* **Soporte de Runtimes:** Soporta **cualquier *runtime*** porque corre contenedores. Ofrece soporte integrado para Python, Java, Node.js, Go, PHP o **.NET**.
* **No Escala a Cero:** Siempre debe haber al menos **una instancia** ejecutándose.

---

## 🗺️ Alcance del Servicio y Restricciones (Aclaración)

* **App Engine por Proyecto:** Es una restricción de diseño. Solo se puede crear **una única aplicación de App Engine por proyecto de GCP**.
* **Región Única:** Al crear la aplicación de App Engine por primera vez, debes seleccionar una **región**. Una vez seleccionada, **todos los recursos de App Engine** (servicios y versiones) de ese proyecto se implementarán en esa región y **no se puede cambiar**.
* **Necesidad de Múltiples Regiones:** Si necesitas una aplicación de App Engine desplegada en **múltiples regiones** (ej. en Europa y Asia), debes crear **proyectos de GCP separados** para cada región de despliegue que necesites.

---

## 📝 Comandos de `gcloud` Relevantes para App Engine

Los comandos `gcloud app` son esenciales para la gestión de App Engine:

| Comando | Descripción |
| :--- | :--- |
| `gcloud app deploy` | Despliega el código de tu aplicación o un archivo de configuración (YAML) en App Engine, creando una **versión** nueva o actualizando una existente. |
| `gcloud app services list` | Muestra un listado de todos los **servicios** (microservicios) configurados en tu aplicación de App Engine. |
| `gcloud app versions list` | Muestra todas las **versiones** de código que están desplegadas actualmente dentro de un servicio específico (o todos). |
| `gcloud app instances list` | Muestra las **instancias** de VM/contenedores que están actualmente en ejecución para una versión específica de la aplicación. |
| `gcloud app browse` | Abre la aplicación en tu navegador web. |
| `gcloud app logs read` | Muestra los *logs* de la aplicación, útil para *troubleshooting*. |

---

## ☁️ Integración de Servicios en Despliegue

### Google Cloud Storage (Almacenamiento en la Nube)

* Es el servicio de almacenamiento de **objetos** de GCP.
* **Relación con App Engine:** Cuando ejecutas `gcloud app deploy`, tu código fuente se comprime y se carga a un *bucket* de Cloud Storage como paso intermedio antes de ser construido y desplegado.

### Cloud Build (Construcción en la Nube)

* Es el servicio de **CI/CD (Integración y Despliegue Continuos)** de GCP.
* **Relación con App Engine:** Cloud Build se encarga de **construir** tu código. Cuando ejecutas el comando `gcloud app deploy`, Cloud Build recibe el código fuente de Cloud Storage, compila tu código, crea una imagen de contenedor (si es necesario) y luego la implementa en App Engine.

---

## ❓ Escenarios de Modelo de Servicio

| Scenario | Solution |
| :--- | :--- |
| **IaaS (Infrastructure as a Service)** or **PaaS (Platform as a Service)** or **SaaS (Software as a Service)**: Deploy Custom Application in **Virtual Machines** | IaaS |
| IaaS or PaaS or SaaS: Using **Gmail** | SaaS |
| IaaS or PaaS or SaaS: Using **App Engine** to deploy your app | PaaS |
| **True or False**: Customer is responsible for **OS updates** when using PaaS | False |
| True or False: In PaaS, customer can configure **auto scaling** needs | True |
| True or False: Customer is completely responsible for **Availability** when using PaaS | False |
| True or False: In PaaS, customer has access to **VM instances** | False |
| True or False: In PaaS, customer can install **custom software** | False |
| True or False: PaaS services only offer **Compute services** | False |