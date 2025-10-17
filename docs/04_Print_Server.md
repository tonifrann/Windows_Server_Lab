# Laboratorio Active Directory: Servidor de Impresión

Configuración de un servidor de impresión y despliegue automático mediante GPO.

---

## 1. Instalación del rol de impresión

1. En **Server Manager**, ir a:  
   `Agregar roles y características → Print and Document Services → Print Server`.  
2. Incluir también el componente **LPD Service** (útil en caso de necesitar conexión desde equipos Linux).

---

## 2. Configuración de la impresora

1. Crear una **impresora ficticia** en el servidor utilizando el puerto `LPT1`.  
2. Compartir la impresora con el grupo **GG_ventas**.

[Ver captura de la configuración](../images/ibm.png)

---

## 3. Creación y vinculación de la GPO

1. Crear una **GPO** llamada `Printers`.  
2. Ir a:  
   `User Configuration → Preferences → Control Panel Settings → Printers`.  
3. Agregar la impresora compartida para que se instale automáticamente.  
4. Vincular la GPO a la **OU Barcelona**.

---

## 4. Verificación desde cliente Windows 11

1. En el equipo con Windows 11, ejecutar:  
   **cmd**
   
   gpupdate /force

2. Iniciar sesión con el usuario Marc
3. Confirmar que la impresora aparece instalada correctamente.