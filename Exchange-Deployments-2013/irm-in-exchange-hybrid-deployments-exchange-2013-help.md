---
title: 'IRM en implementaciones híbridas de Exchange: Exchange 2013 Help'
TOCTitle: IRM en implementaciones híbridas de Exchange
ms:assetid: ba6ec48b-8f79-4807-b74b-fd442bbbe82f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ659052(v=EXCHG.150)
ms:contentKeyID: 49895006
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# IRM en implementaciones híbridas de Exchange

 

_<strong>Se aplica a:</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>Última modificación del tema:</strong>2016-12-09_

**Resumen:** cómo funciona IRM en un entorno de Exchange híbrido y cómo configurar IRM para que funcione entre Exchange Online y sus servidores de Exchange locales.

Information Rights Management (IRM) le ayuda a evitar fugas de información confidencial, ya que proporciona una protección en línea y sin conexión persistente de mensajes y datos adjuntos de correo electrónico. Tanto Exchange en la organización local como Exchange Online en Office 365 para empresas admiten IRM. Sin embargo, existen diferencias entre las dos implementaciones. Por lo tanto, debe configurar IRM en la organización de Exchange Online para que los usuarios de dicha organización puedan usarlo.

IRM usa Active Directory Rights Management Services (AD RMS), que es un componente de Windows Server 2008 y posterior. AD RMS permite que los usuarios creen contenidos protegidos por derechos, como mensajes de correo electrónico y documentos adjuntos y luego controlar cómo se usa ese contenido y a quién puede distribuirse. Los usuarios pueden especificar plantillas que determinen cómo puede usarse el contenido. Por ejemplo, un usuario puede especificar que un mensaje de correo electrónico no puede reenviarse a otros destinatarios o que no puede copiarse la información del mensaje.

