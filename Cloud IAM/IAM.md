# 🛡️ Identity and Access Management (IAM)

**IAM (Identity and Access Management)** es el servicio fundamental de Google Cloud que te permite **gestionar el acceso** (*Manage Access*) a los recursos de la nube.

### 📄 Componentes de Acceso

El servicio IAM implementa el principio de seguridad: **quién** (Identidad) puede realizar **qué acción** (Permisos/Roles) en **qué recurso** (Recurso).

* **Resources (Recursos):** Los activos en la nube (máquinas virtuales, bases de datos, *containers*, *Buckets*, etc.).
* **Identities (Identidades):** Un elemento (humano o no humano) que necesita acceder a un recurso y realizar acciones.
* **Authentication (Autenticación):** Verifica quién es la identidad.
* **Authorization (Autorización):** Verifica lo que la identidad puede hacer.

### 👥 Tipos de Identidades Soportadas

* **A GCP User (Usuario de GCP):** Una cuenta de usuario individual.
* **A Group of GCP Users (Grupo de Usuarios de GCP):** Una colección de usuarios (se recomienda trabajar con grupos para simplificar la gestión).
* **An Application running in GCP (Una Aplicación ejecutándose en GCP):** Representada por una **Service Account**.
* **An Application running in your data center (Una Aplicación ejecutándose en tu centro de datos).**
* **Unauthenticated users (Usuarios no autenticados).**

### 🎯 Control Granular

IAM proporciona **Granular Control** (Control Granular) para limitar una identidad específica a:
* Realizar una **single action** (acción única).
* Sobre un **specific cloud resource** (recurso de la nube específico).
* Desde una **specific IP address** (dirección IP específica).
* Durante una **specific time window** (ventana de tiempo específica).

---

## 🔑 Conceptos de IAM

| Concepto | Definición |
| :--- | :--- |
| **Member (Miembro)** | Es la identidad a la que se le concede acceso (Usuario, Grupo, Cuenta de Servicio). |
| **Resource (Recurso)** | El objeto de GCP al que se intenta acceder. |
| **Action (Acción)** | Una operación específica que se puede realizar (ej. `compute.instances.start`). |
| **Role (Rol)** | Un **set of permissions** (conjunto de permisos) predefinido o personalizado. **Los Roles no conocen a los Miembros**. |
| **Policy (Política)** | El documento que define las asignaciones de acceso. **You assign (or bind) a role to a member** (Asignas o vinculas un rol a un miembro). |

### 🎭 Tipos de Roles (`Roles`)

Existen 3 tipos de roles en Google Cloud:

1.  **Basic Roles (or Primitives roles) (Roles Básicos o Primitivos) - Owner/Editor/Viewer:**
    * **Viewer** (`roles/viewer`): Permite **Read-only actions** (acciones de solo lectura).
    * **Editor** (`roles/editor`): Permite acciones de Viewer + **Edit actions** (acciones de edición).
    * **Owner** (`roles/owner`): Permite acciones de Editor + **Manage Roles and Permissions** (Gestionar Roles y Permisos) + **Billing** (Facturación).
    * **Advertencia:** Son la **EARLIEST VERSION** (Versión más antigua) y **NOT RECOMMENDED** (No recomendados) para uso en producción debido a que conceden permisos demasiado amplios.
2.  **Predefined Roles (Roles Predefinidos):**
    * Roles predefinidos y **manejados por Google**.
    * Proporcionan **diferentes roles from different purposes** (roles diferentes para propósitos diferentes).
    * *Ejemplo:* `Storage Admin`, `Storage Object Viewer`, `Storage Object Creator`.
3.  **Custom Role (Rol Personalizado):**
    * Roles creados por el usuario para aplicar el principio de **Mínimo Privilegio** (*Least Privilege*).
    * Se utilizan cuando los roles predefinidos **no cumplen con las necesidades exactas** de permisos.

---

## 🤖 Service Accounts (Cuentas de Servicio)

Las **Service Accounts** son un tipo especial de miembro (identidad) que se utiliza para permitir que **una aplicación o una máquina** realice llamadas API autorizadas en nombre del usuario.

### ❓ ¿Para qué sirven las Cuentas de Servicio?

* **Identidad No Humana:** Se utilizan para **evitar el uso de cuentas de usuario personales** para acceder a los recursos de GCP.
* **Acceso en Aplicaciones:** Permiten que el código que se ejecuta en una VM, un Pod de GKE, o una Función de Cloud Functions pueda acceder a otros servicios de GCP (ej. escribir en un *Bucket* de Cloud Storage) de forma segura y autorizada.
* **Mecanismo de Seguridad:** Utilizan un par de claves **RSA públicas y privadas** para autenticarse (o tokens generados por Google), **no tienen contraseña** y no pueden usarse para iniciar sesión en la consola web o mediante una *cookie*.

