##1.- Creación del primer Domain Controller (DC1)##

Configuración de la VM

Hyper-V → nueva máquina virtual:

RAM: 2048 MB

Disco: 127 GB (dinámico)

Conmutador de red: Privado (sin acceso a Internet)

Instalación de Windows Server 2022

Configuración de red:

IPv4: 172.16.0.100
DNS: 172.16.0.100
IPv6: Desactivado
Hostname: DC1


Instalación del rol Active Directory Domain Services

Nuevo bosque: empresa.local

Añadir roles de DNS y Global Catalog

Promocionar el servidor a Domain Controller

Comprobación de replicación

repadmin /replsummary

Resultado sin errores (replicación OK).


##2️.- Creación del segundo Domain Controller (DC2)##

Configuración similar a DC1, con IP 172.16.0.101

DNS primario → 172.16.0.100, secundario → 127.0.0.1

Unido al dominio empresa.local

Promocionado como controlador adicional con DNS y Global Catalog

Verificación:

repadmin /replsummary
netdom query fsmo

Ambos DC replican correctamente.


##3.- Configuración DNS y Zona Inversa##

En DC1 → añadir 8.8.8.8 como Forwarder

Crear zona inversa 172.16.0.x

Añadir manualmente los punteros PTR de DC1 y DC2

Verificar resolución con:

nslookup 172.16.0.100


