---
title: 'Cree un archivo basado en la nube para un buzón principal local en una implementación híbrida de Exchange.: Exchange 2013 Help'
TOCTitle: Cree un archivo basado en la nube para un buzón principal local en una implementación híbrida.
ms:assetid: ecc0a687-6c05-47bd-a079-a43d83cba9ea
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Mt791517(v=EXCHG.150)
ms:contentKeyID: 74253083
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Cree un archivo basado en la nube para un buzón principal local en una implementación híbrida de Exchange.

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2017-01-20_

En una implementación híbrida de Exchange, configurar un buzón principal local con un buzón de archivo basado en la nube en Exchange Online.

Paso 1: Habilitar un buzón de almacenamiento en la nube para un buzón principal local

Paso 2: Comprobar que se ha creado el buzón de almacenamiento en la nube

(Opcional) Ejecutar la sincronización de directorios

## Antes de empezar

  - El usuario con el buzón principal local debe tener una cuenta de usuario en su organización de Office 365.

  - La cuenta de usuario de Office 365 debe asignarse un Archivado de Exchange Online para la licencia de Exchange Server. Los pasos para asignar una licencia se incluyen en los procedimientos en el paso 1.

  - Después de habilitar el buzón de archivo basado en la nube en el paso 1, puede que el buzón tarde hasta 30 minutos en aprovisionarse. Esto se debe a que el proceso de sincronización de directorios crea el buzón de archivo basado en la nube, donde la implementación local de Active Directory se sincroniza con Active Directory de Azure (Azure AD) en Office 365. De forma predeterminada, la sincronización de directorios se ejecuta una vez cada 30 minutos.

## Paso 1: Habilitar un buzón de almacenamiento en la nube para un buzón principal local

Use uno de los procedimientos siguientes para habilitar un buzón de archivo basado en la nube para un buzón principal local. Realice estos pasos en el Centro de administración de Exchange en su organización Exchange local y en el Centro de administración de Office 365.

Crear un buzón de almacenamiento en la nube para un nuevo usuario

Crear un buzón de almacenamiento en la nube para un usuario existente

## Crear un buzón de almacenamiento en la nube para un nuevo usuario

1.  En el CEF en la organización local, vaya a **Destinatarios**  \> **Buzones**.

