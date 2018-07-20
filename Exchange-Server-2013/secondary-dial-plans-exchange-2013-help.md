---
title: 'Planes de marcado secundario: Exchange 2013 Help'
TOCTitle: Planes de marcado secundario
ms:assetid: ecf474c2-042d-4aaf-9f5b-d5138c56ef39
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ff629383(v=EXCHG.150)
ms:contentKeyID: 54914908
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Planes de marcado secundario

 

_**Se aplica a:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2015-03-09_

Cuando se habilita un usuario para la mensajería unificada (UM), se le debe asignar un número de extensión y una directiva de buzón de mensajería unificada que lo vinculará a un plan de marcado de mensajería unificada. Después de que se haya habilitado el usuario para la mensajería unificada, podrá asignarle números de extensión adicionales dentro del mismo plan de marcado, pero los números de extensión dentro del plan deben ser únicos. En algunas implantaciones, puede que un usuario necesite que se le asigne el mismo número de extensión en dos planes de marcado distintos. En este caso, puede vincular el usuario a un plan de marcado de mensajería unificada secundario. Esto puede resultar útil, por ejemplo, si el usuario tiene dos teléfonos fijos o se traslada a distintas ubicaciones.

**Contenido**

Información general

Use of secondary extensions

UM features that operate differently for secondary dial plans

## Introducción

Cuando se habilita un usuario para la mensajería unificada, se debe definir un número de extensión y una directiva de buzón de mensajería unificada que vincule al usuario a un plan de marcado de mensajería unificada único. Cuando se habilita el usuario para mensajería unificada y está vinculado a una directiva de buzón de mensajería unificada que está vinculada a un plan de marcado URI SIP o E.164, también se debe proporcionar una dirección SIP o un número E.164, junto con el número de extensión del usuario. La mensajería unificada utiliza el plan de marcado y la extensión, junto con la dirección SIP o el número E.164, para localizar al usuario cuando se envía un mensaje de correo de voz a su buzón.

Si utiliza planes de marcado de extensión de teléfono y necesita proporcionar el mismo número de extensión para un usuario, deberá crear un plan de marcado secundario, habilitar al usuario para mensajería unificada y proporcionar el mismo número de extensión para el usuario. Esto se debe a que el número de extensión debe ser único dentro de un plan de marcado.


> [!NOTE]
> No existe límite para los números de extensión secundarios que pueden agregarse a un usuario habilitado para la mensajería unificada.



Pueden surgir ocasiones en las que un usuario se traslade de un lugar a otro, tenga dos o más teléfonos o desee recibir correo de voz en un número de extensión de marcado interno directo (DID) y recibir faxes en un número de extensión DID diferente. Para ello, se debe agregar una extensión DID adicional al buzón del usuario y, en algunos casos, agregar un plan de marcado secundario.

En algunas configuraciones, después de agregar una segunda extensión en el plan de marcado principal o agregar uno o múltiples números de extensión a un plan de marcado secundario, el usuario puede recibir mensajes de voz o faxes usando uno o más números de la extensión. Si desea que la mensajería unificada responda estas llamadas de fax y las envíe al segundo número de extensión DID, debe configurar el equipo de telefonía de su organización para que reenvíe las llamadas de fax al segundo número de extensión DID.

Al buzón de un usuario habilitado para la mensajería unificada puede asignársele lo siguiente:

  - Un único número de extensión, una dirección del Protocolo de inicio de sesión (SIP) o una dirección E.164 de un único plan de marcado

  - Números de extensión múltiples en un único plan de marcado

  - Números de extensión múltiples en dos planes de marcado independientes

