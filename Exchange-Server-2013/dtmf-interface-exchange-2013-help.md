---
title: 'Interfaz DTMF: Exchange 2013 Help'
TOCTitle: Interfaz DTMF
ms:assetid: 2c7c9d8a-ed12-4dcf-a5b7-3cea0e785e49
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa996919(v=EXCHG.150)
ms:contentKeyID: 54652406
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Interfaz DTMF

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2016-12-09_

En la mensajería unificada (UM), los llamadores pueden usar tonos de marcación multifrecuencia (DTMF), también denominados tonos multifrecuencia, y entradas de voz para interactuar con el sistema. El método que pueden usar depende de cómo estén configurados los planes de marcado de mensajería unificada y los operadores automáticos.

La interfaz DTMF permite usar el teclado telefónico para buscar usuarios y desplazarse por el sistema de menús de mensajería unificada cuando se llama a un número de acceso de suscriptor configurado en un plan de marcado o a un número de teléfono configurado en un operador automático. En este tema, se describe la interfaz DTMF y cómo la usan los llamadores para buscar usuarios y desplazarse por el sistema de menús de correo de voz de UM.

**Contenido**

Introducción a DTMF

Planes de marcado de mensajería unificada y marcado por nombre

Mapas DTMF

Mapas DTMF para los usuarios que no están habilitados para Mensajería unificada

Mapas DTMF para los usuarios que están habilitados para Mensajería unificada

Más información

## Introducción a DTMF

DTMF requiere que el llamador presione una tecla del teléfono que corresponda a una opción de menú de Mensajería unificada o que indique el nombre de un usuario con las letras de las teclas para escribir el nombre o el alias del usuario. Los llamadores pueden usar DTMF porque no se habilitó Reconocimiento de voz automático (ASR) o porque intentaron usar comandos de voz sin éxito. En cualquier caso, las entradas de DTMF se usan para desplazarse por menús y buscar usuarios.

De manera predeterminada, en Mensajería unificada las entradas de DTMF se usan en planes de marcado y son la interfaz predeterminada de llamador para los operadores automáticos de UM.

Los llamadores pueden usar entradas de DTMF para:

  - Acceso telefónico de plan de marcado usando Outlook Voice Access.

  - Búsquedas en directorios de plan de marcado y búsquedas para encontrar usuarios.

  - Operadores automáticos que no están habilitados para voz.

  - Los operadores automáticos habilitados para voz que tienen o no un operador automático de reserva DTMF configurado.

  - Operadores automáticos de reserva DTMF (no habilitados para voz).

## Planes de marcado de mensajería unificada y marcado por nombre

Cuando cree un plan de marcado de mensajería unificada, puede configurar el método de entrada primario y secundario que usarán los llamadores para encontrar nombres cuando buscan un usuario o quieren ponerse en contacto con él. Estas configuraciones están en la página **Configuración** del plan de marcado y se llaman **Forma primaria de buscar nombres** y **Forma secundaria de buscar nombres**. Las opciones siguientes están disponibles para las formas primaria y secundaria de búsqueda de nombres:

  - Apellidos Nombre

  - Nombre Apellidos

  - Dirección SMTP

Además, en la forma secundaria de buscar nombres también está disponible la opción **Ninguno**.

De forma predeterminada, **Apellido Nombre** se selecciona como forma primaria de buscar nombres y **Dirección SMTP** como forma secundaria. Por lo tanto, cuando un llamador marca un número de Outlook Voice Access configurado en el plan de marcado de UM, el mensaje de bienvenida del plan de marcado se reproduce y el operador dice algo parecido a "Bienvenido a Contoso Outlook Voice Access. Le indicará que para acceder al buzón de correo, debe especificar su extensión. Para ponerse en contacto con otra persona, presione la tecla almohadilla." Tras presionar la tecla \#, el sistema le pedirá que escriba el nombre de la persona a la que llama, empezando por el apellido, o que deletree el alias de correo y presione dos veces la tecla \#. En este escenario, según cómo esté configurado el plan de marcado, el sistema pide que indique el apellido y después el nombre del usuario (Apellidos Nombre) o que deletree su alias de correo, excepto el nombre de dominio. Por ejemplo, si el alias de correo del usuario es abermejo@contoso.com, debería indicar abermejo.

