# ⚙️ Google Cloud Functions (GCF)

* **Propósito:** Es un entorno de ejecución **Serverless** (*Sin servidor*) que implementa el modelo **Function as a Service (FaaS)**. Su función principal es ejecutar pequeños fragmentos de código (*functions*) en respuesta a un evento (*Event-Driven Architecture*).
* **Modelo Operacional:** El usuario **solo se preocupa por el código** de la función. No hay que gestionar servidores, *clusters*, escalamiento o disponibilidad.
* **Ejemplos de Eventos (`Triggers`):**
    * Un archivo se actualizó o creó en **Cloud Storage**.
    * Un mensaje llega a un **Cloud Pub/Sub Topic**.
    * Un error es escrito en **Cloud Logging**.
    * Peticiones web HTTP.
    * Cambios en bases de datos (ej. Firestore).

---

## 💻 Entorno y Lenguajes Soportados

Cloud Functions maneja el aprovisionamiento de recursos automáticamente. Los lenguajes soportados dependen de la generación (Gen 1 o Gen 2).

* **Lenguajes Soportados:** Node.js, Python, Go, Java, .NET, Ruby, PHP.
* **Versiones Específicas (Relevantes para la Certificación):**

| Lenguaje | Versiones Comunes Soportadas |
| :--- | :--- |
| **Java** | **Java 11 (Gen 1)**, **Java 17 (Gen 2)** y **Java 21 (Gen 2)**. (Java 8 es obsoleto). |
| **Python** | Python 3.8, Python 3.10, Python 3.11. |
| **Node.js** | Node.js 16, Node.js 18, Node.js 20. |
| **Go** | Go 1.18, Go 1.20, Go 1.21. |
| **.NET** | **.NET Core 3.1**, **.NET 6**, **.NET 7** y **.NET 8**. |
| **Ruby** | Ruby 3.2. |

---

## 💰 Facturación y Límites

El modelo de facturación es puramente por uso, haciéndolo muy rentable para cargas de trabajo esporádicas.

* **Pago por Uso (`Pay-per-use`):** Solo se paga por lo que se consume:
    * **Número de Invocaciones** (cuántas veces se ejecuta la función).
    * **Tiempo de Cómputo** (*Compute Time*) de las invocaciones (tiempo de ejecución).
    * La cantidad de **Memoria y CPU** (*Provisioned Resources*) configurada para cada invocación.
* **Límite de Tiempo de Ejecución (`Timeout`):**
    * Las funciones de **Generación 1** tienen un tiempo límite máximo de **9 minutos** (540 segundos).
    * Las funciones de **Generación 2** (basadas en Cloud Run) pueden tener límites de hasta **60 minutos**.
* **Ejecución Aislada:** Cada ejecución de la función ocurre en una **instancia separada** (*separate instance*); por lo tanto, no se comparte el estado o la memoria entre invocaciones (salvo que sea intencional y dentro de la misma *cold start*).