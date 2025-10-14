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
3. **File Server con cuotas y deduplicación + DFS Namespaces y replicación**
4. **Servidor de Impresión**
5. **CA (Cert Authority) + PowerShell Script Signing**
6. **WSUS y actualizaciones automáticas**
7. **Backup diario hacia almacenamiento remoto**
8. **Migración controladores de dominio a Windows Server 2025**

---

## Documentación completa
Cada módulo está documentado en carpetas separadas con pasos técnicos, comandos PowerShell y comprobaciones de validación:

- [01. Domain Controller Setup & DNS & DHCP Failover](./01_Domain_Controller_Setup.md)
- [02. OU & GPO Management](./gpo_configuration.md)
- [03. File Services & DFS](./file_server_dfs.md)
- [04. Print Server](./print_server.md)
- [05. Security & CA](./certificates_and_powershell_signing.md)
- [07. Backup & WSUS](./backup_and_wsus.md)
- [08. Migration to Windows Server 2025](./migration_steps.md)

---

## Ejemplo visual

![AD Topology]

Ver captura DHCP Failover](https://github.com/tonifrann/Windows_Server_Lab/blob/main/images/DHCP_Failover.png)

---

## Próximos pasos
- Integrar **Linux Samba Server** en el dominio.
- Automatizar backups con PowerShell.
- Añadir **monitorización básica con Nagios o Zabbix**.

---

> **Aprendizaje clave:** Este lab demuestra experiencia práctica en despliegue, replicación y mantenimiento de servicios empresariales en entorno Windows Server. Todo fue configurado y probado manualmente, incluyendo migración a Windows Server 2025.
