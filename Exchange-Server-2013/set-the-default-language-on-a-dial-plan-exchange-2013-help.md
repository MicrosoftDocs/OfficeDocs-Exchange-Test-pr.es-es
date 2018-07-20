---
title: 'Establecer el idioma predeterminado en un plan de marcado: Exchange 2013 Help'
TOCTitle: Establecer el idioma predeterminado en un plan de marcado
ms:assetid: 7a1d2e7e-4053-40af-9ec1-ec714df12ad4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998914(v=EXCHG.150)
ms:contentKeyID: 50556826
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Establecer el idioma predeterminado en un plan de marcado

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2016-12-09_

Puede establecer el idioma predeterminado del plan de marcado de mensajería unificada. Cada plan de marcado que cree usarán el idioma inglés de Estados Unidos (en-US) como idioma predeterminado. El paquete de idioma inglés de Estados Unidos (en-US) se instala en todas las versiones de Microsoft Exchange Server 2013 y no se puede quitar.

Si desea seleccionar otro idioma como idioma predeterminado, por ejemplo, alemán (de-DE), primero debe descargar el alemán UM language pack archivo .exe desde [Exchange Server 2013 UM paquetes de idioma](https://go.microsoft.com/fwlink/p/?linkid=266542) e instalar ese paquete de idiomas en el servidor de buzones mediante el archivo de instalación UMLanguagePack.de-de.exe. Una vez instalado el paquete de idioma, puede establecer el idioma predeterminado a un idioma distinto del inglés (en-US) en los planes de marcado de mensajería UNIFICADA.

Para consultar otras tareas relacionadas con los idiomas de mensajería unificada, vea [Procedimientos de lenguajes, mensajes y saludos de mensajería unificada](um-languages-prompts-and-greetings-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Planes de marcado de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Use el EAC para configurar el idioma predeterminado en un plan de marcado de mensajería unificada

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**.

2.  En la vista de la lista, seleccione el plan de marcado de mensajería unificada que quiere modificar y luego, en la barra de herramientas, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Plan de marcado de mensajería unificada**, haga clic en **Configurar**.

4.  En la página **Configuraciones**, en **Idioma del audio**, seleccione el idioma que desee establecer de la lista desplegable.

5.  Haga clic en **Guardar** para aceptar los cambios.

## Use el Shell para configurar el idioma predeterminado en un plan de marcado de mensajería unificada

En este ejemplo, se establece el idioma predeterminado de un plan de marcado de MU denominado `MyUMDialPlan` en alemán.

    Set-UMDialPlan -Identity MyUMDialPlan -DefaultLanguage de-DE

En este ejemplo, se establece el idioma predeterminado de un plan de marcado de MU denominado `MyUMDialPlan` en alemán.

    Set-UMDialPlan -Identity MyUMDialPlan -DefaultLanguage ja-JP

En este ejemplo, se establece el idioma predeterminado de un plan de marcado de MU denominado `MyUMDialPlan` en japonés.

    Set-UMDialPlan -Identity MyUMDialPlan -DefaultLanguage en-AU

