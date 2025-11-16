# 🛠️ Cloud Build (Construcción en la Nube)

* **Propósito:** Es un servicio gestionado (*Managed Service*) que ejecuta tus compilaciones en la infraestructura de Google Cloud. Es el corazón de las canalizaciones de **CI/CD (Integración y Despliegue Continuos)**.
* **Función Clave:** Toma el código fuente, ejecuta las instrucciones de construcción (*Build Steps*) y produce artefactos (*Artifacts*) como contenedores Docker o paquetes de código.
* **Proceso de Construcción:** Las instrucciones se definen en un archivo de configuración (`cloudbuild.yaml`), que incluye una serie de pasos (*Steps*), donde cada paso se ejecuta en un contenedor.
* **Fuentes de Código:** Puede obtener el código de GitHub, Bitbucket, Cloud Source Repositories, o *Buckets* de Cloud Storage.
* **Artefactos (Salida):** Almacena las imágenes de contenedor creadas en **Artifact Registry** (Registro de Artefactos) para su posterior despliegue en GKE, Cloud Run o App Engine Flexible.
* **Disparadores (*Triggers*):** Se puede configurar para que se ejecute automáticamente cuando hay un cambio de código (ej. un *commit* o una solicitud de *pull*) en el repositorio.
* **Serverless (Sin Servidor):** El usuario no gestiona las VMs de construcción; Cloud Build aprovisiona los recursos bajo demanda y cobra solo por el tiempo de ejecución.