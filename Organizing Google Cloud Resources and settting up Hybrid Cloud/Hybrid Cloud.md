# 🔄 Hybrid Cloud (Nube Híbrida)

Google Cloud ofrece varias opciones para establecer una **Nube Híbrida** (*Hybrid Cloud*), conectando la **red local** (*on-premise network*) del cliente con la **Red de la Nube Privada Virtual** (*VPC Network*) de GCP.

## 1. 🌐 Cloud VPN (Red Privada Virtual en la Nube)

**Cloud VPN** es un servicio que extiende la red local (*on-premise network*) a la red de GCP, creando un túnel seguro.

* **Implementación:** Se implementa mediante un **IPSec VPN Tunnel** (Túnel VPN IPSec).
* **Tráfico:** El tráfico pasa por la **Internet pública** (*public internet*).
* **Seguridad:** El tráfico se **encripta** (*encrypted*) usando el **Internet Key Exchange Protocol** (Protocolo de Intercambio de Claves de Internet - IKE).

### Tipos de Cloud VPN

| Tipo | SLA (Acuerdo de Nivel de Servicio) | Direcciones IP Externas | Enrutamiento |
| :--- | :--- | :--- | :--- |
| **HA VPN** (*High Availability VPN*) | **99.99%** | Dos direcciones IP externas (*external IP addresses*) | Solamente soporta **Enrutamiento Dinámico (BGP)** (*Dynamic Routing*). |
| **Classic VPN** (VPN Clásica) | **99.9%** | Una sola dirección IP Externa (*external IP address*) | Soporta **Enrutamiento Estático** (*Static Routing*) y **Dinámico** (BGP). |

---

## 2. ⚡ Cloud Interconnect (Interconexión en la Nube)

**Cloud Interconnect** proporciona una **conexión física directa** (*direct physical connection*) de alta velocidad entre las redes locales (*on-premise networks*) y las redes VPC de GCP.

* **Beneficios:** Proporciona una **Alta Disponibilidad** (*High Availability*) y **Alto Rendimiento** (*High Performance*).
* **Tráfico:** El intercambio de información se produce a través de una **red privada** (*private network*).
    * **Costos:** Esto reduce los **costos de salida** (*egress costs*), ya que el tráfico no utiliza Internet pública.
    * **Acceso:** Permite utilizar las **direcciones IP internas** (*internal IP addresses*) de la red VPC para comunicarse desde la red local.
* **Acceso a Servicios:** Permite acceder a las **API y servicios de Google compatibles de forma privada** desde las aplicaciones locales.
* **Recomendación:** Se recomienda para necesidades de **gran ancho de banda** (*large bandwidth*) y latencia predecible.

### Tipos de Conexiones de Cloud Interconnect

* **Dedicated Interconnect** (Interconexión Dedicada):
    * Conexión física directa y exclusiva desde tu centro de datos hasta Google.
    * Configuraciones de **10 Gbps o 100 Gbps**.
* **Partner Interconnect** (Interconexión de Socios):
    * Se conecta a GCP a través de un **proveedor de servicios** (*Service Provider*) tercero.
    * Configuraciones de **50 Mbps hasta 10 Gbps**.

---

## 3. 🕸️ Direct Peering (Interconexión Directa)

* **Definición:** Se utiliza para conectar la red del cliente a la red de Google mediante una **Interconexión de Red** (*Network Peering*) directa.
* **Ruta:** Se trata de una ruta directa desde la red optimizada de Google (el *Edge*).
* **Servicio:** **No es un servicio de GCP** gestionado (*managed GCP service*), sino una conexión de red de bajo nivel fuera del ámbito de los servicios de GCP.
* **Recomendación:** **No se recomienda** para conectividad de nube híbrida. Las opciones recomendadas, con SLA y gestión integrada, son **Cloud Interconnect** y **Cloud VPN**.