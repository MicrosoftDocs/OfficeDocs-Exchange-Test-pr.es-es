---
title: 'Opciones de conversión de TNEF: Exchange 2013 Help'
TOCTitle: Opciones de conversión de TNEF
ms:assetid: 989a62fc-4bc1-448f-90c8-7c7b56fe1084
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb310786(v=EXCHG.150)
ms:contentKeyID: 52061912
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Opciones de conversión de TNEF

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

Puede especificar si el Formato de encapsulamiento neutro para el transporte (TNEF) se debería conservar o quitar de los mensajes que dejan la organización de Exchange. TNEF, también conocido como formato de texto enriquecido (RTF) de Outlook o formato de texto enriquecido de Exchange, es un formato específico de Microsoft para encapsular las propiedades de los mensajes MAPI. Todas las versiones de MicrosoftOutlook admiten totalmente TNEF. Outlook Web App traduce TNEF a MAPI y muestra los mensajes con formato. Sin embargo, otros clientes de correo electrónico que no admiten TNEF normalmente muestran mensajes en formato TNEF como mensajes en texto sin formato con documentos adjuntos Winmail.dat o Win.dat.

**Contenido**

Opciones de conversión de TNEF para dominios remotos

Opciones de conversión TNEF para usuarios y contactos de correo

Opciones de conversión TNEF en Outlook

Orden de prioridad para las opciones de conversión TNEF

## Opciones de conversión de TNEF para dominios remotos

