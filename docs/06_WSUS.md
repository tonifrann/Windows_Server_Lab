# Laboratorio Active Directory: Implementación de WSUS

Configuración completa de un servidor **WSUS (Windows Server Update Services)** en la infraestructura del dominio, con base de datos interna (WID) y distribución controlada de actualizaciones a los equipos clientes.

---

## 1. Instalación y configuración inicial del rol WSUS

1. En el servidor **DFS**, abrir **Server Manager → Add Roles and Features**.  
2. Seleccionar el rol **Windows Server Update Services**.  
3. Marcar la característica **WID Connectivity**, ya que se utilizará una **Internal Database (no SQL)**.  
4. Establecer la ruta de almacenamiento de las actualizaciones en:  

## 2. Creación y vinculación de la GPO “WSUS”

1. Crear una nueva **GPO** llamada **"WSUS"**.  
2. Vincular la GPO a la **OU `Clientes`**.  
3. Navegar a la siguiente ruta dentro del Editor de GPO:
   Computer Configuration → Administrative Templates → Windows Components → Windows Update

### Configuración de políticas WSUS

| **Política** | **Configuración** | **Descripción** |
|--------------|------------------|-----------------|
| **Specify intranet Microsoft update service location** | Activado → `http://dfs.empresa.local` | Define el servidor WSUS interno como fuente de actualizaciones. |
| **Configure Automatic Updates** | Opción **4 – Auto download and schedule the install** (Lunes 22:00) | Descarga automática y programación semanal. |
| **Enable client-side targeting** | Activado → Grupo **Clientes** | Asigna los equipos automáticamente al grupo *Clientes* en WSUS. |
| **No auto-restart with logged on users** | Activado | Evita reinicios automáticos si hay usuarios conectados. |

---

## 3. Configuración en la consola WSUS

1. En **WSUS → Computers**, crear el grupo **Clientes**.  
2. Los equipos del dominio que reciban la GPO se añadirán automáticamente a este grupo.  
3. Confirmar que las sincronizaciones se ejecutan correctamente y que aparecen las actualizaciones de **Windows 11**.

---

## 4. Verificación desde el cliente Windows 11

En el equipo **W11**, ejecutar los siguientes comandos en **CMD**:

```cmd
gpupdate /force
gpresult /R
