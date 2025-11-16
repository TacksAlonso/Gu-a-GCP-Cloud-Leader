# 📂 Organizing GCP Resources (Organización de Recursos de GCP)

## 🌳 Resources Hierarchy in GCP (Jerarquía de Recursos en GCP)

GCP implementa un modelo de **jerarquía** (*Hierarchy*) para gestionar los recursos de la nube, aplicar políticas (IAM) y administrar la facturación de forma centralizada.

**Estructura Jerárquica:**

$$\text{Organization} \rightarrow \text{Folder} \rightarrow \text{Project} \rightarrow \text{Resources}$$

* **Organization (Organización):** El nodo raíz (*Root Node*) que representa una empresa. Es el propietario de todos los recursos y es opcional (solo disponible para clientes de G Suite o Cloud Identity).
* **Folder (Carpeta):** Un contenedor (*Container*) opcional que puede contener **múltiples Proyectos** (*multiple Projects*) y otras *Folders*. Se utiliza para agrupar y aislar recursos de grandes unidades de negocio o entornos (ej. "Departamento de Marketing" o "Entorno de Producción").
* **Project (Proyecto):** La unidad de gestión fundamental. Los **Recursos** (*Resources*) (VMs, bases de datos, *Buckets*) son creados **dentro de Proyectos**. Los proyectos definen límites de IAM, facturación y red.
* **Resources (Recursos):** Los servicios específicos que se consumen (VMs, Cloud SQL, Cloud Storage, etc.).

---

## 🏢 Recommendations for Enterprises (Recomendaciones para Empresas)

* **Aislamiento de Entornos:** Crear **Proyectos separados** (*separate Projects*) para diferentes entornos (ej. Desarrollo, Pruebas y Producción). Esto garantiza el **aislamiento completo** (*complete isolation*) entre recursos.
* **Aislamiento Departamental:** Crear **Folders separadas** para cada departamento (ej. Ingeniería, Finanzas). Esto ayuda a aislar las aplicaciones de un departamento a otro. Si se tienen recursos compartidos (ej. un *Data Warehouse*), se puede generar un **Shared Folder** (*Carpeta Compartida*).
* **Estructura Granular:** Implementar un **Project per application per environment** (Un Proyecto por aplicación por entorno) para facilitar la gestión granular de IAM y la facturación.

---

# 💳 Billing Accounts (Cuentas de Facturación)

Una **Billing Account** (Cuenta de Facturación) es **obligatoria** para crear un recurso en un Proyecto que incurra en costos. Contiene los datos de pago y es independiente de la estructura organizativa.

* **Asociación:** Una cuenta de facturación puede estar asociada a **uno o más Proyectos** (*one or more Projects*).
* **Organización:** Puedes tener **múltiples Cuentas de Facturación** en una Organización.
    * *Recomendación:* Las empresas grandes deben crear una cuenta de facturación por departamento o unidad de negocio para simplificar la asignación de costos.

### Tipos de Cuentas de Facturación

1.  **Self Serve (Autoservicio) / Automatic Payment (Pago Automático):** El cobro se realiza automáticamente a una tarjeta de crédito o cuenta bancaria cuando el saldo alcanza un umbral o mensualmente.
2.  **Invoiced (Facturada) / Manual Payment (Pago Manual):** Genera facturas (*Invoices*) mensuales, adecuadas para grandes clientes empresariales.

---

## 💸 Managing Billing - Budget, Alerts and Exports (Gestión de Facturación - Presupuestos, Alertas y Exportaciones)

### 📈 Presupuestos y Alertas

Una de las recomendaciones más importantes es establecer un **Budget** (Presupuesto) de facturación en la nube para **evitar sorpresas** (*Avoid Surprises*) en los costos.

* **Alertas:** Se pueden configurar **Alerts** (Alertas) que notifican a los usuarios cuando el gasto se aproxima o excede el presupuesto.
* **Umbrales por Defecto:** Los umbrales de alerta por defecto están fijados en **50%, 90% y 100%** del presupuesto.
* **Notificaciones Avanzadas:** Opcionalmente, se puede enviar alertas a **Pub/Sub** para que los administradores de facturación y otras herramientas automatizadas reaccionen a los eventos de gasto.

### 📤 Exportación de Datos

* **Finalidad:** Se pueden **Export Billing Data** (Exportar los Datos de Facturación) para un análisis detallado de costos y tendencias.
* **Destinos:** Los datos se pueden exportar a:
    * **BigQuery:** Permite ejecutar consultas SQL sobre los datos de costos para un análisis granular.
    * **Cloud Storage:** Para archivar los datos de facturación en formato CSV o JSON.