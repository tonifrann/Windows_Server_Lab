## Configuración de Backups

### 1. Preparación en el servidor DFS (File Server)
- En el servidor **DFS**, donde se aloja el **File Server**, se agrega un **nuevo disco duro** a la máquina virtual.  
- Se **formatea** el disco y se crea una carpeta compartida llamada `Backups`.  
- Se asignan **permisos de escritura** para el grupo **Administradores**.

### 2. Instalación de la característica de Backup en DC1
- En **DC1**, abrir **Server Manager → Agregar roles y características**.  
- Avanzar con **Next** hasta llegar a **Features** (no es un rol).  
- Seleccionar **Windows Server Backup** y completar la instalación.

### 3. Creación del Backup Programado en DC1
- Abrir **Windows Server Backup**.  
- Crear un **nuevo Backup Schedule** con las siguientes opciones:  
  - **Tipo de backup:** *Bare metal recovery (Todo el sistema)*  
  - **Frecuencia:** *Diario a las 21:00*  
  - **Destino:** `\\dfs.empresa.local\Backups`
  
[Ver captura del backup realizado](../images/backup.png)

### 4. Backup adicional en el servidor DFS
- En el propio servidor **DFS**, crear otro **Backup Schedule**.  
- Configurar para que se realice copia de seguridad de la unidad **E:\\**,  
  que contiene los datos del **File Server**.
  
[Ver captura de la carpeta donde se han  guardado los backups](../images/carpeta.png)