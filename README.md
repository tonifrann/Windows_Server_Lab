Laboratorio Windows Server 2022 – Prácticas y Configuración

Este repositorio documenta prácticas completas de laboratorio en Windows Server 2022, incluyendo Active Directory, DHCP, GPOs, backup, SAN, failover clustering, VPN, certificados, monitorización y Azure (Entra ID). También incluye un escenario de migración a Windows Server 2025.

El objetivo es tener soltura en la práctica, simulando un entorno empresarial, y que sirva como ejemplo para curriculum/GitHub.

📌 Contenido del laboratorio

Active Directory

Dos Controladores de Dominio replicados.

Estructura de OU y usuarios/grupos de prueba.

GPOs: autoenrollment, seguridad, scripts, redirección de carpetas.

Cliente Windows 11 para validar GPOs y DHCP.

DHCP y DNS

Servidor DHCP configurado, con reservas y exclusiones.

Cliente prueba recibe IP correctamente.

DNS integrado con AD.

Servidor de archivos

Carpetas compartidas con permisos NTFS.

Deduplicación activada en carpetas grandes.

Backup y restauración con Windows Server Backup.

Cliente Windows 11 prueba acceso y permisos.

Backup y Disaster Recovery

Windows Server Backup configurado para:

Volúmenes completos.

Estado del sistema.

Hyper-V.

Restauración de archivos individuales y máquinas virtuales.

Práctica de Azure Backup para copia externa.

WSUS

Servidor WSUS para centralizar actualizaciones.

Grupos de equipos: TEST y PRODUCCIÓN.

GPO para apuntar clientes al servidor WSUS.

Sincronización, aprobación y despliegue de actualizaciones.

VPN / Remote Access

Servidor VPN configurado (SSTP/IKEv2 recomendado).

Autenticación MS-CHAPv2 y EAP.

Firewall configurado para tráfico VPN.

Cliente Windows 11 se conecta y valida acceso a recursos.

SAN e iSCSI / Failover Clustering

iSCSI Target Server y discos virtuales configurados.

Nodos conectados como iSCSI Initiators.

Failover Cluster con:

File Server role.

Configuración de Quorum (Node Majority / Node+Disk / Dynamic Witness).

Failover y failback configurados.

Alta disponibilidad y redundancia probadas.

Active Directory Certificate Services (AD CS)

PKI interna: Root y Subordinate CA.

Emisión de certificados de usuario y servidor.

Autoenrollment vía GPO.

Firma de scripts PowerShell y revocación de certificados.

Performance Monitoring

Task Manager, Resource Monitor para supervisión rápida.

Performance Monitor con Data Collector Sets.

Reliability Monitor para índice de estabilidad.

Event Viewer con logs de sistema, aplicación y seguridad.

Buenas prácticas: línea base, automatización y centralización de logs.

Azure / Microsoft Entra ID

Tenant configurado y usuarios/grupos creados.

Sincronización con AD local via Entra Connect.

Storage Account y File Share con script de conexión.

Máquina virtual en Azure y prueba de RDP/SSH.

Resource Groups para gestión de permisos y costes.

Migración Windows Server 2022 → 2025

Preparación: backup y compatibilidad de roles.

Instalación de Windows Server 2025 en nuevas VMs.

Promoción de DC adicional y replicación de AD/DNS/DHCP.

Transferencia de roles FSMO.

Migración de servidor de archivos y deduplicación.

Importación/exportación de DHCP.

Validación de clientes y GPOs.

Buenas prácticas: snapshots, documentación y monitorización post-migración.

🛠️ Scripts y comandos de ejemplo
Export/Import DHCP
# Exportar DHCP 2022
Export-DhcpServer -ComputerName DC1-2022 -File C:\backup\dhcpconfig.xml -Leases

# Importar DHCP 2025
Import-DhcpServer -ComputerName DC1-2025 -File C:\backup\dhcpconfig.xml -Leases -BackupPath C:\dhcpbackup

Firmar scripts PowerShell con certificado
Set-AuthenticodeSignature .\script.ps1 -Certificate (Get-Item Cert:\CurrentUser\My\<Thumbprint>)

Robocopy para migración de archivos
robocopy \\DC1-2022\Share \\DC1-2025\Share /MIR /COPYALL /SEC /R:3 /W:5
