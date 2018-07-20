---
title: 'Re-create the Discovery system mailbox: Exchange 2013 Help'
TOCTitle: Re-create the Discovery system mailbox
ms:assetid: 5ae8426b-5661-4ecb-99c4-cdd342107fb1
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg588318(v=EXCHG.150)
ms:contentKeyID: 49895649
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Re-create the Discovery system mailbox

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2018-01-17_

En la exhibición de documentos electrónicos en contexto se usa un buzón de sistema para almacenar los metadatos de búsqueda. Este buzón de sistema de detección tiene el nombre para mostrar **SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}**. Como los buzones de sistema no son visibles en las listas de direcciones del Centro de administración de Exchange (EAC) ni de Exchange, en raras ocasiones se eliminan de manera inadvertida.

Sin embargo, si el buzón de sistema de detección se elimina por error, los administradores de detección no podrán realizar búsquedas de exhibición de documentos electrónicos en contexto ni administrar las búsquedas existentes. Es este caso, para habilitar la función de exhibición de documentos electrónicos, deberá volver a crear el buzón de sistema de detección.

## Qué necesita saber antes de comenzar

  - Tiempo estimado para finalizar:  10 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Sección "Permisos de aprovisionamiento de destinatarios" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Use el Shell para recrear el buzón del sistema de detección

1.  Elimine la cuenta de usuario SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9} de Active Directory, si existiera. De manera predeterminada, la instalación de Exchange Server 2013 crea el buzón en el contenedor de usuarios en Active Directory. Para obtener información detallada acerca de cómo eliminar una cuenta de usuario de Active Directory, consulte [Eliminación de cuentas de usuario](https://go.microsoft.com/fwlink/p/?linkid=215850).

2.  Use el Shell para habilitar el buzón de sistema de detección.
    

    > [!NOTE]
    > La EAC no permite habilitar el buzón de sistema de detección.<BR>El siguiente comando se debe ejecutar desde el mismo directorio donde extrajo el medio de instalación de Exchange.

    
    Para volver a crear el buzón del sistema de detección, ejecute el siguiente comando:
    
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que el buzón de sistema de detección se volvió a crear correctamente, use el cmdlet **Get-Mailbox** con el modificador*Arbitration* para recuperar los buzones de sistema. Consulte los resultados del comando para comprobar que el buzón de sistema `SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}` se volvió a crear.


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