Si quiere cambiar esta configuración porque el valor predeterminado no cumple los requisitos, puede modificarla para permitir a los llamadores que indiquen primero el alias de correo del usuario, o bien el nombre seguido del apellido. En este caso, debe configurar **Forma primaria para buscar nombres** con la **Dirección SMTP** y **Forma secundaria para buscar nombres** con **Nombre Apellidos**. La configuración de los métodos de marcado por nombre también se aplicará a los operadores automáticos de mensajería unificada asociados al plan de marcado. Para que los llamadores puedan indicar el nombre del usuario con entradas de DTMF o las teclas del teléfono, debe haber en el directorio un mapa DTMF y valores para el usuario.

Para más información sobre cómo cambiar los métodos primario y secundario de marcado por nombre en un plan de marcado de UM, vea [Configurar el modo principal para los usuarios de Outlook Voice Access buscar](configure-the-primary-way-for-outlook-voice-access-users-to-search-exchange-2013-help.md) y [Configurar la forma secundaria para los usuarios de Outlook Voice Access buscar](configure-the-secondary-way-for-outlook-voice-access-users-to-search-exchange-2013-help.md).

Introducción a DTMF

## Mapas DTMF

En una organización de Exchange, se asocia un atributo denominado **msExchUMDtmfMap** con cada usuario que se crea en el directorio. Mensajería unificada usa este atributo para asignar el nombre, el apellido y el alias de correo del usuario a un conjunto de números. Esta asignación se conoce como mapa DTMF. Un mapa DTMF permite al llamador escribir los dígitos correspondientes a las letras del nombre o del alias de correo del usuario en el teclado del teléfono. Este atributo contiene los valores necesarios para crear un mapa DTMF para el nombre del usuario seguido de su apellido, para el apellido del usuario seguido del nombre y para el alias de correo del usuario.

En la tabla siguiente, se muestran los valores del mapa DTMF que se almacenan en Active Directory en el atributo **msExchUMDtmfMap** para un usuario habilitado para UM llamado Antonio Bermejo con el alias abermejo@contoso.com.

**Valores de DTMF almacenados para un usuario habilitado para UM llamado Antonio Bermejo**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Entrada del directorio</th>
<th>Nombre del usuario</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>firstNameLastName:866976484</p></li>
</ul></td>
<td><p>antoniobermejo</p></td>
</tr>
<tr class="even">
<td><ul>
<li><p>lastNameFirstName:764848669</p></li>
</ul></td>
<td><p>bermejoantonio</p></td>
</tr>
<tr class="odd">
<td><ul>
<li><p>emailAddress:876484</p></li>
</ul></td>
<td><p>abermejo</p></td>
</tr>
</tbody>
</table>


Los nombres y alias de correo pueden contener otros caracteres que no sean alfanuméricos, como comas, guiones, signos de subrayado o puntos. Estos caracteres no se usarán en un mapa DTMF para un usuario. Si, por ejemplo, el alias de correo de Antonio Bermejo es antonio-bermejo@contoso.com, el valor del mapa DTMF sería 866976484 y el guión no se incluiría. Sin embargo, si el alias de correo de un usuario contiene números, por ejemplo, antoniobermejo123@contoso.com, los números se usarían en el mapa DTMF que se crea. El mapa DTMF para antoniobermejo123 sería 866976484123.

Para que los llamadores puedan escribir el nombre o alias de correo de un usuario, tiene que existir un mapa DTMF para el usuario. Sin embargo, no todos los usuarios tendrán un mapa DTMF asociado a su cuenta de usuario.

Introducción a DTMF

## Mapas DTMF para los usuarios que no están habilitados para Mensajería unificada