Cuando se habilita un usuario para mensajería unificada, se debe especificar un número de extensión y una directiva de buzón de mensajería unificada. La mensajería unificada requiere que el número de extensión identifique al usuario cuando inicia sesión en Outlook Voice Access para recuperar mensajes. La directiva de buzón de mensajería unificada contiene una colección de propiedades de configuración con valores que la mensajería unificada aplica a cualquier usuario habilitado para la mensajería unificada de esta directiva. La directiva de buzón de mensajería unificada es similar a la "clase de servicio" en otros sistemas (por ejemplo, correo de voz o PBX), con respecto a que un cambio en el valor de la directiva de buzón de mensajería unificada puede afectar el comportamiento de una gran cantidad de usuarios.

Una propiedad en una directiva de correo de mensajería unificada se refiere a un plan de marcado de mensajería unificada. Esto representa un conjunto de extensiones compatible con telefonía. Este conjunto cuenta con un plan de numeración en donde no se permiten números de extensiones duplicados.

Por lo tanto, el número de extensión del usuario es único dentro del plan de marcado de mensajería unificada en el que se habilitó la mensajería unificada. De hecho, el plan de marcado de mensajería unificada y el par de números de extensión deben ser únicos dentro de la organización. De esta manera, la mensajería unificada identifica de forma exclusiva a un usuario habilitado para mensajería unificada en una organización. Usar un plan de marcado secundario permite mantener el plan de marcado y el número de extensión único en una organización más fácilmente. Por ejemplo, suponga que una organización tiene dos planes de marcado de mensajería unificada: plan de marcado A y plan de marcado B. El número de extensión del usuario A en el plan de marcado A es 55555 y en el plan de marcado B es 66666. Al usar un plan de marcado secundario, la extensión del usuario para el plan de marcado A puede ser 55555 y la extensión en el plan de marcado B también puede ser 55555. En ambos casos, la extensión del usuario en el plan de marcado que se usa es única.

En la siguiente tabla, se definen los términos usados al analizar las extensiones principal y secundaria, los números de Outlook Voice Access y los planes de marcado de mensajería unificada.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Término</th>
<th>Definición</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>extensión principal</p></td>
<td><p>El número de extensión específico si el usuario está habilitado para la mensajería unificada.</p></td>
</tr>
<tr class="even">
<td><p>plan de marcado principal</p></td>
<td><p>El plan de marcado de mensajería unificada específico si el usuario está habilitado para la mensajería unificada. El usuario habilitado para la mensajería unificada está asociado con el plan de marcado si el usuario está vinculado a un buzón de mensajería unificada.</p></td>
</tr>
<tr class="odd">
<td><p>número principal de Outlook Voice Access</p></td>
<td><p>El número de Outlook Voice Access para el plan de marcado principal del usuario. Las llamadas del usuario se reenvían a este número si no hay respuesta o si la línea está ocupada. Además, es el número al que el usuario llama cuando desea iniciar sesión en Outlook Voice Access.</p></td>
</tr>
<tr class="even">
<td><p>extensión secundaria</p></td>
<td><p>Uno o más números de extensión que pueden agregarse a la configuración de un usuario habilitada para la mensajería unificada.</p></td>
</tr>
<tr class="odd">
<td><p>plan de marcado secundario</p></td>
<td><p>Plan de marcado de mensajería unificada diferente del plan de marcado principal en el que se pueden configurar una o más extensiones secundarias.</p></td>
</tr>
<tr class="even">
<td><p>número secundario de Outlook Voice Access</p></td>
<td><p>El número de Outlook Voice Access del plan de marcado secundario del usuario. Un usuario puede llamar a este número desde el número de extensión secundario si desea iniciar sesión en Outlook Voice Access.</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Uso de extensiones secundarias

En la mayoría de las implementaciones, se configura únicamente una extensión por usuario habilitado para la mensajería unificada. No obstante, existen implementaciones más avanzadas en las que deben agregarse extensiones secundarias para los usuarios.

