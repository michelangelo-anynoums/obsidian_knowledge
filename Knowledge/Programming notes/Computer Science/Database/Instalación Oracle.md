> [!abstract] ### ⚙️ Guía de Instalación de Oracle
> Enlaces oficiales de descarga y parámetros esenciales para configurar la base de datos local.

### 📥 Enlaces de Descarga

* **Oracle Database (XE):** 💾 [Descargar Oracle XE](https://www.oracle.com/es/database/technologies/xe-downloads.html)
* **IDE de Desarrollo:** 🛠️ [Descargar SQL Developer](https://www.oracle.com/es/database/sqldeveloper/technologies/download/)

---

### 🔌 Parámetros de Conexión (Database Connection)

> [!key] Configuración Local
> Utiliza estos valores exactos al crear tu nueva conexión en SQL Developer.

| Parámetro | Valor Sugerido | Alternativa |
| :--- | :--- | :--- |
| **Service Name** | `XEPDB1` | — |
| **Hostname** | `localhost` | `127.0.0.1` |
| **Port** | `1521` | `1522` |



---
> [!danger] ### ⚠️ Guía de Desinstalación Limpia de Oracle
> Sigue estos pasos de forma secuencial si el programa está fallando en tu PC.

### 📋 Paso 1: Detener procesos activos
Antes de eliminar archivos, es necesario liberar la memoria del sistema.

1. Presiona `Win + R`, escribe **services.msc** y pulsa Enter.
2. Localiza y **detén** todos los servicios que comiencen con la palabra `Oracle`.
	- 🛑 `OracleServiceXE`
	- 🛑 `OracleOraDB21Home1TNSListener`
3. Asegúrate de **cerrar por completo** las siguientes aplicaciones:
	- [ ] SQL Developer
	- [ ] SQL*Plus

---

### 🖥️ Paso 2: Desinstalación del sistema
1. Dirígete a: **Configuración** > **Aplicaciones** > **Aplicaciones instaladas**.
2. Utiliza la barra de búsqueda para encontrar tu versión actual:
	- 🔍 *Oracle Database 21c Express Edition* (o similar).
3. Haz clic en los tres puntos y selecciona **Desinstalar**.
4. Completa todo el proceso guiado por el asistente de Windows.

---

### 🔄 Paso 3: Finalizar el proceso
> [!info] **¡Casi listo!**
> **Reinicia tu equipo** de inmediato para aplicar todos los cambios, limpiar el registro de Windows y liberar los puertos que utilizaba la base de datos.
