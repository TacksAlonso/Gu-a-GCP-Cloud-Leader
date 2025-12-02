# 💾 Almacenamiento en Google Cloud

Los servicios de almacenamiento se categorizan según cómo se organizan y acceden a los datos.

## 🧱 Block Storage (Almacenamiento en Bloques)

El **Block Storage** (Almacenamiento en Bloques) gestiona los datos en bloques de tamaño fijo. Es la capa más básica, similar a un disco duro tradicional.

### 📄 Definición Ampliada

* **Acceso a Nivel de Bloque:** El sistema operativo (OS) de la máquina virtual (VM) monta el disco como un disco duro sin formato y gestiona el sistema de archivos (ej. ext4, NTFS).
* **Conexión Directa:** Una instancia de cómputo (servidor) tiene una relación **uno a uno** con su almacenamiento en bloques.
* **Usos:**
    * **Direct-Attached Storage (DAS):** Almacenamiento conectado directamente al servidor.
    * **Storage Area Network (SAN):** Usado para bases de datos transaccionales y de alta velocidad (ej. Oracle y Microsoft SQL Server).
    * **Unidades de Arranque (*Boot Drives*):** Disco del sistema operativo de una VM.

### ☁️ Solución de Google Cloud: Persistent Disks

Google ofrece el almacenamiento en bloques a través de **Persistent Disks** (Discos Persistentes).

* **Persistent Disks (PD):** Es un servicio de **Block Storage conectado a la red** (*Network Block Storage*). El acceso al disco se realiza a través de la red de Google.
    * **Tipo de Conexión:** Por defecto, solo una VM puede tener acceso de **escritura/lectura** (*read/write*).
    * **Excepción:** Si un PD se configura en modo **solo lectura** (*read-only*), se puede adjuntar a **múltiples VMs** para compartir datos.
* **Tipos de Durabilidad:**
    * **Zonal:** Los datos se replican automáticamente dentro de **una única zona** (*one zone*).
    * **Regional:** Los datos se replican en **múltiples zonas** (*multiple zones*) dentro de una región, ofreciendo mayor disponibilidad ante fallos de zona.

#### Local Block Storage

* **Local SSDs:** Unidades SSD físicas (**Local Block Storage**) conectadas directamente al servidor físico que aloja la VM.
* **Características:** Ofrecen la **latencia más baja** y el **mayor rendimiento**.
* **Restricción:** El almacenamiento en **Local SSDs es efímero** (*ephemeral*); si la VM se detiene, los datos se borran.

---

## 📁 File Storage (Almacenamiento de Archivos)

El **File Storage** (Almacenamiento de Archivos) permite que múltiples usuarios y servidores accedan a los mismos datos de forma concurrente, usando protocolos estándar de sistema de archivos.

### 📄 Definición Ampliada

* **Acceso Compartido:** Diseñado para ser **compartido** (*shared*) entre múltiples instancias de cómputo.
* **Protocolos:** Se accede usando protocolos de red estándar como **NFS (Network File System)**.
* **Relación N:N:** Múltiples VMs pueden conectarse a un solo servicio de *File Storage* simultáneamente.

### ☁️ Solución de Google Cloud: Filestore

Google ofrece **Filestore** como el servicio gestionado (*Managed Service*) de almacenamiento de archivos de alto rendimiento (NFS).

* **Tipos de Almacenamiento:**
    * **HDD (Unidad de Disco Duro):** Alta durabilidad por bajo costo.
    * **SSD (Unidad de Estado Sólido):** Alto rendimiento pero mayor costo.
* **Integración y Acceso:**
    * **Compute Engine:** Para usar Filestore, la VM de Compute Engine debe **montar** (*mount*) la instancia de Filestore utilizando el protocolo **NFS**.
    * **GKE:** Filestore también puede ser usado por **Google Kubernetes Engine (GKE)** para proporcionar almacenamiento persistente y compartido a los *Pods* a través de *Persistent Volumes*.