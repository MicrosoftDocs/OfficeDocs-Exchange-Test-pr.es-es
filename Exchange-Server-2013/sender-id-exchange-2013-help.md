---
title: 'Id. del remitente: Exchange 2013 Help'
TOCTitle: Id. del remitente
ms:assetid: 0f628f83-df8c-43fb-bf49-7aaa9ec69ab1
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa996295(v=EXCHG.150)
ms:contentKeyID: 49895469
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Id. del remitente

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

El Id. del remitente es un agente contra correo electrónico no deseado que está disponible en Microsoft Exchange Server 2013. El agente del Id. de remitente usa el encabezado RECEIVED del SMTP y una consulta al servicio DNS del sistema de envío para determinar qué acción hay que tomar sobre los mensajes entrantes, si hay que tomar alguna.

El Id. de remitente está pensado para combatir la suplantación de remitentes y dominios, una práctica que se suele denominar *suplantación de identidad*. Un *mensaje falsificado* es un mensaje de correo electrónico en el que la dirección del remitente se ha modificado para parecer que ha partido de un remitente que no es el que ha enviado originalmente el mensaje.

Los mensajes falsificados normalmente contiene una dirección De: que pretende ser de una determinada organización. En el pasado, era relativamente fácil suplantar la identidad de la dirección De:, en la sesión de SMTP, como el encabezado MAIL FROM: y en los datos de mensaje RFC 2822, tales como De: "Benito Almudena" benito@contoso.com, ya que los encabezados no se validaban.

**Contenido**

Uso de Id. del remitente para combatir la suplantación de identidad

Actualización del DNS expuesto a Internet de la organización para que admita el Id. de remitente

Especificación de dominios de remitentes y destinatarios que serán excluidos del filtrado de Id. del remitente

## Uso de Id. del remitente para combatir la suplantación

El Id. de remitente dificulta aún más la suplantación de identidad. Al habilitar el Id. del remitente, todos los mensajes contienen un estado de Id. del remitente en sus metadatos. Cuando se recibe un mensaje de correo electrónico, el servidor Exchange consulta al servidor DNS del remitente para comprobar que la dirección IP de la que se recibió el mensaje esté autorizada para enviar mensajes al dominio que se especifica en los encabezados del mensaje. La dirección IP del servidor remitente autorizado se denomina dirección de responsabilidad supuesta (PRA).

