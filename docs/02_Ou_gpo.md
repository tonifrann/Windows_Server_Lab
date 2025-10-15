# Laboratorio Active Directory: OU’s, GPO’s y Alta Disponibilidad

Configuración de Unidades Organizativas, grupos, políticas de grupo (GPO) y verificación de replicación en un dominio con Windows Server 2022.

---

## 1. Creación de la estructura de OU

### Jerarquía definida
- **Empresa**  
  - **Usuarios**  
    - Barcelona  
    - Madrid  
  - **Equipos**  
    - Clientes  
    - Servidores  
  - **Departamentos**  
    - IT  
    - RRHH  
    - Ventas  
	
[Estructura de OU completa](../images/ou.png)

### Implementación en AD
1. Crear las OU según la jerarquía definida.  
2. Mover el PC `Windows 11` a la OU `Clientes`.

---

## 2. Creación y asignación de grupos de seguridad

- **Grupo `GG_RRHH`** → OU `RRHH`  
- **Grupo `IT_admins`** → OU `IT`  

### Delegación de permisos
- OU `Servidores` → Control total delegado al grupo `IT_admins`.  
- OU `RRHH` → Permisos de creación, borrado de usuarios y reseteo de contraseñas delegados al grupo `GG_RRHH`.  

---

## 3. Creación y asignación de usuarios

- **Marc** → OU `Barcelona`, grupo `Ventas`  
- **Juan** → OU `Madrid`, grupo `RRHH`  
- **Administrador principal** → grupo `IT_admins`  

### Asignación de roles
1. Validar que cada usuario tenga privilegios mínimos según su departamento.  
2. Confirmar que la pertenencia a grupos y la delegación de permisos funcionen correctamente.

---

## 4. Creación y aplicación de GPO’s

### GPO `Seguridad` (aplicada a OU `Equipos`)
- Bloqueo de pantalla: 900 segundos  
- Fondo de pantalla corporativo:  
  - Archivo JPG ubicado en `:\resources`  
  - Permisos: lectura a `Authenticated Users`  
  - Sin permisos para listar la carpeta, solo lectura del JPG  

### GPO `Clientes` (aplicada a OU `Clientes`)
- Deshabilitación del uso de USBs  

### GPO `Servidores` (aplicada a OU `Servidores`)
- Auditoría de todos los inicios de sesión (éxitos y fallos)  
- Denegación de inicio de sesión local  
- Inclusión de los grupos `GG_RRHH` y `GG_Ventas` 

[Configuración de GPO's aplicadas a las OU correspondientes](../images/gpo.png) 

---

## 5. Alta disponibilidad y replicación

- Usuarios, grupos y GPO’s replicados correctamente de `DC1` a `DC2`.  
- Verificación de roles FSMO:

```cmd
netdom query fsmo
