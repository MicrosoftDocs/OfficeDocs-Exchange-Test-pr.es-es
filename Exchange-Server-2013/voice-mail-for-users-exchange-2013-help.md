---
title: 'Correo de voz para usuarios: Exchange 2013 Help'
TOCTitle: Correo de voz para usuarios
ms:assetid: 48e1f43b-fb7e-4a52-a2cb-0fb5da6ca65f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997885(v=EXCHG.150)
ms:contentKeyID: 49895609
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Correo de voz para usuarios

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-19_

La mensajería unificada (MU) permite a los usuarios de una organización de Exchange recibir mensajes de correo electrónico y de voz en un buzón. La funcionalidad de mensajería unificada y las características de correo de voz aumentan considerablemente la productividad del usuario y posibilitan una mensajería más flexible dentro de la organización.

Al agregar un usuario a una organización, puede crear un buzón o conectar al usuario a un buzón existente. Después de crear el buzón para el usuario o de que éste se conecte a un buzón existente, puede habilitar el buzón para mensajería unificada de modo que el usuario utilice el sistema de correo de voz y las características incluidas en él. Después de habilitar al usuario para que use la mensajería unificada, todo el correo electrónico, el correo de voz y los mensajes de fax se entregarán al buzón del usuario. Microsoft Office Outlook 2007 y las versiones posteriores permiten que los usuarios tengan acceso a su correo electrónico, a los mensajes de voz, a los contactos personales o a la información del calendario a través de Outlook Web App, de un teléfono móvil habilitado para Microsoft ExchangeActiveSync o de un teléfono fijo o móvil.

**Contenido**

Propiedades de usuarios de correo de voz

Relación entre un usuario de correo de voz y otros componentes de mensajería unificada

Direcciones SIP y números de extensión

Usar el EAC para habilitar a un usuario para correo de voz y mensajería unificada

Usar el Shell para habilitar a un usuario para correo de voz y mensajería unificada

Deshabilitar la mensajería unificada para un usuario

## Propiedades de usuarios de correo de voz

Un usuario debe tener un buzón para que se le pueda habilitar para mensajería unificada. De forma predeterminada, los usuarios que tienen un buzón no están habilitados para mensajería unificada. Después de habilitar a los usuarios para mensajería unificada, podrá administrar, modificar y configurar las propiedades de mensajería unificada y las características de correo de voz para ellos. Para habilitar a un usuario para mensajería unificada, use el EAC o el Shell. Para obtener información más detallada, consulte [Habilitar a un usuario para el correo de voz](enable-a-user-for-voice-mail-exchange-2013-help.md). Para habilitar a varios usuarios para mensajería unificada, use el EAC o el cmdlet **Enable-UMMailbox** en el Shell de administración de Exchange.

## Relación entre un usuario de correo de voz y otros componentes de mensajería unificada

Cuando se habilita a un usuario para la mensajería unificada, éste debe asociarse o vincularse a una directiva de buzón de mensajería unificada existente y, asimismo, se le debe asignar un número de extensión. Para asociar a un usuario con una directiva de buzón de mensajería unificada, use el cmdlet **Enable-UMMailbox** o seleccione la directiva de buzón de mensajería unificada cuando habilite al usuario para mensajería unificada. De forma predeterminada, al crear un plan de marcado de mensajería unificada, se crea una directiva de buzón de mensajería unificada. Esta directiva se puede modificar o se puede crear otra directiva y vincularla al plan de marcado para determinar las características o la configuración que se aplicará a un usuario o grupo de usuarios.

Una directiva de buzón de MU contiene una configuración como, por ejemplo, la relativa a restricción de llamadas y directivas de NIP para un usuario. Cuando se crea una directiva de buzón de mensajería unificada, se debe asociar a un solo plan de marcado de mensajería unificada. Los servidores de buzones o de acceso de clientes podrán responder a las llamadas entrantes y proporcionar servicios de correo de voz para los usuarios habilitados para mensajería unificada que estén vinculados al plan de marcado de mensajería unificada. Después de habilitar al usuario para mensajería unificada, se le aplicará la configuración de una directiva de buzón de mensajería unificada.

