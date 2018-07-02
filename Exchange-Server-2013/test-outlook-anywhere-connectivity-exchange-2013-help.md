---
title: 'Comprobar la conectividad de Outlook en cualquier lugar: Exchange 2013 Help'
TOCTitle: Comprobar la conectividad de Outlook en cualquier lugar
ms:assetid: 0dc5b68f-2316-446a-84c9-5f1c50dc3776
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee633453(v=EXCHG.150)
ms:contentKeyID: 50556741
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Comprobar la conectividad de Outlook en cualquier lugar

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Puede probar la conectividad de un extremo a otro del cliente de Outlook Anywhere usando el Shell o el Analizador de conectividad remota de Exchange (ExRCA). Esto incluye pruebas de conectividad a través del servicio Detección automática, la creación de un perfil de usuario y el inicio de sesión en el buzón de usuario. Todos los valores necesarios se recuperan del servicio Detección automática.

Para otras tareas de administración relacionadas con Outlook Anywhere, consulte [Outlook en cualquier lugar](outlook-anywhere-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  10 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Outlook Anywhere" en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el Shell para comprobar la conectividad de Outlook en cualquier lugar

Para usar el Shell para probar la conectividad de Outlook Anywhere, use el cmdlet **Test-OutlookConnectivity**.

Ejecute el siguiente comando.

    Test-OutlookConnectivity -ProbeIdentity 'OutlookMailboxDeepTestProbe' -MailboxId tony@contoso.com -Hostname contoso.com


> [!NOTE]
> El valor del parámetro <EM>OutlookMailboxDeepTestProbe</EM> prueba la conectividad desde el servidor de buzones. Para probar la conectividad del servidor de acceso de cliente, use <EM>OutlookMailboxCTPProbe</EM> para el valor del parámetro <EM>ProbeIdentity</EM>.



## Use el Analizador de conectividad remota de Exchange para probar la conectividad de Outlook Anywhere

El Analizador de conectividad remota de Exchange (ExRCA) es una herramienta basada en Web diseñada para probar la conectividad con diferentes protocolos de Exchange. Puede obtener acceso a la ExRCA [aquí](https://go.microsoft.com/fwlink/p/?linkid=167905).

1.  En el sitio web de ExRCA, en **Pruebas de conectividad de Microsoft Office Outlook**, seleccione **Outlook Anywhere** y, luego, seleccione Siguiente en la parte inferior de la página.

2.  Especifique la información solicitada en la pantalla siguiente, incluidos la dirección de correo electrónico, el nombre de usuario y de dominio y la contraseña.

3.  Seleccione si la Detección automática detectará la configuración del servidor o si esta se especificará manualmente.

4.  Acepte la declinación de responsabilidades, especifique el código de verificación y, a continuación, seleccione **Comprobar**.

5.  Seleccione **Realizar prueba**.

## ¿Cómo saber si el proceso se ha completado correctamente?

Cuando la prueba de ExRCA finalice, el resultado se mostrará en la página web. Los errores aparecerán en la pantalla.

