# 🏛️ Organization Policy Services (Servicios de Políticas de Organización)

El **Organization Policy Service** (Servicio de Políticas de Organización) permite a las organizaciones definir **restricciones centralizadas** (*Centralized Constraints*) y reglas a nivel de la nube que se aplican a **todos los recursos** dentro de la jerarquía.

### 🎯 Propósito y Enfoque

* **Propósito:** Definir **Restricciones Centralizadas** (*Centralized Restrictions*) para todos los recursos de una Organización.
* **Enfoque:** Se centra en el **QUÉ** (*What*). Define qué acciones **se permiten** o **se niegan** sobre un recurso o una ubicación, independientemente de quién sea el usuario.
    * *Ejemplo:* **Nadie** (`nobody`) en la cuenta debe ser capaz de crear un recurso en una región específica.

### 🆚 Diferencia Clave con IAM

| Servicio | Enfoque | Principio | Precedencia |
| :--- | :--- | :--- | :--- |
| **IAM** | **QUIÉN** (*Who*). Se centra en los **Members** (Miembros: personas, grupos o *Service Accounts*) y qué **Actions** (Acciones) pueden realizar. | Identidad y Autorización. | Precedencia **menor** que la Política de Organización. |
| **Organization Policy** | **QUÉ** (*What*). Se centra en los **Resources** (Recursos) y qué configuraciones se permiten o se prohíben. | Gobernanza y Cumplimiento (*Compliance*). | **Siempre prevalece** sobre lo que se haya configurado en IAM. |

> **Principio de Precedencia:** Si una **Organization Policy** prohíbe la creación de recursos en una región específica, aunque un usuario tenga el acceso para crearlos a través de IAM, **no podrá** crear el recurso en esa región específica.

### 📝 Casos de Uso Comunes (Constraints)

Las políticas se configuran a través de restricciones (**Constraints**) predefinidas que Google proporciona:

* **Restricción de Ubicación de Recursos (`Resource Location Restriction`):**
    * Permite o niega la creación de recursos en **Regiones Específicas** (*Specific Regions*). Esto es clave para el cumplimiento normativo y la soberanía de datos.
* **Restricción de Cuentas de Servicio:** Desactivar la creación de **Service Accounts** (Cuentas de Servicio) en toda la Organización o en un Proyecto.
* **Acceso Público a Servicios:** Prohibir el acceso público a instancias de **Cloud SQL**.
* **Acceso a Buckets:** Obligatorio el **Uniform Bucket Level Access** (Acceso Uniforme a Nivel de Bucket), asegurando que no se pueda crear ningún *Bucket* con *Access Control Lists* (ACLs) específicas a nivel de objeto.
* **Inicio de Sesión:** Hacer obligatorio el **OS Login** (Inicio de Sesión del Sistema Operativo) para las VMs de Compute Engine.

### 🛠️ Configuración y Roles

* **Rol Requerido:** Para configurar una **Organization Policy**, el usuario debe tener el rol de **Organization Policy Administrator** (Administrador de Políticas de Organización).
* **Ubicación:** Las políticas se configuran en la sección **Organization Policies** dentro de **IAM & Admin** en la consola de GCP.