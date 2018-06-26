---
title: 'Establecer la longitud mínima del NIP de correo de voz: Exchange 2013 Help'
TOCTitle: Establecer la longitud mínima del NIP de correo de voz
ms:assetid: b2ecab54-42e6-45af-8322-615cc1f68dd9
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124271(v=EXCHG.150)
ms:contentKeyID: 50556865
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Establecer la longitud mínima del NIP de correo de voz

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2013-02-22_

Puede configurar la longitud mínima del PIN de los usuarios de Outlook Voice Access que estén habilitados para mensajería unificada (UM). Las opciones de PIN que configure en una directiva de buzón de mensajería unificada se aplicarán a todos los usuarios habilitados para mensajería unificada asociados a dicha directiva.

Outlook Voice Access permite a los usuarios habilitados para mensajería unificada obtener acceso al correo de voz, al correo electrónico, a los calendarios y a los datos personales de contacto ubicados en su buzón. Sin embargo, para poder obtener acceso al buzón, los usuarios deben indicar un PIN para que el sistema de correo de voz los pueda autenticar.


> [!NOTE]
> Si cambia el valor de longitud mínima del PIN, se solicitará a los usuarios de Outlook Voice Access existentes que indiquen un nuevo PIN que contenga el nuevo número mínimo de dígitos para que puedan continuar. El valor predeterminado es 6.



Para conocer otras tareas relacionadas con la seguridad del PIN de Outlook Voice Access, consulte [Procedimientos de seguridad PIN](pin-security-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el el contenido "Directivas de buzón de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para configurar la longitud mínima del PIN para Outlook Voice Access

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**.

2.  En la vista de lista, seleccione el plan de marcado que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de **plan de marcado de mensajería unificada**, en **Directivas de buzón de correo de mensajería unificada**, seleccione la directiva de buzones de mensajería unificada que desea cambiar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

4.  Haga clic en **Directivas de NIP** y, al lado de **Longitud mínima de NIP**, escriba un valor entre 4 y 24.

5.  Haga clic en **Guardar**.

## Usar el Shell para configurar la longitud mínima del PIN para Outlook Voice Access

En este ejemplo se establece la configuración de PIN en 8 dígitos para usuarios de Outlook Voice Access asociados a la directiva de buzones de mensajería unificada denominada `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -MinPINLength 8

En este ejemplo, la longitud mínima de PIN se establece en 8 dígitos; asimismo, se define la cantidad de veces que un inicio de sesión puede ser incorrecto antes de establecer en 3 el PIN del usuario. Esta acción se aplica a usuarios habilitados para mensajería unificada asociados con la directiva de buzón de mensajería unificada `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3 -MinPINLength 8

