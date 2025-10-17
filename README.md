#  Windows Server 2022 Enterprise Lab Environment

## Objetivo

Este laboratorio reproduce la infraestructura IT completa de una empresa mediana, incluyendo **Active Directory, DNS, DHCP, GPOs, File Server, WSUS, CA, DFS y replicación entre dos controladores de dominio**.

Diseñado y documentado por **Antonio de Francisco**.

---

## Infraestructura

| Rol | Servidor | IP | Sistema | Descripción |
|------|-----------|------|-----------|-------------|
| **DC1** | 172.0.16.100 | Windows Server 2022 | Controlador de dominio principal + DHCP + CA Root |
| **DC2** | 172.0.16.101 | Windows Server 2022 | Controlador de dominio secundario + DHCP Failover + DFS |
| **DFS** | 172.0.16.102 | Windows Server 2022 | File Server + Print Server + WSUS + Backup + DFS |
| **W11** | DHCP | Windows 11 | Cliente unido al dominio |

---

## Componentes del laboratorio

- **Active Directory + DNS + DHCP Failover**
- **Organizational Units + Delegación de permisos + GPOs**
- **File Server** con cuotas, deduplicación, **DFS Namespaces y replicación**
- **Servidor de Impresión**
- **CA (Autoridad Certificadora)** + firma de scripts PowerShell
- **WSUS** y actualizaciones automáticas
- **Backup diario** hacia almacenamiento remoto
- **Migración completa** de controladores de dominio a *Windows Server 2025*

---

## Documentación técnica

Cada módulo se encuentra documentado en carpetas separadas, con pasos técnicos, comandos PowerShell y validaciones:

- [01. Domain Controller Setup & DNS & DHCP Failover](./docs/01_Domain_Controller_Setup.md)
- [02. OU & GPO Management](./docs/02_Ou_gpo.md)
- [03. File Services & DFS](./docs/03_File_Server_DFS.md)
- [04. Print Server](./docs/04_Print_Server.md)
- [05. Security & CA](./docs/05_CA.md)
- [06. WSUS](./docs/06_WSUS.md)
- [07. Backup](./docs/07_Backup.md)
- [08. Migration to Windows Server 2025](./docs/08_Migration.md)

---

## Ejemplo visual

[AD Topology](./images/ad_topology.png)

---

## Próximos pasos

- Integrar **Linux Samba Server** en el dominio  
- Añadir **monitorización** con Nagios o Zabbix  

---

## Aprendizaje clave

Este laboratorio demuestra experiencia práctica en:
- **Despliegue, replicación y mantenimiento** de servicios empresariales en entornos Windows Server  
- **Configuración manual completa**, desde Active Directory hasta WSUS y Backup  
- **Migración real** a Windows Server 2025 con transferencia de roles FSMO y validación de replicación  

---