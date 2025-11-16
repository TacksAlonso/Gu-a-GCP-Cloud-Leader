# 💾 NoSQL Databases (Bases de Datos NoSQL)

El término **NoSQL** significa generalmente **Not Only SQL** (No solo SQL). Estas bases de datos están diseñadas para modelos de datos específicos, ofreciendo flexibilidad y escalabilidad que las bases de datos relacionales tradicionales no proporcionan fácilmente.

### ✨ Características Principales

* **Flexible Schema (Esquema Flexible):** Permite que la estructura de datos evolucione con el tiempo sin requerir una reestructuración de la base de datos completa. Los datos se almacenan tal como se necesitan en la aplicación.
* **Escalabilidad Horizontal:** La mayoría de las bases de datos NoSQL pueden escalar horizontalmente (*Horizontal Scaling*) hasta **Petabytes** de datos y manejar millones de **TPS (Transacciones por Segundo)**.
* **Compensación (*Trade-off*):** Las bases de datos NoSQL típicamente sacrifican la **Consistencia Fuerte** (*Strong Consistency*) y ciertas características de SQL para lograr **Escalabilidad** (*Scalability*) y **Alto Rendimiento** (*High Performance*).
* **Consistencia:** A menudo utilizan el modelo **BASE** (Basically Available, Soft state, Eventually consistent) en lugar del modelo ACID (Atomicidad, Consistencia, Aislamiento, Durabilidad) de las bases de datos relacionales.

---

## ☁️ Soluciones Gestionadas de Google (NoSQL)

Google ofrece dos soluciones principales de NoSQL: **Cloud Firestore** (para documentos y móviles) y **Cloud BigTable** (para escala masiva).

### 📝 Cloud Firestore

* **Clasificación:** **Base de Datos de Documentos** (*Document Database*) Serverless.
* **Modelo de Datos:** Almacena datos en colecciones de **documentos** (similares a JSON), ofreciendo una estructura jerárquica.
* **Consistencia:** Ofrece **Fuerte Coherencia** (*Strong Coherence*): todas las lecturas devuelven la versión más reciente del dato.
* **Transacciones:** Soporta **ACID Transactions** (Transacciones ACID) para la manipulación de datos.
* **Consultas:** Permite **SQL-like Queries** (Consultas similares a SQL) e **Indexes** (Índices) para búsquedas eficientes.
* **Usos Comunes:**
    * Bases de datos **pequeñas y medianas** (hasta unos pocos Terabytes - TBs).
    * Aplicaciones web y móviles que requieren **sincronización en tiempo real** (*Real-Time Synchronization*) y librerías de cliente (*Client Libraries*) nativas.

### 📊 Cloud BigTable

* **Clasificación:** **Base de Datos de Columnas Anchas** (*Wide-Column Database*) NoSQL.
* **Modelo Operacional:** **No es Serverless**. Requiere que el usuario aprovisione y gestione una **Instancia** (*Instance*) antes de poder crear tablas (*Tables*).
* **Escalabilidad:** Diseñada para una **escala masiva**, ideal para más de **10 Terabytes (TBs)** hasta varios **Petabytes**.
* **Transacciones:** **No soporta transacciones multi-fila** (*Multi-Row Transactions*); solo admite transacciones por fila (*Single-Row Transactions*). Por esta razón, **no se recomienda para cargas de trabajo transaccionales OLTP**.
* **Usos Comunes:**
    * **Grandes cargas de trabajo operativas o analíticas** (*Operational/Analytical Workloads*).
    * Series de tiempo (*Time Series Data*), Internet de las Cosas (IoT), grafos y datos de *AdTech* (Tecnología de Publicidad).
    * Ideal para situaciones que requieren baja latencia y alto rendimiento de lectura/escritura a escala masiva.

---

## 🧐 Cloud Firestore vs. Cloud BigTable

| Característica | Cloud Firestore | Cloud BigTable |
| :--- | :--- | :--- |
| **Modelo** | Documentos / Colecciones | Columnas Anchas (*Wide-Column*) |
| **Escala Típica** | TBs (Pequeña a Mediana) | Petabytes (Masiva) |
| **Tipo de Servicio** | **Serverless** | Provisionado (*Provisioned*) |
| **Consistencia** | Fuerte Coherencia | Consistencia Fuerte/Eventual (según la configuración) |
| **Transacciones** | Soporta ACID Multi-Documento | **Solo Transacciones por Fila** |
| **Uso Principal** | Apps Móviles/Web, Perfiles de Usuario | Datos de IoT, Series de Tiempo, Analítica Operacional |