---
title: 'Habilitar o deshabilitar el correo para una carpeta pública Exchange 2013 Help | Microsoft Docs'
TOCTitle: Habilitar o deshabilitar el correo para una carpeta pública
ms:assetid: 3d69f76d-ff3c-46c1-b962-6a1baa425d8a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997560(v=EXCHG.150)
ms:contentKeyID: 49895588
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Habilitar o deshabilitar el correo para una carpeta pública

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2016-06-15_

Las carpetas públicas están diseñadas para un acceso compartido y ofrecen una manera fácil y efectiva de obtener, organizar y compartir información con otras personas de su grupo de trabajo u organización. La habilitación del correo de una carpeta pública permite a los usuarios publicar en una carpeta pública, enviándole un mensaje de correo electrónico. Cuando una carpeta pública tiene el correo habilitado, su configuración adicional pasa a estar disponible en el Centro de administración de Exchange (EAC), como direcciones de correo electrónico y cuotas de correo. En el Shell, antes de que se habilite el correo en una carpeta pública, puede usar el cmdlet **Set-PublicFolder** para administrar toda su configuración. Después de que se habilite el correo de la carpeta pública, use los cmdlets **Set-PublicFolder** y **Set-MailPublicFolder** para administrar la configuración.

Si desea que los usuarios de Internet envíen correo a una carpeta pública habilitada para correo, debe establecer permisos adicionales mediante el cmdlet **Add-PublicFolderClientPermission**.

Para otras tareas de administración relacionadas con la administración de carpetas públicas, consulte [Procedimientos de carpetas públicas](public-folder-procedures-exchange-2013-help.md).

Para otras tareas de administración relacionadas con las carpetas públicas, consulte [Procedimientos de carpetas públicas en Office 365 y Exchange Online](https://technet.microsoft.com/es-es/library/jj966272\(v=exchg.150\)).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 5 minutos

  - Para garantizar que los usuarios de Internet puedan enviar mensajes de correo electrónico a una carpeta pública habilitada para correo, la carpeta pública debe tener concedido como mínimo el derecho de acceso *CreateItems* para la cuenta anónima. Si desea obtener más información, consulte Permitir a los usuarios anónimos enviar correo electrónico a una carpeta pública habilitada para correo.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Carpetas públicas" en el tema [Permisos de uso compartido y colaboración](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Use el EAC para habilitar o deshabilitar la carpeta pública para correo

1.  Vaya a **Carpetas públicas** \> **Carpetas públicas**.

2.  En la vista de lista, seleccione la carpeta pública que desee habilitar o deshabilitar para el correo.

3.  En el panel de detalles, en **Configuración de correo**, haga clic en **Habilitar** o **Deshabilitar**.

4.  Se mostrará un cuadro de advertencia preguntando si está seguro de que quiere habilitar o deshabilitar el correo de la carpeta pública. Haga clic en **Sí** para continuar.

Si desea que los usuarios externos envíen correo a esta carpeta pública, asegúrese de seguir los pasos de Permitir a los usuarios anónimos enviar correo electrónico a una carpeta pública habilitada para correo.

## Uso del Shell para habilitar una carpeta pública para correo

En este ejemplo se habilita para correo la carpeta pública "Servicio de asistencia".

    Enable-MailPublicFolder -Identity "\Help Desk"

Este ejemplo habilita el correo de la carpeta pública "Informes" en la carpeta pública "Marketing", pero oculta la carpeta de las listas de direcciones.

    Enable-MailPublicFolder -Identity "\Marketing\Reports" -HiddenFromAddressListsEnabled $True

Si desea que los usuarios externos envíen correo a esta carpeta pública, asegúrese de seguir los pasos de Permitir a los usuarios anónimos enviar correo electrónico a una carpeta pública habilitada para correo.

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Enable-MailPublicFolder](https://technet.microsoft.com/es-es/library/aa998824\(v=exchg.150\)).

## Uso del Shell para deshabilitar una carpeta pública para correo

En este ejemplo, se deshabilita la carpeta pública Marketing\\Reports para correo.

    Disable-MailPublicFolder -Identity "\Marketing\Reports"

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Disable-MailPublicFolder](https://technet.microsoft.com/es-es/library/bb123781\(v=exchg.150\)).

## Permitir a los usuarios anónimos enviar correo electrónico a una carpeta pública habilitada para correo

Puede usar Outlook o el Shell para establecer los permisos en una cuenta anónima de una carpeta pública. No puede usar el EAC para establecer permisos en la cuenta anónima.

**Use Outlook para establecer permisos en la cuenta anónima**

1.  Abra Outlook con una cuenta a la que se le concedieron los permisos de propietario en la carpeta pública habilitada para correo electrónico a la cual desea que los usuarios anónimos envíen correo.

2.  Vaya a **Carpetas públicas - \<nombre del usuario\>**.

3.  Vaya a la carpeta pública que desea cambiar.

4.  Haga clic con el botón secundario en la carpeta pública, haga clic en **Propiedades** y, a continuación, seleccione la ficha **Permisos**.

5.  Seleccione la cuenta **Anónimo**, seleccione **Crear elementos** en **Escribir** y, a continuación, haga clic en **Aceptar**.

**Use el Shell para establecer permisos en la cuenta anónima**

Este ejemplo establece el permiso `CreateItems` para la cuenta anónima en la carpeta pública habilitada para correo "Comentarios del usuario".

    Add-PublicFolderClientPermission "\Customer Feedback" -AccessRights CreateItems -User Anonymous

Para obtener información más detallada sobre la sintaxis y los parámetros, consulte [Add-PublicFolderClientPermission](https://technet.microsoft.com/es-es/library/bb124743\(v=exchg.150\)).

