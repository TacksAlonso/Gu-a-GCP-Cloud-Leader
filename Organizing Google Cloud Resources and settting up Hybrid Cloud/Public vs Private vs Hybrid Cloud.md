# ☁️ Public vs Private vs Hybrid Cloud (Nube Pública vs Privada vs Híbrida)

La elección del modelo de nube define la propiedad, la responsabilidad y el modelo financiero de la infraestructura de TI.

---

## 🌎 Public Cloud (Nube Pública)

* **Definición:** Tu *host* (anfitrión) y toda la infraestructura se alojan en la nube del proveedor (ej. Google Cloud).
* **Propiedad y Gasto:**
    * **No necesitas** ningún tipo de **Data Center propio** (*Own Data Center*).
    * **No tienes Gastos de Capital** (*Capital Expenditure* - CapEx), es decir, no hay que invertir dinero por adelantado en infraestructura.
    * **Modelo Financiero:** Es **Pago por Uso** (*Pay-as-you-go*); se paga únicamente por lo que se usa.
* **Escalabilidad:** Tienes a disposición una **Escala Ilimitada** (*Unlimited Scale*). Si se requiere más capacidad, se puede aumentar o disminuir fácilmente (**Elasticidad**).
* **Responsabilidad:** El **hardware es propiedad de Google Cloud**, por lo cual toda la responsabilidad de este hardware es de Google Cloud (Modelo de Responsabilidad Compartida).

---

## 🏢 Private Cloud (Nube Privada)

* **Definición:** Tu *host* (anfitrión) se aloja en tu **Data Center** (*Centro de Datos*) propio (o en una infraestructura dedicada exclusivamente a ti).
* **Propiedad y Gasto:**
    * Necesitas **Gastos de Capital** (*Capital Expenditure* - CapEx) para la compra de equipos.
    * Se tiene que **invertir en infraestructura** (servidores, almacenamiento, red, etc.).
    * **Modelo Financiero:** Se paga por la infraestructura **aunque no se esté usando** en el momento.
* **Escalabilidad:** Requiere una **planeación más elaborada**. Un **escalamiento no es tan sencillo** de realizar y es limitado por el hardware físico.
* **Responsabilidad:** Como dueño de la infraestructura, **toda la responsabilidad** de la seguridad física y la gestión del hardware es **propia**.

---

## 🔄 Hybrid Cloud (Nube Híbrida)

* **Definición:** Es una **combinación** (*Combination*) de **Nube Privada y Nube Pública**, unidas por tecnología que permite la portabilidad de datos y aplicaciones.
* **Distribución de Carga:** La **carga de trabajo** (*Workload*) se distribuye dependiendo de las necesidades. Se realiza una parte en la Nube Pública y otra en la Nube Privada.
* **Ventajas:** Una ventaja considerable es la **Flexibilidad** (*Flexibility*) para mover cargas de trabajo y aprovechar el entorno más adecuado para cada tarea.
* **Desventajas:** La gestión se vuelve **muy compleja** (*very complex to manage*), ya que se tienen recursos en la Nube Pública y recursos propios.

---

## 🌎 Multi Cloud (Multi Nube)

* **Definición:** Ocurre cuando se utiliza **múltiples plataformas en la nube** (*multiple cloud platforms*) (ej. AWS, Azure y Google Cloud) para diferentes propósitos o para evitar la dependencia de un solo proveedor (*Vendor Lock-in*), con o sin infraestructura local.
* **Ventajas:**
    * Ofrece mucha más **Flexibilidad** y capacidad de elegir el mejor servicio de cada proveedor.
    * Mitigación de riesgos al no depender de un solo proveedor.
* **Desventajas:**
    * Aumenta mucho la **Complejidad** (*Complexity*) operativa, de monitoreo y de gestión de seguridad (IAM) al tener que interactuar con múltiples APIs y herramientas.