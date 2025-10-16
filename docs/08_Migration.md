##  Migración de Controladores de Dominio 2022 → 2025

### Infraestructura inicial

| Servidor | Sistema operativo | Dirección IP | Rol |
|-----------|-------------------|---------------|-----|
| DC1 | Windows Server 2022 | 172.0.16.100 | Controlador de dominio principal |
| DC2 | Windows Server 2022 | 172.0.16.101 | Controlador de dominio secundario |
| DC1-25 | Windows Server 2025 | 172.0.16.200 | Nuevo DC principal |
| DC2-25 | Windows Server 2025 | 172.0.16.201 | Nuevo DC secundario |

---

### Proceso de migración

1. **Backup completo** de DC1 y DC2.  
2. Creación de las nuevas VMs (DC1-25 y DC2-25) con **Windows Server 2025**.  
   - Asignación de IP estática y configuración del DNS principal apuntando a `172.0.16.100`.  
   - Cambio de nombre de host a `DC1-25` y unión al dominio.  
   - Instalación del rol **AD Domain Services** y promoción como DC.  
   - Repetir el proceso para **DC2-25**.  
3. Verificación de la **replicación** (OU’s, usuarios, grupos, GPO’s…).  
4. Actualización de DNS en todos los servidores:  
   - DNS principal → `172.0.16.200`  
   - DNS secundario → `172.0.16.201`
   
[Ver captura de los controladores de dominio](../images/dcs.png)

---

### Despromoción de los antiguos controladores

Desde **DC2**:
- Eliminar el rol **AD DS (Demote)**.  
- No marcar *Force removal of this domain controller*.  
- Eliminar posteriormente **AD DS** y **DNS Server**.  

---

### Transferencia de roles FSMO

Comprobar roles actuales:

   **cmd**

netdom query fsmo

## Transferencia de roles FSMO

#### RID, PDC e Infrastructure
1. Abrir **AD Users and Computers** → botón derecho en el dominio → **Operation Masters**  
2. Cambiar los tres roles a **DC1-25**

[Ver captura de la tranferencia de roles](../images/master.png)

#### Domain Naming Master
1. Abrir **AD Domains and Trusts** → botón derecho → **Operations Master**  
2. Cambiar el rol a **DC1-25**

#### Schema Master
1. Registrar snap-in:
   **cmd**
   regsvr32 schmmgmt.dll
2. Abrir MMC → Add Snap-in → Active Directory Schema
3. Conectar a DC1-25, abrir Operations Master y transferir el rol

#### Alternativa PowerShell

	```powershell
Move-ADDirectoryServerOperationMasterRole -Identity "DC1-25" -OperationMasterRole 0,1,2,3,4

   **cmd**
	
netdom query fsmo

[Ver captura de los roles](../images/netdom2025.png)

#### Limpieza y ajuste final

1. Demote de DC1, siguiendo el mismo proceso que con DC2.
2. Problemas menores al hacer el demote por rol de CA (Autoridad Certificadora).
3. Recomendación: los controladores de dominio deben tener solo los roles de AD DS y DNS.
4. Aumento del nivel funcional:

Active Directory Users and Computers → Raise Domain Functional Level
Active Directory Domains and Trusts → Raise Forest Functional Level
