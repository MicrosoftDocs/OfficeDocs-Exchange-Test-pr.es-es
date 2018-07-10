---
title: 'Directivas de dirección de correo electrónico: Exchange 2013 Help'
TOCTitle: Directivas de dirección de correo electrónico
ms:assetid: b63b63bb-6faf-4337-8441-50bc64b49bb8
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb232171(v=EXCHG.150)
ms:contentKeyID: 49895857
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Directivas de dirección de correo electrónico

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-07-21_

En Active Directory, los destinatarios (incluidos los usuarios, recursos, contactos y grupos) son cualquier objeto habilitado para correo al que Microsoft Exchange puede entregar o enrutar mensajes. Para que un destinatario reciba o envíe mensajes de correo electrónico, debe disponer de una dirección de correo electrónico. Las directivas de direcciones de correo electrónico generan direcciones primarias y secundarias para sus destinatarios a fin de que puedan recibir y enviar mensajes de correo electrónico.

De manera predeterminada, Exchange contiene una directiva de direcciones de correo electrónico para cada usuario habilitado para correo electrónico. Esta directiva predeterminada especifica el alias del destinatario como la parte local de la dirección de correo electrónico y usa el dominio aceptado predeterminado. La parte local de una dirección de correo electrónico es el nombre que va delante del signo (@). Sin embargo, puede cambiar el modo en el que se muestran las direcciones de correo electrónico de sus destinatarios. Por ejemplo, puede especificar que las direcciones de correo electrónico de los destinatarios aparezcan como *nombre*.*apellido*@contoso.com.

Además, si desea especificar direcciones de correo electrónico adicionales para todos los destinatarios o para un subconjunto de ellos, puede modificar la directiva predeterminada o crear directivas adicionales. Por ejemplo, el buzón de usuario de David Hamilton puede recibir mensajes de correo electrónicos dirigidos a hdavid@mail.contoso.com y a hamilton.david@mail.contoso.com.

¿Está buscando tareas de administración relacionadas con las directivas de direcciones de correo electrónico? Consulte [Procedimientos de directivas de direcciones de correo electrónico](email-address-policy-procedures-exchange-2013-help.md).

## Comportamientos de las directivas de destinatarios

Exchange aplica una directiva a todos los destinatarios que coincidan con los criterios de filtrado de destinatarios:

  - Las directivas de destinatarios se aplican en orden, desde la prioridad más alta a la prioridad más baja. En caso de conflicto entre dos o más directivas, se aplicará la directiva con la prioridad más alta. La directiva de destinatario predeterminada tiene siempre la prioridad más baja y se aplicará si no coinciden otras directivas.
    
    Cuando se crea una directiva de destinatario, pero no se especifica explícitamente una prioridad, se agrega con la prioridad más alta. Si especifica una prioridad que ya está asociada con una directiva existente, la directiva existente y todas las directivas de menor prioridad se mueven un lugar hacia abajo. La nueva directiva se inserta con la prioridad especificada.
    
    La funcionalidad de directivas de destinatario se divide en dos características: dominios aceptados y directivas de direcciones de correo electrónico. Para obtener más información acerca de los dominios aceptados, consulte [Dominios aceptados](accepted-domains-exchange-2013-help.md).

  - Al ejecutar el cmdlet **Update-EmailAddressPolicy** en el Shell de administración de Exchange, el objeto destinatario se actualiza con la directiva de direcciones de correo electrónico.

  - Cada vez que se modifica un objeto destinatario y se guarda, Exchange impone la aplicación correcta de las configuraciones y criterios de la dirección de correo electrónico. Cuando se modifica y se guarda una directiva de dirección de correo electrónico, todos los destinatarios asociados se actualizan con el cambio. Además, si se modifica un objeto destinatario, la pertenencia a la directiva de dirección de correo electrónico de dicho destinatario se reevalúa y se exige.

## Crear directivas de dirección de correo electrónico

Al crear una política de direcciones de correo electrónico, puede usar los siguientes tipos de direcciones:

  - **Dirección de correo electrónico SMTP predefinida**. Las direcciones de correo electrónico SMTP *predefinida* son los tipos de direcciones de correo electrónico usadas habitualmente y que se le proporcionan.

  - **Dirección de correo electrónico SMTP personalizada**. Si no desea usar una de las direcciones de correo electrónico SMTP predefinidas, puede especificar una dirección de correo electrónico SMTP personalizada.
    
    Al crear una dirección de correo electrónico SMTP personalizada, puede usar las variables de la tabla que aparecen a continuación para especificar valores alternativos para la parte local de la dirección de correo electrónico.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Variable</th>
    <th>Valor</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>%g</p></td>
    <td><p>Nombre (nombre de pila)</p></td>
    </tr>
    <tr class="even">
    <td><p>%i</p></td>
    <td><p>Inicial del segundo nombre</p></td>
    </tr>
    <tr class="odd">
    <td><p>%s</p></td>
    <td><p>Apellido</p></td>
    </tr>
    <tr class="even">
    <td><p>%d</p></td>
    <td><p>Nombre para mostrar</p></td>
    </tr>
    <tr class="odd">
    <td><p>%m</p></td>
    <td><p>Alias de Exchange</p></td>
    </tr>
    <tr class="even">
    <td><p>%<em>x</em>s</p></td>
    <td><p>Utiliza las primeras <em>x</em> letras del apellido. Por ejemplo, si <em>x</em>=2, se utilizan las dos primeras letras del apellido.</p></td>
    </tr>
    <tr class="odd">
    <td><p>%<em>x</em>g</p></td>
    <td><p>Utiliza las primeras <em>x</em> letras del nombre de pila. Por ejemplo, si <em>x</em>=2, se utilizan las dos primeras letras del nombre.</p></td>
    </tr>
    </tbody>
    </table>


  - **Dirección de correo electrónico no SMTP**. Pueden utilizarse los siguientes tipos de direcciones de correo electrónico no SMTP:
    
      - EX (Parámetro DisplayName del prefijo de la dirección proxy de DN heredado)
    
      - X.500
    
      - X.400
    
      - MSMail
    
      - CcMail
    
      - Lotus Notes
    
      - Novell GroupWise
    
      - Dirección proxy de mensajería unificada de Exchange (dirección proxy EUM)
    

    > [!IMPORTANT]
    > En Exchange, todas las direcciones de correo electrónico no SMTP se consideran direcciones personalizadas. Exchange no proporciona cuadros de diálogo exclusivos ni páginas de propiedades para los tipos de direcciones de correo electrónico de X.400, GroupWise o Lotus Notes. Si agrega una dirección de correo electrónico personalizada no SMTP, debe tener los archivos de biblioteca de vínculos dinámicos (DLL) adecuados. Si no proporciona los archivos DLL apropiados, no podrá crear una directiva de direcciones de correo electrónico personalizadas. Se registrará el siguiente error en el Visor de eventos: "Falta el objeto de descripción de direcciones de correo electrónico del directorio de Microsoft Exchange para el tipo de dirección 'SADF' en equipos 'i386'."



Para obtener instrucciones detalladas para crear políticas de direcciones de correo electrónico, consulte los siguientes temas:

[Crear una directiva de dirección de correo electrónico](create-an-email-address-policy-exchange-2013-help.md)

[Crear una directiva de la dirección de correo electrónico mediante filtros de destinatario](create-an-email-address-policy-by-using-recipient-filters-exchange-2013-help.md)

