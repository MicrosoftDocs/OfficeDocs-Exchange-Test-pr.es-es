---
title: 'Ver información de dispositivo móvil para los usuarios: Exchange 2013 Help'
TOCTitle: Ver información de dispositivo móvil para los usuarios
ms:assetid: 4fd263c0-ad61-416c-bd68-339bf66605cf
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997974(v=EXCHG.150)
ms:contentKeyID: 49895622
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Ver información de dispositivo móvil para los usuarios

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-11-29_

Los usuarios pueden configurar varios dispositivos móviles para la sincronización con MicrosoftExchange Server 2013. Puede usar la EMC o el Shell para ver una lista de dispositivos móviles asociados a un usuario específico.

Para consultar otras tareas de administración relacionadas con los dispositivos móviles, vea [Exchange ActiveSync](exchange-activesync-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el entrada "Directiva de buzón de correo de dispositivo móvil" en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Uso del EAC para ver información de dispositivos móviles para los usuarios

El EAC muestra una lista de los dispositivos móviles que se sincronizan con el buzón de un usuario en un momento dado. Puede ver los dispositivos móviles por familia, modelo, número de teléfono o estado.

1.  En el EAC, haga clic en **Destinatarios** \> **Buzones de correo** y elija un buzón.

2.  En el panel de detalles, vaya a **Características de voz y teléfono** y haga clic en **Ver detalles** para mostrar la pantalla **Detalles de dispositivo móvil**.

## Uso del Shell para ver información de dispositivos móviles para los usuarios

El cmdlet Get-MobileDevice permite ver una lista de los dispositivos móviles de un usuario específico.

1.  Ejecute el siguiente comando.
    
    ```powershell
    Get-MobileDevice -Mailbox useralias
    ```

