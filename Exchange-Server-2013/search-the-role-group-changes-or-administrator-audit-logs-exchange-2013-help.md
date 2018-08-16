---
title: 'Buscar informes cambio grupo rol o auditorías administrador Exchange 2013 Help'
TOCTitle: Buscar los informes de cambios del grupo de roles o auditorías de administrador
ms:assetid: c7188d53-e672-492b-b57d-cd711379ddb3
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ff459262(v=EXCHG.150)
ms:contentKeyID: 50553922
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Buscar los informes de cambios del grupo de roles o auditorías de administrador

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2013-12-02_

Se puede buscar en los registros de auditoría de administrador para detectar quién ha efectuado cambios en la configuración de la organización, el servidor y los destinatarios. Esto es útil cuando se hace un seguimiento de la causa de un comportamiento inesperado, se quiere identificar a un administrador malintencionado o bien comprobar si se satisfacen los requisitos de obligado cumplimiento. Para obtener más información acerca del registro de auditoría del administrador, consulte [Registro de auditoría de administrador](administrator-audit-logging-exchange-2013-help.md).

Si desea buscar el registro de auditoría de buzón, consulte [Registro de auditoría de buzones de correo](mailbox-audit-logging-exchange-2013-help.md).


> [!TIP]
> En Exchange Online, puede usar EAC para ver entradas en el registro de auditoría del administrador. Para más información, vea <A href="view-the-administrator-audit-log-exchange-2013-help.md">Ver el registro de auditoría del administrador</A>.



## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: menos de 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Registro de auditoría de administrador de sólo vista" en el tema [Permisos de infraestructura de la Shell y de Exchange](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - El registro de auditoría de administrador está habilitado de forma predeterminada. Para comprobar que se ha habilitado, ejecute el siguiente comando:
    
        Get-AdminAuditLogConfig | FL AdminAuditLogEnabled
    
    El valor `True` indica que el registro de auditoría de administrador está habilitado. Un valor `False` indica que está deshabilitado. Si necesita habilitar el registro de auditoría de administrador para una organización de Exchange local, ejecute el siguiente comando:
    
        Set-AdminAuditLogConfig -AdminAuditLogEnabled $true
    

    > [!NOTE]
    > El cmdlet <STRONG>Set-AdminAuditLogConfig</STRONG> no está disponible en Exchange Online.

    
    Para más información, vea [Administrar el registro de auditoría de administrador](manage-administrator-audit-logging-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Uso de la EAC para ejecutar el informe de cambios de grupo de roles de administración

Si quiere conocer los cambios en la pertenencia al grupo de roles de administración que se han llevado a cabo en los grupos de roles de la organización, utilice el informe de grupo de roles de administrador en el Centro de administración de Exchange (EAC). Gracias al informe de grupo de roles de administrador, puede ver una lista de los grupos de roles que han cambiado durante un intervalo de fechas concreto. También puede seleccionar los grupos de roles específicos de los que desea ver los cambios.

1.  En la EAC, seleccione **Administración de cumplimiento** \> **Auditoría** y, a continuación, haga clic en **Ejecutar un informe de grupo de roles de administrador**.

2.  Seleccione un intervalo de fechas mediante los campos **Fecha de inicio** y **Fecha de finalización**.

3.  Haga clic en **Seleccionar grupos de funciones** y, a continuación, seleccione los grupos de roles para los que desea mostrar los cambios o deje este campo en blanco para ver los cambios en todos los grupos de roles.

4.  Haga clic en **Buscar**.

Si se encuentran cambios con los criterios que ha especificado, se mostrará una lista de cambios en el panel de resultados. Al hacer clic en un grupo de roles, se muestran los cambios en el grupo de roles en el panel de detalles.

## Uso de la EAC para exportar el registro de auditoría de administrador

Si desea crear un archivo XML que contenga los cambios realizados en la organización, utilice el informe de exportar el registro de auditoría del administrador en la EAC. Con el informe de exportar el registro de auditoría del administrador puede especificar un intervalo de fechas para buscar las entradas del registro de auditoría que contienen los cambios realizados por los usuarios que especifique. Después, el archivo XML se envía a un destinatario como datos adjuntos de correo electrónico. El tamaño máximo del archivo XML es 10 megabytes (MB).


> [!NOTE]
> Outlook Web App no permite abrir datos adjuntos en formato XML de forma predeterminada. Puede configurar Exchange para poder ver datos XML adjuntos mediante Outlook Web App o puede recurrir a otro cliente de correo electrónico, como Microsoft Outlook, para ver los datos adjuntos. Para saber cómo configurar Outlook Web App para poder ver un archivo adjunto en formato XML, consulte <A href="view-or-configure-outlook-web-app-virtual-directories-exchange-2013-help.md">Ver o configurar los directorios virtuales de aplicación web de Outlook</A>.



1.  En la EAC, seleccione **Administración de cumplimiento** \> **Auditoría** y, a continuación, haga clic en **Exportar el informe de auditoría del administrador**.

2.  Seleccione un intervalo de fechas mediante los campos **Fecha de inicio** y **Fecha de finalización**.

3.  En el campo **Enviar el informe de auditoría a**, haga clic en **Seleccionar usuarios** y, a continuación, seleccione el destinatario al que desea enviar el informe.

4.  Haga clic en **Exportar**.

Si se encuentran entradas con los criterios especificados, se creará un archivo XML que se enviará como datos adjuntos de correo electrónico al destinatario que especifique.

## Uso del Shell para buscar entradas del registro de auditoría

Puede utilizar el Shell para buscar entradas del registro de auditoría que coincidan con los criterios que especifique. Para obtener una lista de los criterios de búsqueda, consulte [Registro de auditoría de administrador](administrator-audit-logging-exchange-2013-help.md). En este procedimiento se utiliza el cmdlet **Search-AdminAuditLog** y se muestran los resultados de la búsqueda en el Shell. Utilice este cmdlet cuando tenga que devolver un conjunto de resultados que supera los límites definidos en el cmdlet **New-AdminAuditLogSearch** o en los Informes de auditoría de la EAC.

Si desea enviar los resultados de la búsqueda de un registro de auditoría como datos adjuntos de correo electrónico a un destinatario, consulte Uso del Shell para buscar las entradas de registro de auditoría y enviar los resultados a un destinatario más adelante en este tema.

Para buscar en el registro de auditoría los criterios que especifique, utilice la siguiente sintaxis.

    Search-AdminAuditLog - Cmdlets <cmdlet 1, cmdlet 2, ...> -Parameters <parameter 1, parameter 2, ...> -StartDate <start date> -EndDate <end date> -UserIds <user IDs> -ObjectIds <object IDs> -IsSuccess <$True | $False >


> [!NOTE]
> De manera predeterminada, el cmdlet <STRONG>Search-AdminAuditLog</STRONG> devuelve un máximo de 1.000 entradas de registro. Utilice el parámetro <EM>ResultSize</EM> para especificar hasta 250.000 entradas de registro. O utilice el valor <CODE>Unlimited</CODE> para devolver todas las entradas.



En este ejemplo se buscan todas las entradas del registro de auditoría con los siguientes criterios:

  - **Fecha de inicio**   04/08/2012

  - **Fecha de finalización**   10/03/2012

  - **Identificadores de usuario** davids, chrisd, kima

  - **Cmdlets** **Set-Mailbox**

  - **Parámetros** *ProhibitSendQuota*, *ProhibitSendReceiveQuota*, *IssueWarningQuota*, *MaxSendSize*, *MaxReceiveSize*

<!-- end list -->

    Search-AdminAuditLog -Cmdlets Set-Mailbox -Parameters ProhibitSendQuota, ProhibitSendReceiveQuota, IssueWarningQuota, MaxSendSize, MaxReceiveSize -StartDate 08/04/2012 -EndDate 10/03/2012 -UserIds davids, chrisd, kima

En este ejemplo se buscan los cambios realizados en un buzón específico. Esto resulta útil si está resolviendo problemas o necesita proporcionar información para una investigación. Se utilizan los siguientes criterios:

  - **Fecha de inicio**   01/05/2012

  - **Fecha de finalización**   10/03/2012

  - **ID. de objeto** contoso.com/Users/DavidS

<!-- end list -->

    Search-AdminAuditLog -StartDate 05/01/2012 -EndDate 10/03/2012 -ObjectID contoso.com/Users/DavidS

Si las búsquedas devuelven muchas entradas de registro, es recomendable utilizar el procedimiento descrito en Uso del Shell para buscar las entradas de registro de auditoría y enviar los resultados a un destinatario más adelante en este tema. El procedimiento de esta sección envía un archivo XML como dato adjunto de correo electrónico a los destinatarios que especifique, de modo que será más fácil extraer los datos que interesan.

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Search-AdminAuditLog](https://technet.microsoft.com/es-es/library/ff459250\(v=exchg.150\)).

## Ver los detalles de las entradas del registro de auditoría

El cmdlet **Search-AdminAuditLog** devuelve los campos descritos en la sección "Contenido del registro de auditoría" de [Registro de auditoría de administrador](administrator-audit-logging-exchange-2013-help.md). Entre los campos que devuelve el cmdlet, **CmdletParameters** y **ModifiedProperties** contienen información adicional que no se puede ver de manera predeterminada.

Para ver el contenido de los campos **CmdletParameters** y **ModifiedProperties** siga los pasos que se describen a continuación. O utilice el procedimiento expuesto en Uso del Shell para buscar las entradas de registro de auditoría y enviar los resultados a un destinatario más adelante en este tema para crear un archivo XML.

En este procedimiento se aplican los siguientes conceptos:

  - [Matrices](https://technet.microsoft.com/es-es/library/aa998267\(v=exchg.150\))

  - [Variables definidas por el usuario](https://technet.microsoft.com/es-es/library/bb123690\(v=exchg.150\))

<!-- end list -->

1.  Decida los criterios que desea buscar, ejecute el cmdlet **Search-AdminAuditLog** y guarde los resultados en una variable utilizando el siguiente comando.
    
        $Results = Search-AdminAuditLog <search criteria>

2.  Cada entrada del registro de auditoría se almacena como un elemento de matriz en la variable `$Results`. Puede seleccionar un elemento de matriz especificando su índice de elemento de matriz. Los índices de elemento de matriz comienzan en cero (0) para el primer elemento de matriz. Por ejemplo, para recuperar el quinto elemento de matriz, que tiene un índice de 4, utilice el siguiente comando.
    
        $Results[4]

3.  El comando anterior devuelve la entrada de registro almacenada en el elemento de matriz 4. Para ver el contenido de los campos **CmdletParameters** y **ModifiedProperties** para esta entrada de registro, utilice los siguientes comandos.
    
        $Results[4].CmdletParameters
        $Results[4].ModifiedProperties

4.  Para ver el contenido de los campos **CmdletParameters** o **ModifiedParameters** en otra entrada de registro, cambie el índice del elemento de matriz.

## Uso del Shell para buscar las entradas de registro de auditoría y enviar los resultados a un destinatario

Puede utilizar el Shell para buscar las entradas de registro de auditoría que coincidan con los criterios que especifica y enviar los resultados como archivo XML de datos adjuntos al destinatario que especifique. Los resultados se envían al destinatario en 15 minutos. Para obtener una lista de los criterios de búsqueda, consulte [Registro de auditoría de administrador](administrator-audit-logging-exchange-2013-help.md).


> [!NOTE]
> Outlook Web App no permite abrir datos adjuntos en formato XML de forma predeterminada. Puede configurar Exchange para poder ver datos XML adjuntos mediante Outlook Web App o puede recurrir a otro cliente de correo electrónico, como Microsoft Outlook, para ver los datos adjuntos. Para saber cómo configurar Outlook Web App para poder ver un archivo adjunto en formato XML, consulte <A href="view-or-configure-outlook-web-app-virtual-directories-exchange-2013-help.md">Ver o configurar los directorios virtuales de aplicación web de Outlook</A>.



Para buscar en el registro de auditoría los criterios que especifique, utilice la siguiente sintaxis.

    New-AdminAuditLogSearch -Cmdlets <cmdlet 1, cmdlet 2, ...> -Parameters <parameter 1, parameter 2, ...> -StartDate <start date> -EndDate <end date> -UserIds <user IDs> -ObjectIds <object IDs> -IsSuccess <$True | $False > -StatusMailRecipients <recipient 1, recipient 2, ...> -Name <string to include in subject>

En este ejemplo se buscan todas las entradas del registro de auditoría con los siguientes criterios:

  - **Fecha de inicio**   04/08/2012

  - **Fecha de finalización**   10/03/2012

  - **Identificadores de usuario** davids, chrisd, kima

  - **CmdletsSet-Mailbox**

  - **Parámetros***ProhibitSendQuota*, *ProhibitSendReceiveQuota*, *IssueWarningQuota*, *MaxSendSize*, *MaxReceiveSize*

El comando envía los resultados a la dirección SMTP al buzón davids@contoso.com con "Cambios en el límite del buzón" en la línea de asunto del mensaje.

    New-AdminAuditLogSearch -Cmdlets Set-Mailbox -Parameters ProhibitSendQuota, ProhibitSendReceiveQuota, IssueWarningQuota, MaxSendSize, MaxReceiveSize -StartDate 08/04/2012 -EndDate 10/03/2012 -UserIds davids, chrisd, kima -StatusMailRecipients davids@contoso.com -Name "Mailbox limit changes"


> [!NOTE]
> El informe que el cmdlet <STRONG>New-AdminAuditLogSearch</STRONG> genera puede tener un tamaño máximo de 10 MB. Si la búsqueda devuelve un informe de más de 10&nbsp;MB, cambie los criterios que ha especificado. Por ejemplo, reduzca el intervalo de fechas y ejecute varios informes, cada uno con una parte del intervalo de fechas original.



Para obtener más información acerca del formato del archivo XML, consulte [Estructura del registro de auditoría de administrador](administrator-audit-log-structure-exchange-2013-help.md).

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [New-AdminAuditLogSearch](https://technet.microsoft.com/es-es/library/ff459243\(v=exchg.150\)).

