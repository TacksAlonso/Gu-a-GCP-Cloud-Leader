# 🔒 Data States (Estados de los Datos)

En GCP, los datos existen en diferentes estados. El cifrado debe aplicarse en todos ellos para garantizar la seguridad.

| Estado | Definición | Nombres Alternativos | Ejemplos |
| :--- | :--- | :--- | :--- |
| **Data at Rest** (Datos en Reposo) | Datos almacenados de forma persistente en un dispositivo o un *backup*. | *Stored Data* | Datos en un disco duro, en una base de datos, *backups* y archivos (*archives*). |
| **Data in Motion** (Datos en Movimiento) | Datos siendo transferidos a través de una red. | **Data in Transit** (Datos en Tránsito) | Datos copiados desde *on-premises* a **Cloud Storage**, una aplicación comunicándose con una base de datos. |
| **Data in Use** (Datos en Uso) | Datos activos que están siendo procesados en un estado no persistente. | *Active Data* | Datos en la memoria RAM, datos en la CPU de una VM. |

### 🚨 Riesgo y Principios de Seguridad

* **Riesgo:** Si almacenas datos "tal cual" (sin cifrar), una entidad no autorizada que obtenga acceso a los datos podrá leer y utilizar la información directamente.
* **Primera Ley de Seguridad:** **Defense in Depth** (Defensa en Profundidad). Esto significa que la seguridad debe implementarse en múltiples capas para proteger los datos en todos sus estados.
* **Insuficiencia:** **NO es suficiente** cifrar solo los datos "en reposo"; también se debe cifrar los datos **"en tránsito"** (*Data in Transit*) para proteger la comunicación entre servicios.

### 🌐 Tipos de Cifrado

#### 🔐 Cifrado de Clave Simétrica (`Symmetric Key Encryption`)

Los algoritmos de cifrado simétrico utilizan la **misma clave** para el cifrado (*Encryption*) y el descifrado (*Decryption*).

* **Retos Cruciales (`Key Challenges`):**
    1.  **Algoritmo:** Elegir el algoritmo de cifrado correcto (ej. AES, DES).
    2.  **Seguridad de la Clave:** ¿Cómo asegurar la clave de cifrado? (Evitar que caiga en manos no autorizadas).
    3.  **Distribución de la Clave:** ¿Cómo compartir la clave de cifrado? (El emisor y el receptor deben tener la misma clave secreta).

#### 🗝️ Cifrado de Clave Asimétrica (`Asymmetric Key Encryption`)

También se le conoce como **Criptografía de Clave Pública** (*Public Key Cryptography*). Utiliza dos claves:

* **Clave Pública (`Public Key`):** Se comparte con todo el mundo (con cualquiera que necesite enviar información cifrada). Se usa para **Cifrar** la información.
* **Clave Privada (`Private Key`):** Se debe mantener estrictamente privada. Se usa para **Descifrar** la información.

---

# 🔑 Cloud Key Management Service (Cloud KMS)

**Cloud KMS** es el servicio de **gestión de claves criptográficas** (*Cryptographic Key Management*) en la nube de Google. Permite crear, gestionar y utilizar claves criptográficas en servicios de GCP y aplicaciones.

### ✨ Características y Funcionalidad

* **Tipos de Claves:** Permite crear y gestionar tanto **claves simétricas** como **claves asimétricas**.
* **Propósito Central:** Controlar el **uso, rotación y ciclo de vida** de las claves utilizadas para cifrar y descifrar datos.
* **Funciones:** Proporciona una **API** para **cifrar** (*encrypt*), **descifrar** (*decrypt*) y **firmar datos** (*sign data*) de forma programática.
* **Integración:** Tiene **integración nativa** (*Native Integration*) con casi todos los servicios de GCP (Cloud Storage, Compute Engine, BigQuery, etc.).
* **HSM (Hardware Security Module):** Permite almacenar claves en módulos de hardware de seguridad (Cloud HSM) para mayor protección y cumplimiento normativo.

### 🛡️ Opciones de Cifrado para los Servicios de GCP

Cloud KMS ofrece flexibilidad sobre quién gestiona la clave de cifrado utilizada para proteger tus datos:

| Opción | Siglas | Gestión de la Clave | Rol del Cliente |
| :--- | :--- | :--- | :--- |
| **Google-managed key** (Clave Gestionada por Google) | **CMEK (Customer-Managed Encryption Key)** | Google crea, almacena y rota la clave. | **No configuration required** (No se requiere configuración). Es el método por defecto. |
| **Customer-managed key** (Clave Gestionada por el Cliente) | **CMEK (Customer-Managed Encryption Key)** | El cliente crea la clave en **Cloud KMS** y controla su acceso (IAM). | El cliente es responsable de gestionar la clave, la rotación y los permisos. |
| **Customer-supplied key** (Clave Suministrada por el Cliente) | **CSEK (Customer-Supplied Encryption Key)** | El cliente genera la clave **on-premises** y la proporciona a GCP en el momento de la operación (ej. subir un archivo a Cloud Storage). | La clave nunca se almacena en GCP. El cliente es totalmente responsable de la clave. |