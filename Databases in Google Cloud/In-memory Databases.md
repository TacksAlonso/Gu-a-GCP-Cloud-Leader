# ⚡ In-Memory Databases (Bases de Datos en Memoria)

* **Propósito:** Las **In-Memory Databases** son un tipo de almacenamiento que guarda la información en la **RAM** (*Random Access Memory*) del servidor, en lugar de usar discos (*Disks* - HDD/SSD).
* **Beneficio Principal:** Ofrecen una **latencia extremadamente baja** (*Microsecond Latency*), típicamente en el rango de microsegundos, para leer y escribir datos, ya que no hay necesidad de esperar el acceso al disco.
* **Persistencia:** Aunque están en memoria, muchas soluciones permiten configurar la **persistencia de datos** (*Data Persistence*) para evitar la pérdida de información en caso de fallo o reinicio.

## ☁️ Servicio Gestionado de Google: Memorystore

**Memorystore** es el servicio de caché (*Caching*) y bases de datos en memoria totalmente gestionado (*Fully Managed*) por Google Cloud. Soporta dos motores de código abierto líderes en la industria: **Redis** y **Memcached**.

### ✨ Características y Usos

* **Serverless:** Es un servicio gestionado que automatiza parches, alta disponibilidad y escalado.
* **Motores Soportados:**
    * **Memorystore for Redis:** Base de datos en memoria versátil (similar a **Key-Value**). Ofrece estructuras de datos avanzadas (listas, conjuntos, hashes).
    * **Memorystore for Memcached:** Servicio de caché simple y escalable. Ideal para **caching puro** donde se prioriza el escalado horizontal sobre la persistencia.
* **Casos de Uso Comunes:**
    * **Caching:** Almacenar temporalmente los resultados de consultas frecuentes a bases de datos o APIs para reducir la carga de las fuentes de datos principales y acelerar las respuestas.
    * **Session Management (Gestión de Sesiones):** Almacenar datos de sesión de usuario para aplicaciones web escalables.
    * **Gaming Leaderboards (Tablas de Clasificación de Juegos):** Almacenar y ordenar clasificaciones en tiempo real.
    * **Geospatial Applications (Aplicaciones Geoespaciales):** Almacenamiento rápido de datos de ubicación.

### 🗄️ Tipos de Nivel de Servicio (Tier Types) para Redis

Memorystore for Redis ofrece diferentes niveles de servicio que equilibran el costo, la disponibilidad y la persistencia:

| Nivel de Servicio | Características Clave | Alta Disponibilidad (*High Availability*) | Persistencia |
| :--- | :--- | :--- | :--- |
| **Basic (Básico)** | Un solo nodo Redis. El nivel más económico. | **No**. Pérdida de datos si el nodo falla. | **No** (sin alta disponibilidad). |
| **Standard (Estándar)** | Dos nodos (un primario y una réplica). | **Sí**. Conmutación por error (*Failover*) automática si el nodo primario falla. | **Sí**. Soporta **Read Replicas** (Réplicas de Lectura) para descargas de tráfico de lectura. |