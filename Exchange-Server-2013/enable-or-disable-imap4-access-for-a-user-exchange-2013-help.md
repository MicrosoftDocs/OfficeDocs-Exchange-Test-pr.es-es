---
title: 'Habilitar o deshabilitar el acceso a IMAP4 para un usuario: Exchange 2013 Help'
TOCTitle: Habilitar o deshabilitar el acceso a IMAP4 para un usuario
ms:assetid: a685fae4-b6f1-42fe-8bdc-5f99f9617799
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb676481(v=EXCHG.150)
ms:contentKeyID: 49895814
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Habilitar o deshabilitar el acceso a IMAP4 para un usuario

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2013-01-18_

Puede habilitar o deshabilitar IMAP4 para un usuario.


> [!NOTE]
> Tras haber habilitado o deshabilitado el acceso a IMAP4 para un usuario, debe reiniciar el servicio Microsoft Exchange IMAP4 y el servicio Microsoft Exchange IMAP4 Backend. Para obtener más información acerca de cómo reiniciar el servicio IMAP4, consulte <A href="start-and-stop-the-imap4-services-exchange-2013-help.md">Iniciar y detener los servicios IMAP4</A>.



Para obtener más información acerca de la administración de buzones de usuario, vea [Administrar los buzones de usuario](manage-user-mailboxes-exchange-2013-help.md).

Para obtener más información acerca de POP3 e IMAP4, vea [POP3 e IMAP4 en Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 2 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Sección "Permisos de aprovisionamiento de destinatarios" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso del EAC para habilitar o deshabilitar IMAP4 para un usuario

1.  En el EAC, vaya a **Destinatarios** \> **Buzones**.

2.  En el panel de resultados, seleccione el usuario para el que desee habilitar o deshabilitar IMAP4 y, luego, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En el cuadro de diálogo **Buzón de usuario** en el árbol de la consola, haga clic en **Características de buzón**.
    
    En el panel de resultados, en **Conectividad de correo electrónico**, realice una de las siguientes acciones:
    
      - Para deshabilitar IMAP4 para el usuario, en **IMAP4: Habilitado**, haga clic en **Deshabilitar**.
    
      - Para habilitar IMAP4 para el usuario, en **IMAP4: Deshabilitado**, haga clic en **Habilitar**.

4.  Haga clic en **Guardar**.

## Uso del Shell para habilitar o deshabilitar IMAP4 para un usuario

En este ejemplo, se habilita IMAP4 para el usuario John Smith.

    Set-CASMailbox -Identity "John Smith" -IMAPEnabled $true

En este ejemplo, se deshabilita IMAP4 para el usuario John Smith.

    Set-CASMailbox -Identity "John Smith" -IMAPEnabled $false

## ¿Cómo saber si el proceso se ha completado correctamente?

1.  En el EAC, vaya a **Destinatarios** \> **Buzones**.

2.  En el panel de resultados, seleccione el usuario para el que desee habilitar o deshabilitar IMAP4 y, luego, haga clic en **Editar**.

3.  En el cuadro de diálogo **Buzón de usuario** en el árbol de la consola, haga clic en **Características de buzón**.
    
    En el panel de resultados, busque en **Conectividad de correo electrónico**.
    
      - Si IMAP4 está habilitada para el usuario, se verá **IMAP4: Habilitado**.
    
      - Si IMAP4 no está habilitada para el usuario, se verá **IMAP4: Deshabilitado**.

4.  Haga clic en **Guardar**.