## Direcciones SIP y números de extensión

Cuando se habilita un usuario para mensajería unificada, se debe definir al menos un número de extensión para que lo use la mensajería unificada al enviar correo de voz al buzón del usuario. Una vez habilitado el usuario para mensajería unificada, se pueden agregar números de extensión secundarios para el buzón del usuario, así como modificarlos o quitarlos al configurar la dirección proxy de mensajería unificada de Exchange (dirección EUM de proxy) en el buzón del usuario o al agregar o quitar extensiones adicionales o secundarias para el usuario en el EAC. Puede quitar el número de extensión principal en el EAC mediante la eliminación de las direcciones EUM del proxy, aunque se recomienda no hacerlo. Si se quita el número de extensión principal, las llamadas no se podrán reenviar correctamente al buzón del usuario.


> [!NOTE]
> No existe ningún límite en el número de extensiones secundarias que se pueden agregar a un usuario habilitado para mensajería unificada, aunque solo puede haber un número de extensión principal por usuario.



El buzón de un usuario habilitado para MU puede asociarse a un único plan de marcado de mensajería unificada. Al usuario habilitado para mensajería unificada se le puede asignar lo siguiente:

  - Un único número de extensión principal, una dirección del protocolo de inicio de sesión (SIP) o una dirección E.164 de un único plan de marcado.

  - Varios números de extensiones secundarias, direcciones SIP o direcciones E.164 de un único plan de marcado.

  - Varios números de extensiones principales, direcciones SIP o direcciones E.164 de dos planes de marcado independientes.


> [!NOTE]
> Cada número de extensión, dirección SIP o número E.164 debe ser único en un plan de marcado y los números de dígitos del plan de marcado se usarán para todos los usuarios que estén vinculados al plan de marcado.



Por ejemplo, un usuario habilitado para MU viaja frecuentemente de Nueva York a Tokio. El buzón del usuario está asociado al plan de marcado de Nueva York y tiene configurado un número de extensión único en dicho buzón. En el buzón del usuario para el plan de marcado de Tokio se configura un segundo número de extensión. Cuando las personas que llaman marcan un número de extensión y dejan un mensaje de voz para el usuario, el mensaje de voz se entrega al mismo buzón habilitado para MU.

Volver al principio

## Usar el EAC para habilitar a un usuario para correo de voz y mensajería unificada

Después de crear un buzón de Exchange para el usuario, configure los valores del buzón de mensajería unificada mediante la opción **Ver detalles** en **Mensajería unificada** en el EAC. Al habilitar a un usuario, se deben configurar varios valores:

1.  **Dirección SIP**   Esta es la dirección SIP para el usuario. Esta configuración aparece si el usuario que va a habilitar para mensajería unificada se asigna a una directiva de buzón de mensajería unificada vinculada a un plan de marcado URI de SIP. Estos planes de marcado se usan al integrar Office Communications Server 2007 R2 o Microsoft Lync Server. Cuando asigna el usuario a una directiva de buzón de correo de MU vinculada a un plan de marcado de E.164 o URI de SIP, también debe introducir un número de extensión para el usuario. El usuario utiliza el número de extensión principal para tener acceso a Outlook Voice Access.

2.  **Número de extensión**   Debe especificar manualmente el número de extensión para el usuario que va a habilitar para mensajería unificada.
    
    Deberá proporcionar un número de extensión válido para el usuario que deberá contener el mismo número de dígitos especificado en el plan de marcado. Solo se pueden especificar caracteres numéricos o dígitos del 1 al 20. Un número de extensión convencional tiene una longitud entre 3 y 7 caracteres, y se configura en el plan de marcado con el que la directiva de buzón de mensajería unificada se vincula y se asigna al usuario.

