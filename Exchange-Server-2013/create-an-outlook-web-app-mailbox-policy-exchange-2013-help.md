---
title: 'Crear una directiva de buzones de Outlook Web App: Exchange 2013 Help'
TOCTitle: Crear una directiva de buzones de Outlook Web App
ms:assetid: 347207fa-cfb7-40a6-b19a-831dcdb54ad5
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd335191(v=EXCHG.150)
ms:contentKeyID: 49895563
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Crear una directiva de buzones de Outlook Web App

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2013-05-30_

Puede crear una directiva de buzón de correo de Outlook Web App para aplicarla un conjunto común de directivas de configuración. Las directivas de buzón de correo de Outlook Web App son útiles para aplicar y estandarizar la configuración, por ejemplo, la configuración de datos adjuntos de grupos concretos de usuarios.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  5 minutos.

  - Deberá tener asignados permisos antes de poder ejecutar este cmdlet. Aunque todos los parámetros correspondientes a este cmdlet se describen en este tema, tal vez no tenga acceso a algunos parámetros si no están incluidos en los permisos que se le han asignado. Para ver qué permisos necesita, consulte el Entrada "Directivas de buzones de Outlook Web App" en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para crear una directiva de buzones para Outlook Web App

1.  En el EAC, haga clic en **Permisos** \> **Directivas de Outlook Web App**.

2.  Haga clic en el botón **Nuevo**.

3.  
    
    Escriba un nombre para la directiva.

4.  
    
    Utilice las casillas para habilitar o deshabilitar funciones. Las funciones más comunes se muestran de forma predeterminada. Para ver todas las características que se pueden habilitar o deshabilitar, haga clic en **Más opciones**.
    

    > [!NOTE]
    > La configuración de las características de las directivas de buzones de Outlook Web App invalida la configuración del directorio virtual de Outlook Web App. Puede cambiar la configuración de la segmentación de usuarios concretos usando el cmdlet <STRONG>Set-CASMailbox</STRONG> en el Shell.



5.  Haga clic en **Guardar** para guardar la directiva.

## Usar el Shell para crear una directiva de buzones para Outlook Web App

Este ejemplo crea una directiva de buzones de Outlook Web App denominada `Policy1`.

  - En el Shell, ejecute el siguiente comando.
    
        New-OwaMailboxPolicy -Name Policy1

Para obtener más información sobre sintaxis y parámetros, consulte [New-OwaMailboxPolicy](https://technet.microsoft.com/es-es/library/dd351067\(v=exchg.150\)). Si quiere información sobre el uso del Shell para configurar una directiva de buzones de Outlook Web App, consulte [Set-OwaMailboxPolicy](https://technet.microsoft.com/es-es/library/dd297989\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si ha creado una directiva de buzones de correo de Outlook Web App:

  - En el EAC, haga clic en **Permisos** \> **Directivas de Outlook Web App** y busque la nueva directiva de buzones de correo.

