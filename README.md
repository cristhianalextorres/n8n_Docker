# 🚀 Instalación de n8n en Local con Docker (Guía para Campistas)

Este repositorio contiene una guía **paso a paso** para instalar **n8n en local** usando **Docker y Docker Compose**.

El objetivo es que cualquier campista pueda:
- Instalar n8n en su computador
- Ejecutarlo localmente
- Apagarlo y encenderlo cuando lo necesite
- Evitar errores comunes de Docker y WSL

---

## 📌 ¿Qué es n8n?

**n8n** es una plataforma de automatización de procesos que permite crear flujos de trabajo integrando:
- APIs
- Webhooks
- Bases de datos
- Servicios externos
- Inteligencia Artificial

Todo desde una interfaz visual y extensible.

---

## 🧰 Requisitos previos

Antes de comenzar, asegúrate de tener instalado:

- ✅ **Windows 10 / 11 (64 bits)**
- ✅ **Docker Desktop**
  - Descarga: https://www.docker.com/products/docker-desktop/
- ✅ **PowerShell**
- ✅ Virtualización habilitada en la BIOS

---

## 🔍 Verificar instalación de Docker

Abre **PowerShell** y ejecuta:

```powershell
docker --version
docker compose version
```

Si ambos comandos responden correctamente, puedes continuar.

---

## 📁 Estructura del proyecto

```text
n8n/
│
├── docker-compose.yml
└── README.md
```

---

## 🛠️ Paso 1 – Crear el archivo `docker-compose.yml`

Dentro de la carpeta del proyecto, crea un archivo llamado:

```text
docker-compose.yml
```

Pega el siguiente contenido:

```yaml
version: "3.8"

services:
  n8n:
    image: docker.n8n.io/n8nio/n8n
    container_name: n8n
    ports:
      - "5678:5678"
    environment:
      - GENERIC_TIMEZONE=America/Bogota
      - TZ=America/Bogota
      - N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=true
      - N8N_RUNNERS_ENABLED=true
    volumes:
      - n8n_data:/home/node/.n8n
    restart: unless-stopped

volumes:
  n8n_data:
```

📌 Este archivo define:
- El contenedor de n8n
- El puerto de acceso
- La zona horaria
- Persistencia de datos
- Reinicio automático

---

## ▶️ Paso 2 – Levantar n8n

Desde la carpeta donde está el archivo `.yml`, ejecuta:

```powershell
docker compose up -d
```

Este comando:
- Descarga la imagen de n8n
- Crea el contenedor
- Lo deja corriendo en segundo plano

---

## 🔍 Paso 3 – Verificar que el contenedor esté activo

Ejecuta:

```powershell
docker ps
```

Debes ver un contenedor llamado **n8n** con el puerto `5678` expuesto.

---

## 🌐 Paso 4 – Acceder a n8n

Abre tu navegador y entra a:

```
http://localhost:5678
```

🎉 Si ves la interfaz de n8n, la instalación fue exitosa.

---

## ⏹️ Apagar n8n

Cuando no lo estés usando:

```powershell
docker compose down
```

⚠️ Esto **NO elimina** tus flujos ni configuraciones.

---

## ▶️ Encender n8n nuevamente

```powershell
docker compose up -d
```

No es necesario reinstalar nada.

---

## 🔄 Reiniciar n8n

```powershell
docker restart n8n
```

---

## 💾 Persistencia de datos

Toda la información de n8n se guarda en el volumen:

```text
n8n_data
```

Esto incluye:
- Workflows
- Credenciales
- Configuraciones
- Webhooks

Los datos permanecen aunque apagues el contenedor o reinicies el equipo.

---

## 🚨 Errores comunes y soluciones

### ❌ Error: `WSL needs updating`
Solución (PowerShell como Administrador):

```powershell
wsl --update
wsl --shutdown
```

Luego reinicia Docker Desktop.

---

### ❌ Error: `REGDB_E_CLASSNOTREG`
Este error indica que **WSL está mal registrado en Windows**.

Solución recomendada:
1. Desinstalar y reinstalar WSL
2. Reiniciar Windows
3. Volver a abrir Docker Desktop

👉 Este error **no se soluciona solo con `wsl --update`**.

---

### ❌ Puerto 5678 ocupado
Cambia el puerto en el archivo `docker-compose.yml`:

```yaml
ports:
  - "5680:5678"
```

Accede luego a:

```
http://localhost:5680
```

---

## 📚 Próximos pasos

Una vez n8n esté funcionando, podrás:
- Crear flujos con Webhooks
- Integrar APIs
- Automatizar procesos
- Conectar servicios de IA
- Construir proyectos reales

---

## 👨‍🏫 Uso educativo

Este tutorial fue diseñado para uso académico y formativo, con el objetivo de facilitar la adopción de herramientas modernas de automatización y arquitectura local con Docker.

---

🚀 ¡Bienvenido al mundo de la automatización con n8n!