3.  **Configuración de PIN para el usuario:** 
    
      - **Generar PIN automáticamente**   Esta configuración permite generar un PIN de forma automática para el usuario habilitado para mensajería unificada para el acceso al correo de voz a través de Outlook Voice Access. Esta es la configuración predeterminada. Cuando hace clic en este botón, se genera automáticamente un PIN de acuerdo con las directivas de PIN configuradas en la directiva de buzón de correo de MU asignada al usuario. Se recomienda utilizar esta opción para aumentar la protección del PIN del usuario. El PIN se envía al usuario en el mensaje de bienvenida que este recibe después de su habilitación para MU. De manera predeterminada, tendrá que cambiar este PIN la primera vez que inicie sesión en el buzón de correo para obtener el correo de voz.
    
      - **Escriba un PIN**   Esta configuración permite especificar un PIN manualmente que el usuario usará para tener acceso al sistema de correo de voz.
        
        El PIN debe cumplir las opciones de la directiva de PIN configuradas en la directiva de buzón de mensajería unificada que esté asociada al usuario habilitado para mensajería unificada. Por ejemplo, si la directiva de buzón de correo de MU está configurada para aceptar solamente PIN que contengan siete o más dígitos, el PIN que introduzca en este cuadro debe tener al menos siete dígitos.
    
      - **Pedir que el usuario restablezca su PIN la primera vez que inicia sesión**   Esta configuración obliga al usuario a restablecer el PIN de correo de voz cuando tiene acceso al sistema de correo de voz desde un teléfono la primera vez que utiliza Outlook Voice Access. Se le solicitará que introduzca un PIN con el que esté familiarizado. Hacer que los usuarios con habilitación para MU cambien el PIN la primera vez que inician sesión es un procedimiento recomendado de seguridad que los ayuda a protegerse contra el acceso no autorizado a sus datos y su bandeja de entrada. Esta casilla está activada de forma predeterminada.

## Usar el Shell para habilitar a un usuario para correo de voz y mensajería unificada

En este ejemplo se habilita la mensajería unificada y el correo de voz en el buzón de correo de tonysmith@contoso.com, se configura la extensión y se establece manualmente el PIN del usuario y, a continuación, se asigna una directiva de buzón de mensajería unificada denominada `MyUMMailboxPolicy` al usuario.

    Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -PINExpired $true

En este ejemplo se habilita la mensajería unificada y el correo de voz en el buzón de tonysmith@contoso.com, se asigna al usuario a una directiva de buzón de mensajería unificada llamada `MyUMMailboxPolicy` y se establece el número de extensión, la dirección SIP y el PIN para el usuario de forma manual.

    Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -SIPResourceIdentifier "tonysmith@contoso.com" -PINExpired $true

## Deshabilitar la mensajería unificada para un usuario

Cuando deshabilita la mensajería unificada para un usuario, la cuenta del usuario puede seguir incluida si el autor de la llamada realiza una búsqueda en el directorio mediante un menú de operador automático de MU o mediante Outlook Voice Access. Los autores de la llamada pueden buscar a un usuario en el directorio, pero al intentar ponerse en contacto con el usuario, volverán al menú principal de mensajería unificada. Esto puede hacer que los autores de las llamadas no se sientan satisfechos con el sistema. Puede evitar que los autores de las llamadas usen la búsqueda en directorios para ponerse en contacto con un usuario deshabilitado para la mensajería unificada. Para ello, conecte al usuario con otro sistema de correo de voz, elimínelo de la búsqueda en el directorio del operador automático de MU o elimine la cuenta del usuario.

Una vez que se ha deshabilitado una cuenta de usuario habilitado para MU, el usuario todavía puede tener acceso a su buzón individual con mensajería unificada habilitada mediante Outlook Voice Access o Outlook. Esto puede ocurrir cuando todos los cambios no son coherentes en el directorio. Para reducir el riesgo de que un usuario obtenga acceso al buzón, aunque la cuenta se haya deshabilitado para mensajería unificada, puede forzar manualmente la ocurrencia de la replicación o quitar toda la información de mensajería unificada del buzón del usuario cuando este se deshabilita para mensajería unificada.

