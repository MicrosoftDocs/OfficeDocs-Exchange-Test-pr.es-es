---
title: 'Aplicar o quitar una directiva de buzón de Outlook Web App en un buzón: Exchange 2013 Help'
TOCTitle: Aplicar o quitar una directiva de buzón de Outlook Web App en un buzón
ms:assetid: 51d8e269-b0d5-4bc7-9b3d-0460871e54fa
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd876884(v=EXCHG.150)
ms:contentKeyID: 49895626
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Aplicar o quitar una directiva de buzón de Outlook Web App en un buzón

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2012-10-12_

Puede aplicar una directiva de buzón de Outlook Web App a uno o más buzones o eliminar una directiva con el EAC o con el Shell.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  10 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Directivas de buzón de Outlook Web App" en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Aplicar una directiva de buzón de Outlook Web App

## Usar el EAC para aplicar una directiva de buzón de Outlook Web App

1.  En el EAC, haga clic en **Destinatarios** \> **Buzones de correo**.

2.  En el panel de trabajo, seleccione el buzón al que desea aplicarle una directiva de buzón de Outlook Web App. También puede seleccionar varios buzones.

3.  **Si ha seleccionado un buzón:** 
    
    1.  En el panel de detalles, vaya a **Conectividad de correo** y haga clic en **Ver detalles**.
    
    2.  Haga clic en **Examinar** para ver y seleccionar una de las directivas de buzón de correo disponibles.
    
    3.  Haga clic en **Guardar** para asignar la directiva elegida al buzón de correo seleccionado.
    
    **Si ha seleccionado más de un buzón:** 
    
    1.  En el panel de detalles, vaya a **Outlook Web App** y haga clic en **Asignar una directiva**.
    
    2.  Haga clic en **Examinar** para ver y seleccionar una de las directivas de buzón de correo disponibles.
    
    3.  Haga clic en **Guardar** para asignar la directiva elegida a los buzones de correo seleccionados.

## Usar el Shell para aplicar una directiva de buzón de Outlook Web App a un buzón existente

En este ejemplo, se aplica la directiva de buzón de Outlook Web App denominada "Calendario" al buzón del usuario antonio@contoso.com.

    Set-CASMailbox -Identity tony@contoso.com -OwaMailboxPolicy:Calendar

Para obtener más información sobre sintaxis y parámetros, consulte [Set-CASMailbox](https://technet.microsoft.com/es-es/library/bb125264\(v=exchg.150\)).

## Eliminar una directiva de buzón de Outlook Web App

## Uso de EAC para quitar una directiva de buzón de Outlook Web App

1.  En el EAC, haga clic en **Destinatarios** \> **Buzones de correo**.

2.  En el panel de trabajo, seleccione el buzón del que desea eliminar una directiva de buzón de Outlook Web App.

3.  En el panel de detalles, vaya a **Conectividad de correo** y haga clic en **Ver detalles**.
    
    Si se ha asignado alguna directiva de buzón, haga clic en **Borrar** para quitarla del buzón.

4.  Haga clic en **Guardar** para guardar los cambios.

## Usar el Shell para quitar una directiva de buzón de Outlook Web App de un buzón existente.

En este ejemplo, se quita la directiva de buzón de Outlook Web App del buzón del usuario antonio@contoso.com.

    Set-CASMailbox -Identity tony@contoso.com -OwaMailboxPolicy:$null

Para obtener más información sobre sintaxis y parámetros, consulte [Set-CASMailbox](https://technet.microsoft.com/es-es/library/bb125264\(v=exchg.150\)).