Los administradores de dominio publicar registros de framework (SPF) de directiva de remitente en los servidores DNS. Registros de SPF identifican los servidores de correo electrónico saliente autorizada. Si se configura un registro SPF en el servidor del remitente DNS, el servidor de Exchange analiza el registro SPF y determina si la dirección IP desde la que se recibió el mensaje está autorizada a enviar correo electrónico en nombre del dominio que se especifica en el mensaje. Para obtener más información acerca de lo que contiene un registro SPF y cómo crear un registro SPF, consulte [ID de remitente](https://go.microsoft.com/fwlink/p/?linkid=50977).

El servidor Exchange actualiza los metadatos del mensaje con el estado de Id. del remitente según el registro de SPF. Después de que el servidor Exchange actualice los metadatos del mensaje, la entrega de mensajes continúa con normalidad.

## Valores del estado del Id. del remitente

El proceso de evaluación de Id. del remitente genera un estado de Id. del remitente para el mensaje. El estado del Id. de remitente se usa para evaluar la clasificación del nivel de confianza contra correo no deseado (SCL) del mensaje. Este estado se puede establecer en uno de los valores siguientes:

  - **Pass** La dirección IP y la Dirección responsable pretendida (PRA) han superado la comprobación del Id. de remitente.

  - **Neutral** Los datos del Id. de remitente publicados no son explícitamente concluyentes.

  - **Soft fail** Es posible que la dirección IP de la PRA no esté en el conjunto permitido.

  - **Fail** La dirección IP no está permitida; no se encontró ninguna PRA en el correo entrante o no existe el dominio remitente.

  - **None** No hay datos publicados de la SPF en el DNS del remitente.

  - **TempError** Ha ocurrido un error temporal de DNS como, por ejemplo, un servidor DNS no disponible.

  - **PermError** El registro DNS no es válido; por ejemplo, existe un error en el formato de registro.

El estado de Id. del remitente se agrega a los metadatos del mensaje y posteriormente se convierte en una propiedad de MAPI. El filtro de correo no deseado de Microsoft Outlook usa la propiedad MAPI durante la creación del valor de SCL.

Outlook no muestra el estado del Id. del remitente ni necesariamente marca un mensaje como correo no deseado en ciertos valores de Id. del remitente. Outlook usa el estado del Id. del remitente sólo durante el cálculo del valor de SCL.

Además de los siete escenarios que generan los estados Id. del remitente, el proceso de evaluación de Id. del remitente puede revelar instancias en que falte la dirección IP de origen. Si falta la dirección IP de origen, no se puede establecer el estado del Id. de remitente. Si el estado del Id. del remitente no se puede establecer, Exchange sigue procesando el mensaje sin incluir ningún estado del Id. del remitente en él. El mensaje no se descarta ni se rechaza. En esta situación, no se establece el estado del Id. de remitente, y se registra un evento de aplicación.

Para obtener más información acerca de la forma en que se muestra el estado del Id. del remitente en los mensajes, consulte [Marcas de correo no deseado](anti-spam-stamps-exchange-2013-help.md).

## Opciones de Id. del remitente para gestionar el mensaje falsificado y servidores DNS inaccesibles

También es posible definir la forma en que el servidor Exchange gestiona los mensajes que se identifican como mensajes falsificados y también el modo en que gestiona los mensajes cuando no se puede tener acceso a un servidor DNS. Las opciones relativas a la forma en que el servidor Exchange gestiona el mensaje falsificado y los servidores DNS inaccesibles incluyen las siguientes acciones:

  - **Marcar el estado**   Esta opción es la acción predeterminada. Todos los mensajes que entran a la organización tienen el estado de Id. del remitente incluido en los metadatos.

  - **Rechazar** Esta opción rechazará el mensaje y enviará una respuesta de error de SMTP al servidor de envío. La respuesta de error de SMTP es una respuesta del protocolo de nivel 5*xx* con texto que corresponde al estado de Id. de remitente.

  - **Eliminar**   Esta opción elimina el mensaje sin informar al sistema de envío de la eliminación. De hecho, el servidor de Exchange envía un comando Aceptar SMTP falso al servidor de envío y, a continuación, elimina el mensaje. Dado que el servidor de envío asume que se ha enviado el mensaje, no vuelve a intentar enviar el mensaje en la misma sesión.

Para obtener más información sobre cómo configurar el agente del Id. de remitente, consulte [Administración del Id. del remitente](manage-sender-id-exchange-2013-help.md).

Volver al principio

## Actualización del DNS expuesto a Internet de la organización para que admita el Id. de remitente

La eficacia del Id. de remitente depende de los datos concretos del DNS. Cuantas más organizaciones actualicen los servidores DNS expuestos a Internet mediante un registro de SPF, mayor eficacia tendrá el Id. de remitente al identificar mensajes de correo electrónico falsificados.

Para admitir la infraestructura de ID de remitente, debe actualizar sus datos DNS a través de Internet mediante la creación de un registro SPF y aloja el registro SPF en los servidores DNS públicos. Para obtener más información acerca de cómo crear e implementar registros de SPF, consulte [ID de remitente](https://go.microsoft.com/fwlink/p/?linkid=50977).

Volver al principio

## Especificación de dominios de remitentes y destinatarios que serán excluidos del filtrado de Id. del remitente

Quizá desee excluir determinados dominios de remitentes y destinatarios del filtrado de Id. de remitente. Para hacerlo, especifique los dominios de los destinatarios y remitentes con el cmdlet **Set-SenderIdConfig** en el Shell de administración de Exchange. Para obtener más información, consulte [Set-SenderIdConfig](https://technet.microsoft.com/es-es/library/aa998859\(v=exchg.150\)).

Volver al principio