Obtenga más información sobre IRM en Exchange 2010 en: [Comprender Information Rights Management](https://technet.microsoft.com/es-es/library/dd638140\(v=exchg.141\).aspx).

Obtenga más información sobre IRM en Exchange 2013 y Exchange 2016 en [Information Rights Management](https://technet.microsoft.com/es-es/library/dd638140\(v=exchg.150\)).

Para obtener más información acerca de AD RMS, vea [Información general de Active Directory Rights Management Services](http://go.microsoft.com/fwlink/p/?linkid=215243).

## Diferencias entre IRM en Exchange local y Exchange Online

La funcionalidad de IRM que está disponible en la organización de Exchange local es diferente de la funcionalidad disponible en la organización de Exchange Online. La siguiente tabla proporciona un resumen de las características y de las funcionalidades disponibles en cada organización. (Más información sobre estas características en: [Information Rights Management](https://technet.microsoft.com/es-es/library/dd638140\(v=exchg.150\))).

### Características de IRM disponibles

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Característica</th>
<th>Disponible en Exchange 2007 y versiones anteriores</th>
<th>Disponible en Exchange 2010</th>
<th>Disponible en Exchange Online y en Exchange 2013 y versiones posteriores</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Protección manual de mensajes en Outlook</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p>Protección manual de mensajes en Outlook Web App</p></td>
<td><p>No</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p>Ver mensajes protegidos por IRM en Outlook</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p>Ver mensajes protegidos por IRM en Outlook Web App</p></td>
<td><p>No</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p>Agente de licencia previa de IRM</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p>Plantillas de la directiva de RMS</p></td>
<td><p>No</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p>Descifrado de transporte</p></td>
<td><p>No</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p>Descifrado de informe de diario</p></td>
<td><p>No</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p>Descifrado de detección y búsqueda de Exchange</p></td>
<td><p>No</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p>Reglas de protección automática de Outlook</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p>Reglas de protección automática de transporte</p></td>
<td><p>No</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
</tr>
</tbody>
</table>


## IRM en implementaciones híbridas

Exchange usa servidores de AD RMS en el bosque de Active Directory en donde está instalado el servidor de Exchange. Para los servidores locales de Exchange, se usa el servidor de AD RMS. En la organización de Exchange Online se usan servidores de AD RMS que se encuentran dentro de los centros de datos de Office 365. La configuración de AD RMS que usa cada organización de Exchange es independiente de cualquier otra implementación de AD RMS.

La configuración de AD RMS (y, en consecuencia, la configuración de IRM) no se replica automáticamente entre la organización de Exchange local y la organización de Exchange Online. Las plantillas de AD RMS que ha definido no se copian automáticamente en la organización de Exchange Online. Si desea que las mismas plantillas de AD RMS estén disponibles en la organización de Exchange Online, expórtelas manualmente desde la organización local y aplíquelas en la organización de Office 365. Vea Configurar IRM en implementaciones híbridas más adelante en este tema.

## Experiencia de usuario

La configuración de IRM que se aplica a un usuario depende del cliente que el usuario use y de la ubicación del buzón de correo del usuario. La siguiente tabla muestra el servidor de AD RMS que usará un usuario.

### Servidor de AD RMS activo

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Cliente</th>
<th>Buzón de correo local</th>
<th>Buzón de correo Exchange Online</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Clientes de escritorio de Outlook</p></td>
<td><p>AD RMS local</p></td>
<td><p>AD RMS local</p></td>
</tr>
<tr class="even">
<td><p>Outlook en la web</p></td>
<td><p>AD RMS local</p></td>
<td><p>AD RMS de Exchange Online</p></td>
</tr>
<tr class="odd">
<td><p>Dispositivo de ActiveSync</p></td>
<td><p>AD RMS local</p></td>
<td><p>AD RMS de Exchange Online</p></td>
</tr>
</tbody>
</table>


Dependiendo de la configuración de AD RMS que haya establecido en la organización local y en la de Exchange Online, es posible que un usuario que use Outlook 2007 y Outlook en la web pueda ver plantillas de AD RMS diferentes. Por esta razón, recomendamos que aplique las mismas plantillas tanto para la organización local como para la organización de Exchange Online.

No debería existir ningún tipo de diferencia en la experiencia de IRM para los usuarios del cliente de Outlook, independientemente de si su buzón de correo se encuentra ubicado en una organización local o en una organización de Exchange Online.

Un usuario de Outlook en la web cuyo buzón se encuentra ubicado en un servidor Exchange local, solo puede abrir mensajes protegidos por derechos después de instalar el complemento Rights Management para Internet Explorer. No podrá responder ni crear mensajes protegidos por derechos nuevos.

Un usuario de Outlook en la web cuyo buzón de correo se encuentra ubicado en Exchange Online puede abrir mensajes protegidos por derechos sin ningún software adicional y puede crear mensajes protegidos por derechos nuevos y responder a ellos.

## Funcionalidad del servidor

Los servidores locales de Exchange usan el agente de licencia previa de AD RMS para descifrar los mensajes protegidos por derechos para que los usuarios no tengan que presentar credenciales al abrir esos mensajes. El servidor local de Exchange se pone en contacto con el servidor local de AD RMS para comprobar los derechos y las directivas de uso y para solicitar autorización para descifrar el mensaje.

La organización de Exchange Online proporciona varias características adicionales relacionadas con IRM que usan AD RMS de Exchange Online. Estas características, como el descifrado de informe de diario, hacen que el contenido de los mensajes protegidos por derechos esté disponible para los servicios de Exchange para un procesamiento adicional. Por ejemplo, los contenidos descifrados de un mensaje de diario se pueden guardar, junto con el mensaje protegido por derechos original, para que la detección sea más sencilla. Además, las plantillas de IRM se pueden aplicar automáticamente a mensajes mediante el uso de reglas de protección o reglas de transporte de Outlook para garantizar que los mensajes cumplan con las directivas de la organización relacionadas con la protección de información.

## Configurar IRM en implementaciones híbridas

IRM en Exchange depende de la implementación de AD RMS en el bosque de Active Directory en donde se encuentra el servidor de Exchange. La configuración de AD RMS no se sincroniza automáticamente entre la organización local y la de Exchange Online. Debe exportar manualmente la configuración de AD RMS, conocida como un dominio de publicación de confianza (TPD), desde el servidor local de AD RMS, e importar esa configuración en la organización de Exchange Online. El dominio de publicación de confianza (TPD) contiene la configuración de AD RMS, incluidas las plantillas, que la organización de Exchange Online necesita para usar IRM.

Obtenga más información en [Consideraciones sobre el dominio de publicación de confianza de AD RMS](http://go.microsoft.com/fwlink/p/?linkid=215244).

Además de aplicar la configuración local de AD RMS en la organización de Exchange Online, debe asegurarse de que los clientes de Outlook y ActiveSync puedan conectar con los servidores de AD RMS fuera de la red local. Esto debe realizarse si desea que estos clientes tengan acceso a los mensajes protegidos por derechos fuera de la red local.

Después de configurar la red local y de exportar los datos de TPD, configure la organización de Exchange Online mediante la importación de los datos de TPD y la habilitación de IRM.


> [!NOTE]
> Cada vez que modifique la configuración local de AD&nbsp;RMS, aplique manualmente la configuración nueva en la organización de Exchange Online. Para ello, exporte los datos de TPD desde el servidor local de AD&nbsp;RMS e impórtelos en la organización de Exchange Online.



## Cómo configurar IRM en implementaciones híbridas de Exchange

Si usa IRM en su organización local de Exchange y desea que los usuarios basados en Exchange Online también usen IRM, haga lo siguiente:

1.  Configure el servidor local de Active Directory Rights Management Services (AD RMS).

2.  Habilite IRM en la organización de Exchange Online.

3.  Distribuya las plantillas importadas de AD RMS entre los usuarios de la organización de Exchange Online.

## ¿Cómo configuro los servidores locales AD RMS?

Para configurar IRM en una implementación híbrida, debe usar Windows PowerShell para obtener acceso al servidor local de AD RMS. Encontrará más información en: [Artículo sobre el uso de Windows PowerShell para administrar AD RMS](http://go.microsoft.com/fwlink/p/?linkid=214938)

Haga lo siguiente para exportar datos de dominio de publicación de confianza (TPD) desde su servidor local de AD RMS y, a continuación, configure el acceso al servidor de AD RMS para clientes externos.

1.  Exporte los datos TDP de la organización local. Encontrará más información en: [Artículo sobre la exportación de un dominio de publicación de confianza](http://go.microsoft.com/fwlink/p/?linkid=214942)

2.  Configure el acceso a los servidores AD RMS desde los clientes externos. Encontrará más información en: [Artículo sobre la adición de una dirección URL de clúster Extranet](http://go.microsoft.com/fwlink/p/?linkid=214945)

## ¿Cómo habilito IRM en la organización de Exchange Online?

Después de exportar los datos de TPD de los servidores locales de AD RMS, deberá importar los datos en la organización de Exchange Online y, a continuación, habilitar IRM.

1.  En la organización de Exchange Online, importe los datos de TPD.
    
        Import-RMSTrustedPublishingDomain -FileData $( [Byte[]] (Get-Content -Encoding Byte -Path "<Path to exported TPD file>" -ReadCount 0))

2.  Habilite IRM en la organización de Exchange Online.
    
        Set-IRMConfiguration -InternalLicensingEnabled $True

## ¿Cómo distribuyo las plantillas de AD IRM en la organización de Exchange Online?

Después de haber habilitado IRM en la organización de Exchange Online, deberá distribuir las plantillas importadas de AD RMS. Los siguientes usuarios y funciones de Exchange Online utilizan plantillas de AD RMS:

  - Usuarios de Outlook en la web

  - Usuarios de Exchange ActiveSync

  - Reglas de transporte

  - Descifrado de informe de diarios

  - Reglas de protección de Outlook

<!-- end list -->

1.  En la organización de Exchange Online , recupere una lista de plantillas de AD RMS.
    
        Get-RMSTemplate -Type All

2.  Distribuya las plantillas de AD RMS entre los usuarios y las funciones de la organización de Exchange Online.
    
        Set-RMSTemplate <template name> -Type Distributed
    

    > [!NOTE]
    > No puede modificar la plantilla AD RMS "Do Not Forward".



3.  Repita el paso 2 para cada plantilla AD RMS que desea distribuir.

## ¿Cómo saber si el proceso se ha completado correctamente?

Los usuarios de Outlook en la web deberán poder aplicar las plantillas de AD RMS a nuevos mensajes. Los usuarios de Outlook en la web y Exchange ActiveSync deberán poder leer los mensajes con plantillas de AD RMS aplicadas. Asimismo, deben detallarse todas las plantillas de AD RMS que se importaron de la organización local al ejecutar el cmdlet **Get-RMSTemplate**.

Ejecute el siguiente comando en la organización de Exchange Online.

    Get-RMSTemplate 

Encontrará más información en: [Information Rights Management en Outlook Web App](https://technet.microsoft.com/es-es/library/dd876891\(v=exchg.150\))