Los usuarios, incluidos los habilitados para buzón de correo, no están habilitados para mensajería unificada de manera predeterminada. El atributo **msExchUMDtmfMap** se rellena con los valores necesarios para los mapas DTMF de usuarios que no se han habilitado para UM. De forma predeterminada, los siguientes mapas DTMF se crean para todos los usuarios cuando se les crea un buzón:

1.  emailAddress

2.  firstNameLastName

3.  lastNameFirstName

Si un usuario no tiene valores de mapa DTMF definidos en la cuenta, los llamadores no podrán contactar con el usuario cuando presionen una tecla del teléfono desde un operador automático de UM o cuando hagan una búsqueda en el directorio. Además, los usuarios habilitados para UM no podrán enviar mensajes ni transferir llamadas a usuarios que no tengan mapa DTMF a menos que puedan usar el Reconocimiento de voz automático (ASR). Para permitir a los llamadores transferir las llamadas o ponerse en contacto con usuarios no habilitados para UM usando el teclado del teléfono, hay que crear los valores necesarios para el mapa DTMF de los usuarios. Puede usar el cmdlet **Set-User** con el parámetro *-CreateDtmfMap* para crear y actualizar el mapa DTMF de un usuario o actualizar el mapa DTMF para un usuario si el nombre de este cambió después de que se creara un mapa DTMF. De manera opcional, puede crear un script del Shell de administración de Exchange usando este cmdlet para actualizar los valores de mapa DTMF para varios usuarios.

Para más información sobre el cmdlet **Set-User**, vea [Set-User](https://technet.microsoft.com/es-es/library/aa998221\(v=exchg.150\)).

Introducción a DTMF

## Mapas DTMF para los usuarios que están habilitados para Mensajería unificada

De manera predeterminada, se crea un mapa DTMF para los usuarios cuando se habilitan para mensajería unificada. Esto permite que se transfieran a un usuario habilitado para UM llamadas externas, llamadas de usuarios no habilitados para mensajería unificada y llamadas de otros usuarios habilitados para UM que usan el teclado del teléfono para escribir el nombre o el alias de correo del usuario.

Una vez creados los valores de mapa DTMF para un usuario habilitado para UM, los llamadores pueden usar la característica de búsqueda en directorio. usando el teclado del teléfono en las siguientes situaciones:

  - Para identificar o buscar a un usuario que llama a un número de Outlook Voice Access.

  - Para buscar o transferir llamadas a un usuario habilitado para UM que llama a un operador automático de mensajería unificada.

Para más información sobre cómo habilitar a un usuario para la mensajería unificada, vea [Habilitar a un usuario para el correo de voz](enable-a-user-for-voice-mail-exchange-2013-help.md).

En ocasiones, el nombre, apellido o alias de correo de un usuario cambia cuando este se habilita para mensajería unificada. Los valores del mapa DTMF del usuario no se actualizan automáticamente. Si un llamador indica el nuevo apellido o alias de correo del usuario y el mapa DTMF de este no se actualizó para reflejar el cambio, el llamador no podrá encontrar al usuario en el directorio, enviarle un mensaje ni transferirle llamadas. Si tiene que actualizar el mapa DTMF de un usuario una vez habilitado para mensajería unificada, puede usar el cmdlet **Set-User** con el parámetro *-CreateDtmfMap*. Si quiere actualizar los mapas DTMF para varios usuarios habilitados para UM, también puede crear un script del Shell de administración de Exchange usando este cmdlet.


> [!WARNING]
> Le recomendamos que no cambie manualmente los valores de DTMF de los usuarios usando una herramienta como el Editor ADSI, ya que pueden resultar configuraciones no coherentes u otros errores. Recomendamos usar solo el cmdlet <STRONG>Set-UMService</STRONG> o el cmdlet <STRONG>Set-User</STRONG> para crear o actualizar mapas DTMF de usuarios.



## Más información

[Introducción a adsiedit](https://go.microsoft.com/fwlink/p/?linkid=73175)

