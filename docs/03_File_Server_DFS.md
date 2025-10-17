# Laboratorio Active Directory: DFS y File Server

Configuración de discos, File Server, quotas y DFS (Distributed File System) en un entorno con Windows Server 2022.

---

## 1. Preparación de discos y File Server

### Configuración de discos
1. Crear dos discos nuevos en la VM `DC2`.  
2. Inicializar y formatear los discos para su uso en almacenamiento de datos.

### Instalación de roles
- Verificar que el rol **File Server** esté instalado (se instaló automáticamente al compartir la carpeta `resources`).  
- Instalar el rol **File Server Resource Manager (FSRM)**.

### Configuración de Storage Pool y disco virtual
1. Desde **File and Storage Services**, crear un **Storage Pool** con los dos discos nuevos.  
2. Crear un **nuevo disco virtual** en modo `Mirror`.  
3. Configurar **deduplicación** en el disco virtual.

[Ver captura Mirror](../images/mirror.png)

### Configuración de carpetas y permisos
- Crear la carpeta `ventas` en el disco virtual.  
- Asignar permisos de **modificación** al grupo `GG_ventas`.  
- Configurar una **cuota** de 5 GB para la carpeta desde **File Server Resource Manager**.

[Ver captura de la cuota](../images/quota.png)

### Verificación desde PowerShell
**powershell**

Get-Disk
Get-StoragePool
Get-DedupStatus
Get-FSRMQuota

---

# Laboratorio Active Directory: DFS (Distributed File System)

Configuración de DFS Namespaces y DFS Replication para sincronización de carpetas entre servidores.

---

## 1. Preparación del servidor DFS

1. Crear un nuevo servidor llamado `DFS`.  
2. Instalar los roles:
   - **DFS Namespaces**  
   - **DFS Replication**  
   tanto en `DC2` como en `DFS`.

---

## 2. Creación del Namespace DFS

1. Crear el Namespace: `\\empresa.local\Folder`  
2. Añadir carpetas compartidas de ambos servidores:
   - `\\DC2.empresa.local\Folder`  
   - `\\DFS.empresa.local\Folder`  
3. Configurar permisos de **escritura** en `C:\DFSroots\Folder` de cada servidor para el grupo `GG_ventas`.  
4. Verificar que el usuario **Marc** pueda crear archivos desde Windows 11.

[Ver captura Namespace DFS](../images/dfs_name.png)

---

## 3. Configuración de replicación DFS

1. Crear un **Grupo de replicación**.  
2. Añadir los servidores `DC2` y `DFS`.  
3. Seleccionar la carpeta `E:\ventas` de `DC2` como origen y configurar DFS para replicarla en la misma ubicación en `DFS`.  
4. Desde Windows 11, crear un documento en `\\DC2.empresa.local\ventas` y verificar que se replique correctamente en `E:\ventas` del servidor `DFS`.

[Ver captura Replication DFS](../images/dfs_rep.png)



