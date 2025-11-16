# 🆔 Identity Platform (Plataforma de Identidad)

**Identity Platform** es la solución de Google Cloud para el **CIAM (Customer Identity and Access Management)** (Gestión de Identidad y Acceso de Clientes). Su propósito es gestionar la autenticación y autorización de los **usuarios finales** (*end-users*) de tus aplicaciones.

## 🆚 Identity Platform vs. Cloud IAM

Es crucial entender la diferencia de enfoque entre estos dos servicios de identidad:

| Servicio | Enfoque | Quiénes son los Usuarios | Para qué se usa |
| :--- | :--- | :--- | :--- |
| **Cloud IAM** | **Autenticación y Autorización de Recursos** (*Resource Authorization*). | Empleados, Socios y Cuentas de Servicio (*Service Accounts*). | Controlar el acceso a los **recursos de GCP** (VMs, Cloud Storage Buckets, GKE, etc.). |
| **Identity Platform** | **Autenticación y Autorización de Clientes** (*Customer Authorization*). | Usuarios Finales (*End-Users*) o Clientes de tus aplicaciones. | Controlar el acceso a tus **aplicaciones** (web y móvil), no a los recursos subyacentes de GCP. |

### 🛠️ Características Clave

* **Autenticación para Aplicaciones:** Proporciona autenticación y autorización para **aplicaciones web y móviles** (iOS y Android).
* **Múltiples Métodos de Autenticación:** Soporta una amplia gama de métodos, incluyendo:
    * **Email/Password** (Correo Electrónico/Contraseña).
    * **Phone Number** (Número de Teléfono - con envío de código).
    * **Social Logins** (Inicio de Sesión Social): Utilizando cuentas de terceros como Google, Facebook o Twitter.
    * **Standards-Based:** Estándares empresariales como **SAML** (Security Assertion Markup Language) y **OIDC** (OpenID Connect).
* **Gestión de Usuarios:** Ofrece funcionalidades para el **User Enrollment and Registration** (Inscripción y Registro de Usuarios).
* **Seguridad:** Permite la **Multi-Factor Authentication (MFA)** (Autenticación Multifactor) para los usuarios finales.
* **Legado:** Es una **actualización** (*update*) de la solución anterior recomendada: **Firebase Authentication Legacy**.

### 🔗 Integración con GCP

* **Identity-Aware Proxy (IAP):** La Plataforma de Identidad se integra muy bien con **IAP**. IAP se utiliza para agregar autenticación y autorización a aplicaciones desplegadas en servicios como **App Engine** o **Cloud Run**.

---

## 💡 Escenarios: IAM vs. Identity Platform

| Escenario | Solución Recomendada | Razón |
| :--- | :--- | :--- |
| Una aplicación en una **Compute Engine VM** necesita acceso a **Cloud Storage**. | **Cloud IAM** | Se utiliza una **Service Account** (Cuenta de Servicio) adjunta a la VM, con un rol específico para Cloud Storage. |
| Un **usuario de la empresa** o un socio necesita acceso para subir objetos a un *Bucket* de Cloud Storage. | **Cloud IAM** | Controla el acceso directo a los recursos de GCP por parte de empleados/socios. |
| Quieres gestionar los **usuarios finales** (*end-users*) de tu aplicación web o móvil. | **Identity Platform** | Gestiona la autenticación y el perfil de los clientes que usan tu aplicación. |
| Quieres habilitar el **Inicio de Sesión con Facebook o Twitter** para tu aplicación. | **Identity Platform** | Ofrece integraciones nativas para autenticación social de clientes. |
| Quieres crear **flujos de trabajo de registro y *login*** de usuarios para tu aplicación. | **Identity Platform** | Proporciona las herramientas y APIs para construir la experiencia de usuario del cliente. |