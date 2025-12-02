# 🗃️ Databases Categories (Categorías de Bases de Datos)

La selección de la base de datos se basa en las necesidades de la aplicación (rendimiento, consistencia y escalabilidad).

* **Tipos Comunes de Bases de Datos:**
    * **Relational (Relacional):** (OLTP y OLAP)
    * **Document (Documento):** NoSQL (ej. Firestore, MongoDB).
    * **Key Value (Clave-Valor):** NoSQL (ej. Memorystore, Redis).
    * **Graph (Grafo):** (ej. Neo4j).
    * **In-Memory (En Memoria):** (ej. Memorystore).
* **Criterios de Evaluación:** **Fixed Schema** (Esquema Fijo), **Transaction Properties** (Propiedades Transaccionales - ACID), **Latency** (Latencia), volumen de transacciones y volumen de datos.

---

## 🔗 Relational Databases (Bases de Datos Relacionales)

Este tipo de base de datos es muy popular, utiliza un **Schema** (Esquema) predefinido de tablas y relaciones, y proporciona fuertes capacidades **transaccionales** (*Transactional Capabilities*).

### ✍️ OLTP (Online Transaction Processing - Procesamiento de Transacciones en Línea)

Se utiliza cuando un gran número de usuarios genera un gran número de **transacciones pequeñas** (*Small Transactions*).

* **Operaciones Típicas:** Lecturas, actualizaciones y eliminaciones de datos pequeños.
* **Usos Comunes:** Aplicaciones tradicionales, ERP, CRM, *e-commerce* y aplicaciones bancarias.
* **Bases de Datos Populares:** MySQL, PostgreSQL, Oracle, SQL Server.

#### ☁️ Servicios Gestionados de Google (OLTP)

* **Cloud SQL:**
    * Servicio de base de datos relacional gestionada y regional para PostgreSQL, MySQL y SQL Server.
    * Ideal para bases de datos que admiten hasta unos pocos **TBs (Terabytes)** de almacenamiento.
    * **Restricción:** **No se puede generar una instancia global** de Cloud SQL; se limita a una región única (o una *Read Replica* en otra región).
* **Cloud Spanner:**
    * Base de datos relacional gestionada de **misión crítica** (*Mission-Critical*).
    * Proporciona **escala ilimitada** a nivel de Petabytes y una disponibilidad de **99.999%**.
    * Es **globalmente consistente** y está diseñada para aplicaciones globales que requieren **escalado horizontal** (*Horizontal Scaling*) masivo.

### 📊 OLAP (Online Analytics Processing - Procesamiento Analítico en Línea)

El **Análisis de Procesamiento en Línea (OLAP)** está diseñado para el análisis de Petabytes de datos, concentrando la información de múltiples aplicativos.

* **Usos Comunes:** *Reporting applications* (Aplicaciones de Informes), *Data Warehouses* (Almacenes de Datos), *Business Intelligence Applications* (Aplicaciones de Inteligencia de Negocios) y sistemas de analítica.

#### ☁️ Servicio Gestionado de Google (OLAP)

* **BigQuery:**
    * Es el **Almacén de Datos Distribuido** (*Distributed Data Warehouse*) de GCP, escalable a nivel de Petabytes.
    * Diseñado para consultas (*Queries*) analíticas rápidas sobre grandes volúmenes de datos.

### 📝 Relational Databases - OLAP vs OLTP

La diferencia principal entre OLAP y OLTP es la forma en que almacenan los datos, aunque usen estructuras relacionales similares:

| Característica | OLTP (Transaccional) | OLAP (Analítico) |
| :--- | :--- | :--- |
| **Almacenamiento de Datos** | **Row Storage** (Almacenamiento por Fila). | **Column Storage** (Almacenamiento por Columna). |
| **Eficiencia** | Eficiente para almacenar **pequeñas transacciones** y realizar *inserts* rápidos. | **Compresión alta** que permite almacenar Petabytes de datos de forma eficiente. |
| **Consultas** | Típico de consultas de **lectura/escritura** sobre un registro (fila) a la vez. | Permite ejecutar una **única consulta** a través de **múltiples nodos** (*Cluster Nodes*) para un análisis masivo. |
| **Ejemplo GCP** | Cloud SQL, Cloud Spanner. | BigQuery. |


### ☁️ Servicios de Bases de Datos de Google Cloud (Profundización)

Los tres servicios más importantes de bases de datos relacionales y analíticas en GCP se distinguen por su enfoque en transacciones (OLTP) o análisis (OLAP).

#### 1️⃣ Cloud SQL

* **Clasificación:** **OLTP (Online Transaction Processing)**.
* **Definición:** Servicio de base de datos relacional completamente gestionada (*Fully Managed*) que facilita el uso de motores populares de código abierto y comerciales.
* **Motores Soportados:** **PostgreSQL**, **MySQL** y **SQL Server**.
* **Escalabilidad:** Escala verticalmente (aumenta CPU y RAM) y admite hasta unos pocos **TBs** (Terabytes) de almacenamiento.
* **Alcance:** Es un servicio **Regional**. No tiene una instancia global, pero se puede configurar alta disponibilidad (*High Availability*) en una región y **Read Replicas** (Réplicas de Lectura) en otras regiones para mejorar el rendimiento de lectura global.
* **Ventaja Principal:** Minimiza la sobrecarga operativa de gestión de parches, copias de seguridad (*Backups*) y actualizaciones de versión.

#### 2️⃣ Cloud Spanner

* **Clasificación:** **OLTP (Online Transaction Processing)**. (También puede manejar algunas cargas de trabajo analíticas, pero su propósito principal es transaccional).
* **Definición:** Base de datos relacional única de GCP. Combina la estructura y la consistencia de una base de datos relacional tradicional con la escalabilidad horizontal (*Horizontal Scalability*) de una base de datos NoSQL.
* **Escalabilidad:** Escala masivamente a nivel de **PetaBytes**. Diseñada para aplicaciones con requisitos de crecimiento impredecibles y masivos.
* **Alcance:** Es una base de datos **Globalmente Consistente** (*Globally Consistent*). Los datos están sincronizados en todas las réplicas en tiempo real.
* **Disponibilidad:** Ofrece un **SLA** (Acuerdo de Nivel de Servicio) de **99.999%** (cinco nueves), esencial para aplicaciones de **misión crítica** (*Mission-Critical*).
* **Ventaja Principal:** Garantiza la consistencia global inmediata para transacciones ACID, incluso a escala Petabyte.

#### 3️⃣ BigQuery

* **Clasificación:** **OLAP (Online Analytics Processing)**.
* **Definición:** Almacén de Datos Distribuido (*Distributed Data Warehouse*) **Serverless** (*Sin Servidor*) que permite ejecutar consultas (*Queries*) SQL de alto rendimiento sobre Petabytes de datos.
* **Escalabilidad:** Escala a Petabytes de almacenamiento sin necesidad de gestión o redimensionamiento manual del clúster.
* **Modelo de Datos:** Utiliza **Column Storage** (Almacenamiento por Columna), que optimiza la compresión y la velocidad de lectura para consultas analíticas.
* **Modelo de Pago:** Típicamente se cobra por la cantidad de datos **escaneados** por cada consulta.
* **Ventaja Principal:** Permite a los usuarios de *Business Intelligence* (Inteligencia de Negocios) y analistas ejecutar consultas muy complejas sobre conjuntos de datos masivos en segundos.