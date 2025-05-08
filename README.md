🧠 Ansible Lab - Automatización de Casos Prácticos
==================================================

Este repositorio contiene una serie de *playbooks* de Ansible que resuelven casos prácticos comunes en entornos mixtos (Linux y Windows). Incluye verificación de conectividad, consumo de APIs, despliegue de contenido web y gestión de usuarios en Windows.

🛠 Requisitos
-------------

-   Ansible 2.9 o superior

-   Acceso SSH a servidores Linux y WinRM a servidores Windows

-   Inventario configurado (ver archivo `inventory`)

-   Python 3 en el controlador (localhost)

* * * * *

▶️ Ejecución
------------

Para ejecutar un caso específico:

bash

CopiarEditar

`ansible-playbook -i inventory caso1.yml`

> Reemplaza `caso1.yml` por el playbook deseado.

* * * * *

📂 Detalle de cada caso
-----------------------

### ✅ `caso1.yml` - Verificación de Conectividad y Puertos

Este playbook valida la conexión y disponibilidad de servicios esenciales en los servidores:

-   **Ping a hosts Linux y Windows**

-   **Verifica puerto 22 (SSH) en Linux**

-   **Verifica puerto 3389 (RDP) en Windows**

Ideal para validar el estado inicial antes de aplicar configuraciones.

* * * * *

### 🌐 `caso2.yml` - Consumo de API de Cotización del Dólar

Este playbook realiza:

-   Consulta a la API pública de [dolarapi.com](https://dolarapi.com)

-   Obtiene cotizaciones de múltiples tipos de dólar (`oficial`, `blue`, `cripto`, etc.)

-   Genera un archivo HTML con la información usando un *template* Jinja2

> El archivo generado se guarda en: `/tmp/cotizacion.html`

* * * * *

### 🚀 `caso3.yml` - Despliegue Web en Linux

Este playbook despliega un pequeño sitio en servidores Linux:

-   Instala Apache

-   Habilita e inicia el servicio

-   Realiza backup del `index.html` si existe

-   Copia el archivo de cotización HTML generado por `caso2.yml` a `/var/www/html/index.html`

> Este caso depende de que antes se ejecute `caso2.yml`.

* * * * *

### 🪟 `caso4.yml` - Gestión de Usuarios en Windows

Este playbook crea un usuario local en servidores Windows:

-   Nombre de usuario: `demo_user`

-   Contraseña: `Contraseña123!`

-   Grupo: `Administrators`

-   Contraseña sin expiración

-   Cuenta deshabilitada al crearse

* * * * *

📁 Estructura del repositorio
-----------------------------
ansible/
  - caso1.yml                # Conectividad y puertos
  - caso2.yml                # API cotización del dólar
  - caso3.yml                # Despliegue web Linux
  - caso4.yml                # Usuarios en Windows
  - inventory                # Hosts agrupados por sistema
  - templates/
    - plantilla.html.j2    # Plantilla HTML para caso2
    
📌 Notas
--------

-   El playbook `caso2.yml` usa `delegate_to: localhost` para evitar ejecutar `uri` desde los nodos remotos.

-   Asegúrate de que el grupo `linux` y `windows` estén bien definidos en el archivo `inventory`.