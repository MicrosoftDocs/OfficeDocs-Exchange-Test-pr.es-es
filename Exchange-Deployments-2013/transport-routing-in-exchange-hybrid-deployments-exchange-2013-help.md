---
title: 'Enrutamiento de transporte en las implementaciones híbridas de Exchange: Exchange 2013 Help'
TOCTitle: Enrutamiento de transporte en las implementaciones híbridas de Exchange
ms:assetid: 36c2cea3-2e2f-40ac-88bd-7e1b6bd27828
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ659050(v=EXCHG.150)
ms:contentKeyID: 49895003
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Enrutamiento de transporte en las implementaciones híbridas de Exchange

 

_<strong>Se aplica a:</strong>Exchange Server 2013, Exchange Server 2016_

_<strong>Última modificación del tema:</strong>2016-07-29_

Este tema le brinda información sobre opciones de enrutamiento para mensajes entrantes desde Internet y salientes hacia Internet.


> [!IMPORTANT]
> No coloque servidores, servicios o dispositivos entre sus servidores de Exchange locales y Office 365 que procesen o modifiquen el tráfico SMTP. El flujo de correo seguro entre la organización de Exchange local y Office 365 depende de la información contenida en los mensajes enviados en la organización. Se admiten los firewalls que permiten el tráfico SMTP en el puerto TCP 25 sin ninguna modificación. Si un servidor, servicio o dispositivo procesa un mensaje enviado entre su organización de Exchange local y Office 365, esta información se elimina. Si esto ocurre, el mensaje ya no se considerará interno de la organización y estará sujeto al filtrado de correo no deseado, a las reglas de transporte y del diario y a otras directivas que podrían no aplicársele.




> [!NOTE]
> Los ejemplos de este tema no incluyen la adición de servidores de transporte de concentradores en la implementación híbrida. Las rutas que toman los mensajes entre la organización local, la organización de Exchange Online e Internet, no cambian con la adición de un servidor de transporte perimetral. Solo cambia el enrutamiento dentro de la organización local. Para obtener más información acerca de cómo agregar servidores de transporte perimetral a la implementación híbrida, consulte <A href="edge-transport-servers-with-hybrid-deployments-exchange-2013-help.md">Servidores de transporte perimetral con implementaciones híbridas</A>.



## Mensajes entrantes de Internet

Como parte de la planificación y configuración de la implementación híbrida, debe decidir si quiere que todos los mensajes entrantes de los remitentes de Internet se enruten mediante la organización local o mediante la organización de Exchange Online. Todos los mensajes de los remitentes de Internet se entregarán inicialmente a la organización que seleccione y, después, se enrutarán a la ubicación del buzón de voz. La elección de tener los mensajes enrutados mediante la organización local o la organización de Exchange Online dependerá de varios factores, incluidos si quiere aplicar directivas de cumplimiento a todos los mensajes enviados a ambas organizaciones, cuántos buzones de correo hay en cada organización, etc.

Los mensajes de ruta enviados a los destinatarios de las organizaciones local y de Exchange Online dependen de cómo decida configurar su registro MX en la implementación híbrida. El método preferido es configurar el registro MX para que apunte a Exchange Online Protection (EOP) en Office 365, ya que esta configuración proporciona el filtrado de correo no deseado más preciso. El asistente de configuración híbrida no configura la ruta para los mensajes entrantes de Internet para la organización local ni para la organización Exchange Online. Debe configurar manualmente su registro MX si quiere cambiar el modo en el que se envía el correo entrante de Internet.

  - **Si cambia el registro MX para que apunte al servicio de Exchange Online Protection en Office 365** Esta es la configuración recomendada para las implementaciones híbridas. Todos los mensajes enviados a cualquier destinatario en cualquier organización se enrutan primero a través de la organización de Exchange Online. Un mensaje dirigido a un destinatario ubicado en la organización local se enruta primero mediante la organización de Exchange Online y, después, se entrega al destinatario de la organización local. Se recomienda esta ruta cuando tiene más destinatarios en la organización de Exchange Online que en la organización local. Esta opción de configuración es necesaria para que Exchange Online Protection examine y bloquee el correo no deseado.

  - **Si decide que los registros MX sigan apuntando a su organización local** Todos los mensajes enviados a cualquier destinatario de cualquier organización se enrutan primero a través de su organización local. Un mensaje dirigido a un destinatario ubicado en Exchange Online se enruta primero mediante la organización local y, luego, se entrega al destinatario de Exchange Online. Esta ruta puede ser útil para organizaciones donde tiene directivas de cumplimiento que requieren el análisis de una solución de registro en diario de los mensajes enviados desde la organización y hacia esta. Si elige esta opción, Exchange Online Protection no puede examinar con eficacia los mensajes de correo no deseado.

