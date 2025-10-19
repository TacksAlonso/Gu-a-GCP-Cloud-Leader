# 🗄️ Google Cloud Storage (GCS)

* **Propósito:** Es el servicio de **Almacenamiento de Objetos** (*Object Storage*) escalable y unificado de Google Cloud.
* **Modelo de Almacenamiento:** Almacena datos como **objetos** (archivos) dentro de **Buckets** (contenedores lógicos). Los objetos son inmutables (no se modifican, se reemplazan).
* **Jerarquía Plana:** A diferencia de un sistema de archivos tradicional, GCS no utiliza una estructura de carpetas; todos los objetos dentro de un *Bucket* están en el mismo nivel. Las "carpetas" que ves son solo una convención de nomenclatura (ej. `mi-bucket/datos/archivo.txt`).
* **Alcance:** Los nombres de los *Buckets* deben ser **globalmente únicos** (únicos en todo GCP). El almacenamiento en sí puede ser **Regional**, **Dual-Regional** o **Multi-Regional**.
* **Clases de Almacenamiento (Costos y Acceso):** Define el costo y la latencia de acceso a los datos:
    * **Standard (Estándar):** Acceso frecuente (baja latencia).
    * **Nearline (Cercana):** Acceso mensual (baja latencia, pero penalización por lectura temprana).
    * **Coldline (Frecuencia Fría):** Acceso trimestral (baja latencia, pero penalización y costo más bajo).
    * **Archive (Archivo):** Acceso anual (el más bajo costo, ideal para *compliance* y archivo a largo plazo).
* **Integración con Aplicaciones:** Se usa comúnmente para servir contenido estático (imágenes, videos) y almacenar *backups*.