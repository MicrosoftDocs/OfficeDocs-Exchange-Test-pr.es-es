---
title: 'Seleccione el idioma para el operador automático: Exchange 2013 Help'
TOCTitle: Seleccione el idioma para el operador automático
ms:assetid: 3a1c1ec0-c726-41fb-a294-59faab205609
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997306(v=EXCHG.150)
ms:contentKeyID: 50556761
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Seleccione el idioma para el operador automático

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2016-12-09_

Puede configurar el idioma predeterminado del mensaje en un operador automático de mensajería unificada (MU). La opción de idioma que está disponible en un operador automático de MU permite configurar el idioma de los mensajes predeterminados del operador automático. Cuando usa los mensajes predeterminados del sistema para el operador automático, el idioma de dichos mensajes será el que escuche la persona que llama cuando el operador automático responda la llamada entrante. Esta configuración de idioma solo afecta los mensajes predeterminados del sistema que se proporcionan después de la instalación del servidor de buzones que ejecuta el servicio de mensajería unificada de Microsoft Exchange. Esta configuración no afecta a los mensajes personalizados que están configurados en un operador automático. Los idiomas disponibles están basados en los paquetes de idioma de mensajería unificada que están instalados en el servidor de buzones.

Cada operador automático que crea utilizará inicialmente inglés (en-US) como el idioma predeterminado. El paquete de idioma inglés (en-US) se instala de forma predeterminada en todas las versiones de Microsoft 2013 de Exchange y no puede quitarse. Si desea seleccionar otro idioma, por ejemplo, alemán (de-DE), primero debe descargar el alemán UM language pack archivo .exe desde [Exchange Server 2013 UM paquetes de idioma](https://go.microsoft.com/fwlink/?linkid=266542) e instalar el paquete de idioma de mensajería UNIFICADA en el servidor de buzones mediante el archivo de instalación UMLanguagePack.de-de.exe. Una vez instalado el paquete de idioma de mensajería UNIFICADA, puede establecer el idioma predeterminado a un idioma distinto del inglés (en-US) en operadores automáticos de mensajería UNIFICADA.

Para consultar otras tareas relacionadas con los idiomas de mensajería unificada, vea [Procedimientos de lenguajes, mensajes y saludos de mensajería unificada](um-languages-prompts-and-greetings-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el contenido "Operadores automáticos de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un operador automático de MU. Para conocer los pasos detallados, consulte [Crear un operador automático de mensajería unificada](create-a-um-auto-attendant-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso del Centro de Administración de Exchange para configurar el idioma predeterminado

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**.

2.  En la vista de la lista, seleccione el plan de marcado de mensajería unificada que quiere modificar y luego, en la barra de herramientas, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Plan de marcado de MU**, en **Operadores automáticos de mensajería unificada**, seleccione el operador automático de MU que desee cambiar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

4.  En la página **General**, en **Idioma de la interfaz de voz automatizada**, seleccione el idioma requerido de la lista desplegable.

5.  Haga clic en **Guardar** para aceptar los cambios.

## Usar el Shell para configurar el idioma predeterminado

En este ejemplo, el idioma predeterminado en el operador automático de MU `MyUMAutoAttendant` es inglés (Reino Unido).

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -Language en-GB

En este ejemplo, el idioma predeterminado en el operador automático de MU `MyUMAutoAttendant` es alemán.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -Language de-DE