2.  Haga clic en **Nuevo**![Agregar icono](images/JJ906432.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono")\>**Buzón de usuario**.

3.  En la página **Nuevo buzón de correo de usuario**, cree un buzón para un usuario nuevo o existente. Para obtener más información acerca de la creación un buzón de correo de usuario, vea [Crear buzones de usuario](https://technet.microsoft.com/es-es/library/jj991919\(v=exchg.150\)).

4.  Haga clic en **Más opciones** para habilitar un buzón de archivo basado en la nube.

5.  En **Archivo**, haga clic en la casilla **Crear un archivo local para este usuario** y, a continuación, haga clic en **Archivo basado en la nube**. Se muestra el nombre del dominio en el que se aprovisionará el buzón de archivo.
    
    ![En Archivo, haga clic en la casilla y, a continuación, haga clic en Archivo basado en la nube](images/Mt791517.43d0473e-30ad-4021-94bc-a9c5449f43ba(EXCHG.150).png "En Archivo, haga clic en la casilla y, a continuación, haga clic en Archivo basado en la nube")  

6.  Haga clic en **Guardar** para crear el buzón y el archivo basado en la nube.
    
    Nota sobre la página **Buzones de correo**, el valor **Usuario (archivo)** se muestra en la columna **Tipo de buzón** del buzón seleccionado.

7.  Espere hasta 30 minutos para que la sincronización de directorios cree una cuenta de usuario correspondiente en Office 365.
    

    > [!TIP]
    > En el Centro de administración de Office 365, vaya a <STRONG>Salud</STRONG>&gt; <STRONG>Estado de sincronización de directorio</STRONG> para ver cuándo se produjo la última sincronización de directorios.



8.  Después de comprobar que la sincronización de directorios se ha producido después de crear el nuevo buzón local, en el Centro de administración de Office 365, vaya a **Usuarios** \> **Usuarios activos** y, a continuación, seleccione la nueva cuenta de usuario de Office 365 que se ha creado para el nuevo buzón local.

9.  En la página de propiedades de usuario que se muestra, haga clic en **Editar** en la sección **Licencias de producto**.
    
    ![Haga clic en Editar en el panel de detalles para asignar una licencia al usuario seleccionado](images/Mt791517.383a9068-53cb-420a-a05e-823e8b5a2c25(EXCHG.150).png "Haga clic en Editar en el panel de detalles para asignar una licencia al usuario seleccionado")  

10. En el menú desplegable **Ubicación**, seleccione una ubicación para el usuario.

11. Expanda la lista de licencias de Office 365 Enterprise, asigne la licencia de **Archivado de Exchange Online para Exchange Server** y, a continuación, guarde los cambios.
    
    En la columna **Estado** columna en la lista de usuarios, fíjese en que ahora se ha asignado una licencia al usuario.

12. Una vez más, espere hasta 30 minutos para que la sincronización de directorios aprovisione un buzón de almacenamiento en la nube. Vaya al paso 2 para ver cómo comprobar que se ha creado el buzón de archivo basado en la nube. Después de crea el buzón de archivo, el usuario puede acceder a él mediante Outlook o Outlook en la web.

Volver al principio

## Crear un buzón de almacenamiento en la nube para un usuario existente

1.  En el Centro de administración de Office 365, vaya a **Usuarios** \> **Usuarios activos** y, a continuación, seleccione la cuenta de usuario para la que desea crear un buzón de archivo basado en la nube.

2.  En la página de propiedades de usuario que se muestra, haga clic en **Editar** en la sección **Licencias de producto**.
    
    ![Haga clic en Editar en el panel de detalles para asignar una licencia al usuario seleccionado](images/Mt791517.383a9068-53cb-420a-a05e-823e8b5a2c25(EXCHG.150).png "Haga clic en Editar en el panel de detalles para asignar una licencia al usuario seleccionado")  

3.  En el menú desplegable **Ubicación**, seleccione una ubicación para el usuario.

4.  Expanda la lista de licencias de Office 365 Enterprise, asigne la licencia de **Archivado de Exchange Online para Exchange Server** y, a continuación, guarde los cambios.
    
    En la columna **Estado** columna en la lista de usuarios, fíjese en que ahora se ha asignado una licencia al usuario.

5.  En el CEF en la organización local, vaya a **Destinatarios**  \> **Buzones**.

6.  En la lista de buzones, seleccione el usuario que asignó la licencia.

7.  En el panel de detalles, en **Archivo local**, haga clic en **Habilitar**.
    
    ![Haga clic en Activar en el panel de detalles para habilitar el buzón de archivo del usuario seleccionado](images/Mt791517.17ce99f7-d154-4e21-bec1-c938af1d4a0a(EXCHG.150).png "Haga clic en Activar en el panel de detalles para habilitar el buzón de archivo del usuario seleccionado")  

8.  En la página **Crear archivo local**, haga clic en **Archivo basado en la nube** y, a continuación, haga clic en **Aceptar**. Se muestra el nombre del dominio en el que se aprovisionará el buzón de archivo.
    
    ![En la página Crear archivo local, haga clic en Archivo basado en la nube](images/Mt791517.9ad047c9-ef47-47df-93cc-0fab872f1ae1(EXCHG.150).png "En la página Crear archivo local, haga clic en Archivo basado en la nube")  
    
    Nota sobre la página **Buzones de correo**, el valor **Usuario (archivo)** se muestra en la columna **Tipo de buzón** del buzón seleccionado.

9.  Espere hasta 30 minutos para que la sincronización de directorios cree el buzón de almacenamiento en la nube. Vaya al paso 2 para ver cómo comprobar que se ha creado el buzón de archivo basado en la nube. Después de crea el buzón de archivo, el usuario puede acceder a él mediante Outlook o Outlook en la web.
    

    > [!TIP]
    > En el Centro de administración de Office 365, vaya a <STRONG>Mantenimiento</STRONG>&gt; <STRONG>Directory sync status</STRONG> (Estado de sincronización de directorios) para ver cuándo se produjo la última sincronización de directorios.



Volver al principio

## Paso 2: Comprobar que se ha creado el buzón de almacenamiento en la nube

Como se ha explicado anteriormente, puede haber un retraso entre el momento en el que habilita un buzón de archivo basado en la nube y el de su creación real. Esto es porque se tiene que ejecutar la sincronización de directorios para crear el buzón de archivo basado en la nube. Aquí le mostramos algunas formas de comprobar que se ha creado el buzón de archivo basado en la nube.

En su organización Exchange Online, ejecute el siguiente comando de PowerShell para mostrar las propiedades relacionadas con el buzón de un usuario archivado. Para conectarse a Exchange Online uso de PowerShell remoto, vea [conectarse a Exchange Online PowerShell](https://go.microsoft.com/fwlink/?/linkid=396554).

    Get-MailUser <cloud mail user> | FL *archive*

Las capturas de pantalla siguientes muestran las propiedades que se devuelven cuando el aprovisionamiento del buzón de archivo basado en nube está pendiente y tras la creación del buzón de archivo.

**Propiedades de usuario de correo antes de que la sincronización de directorios aprovisione el buzón de archivo basado en la nube**

![Propiedades del usuario de correo basado en la nube antes de aprovisionar el archivo basado en la nube](images/Mt791517.c6a42713-f061-4761-93c1-2b5478953e46(EXCHG.150).png "Propiedades del usuario de correo basado en la nube antes de aprovisionar el archivo basado en la nube")

Antes de que la sincronización de directorios aprovisione el archivo basado en la nube, la propiedad *ArchiveStatus* se establece en `None`. Tenga en cuenta también que las propiedades *ArchiveGuid* y *ArchiveName* están vacías.

**Propiedades de usuario de correo después de que la sincronización de directorios aprovisione el buzón de archivo basado en la nube**

![Propiedades del usuario de correo basado en la nube después de aprovisionar el archivo basado en la nube](images/Mt791517.005fcc87-6253-4218-aafc-50f212de54fa(EXCHG.150).png "Propiedades del usuario de correo basado en la nube después de aprovisionar el archivo basado en la nube")

Después de que la sincronización de directorios aprovisione el archivo basado en la nube, la propiedad *ArchiveStatus* se establece en `Active` y se rellenan las propiedades *ArchiveGuid* y *ArchiveName*. En este punto, el usuario podrá acceder a su buzón de archivo basado en la nube en Outlook o Outlook en la web.

![El usuario puede acceder a su buzón de archivo basado en la nube en Outlook o Outlook en la web](images/Mt791517.8777bc4d-05c3-4489-8d8c-ff5429a0b2c3(EXCHG.150).png "El usuario puede acceder a su buzón de archivo basado en la nube en Outlook o Outlook en la web")

También puede ejecutar el siguiente comando de PowerShell en su organización de Exchange local para mostrar las propiedades relacionadas con el buzón de archivo basado en la nube de un usuario.

    Get-Mailbox <on-premises user mailbox> | FL *archive*

**Propiedades de buzón local antes de que la sincronización de directorios aprovisione el buzón de archivo basado en la nube**

![Propiedades del buzón antes de aprovisionar el archivo basado en la nube](images/Mt791517.d5625bc8-03de-439a-8a0a-051ff537a0bf(EXCHG.150).png "Propiedades del buzón antes de aprovisionar el archivo basado en la nube")

Antes de que la sincronización de directorios aprovisione el archivo basado en la nube, la propiedad *ArchiveStatus* se establece en `None` y la propiedad *ArchiveState* se establece en `HostedPending`.

**Propiedades de buzón local después de que la sincronización de directorios aprovisione el buzón de archivo basado en la nube**

![Propiedades del buzón tras aprovisionar el archivo basado en la nube](images/Mt791517.9b42d562-1b0a-4722-97aa-35d0ef6f9372(EXCHG.150).png "Propiedades del buzón tras aprovisionar el archivo basado en la nube")

Después de que la sincronización de directorios aprovisione el archivo basado en la nube, la propiedad *ArchiveStatus* se establece en `Active` y la propiedad *ArchiveState* se establece en `HostedProvisioned`. En este punto, el usuario podrá acceder a su buzón de archivo basado en la nube en Outlook o Outlook en la web.

Volver al principio

## (Opcional) Ejecutar la sincronización de directorios

Como se ha explicado anteriormente, el proceso de sincronización de directorios crea el buzón de archivo basado en la nube. De forma predeterminada, la implementación local de Active Directory se sincroniza con Azure AD en Office 365 una vez cada 30 minutos. Para ver cuándo se produjo la última sincronización de directorios, vaya a **Mantenimiento** \> **Directory sync status** (Estado de sincronización de directorios) en Centro de administración de Office 365.

En algunos casos, podría interesarle iniciar la sincronización de directorios para aprovisionar el buzón de archivo basado en la nube antes de la siguiente sincronización programada. Para hacerlo, ejecute el siguiente comando de PowerShell en el servidor donde esté instalado Azure AD Connect.

    Start-ADSyncSyncCycle -PolicyType Delta

Para obtener más información, consulte [Sincronización de Azure AD Connect: Programador](https://go.microsoft.com/fwlink/p/?linkid=836813).

Volver al principio