Cuando se configuran las opciones de conversión TNEF para un dominio remoto, dichas opciones se aplican a todos los mensajes enviados a ese dominio.

  - En el caso de Exchange Online dedicado, se usa el Centro de administración de Exchange (EAC) para establecer las opciones de conversión de TNEF para un dominio remoto en **Flujo de correo**\>**Dominios remotos**\>**Editar** (![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar")) \>**Utilizar el formato de texto enriquecido de Exchange**.

  - En el caso de Exchange Online y Exchange 2013, puede usar el parámetro *TnefEnabled* en el cmdlet **Set-RemoteDomain** para establecer las opciones de conversión TNEF para un dominio remoto.

Para los dominios remotos de su organización, tendrá las siguientes opciones de configuración de conversión TNEF:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Configuración</th>
<th>En el EAC</th>
<th>En el Shell</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Use el formato TNEF para todos los mensajes enviados al dominio remoto.</p></td>
<td><p><strong>Always</strong></p></td>
<td><p><code>$true</code></p></td>
</tr>
<tr class="even">
<td><p>Nunca utilice el formato TNEF para los mensajes enviados al dominio remoto.</p></td>
<td><p><strong>Never</strong></p></td>
<td><p><code>$false</code></p></td>
</tr>
<tr class="odd">
<td><p>Los mensajes TNEF no se permiten de forma específica o se evitan para los destinatarios del dominio remoto. El que se envíen mensajes TNEF a destinatarios del dominio remoto depende de la configuración concreta del contacto de correo o del usuario de correo, o de la especificada por el remitente de Outlook. Es el valor predeterminado.</p></td>
<td><p><strong>Seguir la configuración del usuario</strong></p></td>
<td><p><code>$null</code> (en blanco)</p></td>
</tr>
</tbody>
</table>


Para más información sobre los dominios remotos, vea [Dominios remotos](remote-domains-exchange-2013-help.md) o [Dominios remotos en Exchange Online](https://technet.microsoft.com/es-es/library/jj966211\(v=exchg.150\)).

Volver al principio

## Opciones de conversión TNEF para usuarios y contactos de correo

Cuando configure las opciones de conversión TNEF para un contacto o usuario de correo, esas opciones se aplicarán a todos los mensajes que se envíen a ese destinatario específico. Se usa el parámetro *UseMapiRichTextFormat* en los cmdlets **Set-MailUser** y **Set-MailContact** para configurar las opciones de conversión TNEF de los usuarios de correo y los contactos de correo.

Para los contactos o usuarios de correo de su organización, tendrá las siguientes opciones de configuración de conversión TNEF:

  - **Siempre**   TNEF se usa para todos los mensajes enviados al destinatario. El valor correspondiente del parámetro *UseMapiRichTextFormat* es `Always`.

  - **Nunca**   TNEF no se usa para ningún mensaje enviado al destinatario. El valor correspondiente del parámetro *UseMapiRichTextFormat* es `Never`.

  - **Usar la configuración predeterminada**   No se permiten los mensajes TNEF o dichos mensajes se evitan para el usuario o contacto de correo. El que se envíen mensajes TNEF al destinatario depende de la configuración concreta del dominio remoto correspondiente o de la especificada por el remitente de Outlook. El valor correspondiente del parámetro *UseMapiRichTextFormat* es `UseDefaultSettings`. Esta es la configuración predeterminada.

Volver al principio

## Opciones de conversión TNEF en Outlook

Los remitentes pueden controlar las opciones de conversión de mensajes TNEF predeterminadas para los mensajes TNEF que se envían a todos los destinatarios fuera de la organización de Exchange. Estas opciones se denominan opciones *Formato de mensajes de Internet*. Las opciones solo se aplican a destinatarios remotos y no se aplican a los destinatarios en la organización de Exchange.


> [!NOTE]
> Las siguientes opciones definen cómo se gestionan los mensajes que contienen texto enriquecido de Outlook cuando se envían a destinatarios externos. Si el formato del mensaje es HTML o texto sin formato, esta configuración no se aplicará.



Tiene las siguientes opciones de conversión de TNEF en Outlook:

  - **Convertir a formato HTML**   Es la opción predeterminada. Todos los mensajes TNEF que se envían a destinatarios remotos se convierten a HTML. Todos los formatos del mensaje se deberían parecer mucho al mensaje original. Los mensajes HTML codificados en MIME los admiten muchos, aunque no todos, clientes de correo electrónico.

  - **Convertir a texto sin formato**   Todos los mensajes TNEF que se envían a destinatarios remotos se convierten a texto sin formato. Se pierden todos los formatos del mensaje.

  - **Enviar con formato de texto enriquecido (RTF) de Outlook**   Todos los mensajes TNEF enviados a destinatarios remotos continúan siendo mensajes TNEF.

Puede configurar estas opciones en las siguientes ubicaciones en Outlook:

  - **Outlook 2010 o Outlook 2013** **Archivo**\>**Opciones**\>**Correo**\>**Formato de mensaje**.

  - **Outlook 2007** **Herramientas**\>**Opciones**\>**Formato de correo**\>**Formato Internet**.

Los remitentes también pueden controlar las opciones de conversión de mensajes TNEF predeterminadas para los mensajes TNEF que se envían a destinatarios específicos fuera de la organización de Exchange. Estas opciones se denominan opciones *Formato de los mensajes de destinatario de Internet*. Las opciones solo se aplican a destinatarios remotos almacenados en su carpeta de Contactos y no se aplican a los destinatarios en la organización de Exchange. Las siguientes opciones de conversión TNEF están disponibles para destinatarios remotos de la carpeta Contactos:

  - **Dejar que Outlook decida el mejor formato de envío**   Es el valor predeterminado. Esta configuración obliga a Outlook a usar la opción de conversión TNEF que especifica el formato Internet predeterminado. Los valores posibles son **Convertir a formato HTML**, **Convertir a texto sin formato** o **Enviar con formato de texto enriquecido (RTF) de Outlook**. Por lo tanto, el mensaje TNEF se puede dejar como TNEF, convertir a HTML o convertir a texto sin formato. Si desea asegurarse de que el mensaje TNEF permanece en TNEF para este destinatario, debería cambiar esta configuración de **Dejar que Outlook decida el mejor formato de envío** a **Enviar con formato de texto enriquecido (RTF) de Outlook**.

  - **Enviar sólo texto sin formato**   Todos los mensajes TNEF que se envían al destinatario se convierten a texto sin formato. Se pierden todos los formatos del mensaje.

  - **Enviar con formato de texto enriquecido (RTF) de Outlook**   Todos los mensajes TNEF enviados a destinatarios remotos continúan siendo mensajes TNEF.

Puede configurar estas opciones para un contacto en las siguientes ubicaciones en Outlook:

  - **Outlook 2010 o Outlook 2013**   Abra la tarjeta de contacto, haga doble clic en la dirección electrónica, haga clic en el icono **Muestra más opciones para interactuar con esta persona** y seleccione **Propiedades de Outlook**. En el cuadro de diálogo **Propiedades del correo electrónico**, seleccione **Formato Internet**.

  - **Outlook 2007**   Abra la tarjeta de contacto, haga doble clic en el campo **Correo electrónico** y seleccione **Formato Internet**.

Volver al principio

## Orden de prioridad para las opciones de conversión TNEF

Exchange utiliza el orden de prioridad como se describe en la siguiente lista para determinar las opciones de conversión TNEF de los mensajes salientes que se envían a destinatarios fuera de la organización de Exchange:

1.  Configuración del dominio remoto

2.  Configuración del usuario de correo o el contacto de correo

3.  Configuración de Outlook

La lista especifica el orden de prioridad de mayor a menor. La opción TNEF en el dominio remoto reemplaza la configuración de TNEF en el usuario de correo, contacto de correo o Outlook. Por ejemplo, suponga que envía un mensaje de texto enriquecido en Outlook, pero el destinatario está en un dominio en el que la opción de dominio remoto no permite específicamente mensajes con formato TNEF. El mensaje recibido por el destinatario estará sin formato o en HTML, pero no en TNEF.

Además, Exchange nunca envía mensajes de formato para codificación neutra para el transporte (STNEF) a destinatarios externos. Solamente se pueden enviar mensajes TNEF a destinatarios fuera de la organización de Exchange.

Volver al principio

