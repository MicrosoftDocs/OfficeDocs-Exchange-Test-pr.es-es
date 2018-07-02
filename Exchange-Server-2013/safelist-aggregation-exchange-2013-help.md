---
title: 'Agregación de lista segura: Exchange 2013 Help'
TOCTitle: Agregación de lista segura
ms:assetid: f05430a0-0405-4b65-a18d-18c9e86a13c4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb125168(v=EXCHG.150)
ms:contentKeyID: 49896005
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Agregación de lista segura

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2013-09-30_

En Microsoft Exchange Server 2013, la *agregación de lista segura* hace referencia a la funcionalidad contra correo electrónico no deseado compartida entre Microsoft Outlook y Exchange. Esta funcionalidad recopila datos de las listas contra correo electrónico no deseado de destinatarios seguros, de remitentes seguros, de remitentes bloqueados y datos de contacto que configuran los usuarios de Outlook y los pone a disposición de los agentes contra correo electrónico no deseado de Exchange.

Si se habilita y configura correctamente la agregación de lista segura, el agente de filtrado de contenido pasa los mensajes de correo electrónico seguros al buzón de correo de la empresa, sin que se realice ningún otro procesamiento adicional. El agente de filtrado de contenido identifica como seguros los mensajes de correo electrónico que los usuarios de Outlook reciben de los contactos en quienes han confiado o que han agregado a las listas de destinatarios seguros o de remitentes seguros de Outlook. Un *contacto* de Outlook es una persona, dentro o fuera de la organización del usuario, de la que el usuario puede guardar distinta información, como correo electrónico, direcciones, números de teléfono y de fax, y direcciones URL de páginas web.

En Exchange 2013, el proceso de agregación de lista segura permite que el agente de filtrado de remitentes bloquee mensajes entrantes de la lista de remitentes bloqueados por destinatario.

La agregación de lista segura puede ayudar a reducir los casos de falsos positivos generados por el filtrado contra correo electrónico no deseado que realiza Exchange. En el contexto de filtrado de correo electrónico no deseado, un *falso positivo* se produce cuando el filtro de correo no deseado identifica de forma incorrecta un mensaje legítimo como correo electrónico no deseado.

En las organizaciones que filtran cientos de miles de mensajes de Internet a diario, aun un porcentaje pequeño de falsos positivos significa que es posible que los usuarios no reciban muchos mensajes que se identificaron incorrectamente como correo no deseado y se colocaron en cuarentena o se eliminaron.

La agregación de lista segura es probablemente el método más efectivo para reducir los falsos positivos. En Outlook 2010 o versiones posteriores, los usuarios pueden crear *listas de remitentes seguros*. Las listas de remitentes seguros especifican una lista de nombres de dominio y direcciones de correo electrónico de las que el usuario de Outlook desea recibir mensajes. De manera predeterminada, las direcciones de correo electrónico de los contactos de Outlook y la lista de direcciones globales de Exchange se incluyen en esta lista. Además, Outlook agrega a la lista de remitentes seguros todos los contactos externos a los que el usuario envía correos.

**Contenido**

Information stored in the Outlook user's safelist collection

How Exchange uses the safelist collection

Hashing of safelist collection entries

Enabling safelist aggregation

## Información almacenada en la colección de listas seguras del usuario de Outlook

Una *recopilación de listas seguras* es la combinación de datos de la lista de remitentes seguros, la lista de destinatarios seguros, la lista de remitentes bloqueados y los contactos externos. Estos datos se almacenan en Outlook y en el buzón de Exchange.

Los siguientes tipos de información se almacenan en una recopilación de listas seguras del usuario de Outlook:

  - **Remitentes seguros y destinatarios seguros**    En el mensaje, el encabezado De indica un remitente. El campo Para del mensaje de correo electrónico indica un destinatario. Tanto los remitentes seguros como los destinatarios seguros se representan mediante direcciones SMTP completas, como masato@contoso.com. Los usuarios de Outlook pueden agregar remitentes y destinatarios a sus listas seguras.

  - **Remitentes bloqueados**   Al igual que hacen con los remitentes seguros, los usuarios pueden bloquear a los remitentes no deseados agregándolos a sus listas de remitentes bloqueados.

  - **Dominio seguro**   El dominio es la parte de una dirección SMTP que va detrás del símbolo @. Por ejemplo, contoso.com es el dominio de la dirección masato@contoso.com. Los usuarios de Outlook pueden agregar dominios remitentes a sus listas seguras.
    

    > [!IMPORTANT]
    > De manera predeterminada, Exchange no incluye los dominios durante la agregación de lista segura. Sin embargo, puede configurar la agregación de lista segura para que incluya datos de dominios seguros para los agentes contra el correo no deseado. Para obtener más información, consulte <A href="configure-content-filtering-to-use-safe-domain-data-exchange-2013-help.md">Configurar el filtrado de contenido para usar datos de dominio seguro</A>.



  - **Contactos externos**   En la agregación de listas seguras se pueden incluir dos tipos de contactos externos. El primer tipo de contacto externo incluye los contactos a los que los usuarios de Outlook han enviado correo. Esta clase de contacto se agrega a la lista de remitentes seguros únicamente si un usuario de Outlook selecciona la opción correspondiente en la configuración de correo electrónico no deseado de Outlook 2007.
    
    El segundo tipo de contacto externo incluye los contactos de Outlook de los usuarios. Los usuarios pueden agregar o importar estos contactos en Outlook. Esta clase de contacto se agrega a la lista de remitentes seguros únicamente si un usuario de Outlook selecciona la opción correspondiente en la configuración de filtro de correo electrónico no deseado de Outlook 2010 o Outlook 2007.

