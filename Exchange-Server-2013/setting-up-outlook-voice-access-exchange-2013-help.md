---
title: 'Configuración de Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Configuración de Outlook Voice Access
ms:assetid: 5ce8c877-35f3-4e55-a65e-5ca469aeae99
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd298010(v=EXCHG.150)
ms:contentKeyID: 50556789
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuración de Outlook Voice Access

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2015-03-09_

Microsoft Outlook Voice Access permite a los usuarios habilitados para mensajería unificada (MU) de Exchange obtener acceso a sus buzones de correo mediante teléfonos analógicos, digitales o celulares.

Un usuario de Outlook Voice Access (también denominado un *suscriptor*), es un usuario en una organización, habilitado para la mensajería unificada. Los suscriptores usan Outlook Voice Access para obtener acceso a sus buzones de correo en su teléfono para recuperar su correo electrónico, sus mensajes de correo de voz, sus contactos personales e información de calendario.

**Contenido**

Introducción a Outlook Voice Access

Interfaces de Outlook Voice Access

Escenarios de Outlook Voice Access

Grupos de distribución y grupos de contacto

Elección de un idioma

Control de las características de Outlook Voice Access

## Introducción a Outlook Voice Access

En la mensajería unificada de Microsoft Exchange, un usuario habilitado para la mensajería unificada puede llamar a un número de teléfono interno o externo configurado en un plan de marcado de MU para obtener acceso a su buzón de correo y usar el sistema de menús de Outlook Voice Access. Gracias a este menú, dichos usuarios pueden leer su correo electrónico, escuchar los mensajes de voz, interactuar con su calendario de Outlook, tener acceso a sus contactos personales y realizar tareas tales como configurar su PIN de Outlook Voice Access y grabar saludos de correo de voz.

Hay dos tipos de usuarios que pueden llamar a un número de Outlook Voice Access: los usuarios autenticados y los no autenticados. Cuando un usuario no autenticado llama a un número de Outlook Voice Access establecido en un plan de marcado de MU, solo puede hacer búsquedas en directorios para usuarios. Los usuarios autenticados, aquellos que indican su PIN, pueden hacer búsquedas en directorios e iniciar sesión en su buzón para escuchar el correo electrónico, los elementos de calendario y el correo de voz, así como para buscar contactos personales. Cuando buscan a un usuario en el directorio o en los contactos personales y lo encuentran, pueden transferir las llamadas a un usuario o llamar a la extensión del usuario.

## Interfaces de Outlook Voice Access

Existen dos interfaces de usuario de mensajería unificada disponibles para los usuarios de Outlook Voice Access: la interfaz de usuario de teléfono (TUI) y la interfaz de usuario de voz (VUI) que usa el reconocimiento de voz automático (ASR).

Antes de que los usuarios puedan usar la VUI en Outlook Voice Access, esta debe estar habilitada en el plan de marcado de la MU, en la directiva de buzón de correo de MU y para el usuario. De manera predeterminada, cuando crea un plan de marcado y una directiva de buzón de correo de MU y habilita el correo de voz para el usuario, este puede usar el ASR o la VUI de Outlook Voice Access para navegar en los menús, los mensajes y otras opciones. Sin embargo, incluso si el usuario puede usar la VUI, deberá usar el teclado numérico del teléfono para especificar su PIN, navegar por las opciones personales y realizar una búsqueda de directorio. En la tabla siguiente, se muestra la configuración predeterminada.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Componente de mensajería unificada</th>
<th>Valor predeterminado</th>
<th>Ejemplo de Shell de administración de Exchange para habilitar el acceso de VUI</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Plan de marcado de mensajería unificada</p></td>
<td><p>Habilitado</p></td>
<td><p><code>Set-UMDialPlan -id MyUMDialPlan -AutomaticSpeechRecognitionEnabled  $true</code></p></td>
</tr>
<tr class="even">
<td><p>Directiva de buzón de mensajería unificada</p></td>
<td><p>Habilitado</p></td>
<td><p><code>Set-UMMaiboxPolicy -id MyUMPolicy -AllowAutomaticSpeechRecognition  $true</code></p></td>
</tr>
<tr class="odd">
<td><p>Buzón de usuario</p></td>
<td><p>Habilitado</p></td>
<td><p><code>Set-UMMailbox -id tonysmith -AutomaticSpeechRecognitionEnabled $true</code></p></td>
</tr>
</tbody>
</table>


En la siguiente sección, se incluyen escenarios que describen la funcionalidad de VUI.

Introducción a Outlook Voice Access

## Escenarios de Outlook Voice Access

