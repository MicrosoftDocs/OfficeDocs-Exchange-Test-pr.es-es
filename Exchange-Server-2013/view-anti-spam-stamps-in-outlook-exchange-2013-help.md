---
title: 'Ver marcas de correo electrónico no deseado en Outlook: Exchange 2013 Help'
TOCTitle: Ver marcas de correo electrónico no deseado en Outlook
ms:assetid: cddb5dbf-ad1e-471c-9fc8-28ddcf7ec1d0
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124595(v=EXCHG.150)
ms:contentKeyID: 49895922
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ver marcas de correo electrónico no deseado en Outlook

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2012-10-03_

Puede utilizar Microsoft Outlook para ver las marcas de correo electrónico no deseado que Microsoft Exchange aplicó a un mensaje de correo electrónico. Las marcas de correo electrónico no deseado lo ayudan a diagnosticar los problemas relacionados con el correo no deseado mediante la aplicación de metadatos de diagnóstico, o marcas, como información específica del remitente, resultados de la validación del puzzle y resultados del filtrado de contenido a los mensajes mientras pasan a través de agentes contra correo no deseado que filtran los mensajes entrantes de Internet.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 15 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Acceso al buzón" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Usar Outlook 2010 o Outlook 2013 para ver marcas de correo electrónico no deseado

1.  En un equipo de cliente, en Outlook 2010 o Outlook 2013, vaya a la vista **Correo** y haga doble clic en el mensaje para abrirlo.

2.  En la sección **Etiquetas** de la Cinta, haga clic en el icono **Opciones** para mostrar el cuadro de diálogo **Propiedades** del mensaje.

3.  En el cuadro de diálogo **Propiedades**, vaya a la sección **Encabezados de Internet** y use la barra de desplazamiento para ver las marcas de correo electrónico no deseado, como se muestra en el siguiente ejemplo.
    
        X-MS-Exchange-Organization-PCL:7
        X-MS-Exchange-Organization-SCL:6
        X-MS-Exchange-Organization-Antispam-Report: DV:3.1.3924.1409;SID:SenderIDStatus Fail;PCL:PhishingLevel SUSPICIOUS;CW:CustomList;PP:Presolved;TIME:TimeBasedFeatures

## Usar Outlook 2007 para ver marcas de correo no deseado

1.  En un equipo cliente de Outlook 2007, vaya a la vista**Correo** y haga doble clic en un mensaje para abrirlo.

2.  En la ficha **Mensaje**, vaya al grupo **Opciones** y haga clic en **Opciones de mensaje**.

3.  En el cuadro de diálogo **Opciones de mensaje**, vaya a la sección **Encabezados de Internet** y use la barra de desplazamiento para ver las marcas de correo electrónico no deseado, como se muestra en el siguiente ejemplo.
    
        X-MS-Exchange-Organization-PCL:7
        X-MS-Exchange-Organization-SCL:6
        X-MS-Exchange-Organization-Antispam-Report: DV:3.1.3924.1409;SID:SenderIDStatus Fail;PCL:PhishingLevel SUSPICIOUS;CW:CustomList;PP:Presolved;TIME:TimeBasedFeatures

