# 💻 Compute Engine - Máquinas Virtuales (VM)

## 📌 Conceptos Clave de Instancia

* **Creación:** Las VM se lanzan desde la consola de GCP.
* **Personalización:** Al crear una VM, se definen:
    * **Imagen del OS:** Amplia selección (Linux, Windows).
    * **Región y Zona:** Ubicación geográfica para la latencia y disponibilidad.
    * **Características:** Tipo de máquina (CPU, RAM, red).
    * **Firewall:** Configuración para el tráfico de red (ej. HTTP/HTTPS).
    * **Static IP Address:** Por defecto se tienen IP externas efimeras que cada que la instancia sea detenida o reiniciada cambiaran, se puede asignar una IP estatica pero refleja un costo extra y debe ser asociado una vez ya creada la instancia
* **Scripts de Inicio (`Startup Scripts`):** Comandos que se ejecutan automáticamente cuando la VM inicia o reinicia. Son ideales para instalar software, actualizar paquetes, o aplicar parches (como *boostrap scripts*).

---

## 📝 Plantillas de Instancia (`Instance Templates`)

* **Propósito:** Son **borradores predefinidos** que permiten crear VM de forma rápida, repetible y con una configuración idéntica.
* **Uso:** Ideales para generar múltiples instancias (ej. para un grupo de instancias gestionadas).
* **Inmutabilidad:** Una vez creadas, **no se pueden modificar**. Para hacer cambios, se debe copiar la plantilla existente y generar una versión nueva.
* **Beneficio:** Reducen significativamente los tiempos de despliegue al predefinir los valores por defecto.

---

## 🖼️ Imágenes Personalizadas (`Custom Images`)

* **Propósito:** Crear una imagen de disco a partir de una VM existente para capturar su configuración, software y datos específicos.
* **Beneficio:** Permiten generar nuevas instancias preconfiguradas rápidamente, reduciendo errores y tiempo de configuración manual.
* **Proceso:**
    * La imagen se genera a partir de un **disco persistente**.
    * **Recomendación:** Google sugiere **apagar la instancia de VM** antes de la creación para garantizar la integridad de la imagen. La creación en caliente es bajo tu riesgo.
* **Alcance:** Se pueden configurar para ser **regionales** o **multirregionales** según las necesidades de disponibilidad y costo.
* **Gestión:** Permite el control del ciclo de vida, pudiendo marcar versiones como obsoletas o **deprecadas** para asegurar el cumplimiento de políticas de seguridad.
* **Integración:** Las Plantillas de Instancia pueden utilizar estas nuevas imágenes preconfiguradas.

---

## 💸 Descuentos por Uso Sostenido (`Sustained Use Discounts - SUDs`)

* **Naturaleza:** Son **descuentos automáticos** aplicados al uso continuo de las VM durante el mes de facturación.
* **Mecánica:** No requieren ninguna acción o habilitación. A **mayor** tiempo de ejecución continua (ej. 80% del mes), **mayor** es el porcentaje de descuento.
* **Aplicación:** Se aplican a instancias directas de **Compute Engine** y a las utilizadas en **Google Kubernetes Engine (GKE)**.
* **Restricciones (No Aplica):**
    * Instancias generadas por **App Engine Flexible**.
    * Instancias utilizadas por **Dataflow**.
    * Ciertos tipos específicos de máquinas de Compute Engine (se debe verificar la elegibilidad).

---

## 💸 Descuentos por Uso Comprometido (`Committed Use Discounts - CUDs`)

* **Naturaleza:** Es un contrato por un periodo de uso específico (normalmente **uno o tres años**) a cambio de un descuento significativo en los precios de los recursos de Compute Engine.
* **Descuento:** Puede alcanzar hasta un **70%** (dependiendo del recurso y la duración del compromiso).
* **Ventaja Clave:** El descuento es **mayor** que el ofrecido por los Descuentos por Uso Sostenido (SUDs).
* **Aplicación:** Se aplica a instancias directas de **Compute Engine** y a las utilizadas en **Google Kubernetes Engine (GKE)**.
* **Restricciones:** El compromiso **no se puede cancelar**. Si hay errores de facturación o necesitas un cambio, debes contactar a Cloud Billing Support.

---

## 🛑 VM Preemptivas (`Preemptible VMs - Legacy`)

* **Definición:** Instancias de corta duración que GCP puede **detener** en cualquier momento debido a la demanda de recursos.
* **Límite de Ejecución:** Tienen un tiempo máximo de funcionamiento de **24 horas** (aunque pueden ser finalizadas antes por GCP).
* **Alerta de Finalización:** GCP envía un aviso de **30 segundos** antes de detener la instancia, dando tiempo para guardar el estado.
* **Casos de Uso:**
    * **Tolerancia a Fallos:** Para aplicaciones que pueden ser interrumpidas y reiniciadas sin gran impacto (ej. procesamiento por lotes).
    * **Costo:** Son muy accesibles y con descuento.
    * **Carga de Trabajo No Inmediata:** Se usan para **tareas asíncronas** o **de baja prioridad** donde no importa si la ejecución se detiene y se reanuda más tarde.
* **Restricciones:**
    * Disponibilidad no garantizada.
    * No tienen **SLA** (Acuerdo de Nivel de Servicio).
    * No se pueden migrar a una VM estándar.
    * No se reinician automáticamente tras una detención.
    * Los créditos gratuitos de GCP no se aplican.

