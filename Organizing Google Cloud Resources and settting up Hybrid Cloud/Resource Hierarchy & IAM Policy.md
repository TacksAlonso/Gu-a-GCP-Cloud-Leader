# 🏛️ Resource Hierarchy & IAM Policy (Jerarquía de Recursos y Política de IAM)

La **Resource Hierarchy** (Jerarquía de Recursos) de GCP (Organización → Carpeta → Proyecto → Recursos) es fundamental para cómo se aplican y heredan las políticas de **IAM (Identity and Access Management)**.

## 🔗 Aplicación y Herencia de Políticas

* **Niveles de Aplicación:** Las políticas de IAM pueden establecerse en **cualquier nivel de la jerarquía** (*any level of the hierarchy*): **Organization** (Organización), **Folder** (Carpeta), **Project** (Proyecto) y **Resource** (Recurso).
* **Herencia Descendente (`Downstream Inheritance`):** Los **Resources** (Recursos) **heredan las políticas** de todos sus padres. Si una política se configura a nivel de **Organización**, **Carpeta** o **Proyecto**, los recursos la heredarán.
* **Política Efectiva (`Effective Policy`):** La política efectiva para un recurso es la **unión** (*union*) de:
    1.  La política establecida directamente sobre **ese recurso**.
    2.  La política establecida en **todos sus niveles de padres** (Proyecto, Carpeta y Organización).

> **La herencia de políticas es transitiva** (*Policy inheritance is transitive*). Un permiso otorgado a nivel de la Organización será efectivo para el Recurso más bajo.

## 🚫 Principio de Denegación Implícita

* **Principio Clave:** El **permiso otorgado a un nivel superior NO puede ser anulado y denegado** (`cannot be overridden and denied`) a un nivel inferior.
* **Implicación:** Si un permiso (ej. `storage.object.create`) se concede a nivel de **Organización**, no se puede restringir o denegar ese mismo permiso a nivel de **Proyecto** o **Recurso**. Una vez que se concede un permiso en un nivel superior, este fluye hacia abajo en la jerarquía.
* **Excepción:** Si el objetivo es restringir algo en un nivel inferior, se debe usar **Organization Policies** (Políticas de Organización), no IAM.