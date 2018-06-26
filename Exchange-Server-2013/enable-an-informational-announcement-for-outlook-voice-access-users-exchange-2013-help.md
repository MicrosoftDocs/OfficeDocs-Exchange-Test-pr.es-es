---
title: 'Habilitar un anuncio informativo para los usuarios de Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Habilitar un anuncio informativo para los usuarios de Outlook Voice Access
ms:assetid: b69ed0e1-f978-498a-963e-42a047678db4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124344(v=EXCHG.150)
ms:contentKeyID: 50556871
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar un anuncio informativo para los usuarios de Outlook Voice Access

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2016-12-09_

Puede habilitar un anuncio informativo en un plan de marcado de mensajería unificada (UM). Los anuncios informativos se usan para avisos generales que cambian con mayor frecuencia que los saludos de bienvenida o para anuncios requeridos por las directivas de conformidad corporativas.

De manera predeterminada, los autores de llamadas, incluidos los usuarios de Outlook que marcan un número de Outlook Voice Access que se ha configurado, no escuchan los anuncios informativos. Si desea que se reproduzca uno, debe crear un archivo .wav o .wma que se usará con el anuncio informativo tras crear un plan de marcado de mensajería unificada y, a continuación, habilitar el anuncio informativo en el plan de marcado.

Cuando es importante que se escuche todo el anuncio informativo, se puede configurar para que no se pueda interrumpir su reproducción. Esto evita que quien llame presione una tecla o pronuncie un comando para interrumpir y detener el anuncio.

Para obtener más información acerca de las opciones de menú que están disponibles para los usuarios de Voice Access Outlook, consulte a la Guía de referencia rápida para Outlook Voice Access, que está disponible en el [Centro de descarga de Microsoft](https://go.microsoft.com/fwlink/p/?linkid=272767).

Para otras tareas de administración relacionadas con los planes de marcado de mensajería unificada, consulte [Procedimientos de plan de marcado de mensajería unificada](um-dial-plan-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Planes de marcado de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso de la EAC para habilitar un anuncio informativo

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**.

2.  En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea modificar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Plan de marcado de mensajería unificada**, haga clic en **Configurar**.

4.  En **Outlook Voice Access**, en **Anuncio informativo**, haga clic en **Cambiar** y, a continuación, en **Examinar** para buscar el archivo de anuncio.
    

    > [!IMPORTANT]
    > El archivo que use para el anuncio informativo debe ser .wav o .wma.



5.  Después de encontrar el archivo, haga clic en **Abrir** y, a continuación, en **Guardar**.

## Uso del Shell para habilitar un anuncio informativo

En este ejemplo se habilita un anuncio informativo que usa el archivo informational.wav en un plan de marcado de mensajería unificada con el nombre de `MyUMDialPlan`.

    Set-UMDialPlan -Identity MyUMDialPlan -InfoAnnouncementEnabled $true-InfoAnnouncementFilename c:\UMGreetings\informational.wav