Para obtener más información, consulte [Procedimientos recomendados de flujo de correo para Exchange Online y Office 365 (descripción general)](https://technet.microsoft.com/es-es/library/jj937232\(v=exchg.150\)).

Lea la sección a continuación que muestra cómo planear el enrutamiento de mensajes enviados desde destinatarios de Internet a sus destinatarios de la organización local y de Exchange Online. En cada sección, el "servidor de Exchange local" puede ser un servidor de acceso de cliente de Exchange 2013 o un servidor de buzones de correo de Exchange 2016.

## Enrutar mensajes entrantes de Internet mediante la organización de Exchange Online

Los pasos y diagramas a continuación ilustran la ruta de mensajes entrantes que se traza en su implementación híbrida si decide apuntar su registro MX al servicio EOP en la organización Office 365. La ruta del mensaje será distinta si elige habilitar el transporte de correo centralizado.


> [!IMPORTANT]
> Es posible que necesite comprar licencias de EOP para cada buzón de correo local que reciba mensajes que se entreguen primero a EOP y que, a continuación, se enruten mediante la organización de Exchange Online. Póngase en contacto con su revendedor de Microsoft para obtener más información.



Cuando el transporte de correo centralizado está **deshabilitado** (configuración predeterminada), los mensajes de Internet entrantes se enrutan de la siguiente manera en una implementación híbrida:

1.  Se envía un mensaje entrante desde un remitente de Internet a los destinatarios julie@contoso.com y david@contoso.com. El buzón de correo de Julie está ubicado en un servidor de buzones de correo de Exchange en la organización local. El buzón de David está ubicado en Exchange Online.

2.  Dado que ambos destinatarios tienen direcciones de correo electrónico contoso.com y que el registro MX para contoso.com apunta a EOP, el mensaje se entrega a EOP.

3.  EOP enruta los mensajes para ambos destinatarios a Exchange Online.

4.  Exchange Online examina los mensajes en busca de virus y realiza una búsqueda para cada destinatario. Mediante la búsqueda, determina que el buzón de correo de Julie está ubicado en la organización local mientras que el buzón de correo de David está en la organización de Exchange Online.

5.  Exchange Online divide el mensaje en dos copias. Una copia del mensaje se entrega al buzón de correo de David.

6.  La segunda copia se envía desde Exchange Online de vuelta a EOP.

7.  EOP envía el mensaje a un servidor de Exchange local en la organización local.

8.  Exchange envía el mensaje al servidor de buzones de correo de Exchange, donde se entrega al buzón de Julie.

**Enrutar el correo mediante la organización de Exchange Online para ambas organizaciones, local y de Exchange Online, con el transporte de correo centralizado deshabilitado (configuración predeterminada)**

![Entrada centralizada a EXO](images/JJ659050.f98341e0-088d-49f0-bf8e-09f35255bf9e(EXCHG.150).png "Entrada centralizada a EXO")

Cuando el transporte de correo centralizado está **habilitado**, los mensajes de Internet entrantes se enrutan de la siguiente manera en una implementación híbrida:

1.  Se envía un mensaje entrante desde un remitente de Internet a los destinatarios julie@contoso.com y david@contoso.com. El buzón de correo de Julie está ubicado en un servidor de buzones de correo de Exchange en la organización local. El buzón de David está ubicado en Exchange Online.

2.  Dado que ambos destinatarios tienen direcciones de correo electrónico contoso.com y que el registro MX para contoso.com apunta a EOP, el mensaje se entrega a EOP, donde se examina en busca de virus.

3.  Dado que el transporte de correo centralizado está habilitado, EOP enruta los mensajes para ambos destinatarios a un servidor de Exchange local.

4.  El servidor de Exchange local realiza una búsqueda para cada destinatario. Mediante la búsqueda, determina que el buzón de correo de Julie está ubicado en la organización local mientras que el buzón de correo de David está en la organización de Exchange Online.

5.  El servidor de Exchange local divide el mensaje en dos copias. Una copia del mensaje se entrega en el buzón de Julie en el servidor de buzones de correo de Exchange local.

6.  La segunda copia se envía desde el servidor de Exchange local de vuelta a EOP.

7.  EOP envía el mensaje a Exchange Online.

8.  Exchange entrega el mensaje al buzón de David.

**Enrutar el correo mediante la organización Exchange Online para ambas organizaciones, local y de Exchange Online, con el transporte de correo centralizado habilitado**

![EXO entrante, centralizado habilitado](images/JJ659050.062422d5-9cb6-42c2-9ec0-31962cd7ada6(EXCHG.150).png "EXO entrante, centralizado habilitado")

## Enrutamiento de los mensajes entrantes de Internet a través de su organización local

Los siguientes pasos y el diagrama a continuación ilustran la ruta de los mensajes entrantes de Internet que se trazará en su implementación híbrida si decide mantener su registro MX apuntando a su organización local.

1.  Se envía un mensaje entrante desde un remitente de Internet a los destinatarios julie@contoso.com y david@contoso.com. El buzón de correo de Julie está ubicado en un servidor de buzones de correo de Exchange en la organización local. El buzón de David está ubicado en Exchange Online.

2.  Dado que ambos destinatarios tienen direcciones de correo electrónico contoso.com y el registro MX para contoso.com apunta a la organización local, el mensaje se entrega a un servidor de Exchange local.

3.  El servidor de Exchange local realiza una búsqueda para cada destinatario usando un servidor de catálogo global local. Mediante la búsqueda de catálogo global se determina que el buzón de Julie está ubicado en un servidor de buzones de correo de Exchange local, mientras que el buzón de David está ubicado en la organización de Exchange Online y tiene la dirección de enrutamiento híbrida david@contoso.mail.onmicrosoft.com.

4.  El servidor de Exchange local divide el mensaje en dos copias. Una copia del mensaje se envía al servidor de buzones de correo de Exchange local, desde donde se entrega al buzón de correo de Julie.

5.  La segunda copia del mensaje es enviada mediante el servidor de Exchange local a EOP, que recibe el mensaje enviado a la organización de Exchange Online mediante un conector de envío configurado para su uso con TLS.

6.  EOP envía el mensaje a la organización de Exchange Online, donde se examina el mensaje en busca de virus y se entrega al buzón de correo de David.

**Enrutar el correo entrante mediante la organización local para ambas organizaciones local y de Exchange Online**

![Correo entrante centralizado, local](images/JJ659050.a246a1e2-7593-4d13-9426-73622a545c9a(EXCHG.150).png "Correo entrante centralizado, local")

## Mensajes salientes a Internet

Además de elegir cómo enrutar los mensajes entrantes dirigidos a los destinatarios de la organización, también puede elegir cómo enrutar los mensajes salientes enviados por parte de los destinatarios de Exchange Online. Cuando ejecuta el Asistente de configuración híbrida, puede seleccionar una de dos opciones:

  - **No habilitar el transporte de correo centralizado**   Esta opción está seleccionada de manera predeterminada en el Asistente de configuración híbrida y es la que enruta los mensajes salientes enviados desde la organización de Exchange Online directamente a Internet. Use esta opción si no necesita aplicar directivas de cumplimiento locales u otras reglas de procesamiento a los mensajes que se envían por parte de los destinatarios en la organización de Exchange Online.

  - **Habilitar el transporte de correo centralizado**   Esta opción enruta los mensajes salientes enviados desde la organización Exchange Online mediante la organización local. A excepción de los mensajes enviados a otros destinatarios en la misma organización de Exchange Online, todos los mensajes enviados de los destinatarios de la organización de Exchange Online se envían mediante la organización local. Esto permite aplicar las reglas de cumplimiento a estos mensajes y otros procesos o requisitos que se deben aplicar a todos los destinatarios, independientemente de si están ubicados en la organización de Exchange Online o en la organización local.
    

    > [!NOTE]
    > El transporte de correo centralizado solo se recomienda para las organizaciones con necesidades de transporte específicas relacionadas con el cumplimiento. Nuestra recomendación para las organizaciones Exchange típicas es que no se habilite el transporte de correo centralizado.



Los mensajes enviados desde destinatarios locales siempre se envían directamente a los destinatarios de Internet mediante DNS, independientemente de cuáles de las opciones de arriba seleccione en el Asistente de configuración híbrida.

Los siguientes pasos y el siguiente diagrama ilustran la ruta de mensajes salientes para los mensajes enviados desde los destinatarios locales.

1.  Julie, que tiene un buzón en el servidor de buzones de correo de Exchange, envía un mensaje a un destinatario externo de Internet, erin@cpandl.com.

2.  El servidor de Exchange busca el registro MX para cpandl.com y envía el mensaje a los servidores de correo de cpandl.com ubicados en Internet.

**Mensajes de remitentes locales a destinatarios de Internet**

![Correo saliente desde organización local](images/JJ659050.71f287d6-b814-4820-a0dc-575f17d13894(EXCHG.150).png "Correo saliente desde organización local")

Lea la sección a continuación que muestra cómo planear el enrutamiento de mensajes enviados por parte de destinatarios de la organización de Exchange Online a destinatarios de Internet.

## Entrega de mensajes de Internet desde Exchange Online mediante DNS (transporte de correo centralizado deshabilitado)

Los pasos y el diagrama a continuación ilustran la ruta que recorren los mensajes salientes enviados desde los destinatarios de Exchange Online a un destinatario en Internet cuando la opción **Habilitar el transporte de correo centralizado** no está seleccionada en el Asistente de implementación híbrida, que es la configuración predeterminada.

1.  David, que tiene un buzón de correo en el servidor de Exchange Online, envía un mensaje a un destinatario externo de Internet, erin@cpandl.com.

2.  Exchange Online examina el mensaje en busca de virus y envía el mensaje a la empresa EOP de Exchange Online.

3.  EOP busca el registro MX para cpandl.com y envía el mensaje a los servidores de correo de cpandl.com ubicados en Internet.

**Correo de los remitentes de Exchange Online enrutado directamente a Internet con la opción de transporte de correo centralizado deshabilitada (configuración predeterminada)**

![Correo saliente directo EXO](images/JJ659050.fe1c4241-0d6e-47bf-b61d-5af732d2dbbc(EXCHG.150).png "Correo saliente directo EXO")

## Enrutar los mensajes enlazados a Internet desde Exchange Online mediante la organización local (transporte de correo centralizado habilitado)

Los pasos y el diagrama a continuación ilustran la ruta que recorren los mensajes salientes enviados desde los destinatarios de Exchange Online a un destinatario en Internet cuando la opción **Habilitar el transporte de correo centralizado** está seleccionada en el asistente de implementación híbrida.

1.  David, que tiene un buzón de correo en el servidor de Exchange Online, envía un mensaje a un destinatario externo de Internet, erin@cpandl.com.

2.  Exchange Online examina el mensaje en busca de virus y envía el mensaje a EOP.

3.  EOP se configura para enviar todos los mensajes enlazados a Internet a un servidor local, de modo que el mensaje se enruta a un servidor de Exchange local. El mensaje se envía mediante TLS.

4.  El servidor de Exchange local realiza procesos de cumplimiento, antivirus y otros procesos configurados por el administrador en el mensaje de David.

5.  El servidor de Exchange local busca el registro MX para cpandl.com y envía el mensaje a los servidores de correo de cpandl.com ubicados en Internet.

**El correo de los remitentes de Exchange Online enrutado mediante la organización local con la opción de transporte de correo centralizado habilitada**

![Correo EXO saliente a través de organización local](images/JJ659050.7ea9ffee-944b-45ae-ba4d-c3484100399b(EXCHG.150).png "Correo EXO saliente a través de organización local")

