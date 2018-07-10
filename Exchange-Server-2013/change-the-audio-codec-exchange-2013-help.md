---
title: 'Cambio del códec de audio: Exchange 2013 Help'
TOCTitle: Cambio del códec de audio
ms:assetid: 139b2ccd-28c5-46c0-9050-777f4f59aade
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa996342(v=EXCHG.150)
ms:contentKeyID: 49895484
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Cambio del códec de audio

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-22_

La mensajería unificada puede usar uno de cuatro códecs para crear mensajes de correo voz: MP3, Windows Media Audio (WMA), Group System Mobile (GSM) 06.10 y G.711 Pulse Code Modulation (PCM) Linear. De forma predeterminada, al crear un plan de marcado de mensajería unificada, éste usa el códec de audio MP3 para grabar mensajes de voz. El formato de audio MP3 es un formato de audio popular que se usa en varios sistemas operativos, clientes de correo electrónico y reproductores de MP3. Después de crear el plan de marcado de mensajería unificada, puede configurarlo de forma que use uno de los formatos de audio que incluyen los códecs de audio WMA, GSM 06.10 o G.711 PCM Linear. Para escuchar un mensaje de voz, un teléfono móvil o un equipo deben tener una aplicación de software compatible instalada.

Para obtener más información acerca de otras tareas relacionadas con los planes de marcado de mensajería unificada, consulte [Procedimientos de plan de marcado de mensajería unificada](um-dial-plan-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Planes de marcado de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para cambiar el códec de audio en un plan de marcado de mensajería unificada

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**.

2.  En la vista de lista, seleccione el plan de marcado de MU que desea modificar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Plan de marcado de la mensajería unificada**, haga clic en **Configurar**.

4.  En **Configuración**, en **Códec de audio**, use la lista desplegable para seleccionar una de las opciones:
    
      - MP3
    
      - WMA
    
      - GSM
    
      - G711

5.  Haga clic en **Guardar**.

## Usar el Shell para cambiar el códec de audio en un plan de marcado de mensajería unificada

En este ejemplo, se establece el códec de audio en un plan de marcado de MU denominado `MyUMDialPlan` para G.711.

    Set-UMDialPlan -Identity MyUMDialPlan -AudioCodec G711

En este ejemplo, se establece el códec de audio en un plan de marcado de MU denominado `MyUMDialPlan` para WMA.

    Set-UMDialPlan -Identity MyUMDialPlan -AudioCodec Wma