Cuando Microsoft Lync Server se utiliza para Telefonía IP empresarial, la mensajería unificada puede proporcionar el sistema de correo de voz. No obstante, el plan de marcado de mensajería unificada usado para Telefonía IP empresarial debe ser un plan de marcado URI de SIP específico de configuraciones de mensajería unificada con Lync Server. En estas implementaciones, el extremo Unified Communications de Microsoft proporciona la extensión del usuario, por ejemplo Communicator de MicrosoftOffice que se ejecuta en el equipo del usuario; o bien, Communicator Phone Edition Office que se ejecuta en un dispositivo telefónico compatible con IP. De esta manera, en la mayoría de los casos, el plan de marcado principal del usuario debe ser el mismo que el plan de marcado URI de SIP utilizado con Lync Server. Sin embargo, si el usuario necesita más números de extensión, no se debe agregar otra extensión secundaria al plan de marcado principal. Se debe agregar un plan de marcado secundario y, luego, agregar una extensión secundaria o una dirección de proxy EUM al usuario habilitado para la mensajería unificada.

Para obtener más información sobre la adición, la eliminación o el cambio de extensiones consulte uno de los siguientes temas:

  - [Cambiar un número de extensión](change-an-extension-number-exchange-2013-help.md)

  - [Agregar un número de extensión](add-an-extension-number-exchange-2013-help.md)

  - [Quitar un número de extensión](remove-an-extension-number-exchange-2013-help.md)

Si necesita cambiar las direcciones SIP o los números E.164 para los usuarios habilitados para mensajería unificada, consulte:

  - [Agregar una dirección SIP](add-a-sip-address-exchange-2013-help.md)

  - [Cambiar una dirección SIP](change-a-sip-address-exchange-2013-help.md)

  - [Quitar una dirección SIP](remove-a-sip-address-exchange-2013-help.md)

  - [Agregar un número E.164](add-an-e-164-number-exchange-2013-help.md)

  - [Cambiar un número E.164](change-an-e-164-number-exchange-2013-help.md)

  - [Quitar un número E.164](remove-an-e-164-number-exchange-2013-help.md)

## Contestador automático

La mensajería unificada proporciona las siguientes opciones:

  - **Contestador automático**   Se produce cuando un usuario no responde el teléfono y la mensajería unificada atiende la llamada.

  - **Outlook Voice Access**   Usado por los usuarios cuando llaman al sistema de correo de voz para obtener acceso al buzón.

Con frecuencia, se usan dos configuraciones:

  - El usuario habilitado para la mensajería unificada tiene dos números de extensión (uno principal y otro secundario) en el plan de marcado principal. Estas extensiones corresponden a teléfonos diferentes en el escritorio del usuario y están conectados al mismo PBX. Estos números diferentes están disponibles para dos audiencias independientes. En esta configuración, la extensión principal es el número de trabajo "general" y la extensión secundaria es el número "específico por tarea", posiblemente una línea del departamento de soporte técnico o un número exclusivamente para fax.

  - Un usuario habilitado para mensajería unificada pasa un determinado período de tiempo, quizás tres de las cuatro semanas, en la oficina principal de la empresa y, el resto del tiempo, en otra oficina de las ubicaciones remotas de la empresa. Las dos oficinas tienen PBX diferentes, y los números de extensión son únicos para cada PBX. En este ejemplo, en la configuración del usuario se estableció una extensión principal en plan de marcado primerio en el PBX de la oficina central y una extensión secundaria en el plan de marcado secundario en el PBX de la otra oficina.

En cualquier configuración, los mensajes de voz o los mensajes de notificación de llamada generados por las llamadas sin responder a cualquiera de las extensiones se enviarán a la bandeja de entrada del usuario.

## Outlook Voice Access

Es posible que los usuarios habilitados para mensajería unificada puedan iniciar sesión en Outlook Voice Access desde cualquier extensión, principal o secundaria. Si bien esto es posible, quizá existan restricciones de arquitectura que no permitan el funcionamiento idéntico de todas las extensiones. Para iniciar sesión en Outlook Voice Access, los usuarios habilitados para mensajería unificada deben seguir los pasos siguientes:

1.  Llamar a un número de Outlook Voice Access.

2.  Asignar una clave al número de extensión si llaman desde otro número telefónico.

