# 🧑‍💻 User Identity Management in Google Cloud (Gestión de Identidades de Usuario en Google Cloud)

La gestión de identidades de usuario es el proceso de controlar quiénes son los usuarios y cómo se les permite acceder a los recursos de GCP.

## 👥 Cuentas y Roles Iniciales

* **Súper Administrador (`Super Administrator`):** El usuario inicial (típicamente una cuenta de Gmail) que crea la cuenta de prueba gratuita o la Organización. Este usuario tiene el rol de **Propietario** (`Owner`) y puede hacer **cualquier cosa** (*access everything*) dentro de la Organización.
* **Añadir Usuarios Individuales:** Puedes añadir otros usuarios a proyectos específicos.
    * **IAM Policy (Política de IAM):** La **Policy** es la lista de **Bindings** (Vinculaciones) adjuntos a un proyecto.
    * **Binding (Vinculación):** Una correspondencia entre una **Identity** (Identidad) y un **Role** (Rol).
    * **Proceso:** Asignar un rol a una cuenta de Gmail en un proyecto permite al usuario acceder a ese recurso específico en el proyecto.

> **⚠️ Advertencia Empresarial:** No se recomienda utilizar **cuentas individuales de Gmail** (`individual Gmail accounts`) para la gestión de acceso en entornos corporativos (producción). Las empresas deben utilizar soluciones de identidad centralizadas.

---

## 🏢 Gestión de Identidades a Nivel Empresarial

Las empresas utilizan proveedores de identidad centralizados para la autenticación de clientes (`client authentications`). GCP ofrece dos caminos para integrar estas identidades corporativas:

### 1. 💼 Integración con Google Workspace

* **Google Workspace (Espacio de Trabajo de Google):** Anteriormente conocido como G Suit (o Google Cloud Apps for your domain). Es el servicio de Google que proporciona correo electrónico personalizado y herramientas de colaboración (Gmail, Calendar, Drive, etc.).
* **Proceso:** Si la empresa ya utiliza **Google Workspace**, se debe **vincular** (`link`) la **GCP Organization** (Organización de GCP) con la **Google Workspace Account** (Cuenta de Google Workspace). Esto permite utilizar los usuarios y grupos ya existentes en Workspace para autenticar el acceso a GCP.

### 2. 🤝 Federación de Directorios Corporativos (`Corporate Directory Federation`)

* **Definición:** Ocurre cuando la empresa no utiliza Google Workspace, sino un **External Identity Provider (IdP)** (Proveedor de Identidad Externo) propio (ej. Active Directory, Azure Active Directory, u otro IdP).
* **Proceso de Federación:** Consiste en vincular la plataforma de Google Cloud con el **IdP externo** para que este último autentique a los usuarios.

#### ☁️ Cloud Identity (Identidad en la Nube)

* **Definición:** **Cloud Identity** es una plataforma unificada de **Identity Access and Endpoint Management** (Acceso a la Identidad y Gestión de Terminales) de GCP.
* **Función:** Actúa como el puente (*bridge*) que gestiona las identidades en la nube y facilita la **Federación** con el IdP externo.

#### 🔄 Protocolos y SSO

* **Autenticación:** La federación suele utilizar protocolos estándar como **SAML** (Security Assertion Markup Language) u **OpenID Connect** (OIDC).
    * **SAML:** Es el protocolo más común cuando se utiliza **Active Directory**.
* **Beneficio Clave:** Activa el **Single Sign-On (SSO)** (Inicio de Sesión Único). Los usuarios inician sesión en su directorio corporativo (IdP externo) y automáticamente se les permite el acceso a la plataforma Google Cloud.
* **Flujo SSO:** Los usuarios son redirigidos al IdP externo para autenticarse. Una vez autenticados, se envía una **SAML Session** (Sesión SAML) a Google Sign In, lo que les concede acceso a GCP.

#### Ejemplos de Federación

* **Federar Active Directory:** Utilizando herramientas como **Google Cloud Directory Sync** y **Active Directory Federation Services (ADFS)**.
* **Federar Azure Active Directory:** Conectando **Azure Active Directory** (un servicio de Azure) con **Cloud Identity**.

---

## ✅ Resumen de la Gestión de Identidades

1.  Si usas **Google Workspace**, vincúlalo directamente con la **Organización de GCP**.
2.  Si usas **cualquier otro IdP externo** (Active Directory, Azure AD, etc.), configura la **Federación** a través de **Cloud Identity**.
3.  Ambos caminos permiten utilizar las **Identidades Corporativas** para acceder a los recursos de GCP con **Single Sign-On**.