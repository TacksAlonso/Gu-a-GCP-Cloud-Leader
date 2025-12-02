# 📈 Cloud Monitoring (Monitoreo en la Nube)

* **Propósito:** Es el servicio para **recolectar métricas** (datos numéricos en el tiempo) sobre el rendimiento, **Uptime** (tiempo de actividad) y salud de las aplicaciones y la infraestructura de GCP.
* **Funcionalidades Clave:**
    * **Dashboards (Paneles de Control):** Visualiza las métricas en tiempo real.
    * **Alerting (Alertas):** Permite configurar notificaciones que se disparan cuando una métrica excede o cae por debajo de un umbral definido (ej. CPU > 80%).
    * **Uptime Checks (Comprobaciones de Actividad):** Monitorea la disponibilidad de los puntos finales públicos y privados.
* **Integración con GKE:** Monitorea el rendimiento del *Cluster* (CPU, memoria de los *Nodes*) y el rendimiento de los *Pods* (el HPA usa estas métricas).