Volver al principio

## Cómo usa Exchange la colección de listas seguras

La colección de listas seguras se almacena en el servidor de buzones de correo del usuario. Un usuario puede tener hasta 1.024 entradas exclusivas en una colección de listas seguras. Exchange 2013 tiene un asistente de buzón de correo, llamado asistente de buzón de correo para opciones de correo electrónico no deseado, que supervisa los cambios en la colección de listas seguras para los buzones de correo. A continuación, replica esos cambios en Active Directory, donde la colección de listas seguras se almacena en cada objeto de usuario. Cuando la colección de listas seguras se almacena en el objeto de usuario en Active Directory, también se agrega a la funcionalidad contra correo electrónico no deseado de Exchange 2013 y se optimiza para minimizar el almacenamiento y la replicación. Exchange usa los datos de colección de listas seguras durante el filtrado de contenido. Si tiene un servidor de transporte perimetral suscrito en la red perimetral, el servicio Microsoft Exchange EdgeSync replica la colección de listas seguras en la instancia Active Directory Lightweight Directory Services (AD LDS) en el servidor de transporte perimetral.


> [!IMPORTANT]
> Aunque los datos de destinatarios seguros se almacenan en Outlook y se pueden agregar a la colección de listas seguras, la funcionalidad de filtrado de contenido no procesa los datos de destinatarios seguros.



Volver al principio

## Hash en las entradas de la colección de listas seguras

A las entradas de la colección de listas seguras se les aplica un algoritmo hash (SHA-256) unidireccional, antes de almacenarlas como conjuntos de matrices en tres atributos de objeto de usuario, **msExchSafeSenderHash**, **msExchSafeRecipientHash** y **msExchBlockedSendersHash**, como objeto binario de gran tamaño. Al aplicar el algoritmo hash a los datos, se crea una salida de longitud fija, que también es probable que sea única. Para cifrar las entradas de la colección de listas seguras mediante hash, se crea un hash de 4 bytes. Cuando se recibe un mensaje de Internet, Exchange aplica un algoritmo hash a la dirección del remitente y la compara con los algoritmos hash almacenados en nombre del usuario de Outlook al que se envió el mensaje. Si el hash del remitente coincide con el de los remitentes seguros, el mensaje se salta el filtro de contenido. Si el hash del remitente coincide con el de los remitentes bloqueados, el mensaje se bloquea.

El cifrado unidireccional mediante hash de las entradas de la recopilación de listas seguras realiza las siguientes funciones importantes:

  - **Reduce el espacio de almacenamiento y replicación**   La mayor parte de las veces, la aplicación de hash reduce el tamaño de los datos. Por tanto, para guardar y transmitir una versión cifrada mediante hash de una entrada de la recopilación de listas seguras hace falta menos espacio y el tiempo de replicación se reduce. Por ejemplo, un usuario que tiene 200 entradas en su colección de listas seguras crearía alrededor de 800 bytes de datos con hash almacenados y replicados en Active Directory.

  - **Genera colecciones de listas seguras que los usuarios malintencionados no pueden usar**   Dado que no es posible hacer ingeniería inversa de los valores con hash unidireccional y devolverlos a su dirección SMTP o dominio original, las colecciones de listas seguras no generan direcciones de correo electrónico que los usuarios malintencionados puedan usar y que puedan poner en peligro un servidor de Exchange.

Volver al principio

## Habilitación de la agregación de lista segura

La agregación de lista segura está habilitada de forma predeterminada en Exchange 2013. A diferencia de Exchange Server 2007, no es necesario ejecutar manualmente el cmdlet **Update-SafeList** para cifrar con hash y escribir los datos de la colección de listas seguras en Active Directory. En Exchange 2013, los datos de la colección de listas seguras se escriben en Active Directory mediante el asistente de buzón de correo para opciones de correo electrónico no deseado.

Para que los datos de la agregación de lista segura en Active Directory estén disponibles para servidores de transporte perimetral en la red perimetral, se debe instalar y configurar el servicio Microsoft Exchange EdgeSync a fin de que los datos de la agregación de lista segura se repliquen en AD LDS.

Aun así, puede ejecutar manualmente la agregación de lista segura activando el cmdlet **UpdateSafelist**. No obstante, debe tener en cuenta el tráfico de red y de replicación que posiblemente se genere cuando ejecuta este comando. Si ejecuta **Update-Safelist** en varios buzones de correo en los que las listas seguras se utilizan ampliamente, es posible que se genere una cantidad significativa de tráfico. Si ejecuta el comando en varios buzones, se recomienda que ejecute el comando durante el horario no comercial y de poca actividad.

El cmdlet **Update-SafeList** lee la colección de listas seguras del buzón del usuario, cifra mediante hash todas las entradas, ordena las entradas para facilitar la búsqueda y convierte el hash en un atributo binario. Por último, el cmdlet **Update-SafeList** compara el atributo binario que se creó con cualquier valor almacenado en el atributo. Si los dos valores son idénticos, el cmdlet **Update-SafeList** no actualiza el valor del atributo del usuario con los datos de la agregación de lista segura. Si los dos valores del atributo son diferentes, el cmdlet **Update-SafeList** actualiza el valor de la agregación de lista segura.

Volver al principio