3.  Especificar el PIN si no están habilitados para Telefonía IP empresarial y llaman desde un teléfono de comunicaciones unificadas, Office Communicator o Lync Server.

**Escenarios de uso**

  - **Extensión única con Outlook Voice Access**   Si el usuario tiene una extensión principal única, siempre debe llamar al número de Outlook Voice Access correspondiente a su plan de marcado de mensajería unificada principal. Si llama desde su número de extensión, no se le solicitará introducir el número de extensión y se omitirá el paso 2 de los pasos anteriores.

  - **Dos extensiones en el plan de marcado principal con Outlook Voice Access**   Si el usuario únicamente tiene dos extensiones, principal y secundaria, y las dos extensiones se encuentran en el mismo plan de marcado de mensajería unificada, siempre debe llamar al número de Outlook Voice Access del plan de marcado. Si llama desde la extensión principal o secundaria, no se le solicitará introducir el número de extensión y se omitirá el paso 2 de los pasos anteriores. Las características de Outlook Voice Access funcionarán de la misma manera, independientemente de la extensión que se use para iniciar sesión.

  - **Extensiones en el plan de marcado principal y secundario con Outlook Voice Access**   Si el usuario únicamente tiene dos extensiones, principal y secundaria, y ambas extensiones se encuentran en planes de marcado de mensajería unificada diferentes (principal y secundario), debe llamar al número de Outlook Voice Access correspondiente a su plan de marcado. Desde la extensión principal, debe llamar al número de Outlook Voice Access del plan de marcado principal y, desde la extensión secundaria, debe llamar al número de Outlook Voice Access del plan de marcado secundario. De esta manera, no se le solicitará introducir el número de extensión y se omitirá el paso 2 de los pasos anteriores.
    
    Las características de Outlook Voice Access que no requieren al marcado externo (por ejemplo, "Llamar al remitente" o "Llamar a la oficina") funcionarán de la misma manera, independientemente de la extensión usada para iniciar sesión. No obstante, las características de Outlook Voice Access que sí requieren marcado externo no funcionarán como se espera cuando el usuario inicie sesión en el plan de marcado secundario, a menos que las reglas de marcado externo sean exactamente las mismas en ambos planes. Para que el comportamiento del marcado externo sea exactamente el mismo, debe asegurarse de que las siguientes propiedades estén idénticamente configuradas en los planes de marcado principales y secundarios.
    
      - Códigos de marcado (acceso troncal, nacional e internacional)
    
      - Códigos de marcado en el país o región
    
      - Reglas de marcado
    
      - Nombres del grupo de reglas de marcado

Un usuario habilitado para mensajería unificada está asociado con la directiva de buzón de mensajería unificada y esta directiva está vinculada con el plan de marcado principal del usuario. Se aplicará al usuario la configuración de la directiva de buzón de mensajería unificada que se asocia con el plan de marcado principal del usuario habilitado para la mensajería unificada. Si un usuario está asociado con un plan de marcado secundario con un número de extensión en el plan de marcado secundario, también se aplicará la configuración de la directiva de buzón de mensajería unificada que se asocia con el plan de marcado principal. En Outlook Voice Access, se aplica la misma configuración de la directiva de buzón de mensajería unificada que se asocia con el plan de marcado principal si el usuario llama al plan de marcado principal o a un plan de marcado secundario.

Las propiedades **AllowedInCountryOrRegionGroups** y **AllowedInternationalGroups** en la directiva de buzón de mensajería unificada contienen los nombres de grupos de reglas de marcado configurados en las propiedades **ConfiguredInCountryOrRegionGroups** y **ConfiguredInternationalGroups** de un plan de marcado de mensajería unificada. Si un usuario habilitado para mensajería unificada llama a Outlook Voice Access, las reglas de llamadas externas de la directiva de buzón de mensajería unificada que se asocien con el plan de marcado principal o secundario se aplicarán a las llamadas que el usuario realice, según si el usuario habilitado para mensajería unificada llamó al número de Outlook Voice Access del plan de marcado secundario o principal.

