# Windows Server 2022 Enterprise Lab Environment

## Objetivo
Este laboratorio reproduce la infraestructura IT básica de una empresa mediana con Active Directory, DNS, DHCP, GPOs, File Server, WSUS, CA, DFS y replicación entre dos controladores de dominio.

Diseñado y documentado por **Antonio de Francisco**.

---

## Infraestructura

| Rol | Servidor | IP | Sistema | Descripción |
|------|-----------|---------|--------------|-------------|
| DC1 | `172.16.0.100` | Windows Server 2022 | Controlador de dominio principal + DHCP + CA Root |
| DC2 | `172.16.0.101` | Windows Server 2022 | Controlador de dominio secundario + DHCP Failvover + DFS|
| DFS | `172.16.0.102` | Windows Server 2022 | File Server + Print Server + WSUS + Backup + DFS|
| W11 | DHCP | Windows 11 | Cliente unido al dominio |

---

## Componentes del laboratorio
1. **Active Directory + DNS + DHCP Failover**
2. **Organizational Units + Delegación de permisos + GPOs**
3. **File Server con cuotas y deduplicación**
4. **DFS Namespaces y replicación**
5. **Servidor de Impresión**
6. **CA (Cert Authority) + PowerShell Script Signing**
7. **WSUS y actualizaciones automáticas**
8. **Backup diario hacia almacenamiento remoto**
9. **Migración controladores de dominio a Windows Server 2025**

---

## Documentación completa
Cada módulo está documentado en carpetas separadas con pasos técnicos, comandos PowerShell y comprobaciones de validación:

- [01. Domain Controller Setup](./01_Domain_Controller_Setup.md)
- [02. Network & DHCP](./02_Network_and_DHCP/dhcp_dns_config.md)
- [03. OU & GPO Management](./03_OUs_and_GPOs/gpo_configuration.md)
- [04. File Services & DFS](./04_File_Services/file_server_dfs.md)
- [05. Print Server](./05_Print_Server/print_server.md)
- [06. Security & CA](./06_Security_and_CA/certificates_and_powershell_signing.md)
- [07. Backup & WSUS](./07_Backup_and_WSUS/backup_and_wsus.md)
- [08. Migration to Windows Server 2025](./08_Migration_to_Server2025/migration_steps.md)

---

## Ejemplo visual

![AD Topology](./screenshots/ad_topology.png)

---

## Próximos pasos
- Integrar **Linux Samba Server** en el dominio.
- Automatizar backups con PowerShell.
- Añadir **monitorización básica con Nagios o Zabbix**.

---

> **Aprendizaje clave:** Este lab demuestra experiencia práctica en despliegue, replicación y mantenimiento de servicios empresariales en entorno Windows Server. Todo fue configurado y probado manualmente, incluyendo migración a Windows Server 2025.