### 🌐 ¿Se pueden emplear en todos los servicios de Google?

* **Alcance Universal:** Sí, las **Service Accounts** se pueden emplear en **prácticamente todos los servicios de Google Cloud** que requieren realizar acciones autenticadas, no solo para máquinas virtuales.
* **Servicios Comunes:** Son la identidad estándar para **Compute Engine** (VMs), **GKE** (*Pods*), **App Engine**, **Cloud Run**, **Cloud Functions**, y **Cloud Build**.

### 🛠️ Tipos de Cuentas de Servicio

1.  **Default Service Account (Cuenta de Servicio por Defecto):**
    * Creada automáticamente cuando se utilizan algunos servicios (ej. Compute Engine).
    * **Advertencia:** Por defecto, a menudo tienen un rol de **Editor**, lo cual es **NOT RECOMMENDED** (No recomendado) por el riesgo de conceder demasiados permisos.
2.  **User Managed (Gestionada por el Usuario):**
    * Cuentas de servicio **creadas y gestionadas por el usuario**.
    * **RECOMENDED** (Recomendado) porque permite un **fine grained access control** (control de acceso granular) al asignar solo los roles necesarios a la cuenta.
3.  **Google-managed service accounts (Cuentas de Servicio Gestionadas por Google):**
    * Creadas y **gestionadas por Google** para que los servicios de GCP puedan realizar operaciones en nombre del usuario (ej. Cloud SQL realizando copias de seguridad).
    * En general, **we DO NOT need to worry about them** (no necesitamos preocuparnos por ellas).

# ✨ Mejores Prácticas de IAM (`IAM Best Practices`)

La gestión de acceso e identidad (`Identity and Access Management` - IAM) es fundamental para la seguridad en la nube. Estas prácticas aseguran un entorno seguro y bien gobernado.

## 1. 🔑 Principio del Mínimo Privilegio (`Principle of Least Privilege`)

* **Definición:** Otorgar el **menor privilegio posible** necesario para una función o rol específico. Una identidad debe tener solo los permisos estrictamente necesarios para realizar su trabajo y nada más.

* **Recomendaciones:**
    * **Evitar:** No se recomiendan los **Basic Roles** (Roles Básicos - Owner/Editor/Viewer) debido a que conceden permisos demasiado amplios (violando este principio).
    * **Preferir:** Usa **Predefined Roles** (Roles Predefinidos) siempre que sea posible, ya que son roles granulares gestionados por Google.
    * **Identidades No Humanas:** Utiliza **Service Accounts** (Cuentas de Servicio) con privilegios mínimos para las aplicaciones.
    * **Diferenciación:** Usa **diferentes Cuentas de Servicio** para diferentes aplicaciones o propósitos para aislar los permisos.

## 2. 🔀 Separación de Deberes (`Separation of Duties`)

* **Definición:** Involucrar al menos a **dos personas** con diferentes roles para completar tareas sensibles o de alto riesgo. Esto previene el fraude y los errores.

* **Ejemplo en App Engine:** Se utiliza para evitar que una sola persona pueda implementar (*deploy*) código y también controlar el tráfico, asegurando que un cambio requiera la aprobación o la acción de otra entidad.
    * **App Engine Deployer:** Puede implementar una **nueva versión**, pero **no puede cambiar el tráfico** (*traffic migrator*).
    * **App Engine Service Admin:** Puede **cambiar el tráfico**, pero **no puede implementar una nueva versión**.

## 3. 🔍 Monitoreo Constante (`Constant Monitoring`)

* **Acción:** Es esencial revisar los **Cloud Audit Logs** (Registros de Auditoría en la Nube) para auditar:
    * Los cambios en las **Políticas de IAM** (*IAM Policies*).
    * El acceso y uso de las **claves de la Cuenta de Servicio**.
* **Práctica:** Archivar los Registros de Auditoría en **Cloud Storage Buckets** (Depósitos de Cloud Storage) para una **retención a largo plazo** (*Long-Term Retention*) y análisis forense.

## 4. 👥 Usar Grupos cuando sea Posible

* **Beneficio:** Asignar roles a **Grupos de Usuarios** (en lugar de a usuarios individuales) facilita la gestión de usuarios y permisos. Cuando un empleado se une o deja un equipo, solo se modifica la membresía del grupo, y sus permisos de IAM se actualizan automáticamente, simplificando la administración.