Por ejemplo, si el plan de marcado principal denominado \&quot;Plan de marcado 1 Contoso\&quot; tiene una regla de marcado denominada \&quot;EE.UU. y Canadá\&quot; en la propiedad **ConfiguredInCountryOrRegionGroups**, la directiva de buzón de mensajería unificada \&quot;Directiva de mensajería unificada 1 Contoso\&quot; también puede tener \&quot;EE.UU. y Canadá\&quot; en su propiedad **AllowedInCountryOrRegionGroups**. Si desea agregar una extensión secundaria en \&quot;Plan de marcado 2 Contoso\&quot; para un usuario en \&quot;Directiva de mensajería unificada 2 Contoso\&quot;, debe asegurarse de que la propiedad **ConfiguredInCountryOrRegionGroups** del \&quot;Plan de marcado 2 Contoso\&quot; también contenga una regla denominada \&quot;EE.UU. y Canadá\&quot;. De lo contrario, si el usuario inicia sesión en Outlook Voice Access desde la extensión secundaria, la mensajería unificada no podrá encontrar una regla en el plan de marcado secundario denominado \&quot;EE. UU. y Canadá\&quot;. En ese caso, la mensajería unificada únicamente permitirá que el usuario llame a los números permitidos a cualquier usuario del plan de marcado secundario, lo cual podría ser más restrictivo.

Volver al principio

## Características de mensajería unificada que funcionan de manera diferente para los planes de marcado secundarios

Existe un conjunto de funciones de mensajería unificada que usan los planes de marcado secundarios, pero es posible que no funcionen correctamente en determinadas situaciones. Es importante que comprenda de qué forma estas características pueden verse afectadas cuando configura que los usuarios habilitados para la mensajería unificada usen un plan de marcado secundario.

## Reproducir en teléfono

En Outlook Web App, Reproducir en teléfono usa la puerta de enlace VoIP asociada al plan de marcado principal del usuario para realizar una llamada externa. Aplica las reglas de marcado del plan de marcado principal y la directiva de buzón de mensajería unificada asociada con el buzón del usuario.

## Búsqueda en directorios (Outlook Voice Access)

Las siguientes son las reglas para la búsqueda en el directorio de un usuario que ha sido autenticado:

  - La posibilidad de buscar un usuario y dejarle un mensaje de voz o llamar a un usuario solo estará disponible si el usuario que realiza la búsqueda está habilitado para mensajería unificada y tiene una extensión principal en el mismo plan de marcado que el usuario al que llama. En ese caso, la búsqueda por nombre, alias y extensión principal encontrará al usuario. No obstante, la búsqueda mediante la extensión secundaria no encontrará al usuario.

  - Si el usuario que se busca está habilitado para la mensajería unificada y tiene una extensión secundaria en el plan de marcado al que se llama, la búsqueda por nombre, alias y extensión secundaria encontrará al usuario. No obstante, aunque se ofrezcan opciones como dejar un mensaje de voz o llamar al contacto, esta última no podrá llevarse a cabo. En este caso, la búsqueda por extensión principal no encontrará al usuario.

  - Para buscar un usuario y poder llamarlo o dejarle un mensaje de voz, el usuario habilitado para mensajería unificada debe usar Outlook Voice Access mediante el número de Outlook Voice Access de su plan de marcado principal y buscar por nombre, alias o extensión principal. Si llama al usuario que buscó usando el número de Outlook Voice Access del plan de marcado secundario, solo lo encontrará si la búsqueda se realiza por nombre, alias o extensión secundaria. Si se usa la extensión principal, la única opción que estará disponible es que el usuario deje un correo de voz.

## Búsqueda en directorios (Outlook Voice Access)