---

## 💰 VM Spot (`Spot VMs - Recommended`)

* **Definición:** Es la **versión mejorada** de las VM Preemptivas (sustituto recomendado).
* **Diferencia Clave:** **No tienen límite de tiempo de ejecución** (pueden ejecutarse indefinidamente si hay recursos).
* **Características Compartidas (con Preemptivas):**
    * GCP las puede finalizar en cualquier momento con un aviso de **30 segundos**.
    * Disponibilidad no garantizada.
    * Los créditos gratuitos de GCP no se aplican.
* **Costo:** Tienen una tarifa de descuento **dinámica** y generalmente más profunda (entre 60% y 91% de descuento) que las VM estándar.

---

## 🔒 Nodos de Inquilino Único (`Sole-Tenant Nodes`)

* **Shared Tenancy (Default):** El host físico se comparte con instancias de VM de otros clientes de GCP.
* **Sole-Tenant:** Un host físico está **dedicado** a las instancias de VM de un **solo cliente**, asegurando aislamiento.
* **Casos de Uso:**
    * **Seguridad y Conformidad:** Requerimientos regulatorios que exigen separación física del hardware.
    * **Licenciamiento:** Para usar licencias por CPU o por procesador existentes (función **Bring Your Own License - BYOL**).
    * **Alto Rendimiento:** Para cargas de trabajo que requieren un aislamiento de hardware para optimizar el rendimiento.

---

## ⚙️ Tipos de Máquina Personalizados (`Custom Machine Types`)

* **Uso:** Cuando las configuraciones de VM predefinidas no satisfacen los requerimientos exactos de la aplicación.
* **Personalización:** Permite elegir el **número de vCPUs** y la **cantidad de memoria** dentro de rangos específicos.
* **Tipos Aplicables:** Solo disponible para series de máquinas como **E2, N2 o N1**.
* **Facturación:** Se paga por la cantidad exacta de vCPU y memoria provisionadas.

---

## 💲 Costos de VM (`VM Cost`)

* **1. Costo de Infraestructura:** Incluye el aprovisionamiento de recursos como **vCPU, RAM, GPU** y **almacenamiento en disco**.
* **2. Costo de Licenciamiento:** Para sistemas operativos que requieren licencia (como imágenes *Premium* de Windows o Red Hat).
    * **Pay-As-You-Go (PAYG):** Pago por el tiempo de uso de la licencia.
    * **Bring Your Own License/Subscription (BYOL/BYOS):** El cliente usa sus propias licencias existentes para evitar el costo de licenciamiento de Google.

---

## 📝 Escenarios de Uso Común

* **Personalizar OS y Software:** `Custom Image`
* **Optimizar Carga de Trabajo con Mix Único de Recursos:** `Custom Machine Types`
* **Necesidad de IP Fija tras Reinicios:** `Static IP Addresses`
* **Necesidades Predecibles y Descuentos Profundos (1 o 3 años):** `Committed Use Discounts`
* **Cargas de Trabajo Tolerantes a Fallos y de Bajo Costo (Asíncronas):** `Preemptible VMs` / `Spot VMs`

---

## 🔄 Grupos de Instancias (`Instance Group`)

* **Definición:** Conjunto de instancias de VM gestionadas como una única entidad lógica.
* **Tipos:**
    * **Managed Instance Group (MIG):** Instancias **idénticas** (misma plantilla, tipo de máquina, imagen).
        * **Tipos de Carga:**
            * **Stateless:** Para servicios web, APIs (pueden escalar/morir fácilmente).
            * **Stateful:** Para bases de datos o servicios con estado (se mantiene la configuración del disco y metadatos al reiniciar/reemplazar).
        * **Features (Funcionalidades):**
            * **Autoescalado:** Sube/baja el número de instancias basado en métricas (Utilización de CPU, Load Balancer, Stackdriver).
            * **Auto Healing:** Reemplaza automáticamente las instancias que fallan las *Health Checks*.
            * **Lanzamientos Gestionados:** Permite actualizaciones de software controladas (*Rolling Updates*, *Canary Deployment*).
            * **Integración con Load Balancer.**
    * **Unmanaged Instance Group:** Contiene VM que **pueden ser distintas** (diferentes imágenes, hardware). No ofrece las funcionalidades automáticas (Autoescalado, Auto Healing). No recomendado a menos que sea estrictamente necesario.
* **Locación:** Pueden ser **Zonales** o **Regionales** (lo último es recomendado para alta disponibilidad).

---

## 🌐 Cloud Load Balancing

* **Propósito:** Distribuye el tráfico de red entre las instancias de VM, a través de una o más regiones.
* **Servicio Gestionado:** GCP se encarga de la disponibilidad y el autoescalado del balanceador de carga.
* **Visibilidad:**
    * **Público (External):** Disponible para todo Internet.
    * **Privado (Internal):** Solo disponible dentro de una VPC específica.
* **Tipos Comunes (Global/Regional):**
    * **External HTTP(S):** Global, para tráfico web.
    * **Internal HTTP(S):** Regional, para servicios internos.
    * **SSL Proxy, TCP Proxy:** Global.
    * **External Network TCP/UDP, Internal TCP/UDP:** Regional (Nota: UDP no es multiregional).
* **Creación:** Se configura en la sección **Network Services**.
