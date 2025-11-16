# 📦 Cloud Storage (Almacenamiento en la Nube)

**Cloud Storage** (CS) es el servicio de **Almacenamiento de Objetos** (*Object Storage*) altamente escalable, flexible y económico de Google Cloud Platform (GCP).

* **Tipo de Servicio:** Es **Serverless** (*Sin Servidor*).
* **Escalabilidad:** Ofrece **Auto Scaling** (Autoescalado) y **Escala Infinita** (*Infinite Scale*). Al definir un *Bucket*, no es necesario predefinir un tamaño; se ajusta automáticamente a las necesidades o demanda.
* **Modelo de Datos:** Almacena objetos de cualquier tamaño (hasta 5 TB cada uno) utilizando un enfoque de **key-value** (clave-valor).
* **Objetos Inmutables (Aclaración):** El almacenamiento trata un objeto completo (ej. un archivo de 5 MB) como una unidad. **No se pueden realizar actualizaciones parciales** (*Partial Updates*). Para modificar una pequeña parte de un archivo, debes descargar el objeto completo, realizar la modificación y luego volver a subir el objeto completo, reemplazando la versión anterior.

### ✨ Características Generales

* **Acceso API:** Proporciona una **REST API** para acceder y modificar objetos.
    * Se utiliza la herramienta de línea de comandos **CLI (Command Line Interface)** llamada `gsutil` y **Client Libraries** (para C++, C#, Java, Node.js, PHP, Python y Ruby).
* **Control de Acceso:** Ofrece **Access Control at Object level** (Control de Acceso a nivel de Objeto) a través de IAM y *Access Control Lists* (ACLs).
* **Tipos de Archivos:** Acepta todo tipo de archivos: texto, binario, *backups* y archivos (*archives*).
    * Usos comunes: Archivos multimedia, paquetes de aplicaciones (*Application Packages*), *logs*, *backups* de bases de datos y datos de *staging* durante migraciones.
* **Alta Durabilidad:** Ofrece una **High Durability** (Alta Durabilidad) de **99.999999999%** anual.
* **Baja Latencia:** Se caracteriza por una **Low Latency** (Baja Latencia), independientemente de la *Storage Class*.
* **Mismo API entre Clases:** Se usa el **Same API's acros storage classes** (Mismas APIs a través de clases de almacenamiento).

---

## 🗑️ Bucket

Un **Bucket** es el contenedor (*Container*) lógico para todos los objetos que se desean colocar en Cloud Storage.

* **Nombres Globales:** El nombre del *Bucket* debe ser **único a nivel mundial** (*globally unique*) en todo GCP.
* **Ubicación (`Location`):** Se debe definir el lugar de almacenamiento:
    * **Region (Región):** Una sola ubicación geográfica (ej. `us-central1`).
    * **Dual-region (Doble Región):** Un par de regiones (ej. Iowa y Carolina del Sur) para alta disponibilidad.
    * **Multi-region (Múltiples Regiones):** Un área geográfica grande (ej. `US` o `EU`) para máxima disponibilidad y distribución.
* **Clase por Defecto:** Se define una **Storage Class** (Clase de Almacenamiento) por defecto para los objetos que se suban al *Bucket*. Esta puede ser sobrescrita a nivel de objeto.

---

## 🗃️ Storage Classes (Clases de Almacenamiento)

Las **Storage Classes** ayudan a la **optimización de costos** (*Cost Optimization*) basado en las necesidades de acceso a los datos.

| Clase | Uso Recomendado | Mínimo de Duración | SLA de Disponibilidad (Multi/Dual Region) |
| :--- | :--- | :--- | :--- |
| **Standard (Estándar)** | Acceso frecuente o de corta duración de tiempo. | No tiene mínimo de duración de almacenamiento. | 99.99% |
| **Nearline (Cercana)** | Acceso a los datos en menos de una vez al mes. | Mínima de **30 días**. | 99.95% |
| **Coldline (Frecuencia Fría)** | Acceso a los datos en menos de una vez al trimestre. | Mínima de **90 días**. | 99.95% |
| **Archive (Archivo)** | Acceso a los datos en menos de una vez al año. | Mínima de **365 días**. | 99.95% |

> **Nota de SLA:** El **Committed SLA (Acuerdo de Nivel de Servicio Comprometido)** de GCP es: 99.95% para *Multi-Region/Dual-Region* y 99.9% para *Single Region* (para todas las clases).

---

## 🔁 Object Lifecycle Management (Gestión del Ciclo de Vida del Objeto)

El **Object Lifecycle Management** es una característica que permite **automatizar acciones** (*Automate Actions*) sobre los objetos en un *Bucket* basándose en un conjunto de **condiciones** (*Conditions*).

* **Propósito:** Optimizar costos al mover datos de una clase de almacenamiento costosa a una más barata a medida que envejecen, o eliminarlos.
* **Condiciones Comunes:**
    * **Age (Antigüedad):** Número de días desde la creación.
    * **CreatedBefore (Creado Antes):** Una fecha específica.
    * **IsLive (Está Vivo):** Indica si es la versión actual del objeto (útil con versionado).
    * **MatchesStorageClass (Coincide con Clase):** La clase de almacenamiento actual.
    * **NumberOfNewerVersions (Número de Versiones Más Recientes).**
* **Acciones Posibles:**
    * **SetStorageClass:** Cambiar la clase de almacenamiento.
    * **Deletion:** Borrar el objeto.
* **Restricciones de Cambio de Clase:** Solo se puede pasar de una clase más "caliente" (acceso frecuente) a una más "fría" (acceso menos frecuente):
    * **Standard** (o Multi/Regional) a **Nearline**, **Coldline** o **Archive**.
    * **Nearline** a **Coldline** o **Archive**.
    * **Coldline** a **Archive**.

Ejemplo de regla:
```json
{
  "lifecycle": {
    "rule": [
      {
        "action": {
          "type": "Delete"
        },
        "condition": {
          "age": 30,
          "isLive": true
        }
      },
      {
        "action": {
          "type": "SetStorageClass",
          "storageClass": "NEARLINE"
        },
        "condition": {
          "age": 365,
          "matchesStorageClass": ["STANDARD"]
        }
      }
    ]
  }
}
```

---

## 🚚 Transferring Data to Cloud (Transferencia de Datos a la Nube)

Antes de mover datos a cualquier base de datos o servicio de GCP (como BigQuery o Cloud SQL), los datos deben subirse primero a **Cloud Storage** como punto de *staging* (puesta en escena).

| Opción de Transferencia | Uso Recomendado | Características Clave |
| :--- | :--- | :--- |
| **Online Transfer (Transferencia en Línea - gsutil/API)** | Menos de 1 TB desde *on-premises* o de otro *Bucket*. | Simple y directo a través de la red existente. |
| **Storage Transfer Service (STS)** | Transferencia de **grandes volúmenes** (Petabytes) desde **Private Data Centers** o **Otras Nubes** (AWS, Azure, etc.). | **Soporta transferencias incrementales** (*Incremental Transfers*): solo copia los archivos que han cambiado desde la última transferencia. Es programable y tolerante a fallos. |
| **Transfer Appliance (TA)** | Si los datos superan **20 TB** o la transferencia por red tarda más de una semana. | Es una **Transferencia Física de Datos** (*Physical Data Transfer*). Google envía un dispositivo de almacenamiento cifrado que se llena con datos y se envía de vuelta a Google para su carga. |

### Proceso de Transfer Appliance

* **Process:**
    * **Request an appliance** (Solicitar un dispositivo).
    * **Upload your data** (Subir tus datos) al dispositivo localmente (rápido, hasta 40 Gbps).
    * **Ship the appliance back** (Enviar el dispositivo de vuelta).
    * **Google uploads the data** (Google carga los datos) a tu *Bucket* de GCS.
* **Seguridad:** Utiliza **AES 256 encryption** (cifrado AES 256) con **Customer-managed encryption keys** (claves de cifrado gestionadas por el cliente).