Las siguientes son las reglas para la búsqueda en el directorio de un usuario que no ha sido autenticado:

  - Se encuentra el usuario que se busca y estará disponible la opción de dejar un mensaje de voz o llamar al usuario únicamente si el usuario está habilitado para la mensajería unificada y si tiene una extensión principal en el plan de marcado al que se llama. En ese caso, la búsqueda por nombre, alias y extensión principal encontrará al usuario. No obstante, la búsqueda mediante la extensión secundaria no encontrará al usuario.

  - Si el usuario que se busca está habilitado para mensajería unificada, tiene una extensión secundaria en el plan de marcado al que se llama y está seleccionada la opción **Transferir y buscar** \> **Permitir a quienes llaman** \> **Dejar mensajes de voz sin que el teléfono de un usuario suene** en el plan de marcado al que se llama, entonces la búsqueda por nombre, alias y extensión secundaria encontrará al usuario. No obstante, estará disponible la opción de dejar un correo de voz, pero no se podrá llamar al usuario.

  - Para buscar un usuario y poder llamarlo o dejarle un mensaje de voz, la persona que llama debe llamar al número de Outlook Voice Access del plan de marcado principal del usuario y buscar por nombre, alias o extensión secundaria del usuario. Si se llama al número de Outlook Voice Access secundario, solo se encontrará al usuario si la opción **Permitir a los autores de llamadas buscar por nombre o por alias** está establecida en **En toda la organización**. Es este caso, sólo está disponible la opción de dejar un mensaje de voz.

## Llamar al remitente (Outlook Voice Access)

Cuando un usuario llama a Outlook Voice Access y elije la opción Llamar al remitente, puede enviar un mensaje de correo electrónico o un mensaje de correo de voz a un usuario habilitado para mensajería unificada. Las opciones disponibles dependen de si la persona que llama está asociada con el mismo plan de marcado que el remitente al que se llama. Las siguientes son las reglas para las llamadas a un usuario habilitado para mensajería unificada si la persona que llama marca el número de Outlook Voice Access y la persona que llama está autenticada:

  - **Mensajes de correo electrónico**   Si el remitente del mensaje de correo electrónico es un usuario habilitado para mensajería unificada, seleccionar la opción de llamar al remitente resultará en una llamada a la extensión principal del remitente que esté configurado en el plan de marcado principal del usuario. En caso de que la extensión principal del remitente esté en un plan de marcado diferente del de la persona que llama, la opción \&quot;Llamar al remitente\&quot; solo se proporcionará si un teléfono particular, móvil o de una empresa está configurado para el remitente y las reglas de marcado están configuradas para permitir la llamada.

  - **Mensajes de correo de voz**   Si la persona que llama es un usuario habilitado para mensajería unificada, mediante la opción de llamar al remitente siempre se llamará a la extensión que el remitente usa para dejar un mensaje de voz. Si esta extensión tiene un número de dígitos diferentes de los números del plan de marcado al que se llama, la opción de llamar al remitente no estará disponible, a menos que las reglas de marcado permitan realizar esta llamada. Por ejemplo:
    
      - La opción "Quienes llaman pueden ponerse en contacto con" estará disponible si el remitente usa una extensión en el plan de marcado usado para enviar el mensaje de voz.
    
      - La opción \&quot;Quienes llaman pueden ponerse en contacto con\&quot; estará habilitada si el remitente usa una extensión de un plan de marcado diferente del plan de marcado que se usa con Outlook Voice Access para enviar el mensaje de voz, y si ambos planes tienen la misma cantidad de dígitos. Una llamada se efectuará correctamente si la puerta de enlace VoIP y la infraestructura de PBX permiten la transferencia de llamadas.
    
      - La opción \&quot;Quienes llaman pueden ponerse en contacto con\&quot; no estará habilitada si el remitente usa una extensión de un plan de marcado diferente del plan de marcado que se usa con Outlook Voice Access para enviar el mensaje de voz, si los planes de marcado tienen una cantidad diferente de dígitos y si no hay reglas de llamada externa que coincidan con la extensión del remitente.

Volver al principio

