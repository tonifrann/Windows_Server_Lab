# 🧩 Laboratorio Active Directory con Windows Server 2022

Configuración paso a paso de un entorno de dominio completo con dos controladores de dominio (DC1 y DC2), servicio DNS, zona inversa y replicación funcional.

---

## 1. Creación del primer Domain Controller (DC1)

### Configuración de la máquina virtual
**Hyper-V → Nueva VM:**
- **RAM:** 4096 MB  
- **Disco:** 127 GB (dinámico)  
- **Conmutador de red:** Privado (sin acceso a Internet)

### Instalación del sistema operativo
- **SO:** Windows Server 2022  
- **Configuración de red:**
  - **IPv4:** 172.16.0.100  
  - **DNS:** 172.16.0.100  
  - **IPv6:** Desactivado  
  - **Hostname:** `DC1`

### Instalación del rol Active Directory Domain Services
1. Instalar el rol **Active Directory Domain Services (AD DS)**.  
2. Crear un **nuevo bosque**: `empresa.local`.  
3. Incluir los roles de **DNS** y **Catálogo global (Global Catalog)**.  
4. Promocionar el servidor como **Domain Controller principal (DC1)**.

### Verificación
```bash
repadmin /replsummary

Resultado sin errores (replicación OK).


## 🧩 2. Creación del segundo Domain Controller (DC2)

Configuración del segundo controlador de dominio para asegurar la **redundancia**, **alta disponibilidad** y **replicación automática** del directorio activo.

---

### Configuración de la máquina virtual
**Hyper-V → Nueva VM:**
- **RAM:** 4096 MB  
- **Disco:** 127 GB (dinámico)  
- **Conmutador de red:** Privado (sin acceso a Internet)  
- **IPv4:** 172.16.0.101  
- **DNS primario:** 172.16.0.100  
- **DNS secundario:** 127.0.0.1  
- **Hostname:** `DC2`

---

### Unión al dominio existente
Unir el servidor al dominio **empresa.local**:
1. Cambiar el nombre del equipo a `DC2`.
2. En **Propiedades del sistema → Nombre de equipo → Dominio**, ingresar `empresa.local`.
3. Usar credenciales de administrador del dominio (por ejemplo: `Administrador@empresa.local`).

Una vez unido, **reiniciar** el servidor para aplicar los cambios.

---

### Promoción como Domain Controller adicional
1. Instalar el rol **Active Directory Domain Services (AD DS)** desde el **Server Manager**.  
2. Seleccionar **Agregar un controlador de dominio a un dominio existente**.  
3. Confirmar el dominio `empresa.local`.  
4. Habilitar las opciones:  
   - **Servidor DNS**  
   - **Catálogo global (Global Catalog)**  
5. Completar el asistente para promover `DC2` como segundo **Domain Controller**.

---

### Comprobación de replicación y roles FSMO

Verificar el estado de la replicación entre controladores de dominio:
```bash
repadmin /replsummary



##3.- Configuración DNS y Zona Inversa##

En DC1 → añadir 8.8.8.8 como Forwarder

Crear zona inversa 172.16.0.x

Añadir manualmente los punteros PTR de DC1 y DC2

Verificar resolución con:

nslookup 172.16.0.100


