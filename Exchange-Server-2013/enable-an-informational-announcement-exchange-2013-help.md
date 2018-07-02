---
title: 'Habilitar un anuncio informativo: Exchange 2013 Help'
TOCTitle: Habilitar un anuncio informativo
ms:assetid: 07f6c13e-3781-4127-9321-f0f85f054259
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb266918(v=EXCHG.150)
ms:contentKeyID: 50556735
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar un anuncio informativo

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-04-19_

Puede habilitar un anuncio informativo para un operador automático de mensajería unificada (UM). Cuando se habilita un mensaje informativo automático, se reproduce justo después del saludo, ya sea dentro o fuera de horas de oficina. De forma predefinida, no se configura ningún mensaje informativo. Para habilitar un anuncio informativo, cree un archivo .wav o .wma para usarlo como anuncio informativo y luego configure el operador automático para que use este archivo de audio.

Para conocer tareas de administración adicionales relacionadas con los operadores automáticos de mensajería unificada, consulte [Procedimientos operador automático de mensajería unificada](um-auto-attendant-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el contenido "Operadores automáticos de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un operador automático de MU. Para conocer los pasos detallados, consulte [Crear un operador automático de mensajería unificada](create-a-um-auto-attendant-exchange-2013-help.md).

  - Cree el archivo .wav o .wma que se usará para el anuncio informativo.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para habilitar un anuncio informativo

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de UM que quiere cambiar y, luego, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Operadores automáticos de mensajería unificada**, seleccione el operador automático de UM en el que quiere habilitar un anuncio informativo y luego haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Operador automático de mensajería unificada**, \> **Saludos**, en **Anuncio informativo**, haga clic en **Cambiar** y luego en **Examinar** para buscar el archivo del anuncio informativo que creó antes de iniciar este proceso.
    

    > [!IMPORTANT]
    > El archivo que use para el saludo debe ser un archivo .wav o .wma.



4.  Cuando encuentre el archivo, haga clic en **Abrir** y luego en **Guardar**.

## Uso del Shell para habilitar un anuncio informativo

En este ejemplo se habilita un anuncio informativo que usa el archivo `MyInfoAnnouncement.wav` en un operador automático de UM denominado `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -InfoAnnouncementEnabled $true -InfoAnnouncementFilename MyInfoAnnouncement.wav

