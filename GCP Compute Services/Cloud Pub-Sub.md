# 📨 Cloud Pub/Sub

* **Propósito:** Es un servicio de **mensajería asíncrona** (*Asynchronous Messaging Service*) totalmente gestionado y escalable. Se utiliza para desacoplar (*Decouple*) los servicios que producen datos (*Publishers*) de los servicios que procesan esos datos (*Subscribers*).
* **Modelo de Comunicación:** Implementa el modelo de **publicador/suscriptor** (*Publisher/Subscriber*), donde los mensajes se envían a un canal lógico llamado **Topic** (Tema).
* **Componentes Clave:**
    * **Publisher (Publicador):** La aplicación o servicio que crea y envía mensajes a un *Topic*.
    * **Topic (Tema):** Un canal de mensajes central al que los *Publishers* envían datos.
    * **Subscriber (Suscriptor):** La aplicación o servicio que recibe y procesa los mensajes del *Topic* a través de una **Subscription** (Suscripción).
* **Entrega de Mensajes:** Garantiza la entrega de mensajes **At Least Once** (Al menos una vez), asegurando que ningún mensaje se pierda.
* **Tipos de Suscripción:**
    * **Pull (Jalar):** El *Subscriber* inicia la conexión y "jala" los mensajes del *Topic*.
    * **Push (Empujar):** Pub/Sub entrega (empuja) los mensajes al *Subscriber* (típicamente un *webhook* HTTPS).
* **Escalabilidad y Fiabilidad:** El servicio gestiona automáticamente el escalado para manejar millones de mensajes por segundo.