A continuación, se muestran ejemplos de cómo se puede usar Outlook Voice Access desde un teléfono:

  - **Acceso al correo electrónico**   Un usuario de Outlook Voice Access realiza una llamada a un número de Outlook Voice Access desde un número de teléfono y desea obtener acceso a su correo electrónico. El mensaje de voz dice: "Bienvenido. Se ha conectado a Microsoft Exchange. Para obtener acceso a su buzón de correo, especifique su extensión. Para ponerse en contacto con otra persona, presione la tecla almohadilla." Una vez que el usuario escriba su número de extensión de buzón de correo, el mensaje de voz dirá: "Introduzca su PIN y presione la tecla almohadilla." Una vez que el usuario escriba un PIN, el mensaje de voz dirá: "Tiene dos correos de voz nuevos, diez mensajes de correo electrónico nuevos y su próxima reunión es a las 10:00 a. m. Diga correo de voz, correo electrónico, calendario, contactos personales, directorio u opciones personales." Cuando el usuario diga "Correo electrónico", el sistema de correo de voz leerá el encabezado del mensaje y, a continuación, el nombre, el tema, la hora y la prioridad de los mensajes del buzón de correo del usuario.

  - **Acceso al calendario**   Un usuario de Outlook Voice Access realiza una llamada a un número de Outlook Voice Access desde un número de teléfono y desea obtener acceso a su calendario. El mensaje de voz dice: "Bienvenido. Se ha conectado a Microsoft Exchange. Para obtener acceso a su buzón de correo, especifique su extensión. Para ponerse en contacto con otra persona, presione la tecla almohadilla." Una vez que el usuario escriba su número de extensión de buzón de correo, el mensaje de voz dirá: "Introduzca su PIN y presione la tecla almohadilla." Una vez que el usuario escriba un PIN, el mensaje de voz dirá: "Tiene dos correos de voz nuevos, diez mensajes de correo electrónico nuevos y su próxima reunión es a las 10:00 a. m. Diga correo de voz, correo electrónico, calendario, contactos personales, directorio u opciones personales." Cuando el usuario dice "calendario", el sistema de correo de voz dice "¿Qué día desea abrir?" El usuario dice: "El calendario de hoy." El sistema de correo de voz responde: "Abriendo el calendario de hoy." El sistema de correo de voz lee todas las citas del calendario de ese día para el usuario.
    

    > [!NOTE]
    > Si un servidor de buzones de correo que ejecuta el servicio de mensajería unificada de Microsoft Exchange encuentra un elemento de calendario dañado en el buzón de correo del usuario, no conseguirá leerlo, pero devolverá al autor de la llamada al menú principal de Outlook&nbsp;Voice Access y dejará de leer cualquier reunión adicional que pudiese estar programada para el resto del día.



  - **Acceso al correo de voz**   Un usuario de Outlook Voice Access realiza una llamada a un número de Outlook Voice Access desde un número de teléfono y desea obtener acceso a su correo de voz. El mensaje de voz dice: "Bienvenido. Se ha conectado a Microsoft Exchange. Para obtener acceso a su buzón de correo, especifique su extensión. Para ponerse en contacto con otra persona, presione la tecla almohadilla." Una vez que el usuario escriba su número de extensión de buzón de correo, el mensaje de voz dirá: "Introduzca su PIN y presione la tecla almohadilla." Una vez que el usuario escriba un PIN, el mensaje de voz dirá: "Tiene dos correos de voz nuevos, diez mensajes de correo electrónico nuevos y su próxima reunión es a las 10:00 a. m. Diga correo de voz, correo electrónico, calendario, contactos personales, directorio u opciones personales." Cuando el usuario diga "Correo de voz", el sistema de correo de voz leerá el encabezado del mensaje y, a continuación, el nombre, el tema, la hora y la prioridad de los mensajes de voz del buzón de correo del usuario.
    

    > [!NOTE]
    > Si está habilitado el reconocimiento de voz, los usuarios pueden tener acceso al buzón de correo habilitado para mensajería unificada mediante la entrada de voz. Los suscriptores también pueden usar el teclado, característica conocida como tono de marcado de frecuencia múltiple (DTMF), presionando 0. El reconocimiento de voz no está habilitado para introducción de PIN.



  - **Ubicar un usuario en el directorio**   Un usuario de Outlook Voice Access realiza una llamada a un número de Outlook Voice Access desde un teléfono y desea ubicar a una persona en el directorio deletreando su alias de correo electrónico. El mensaje de voz dice: "Bienvenido. Se ha conectado a Microsoft Exchange. Para ponerse en contacto con otra persona, presione la tecla almohadilla." El usuario presiona la tecla almohadilla y, luego, usa las entradas de teclado para deletrear la dirección SMTP de la persona.
    

    > [!NOTE]
    > La característica de búsqueda de directorio con un número de Outlook Voice Access no está habilitada para voz. Los usuarios pueden deletrear el nombre de la persona con la que desean ponerse en contacto mediante solamente entradas de teclado.

    

    > [!IMPORTANT]
    > En algunas empresas (sobre todo en Asia oriental), los teléfonos de las oficinas pueden no tener letras en las teclas. De esta manera, es casi imposible usar la característica de deletreo de nombres que usa la interfaz de teclado si no se conoce el funcionamiento de la asignación de claves. De manera predeterminada, la mensajería unificada usa la asignación de teclas E.161. Por ejemplo, 2=ABC, 3=DEF, 4=GHI, 5=JKL, 6=MNO, 7=PQRS, 8=TUV, 9=WXYZ.

    
    Al especificar la combinación de letras y números, por ejemplo Mike1092, los dígitos numéricos se asignan a sí mismos. Para escribir el alias de correo electrónico Mike1092 correctamente, el usuario debe presionar los números 64531092. Además, los caracteres que no se incluyan entre A-Z y 0-9 no tienen equivalente en las teclas del teléfono. Por lo tanto, dichos caracteres no deben escribirse. Por ejemplo, el alias de correo electrónico jim.wilson se escribiría 546945766. Aunque hay 10 caracteres, solamente se introducen 9, dado que no hay un dígito equivalente al punto (.).

Introducción a Outlook Voice Access

## Grupos de distribución y grupos de contacto

Los usuarios pueden usar Outlook Voice Access para enviar o reenviar un mensaje de voz, un mensaje de correo electrónico o una convocatoria de reunión. Pueden enviar o reenviar el mensaje o la convocatoria de reunión a:

  - Una persona de su carpeta de contactos personales

  - Una persona de la libreta de direcciones compartida de la organización

  - Un grupo de contacto que han creado en su carpeta de contactos

  - Un grupo de distribución incluido en la libreta de direcciones compartida de la organización

Pueden enviar mensajes y convocatorias de reunión mediante la VUI (si se activó el ASR) o las entradas de su teclado telefónico. También pueden usar Outlook Voice Access para escuchar los detalles sobre un grupo, incluidos los miembros del grupo.


> [!NOTE]
> Si un usuario intenta enviar un mensaje a un grupo (ya sea un grupo de distribución en su libreta de direcciones compartida o un grupo de contactos en la carpeta de contactos personales) que no incluye ningún miembro, el sistema de correo de voz no le dará la opción de enviar o reenviar el mensaje o la convocatoria de reunión. Si intenta agregar un grupo sin miembros como uno de los destinatarios del mensaje o la convocatoria de reunión que está creando por teléfono, el sistema de correo de voz no agregará el grupo al mensaje, y dirá "El mensaje no se pudo enviar porque el contacto no parece tener una dirección de correo electrónico válida."



## Elección de un idioma

Los usuarios no pueden cambiar el idioma que Outlook Voice Access usa para hablarles y que ellos usan para responderle. El sistema de correo de voz intenta encontrar y usar la mejor coincidencia para el idioma que el usuario escogió cuando inició sesión en MicrosoftOutlook Web App, o el idioma que escogió en la configuración regional en Outlook Web App. Si el idioma que eligió no es compatible con Outlook Voice Access, el sistema de correo de voz usará el mismo idioma que oyen los autores de llamadas cuando se les solicita que dejen un mensaje de voz.

Introducción a Outlook Voice Access

## Control de las características de Outlook Voice Access

De manera predeterminada, cuando los usuarios marcan en Outlook Voice Access, pueden usar el teléfono para obtener acceso al calendario, el correo electrónico y los contactos personales, y realizar búsquedas en el directorio. Puede usar el Shell para evitar que los usuarios obtengan acceso a una o más de estas características cuando usen Outlook Voice Access para obtener acceso a su buzón de correo. Cuando modifique las características de Outlook Voice Access en una directiva de buzón de MU, los cambios afectarán a todos los usuarios asociados a la directiva de buzón de MU. También puede deshabilitar algunas de las características en un solo buzón de correo de usuario, aunque otras solo pueden deshabilitarse en una directiva de buzón de MU y no están disponibles en un buzón de correo individual.


> [!NOTE]
> Solamente puede usar el Shell para modificar la configuración de TUI de Outlook&nbsp;Voice Access para buzones habilitados para MU o directivas de buzones de correo de MU.



**Configuración de la directiva de buzón de MU**   Puede deshabilitar el acceso de los usuarios a las siguientes características de Outlook Voice Access en una directiva de buzón de MU:

  - Reconocimiento automático de voz

  - Acceso sin PIN al correo de voz

  - Respuestas de voz a otros mensajes

  - Acceso a su calendario mediante TUI

  - Acceso al directorio mediante TUI

  - Acceso a su correo electrónico mediante TUI

  - Acceso a sus contactos personales mediante TUI

**Configuración de buzones habilitados para la MU**   Puede deshabilitar el acceso de los usuarios a las siguientes características de Outlook Voice Access en el buzón de correo de un usuario:

  - Acceso al calendario mediante la TUI

  - Acceso de la TUI al correo electrónico

  - Reconocimiento automático de voz

Puede impedir que los usuarios reciban correo de voz, pero puede permitirles el acceso a su buzón de correo mediante Outlook Voice Access. También puede habilitar un usuario para la MU y configurar su buzón de correo de usuario con un número de extensión que no esté usando actualmente otro usuario de la organización.

Introducción a Outlook Voice Access

