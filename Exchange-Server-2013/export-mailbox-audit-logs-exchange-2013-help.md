---
title: 'Exportar registros de auditoría de buzones: Exchange 2013 Help'
TOCTitle: Exportar registros de auditoría de buzones
ms:assetid: b458a95a-3321-4647-8884-cf97f8e7186a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150552(v=EXCHG.150)
ms:contentKeyID: 48268579
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exportar registros de auditoría de buzones

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2015-04-07_

Cuando un buzón de correo tiene habilitada la auditoría, Microsoft Exchange guarda la información en el *registro de auditoría de buzones de correo* siempre que un usuario que no sea el propietario obtenga acceso al buzón de correo. Cada entrada de registro incluye información acerca de quién tuvo acceso al buzón y en qué momento, las acciones realizadas por el usuario que es no propietario y si la acción se realizó correctamente. Las entradas del registro de auditoría de buzones de correo se retienen, de manera predeterminada, durante 90 días. Puede usar el registro de auditoría de buzones de correo para determinar si un usuario que no es el propietario ha tenido acceso a un buzón de correo.

Al exportar las entradas de los registros de auditoría de buzones de correo, Microsoft Exchange registra las entradas en un archivo XML y lo adjunta a un mensaje de correo electrónico que se envía a los destinatarios especificados.

**Contenido**

Antes de empezar

Configuración del registro de auditoría de buzones de correo

Exportación del registro de auditoría de buzones de correo

Consulta del registro de auditoría de buzones de correo

Más información

## Antes de empezar

  - Tiempo estimado para completar cada procedimiento: Los tiempos varían. En Exchange Online, el registro de auditoría de buzones de correo se envía unos días después de haberlo exportado.

  - En Exchange Online, tiene que usar Windows PowerShell remoto para realizar muchos de los procedimientos de este tema. Para obtener más información, vea [Conectarse a Exchange Online mediante PowerShell remoto](https://technet.microsoft.com/es-es/library/jj984289\(v=exchg.150\)).

  - Los procedimientos descritos en este tema requieren permisos específicos. Vea cada procedimiento para ver la información de permisos.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Configuración del registro de auditoría de buzones de correo

Desde habilitar registro de auditoría de buzones de correo en cada buzón que desee auditar para poder exportar y consultar los registros de auditoría. También debe configurar Microsoft Outlook Web App para permitir que los documentos adjuntos XML utilicen Outlook Web App para acceder el registro de auditoría.

## Paso 1: Habilitación del registro de auditoría de buzones de correo

Tiene que habilitar el registro de auditoría de buzones de correo para el que desee ejecutar un informe de acceso al buzón de correo del que no se es propietario. Si el registro de la auditoría de buzones de correo no está habilitado para un buzón de correo, no obtendrá ningún resultado para él cuando exporte dicho registro de auditoría de buzones de correo.

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Registro de auditoría de buzones" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

Para habilitar el registro de auditoría de buzones de correo para un solo buzón de correo, ejecute el comando en el Shell.

    Set-Mailbox <Identity> -AuditEnabled $true

Para habilitar la auditoría de buzones de correo para todos los buzones de usuarios de la organización, ejecute los siguientes comandos.

    $UserMailboxes = Get-mailbox -Filter {(RecipientTypeDetails -eq 'UserMailbox')}

    $UserMailboxes | ForEach {Set-Mailbox $_.Identity -AuditEnabled $true}

## Paso 2: Configuración de Outlook Web App para permitir datos adjuntos de XML

Al exportar el informe de auditoría de buzones de correo, Microsoft Exchange adjunta el registro de auditoría, que es un archivo XML, a un mensaje de correo electrónico. Sin embargo, Outlook Web App bloquea los datos adjuntos de XML de forma predeterminada. Para acceder al registro de auditoría exportado, debe usar Microsoft Outlook o configurar Outlook Web App para permitir adjuntos XML.

Entrada "Directivas de buzones de Outlook Web App" Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

Realice los procedimientos siguientes para permitir datos adjuntos de XML en Outlook Web App. En Exchange Server 2013, use el valor `Default` para el parámetro *Identity*.

1.  Ejecute el siguiente comando para agregar XML a la lista de tipos de archivo permitidos en Outlook Web App.
    
        Set-OwaMailboxPolicy -Identity OwaMailboxPolicy-Default -AllowedFileTypes @{add='.xml'}

2.  Ejecute el siguiente comando para quitar XML de la lista de tipos de archivos bloqueados en Outlook Web App.
    
        Set-OwaMailboxPolicy -Identity OwaMailboxPolicy-Default -BlockedFileTypes @{remove='.xml'}

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que configuró correctamente el registro de auditoría de buzones de correo, haga lo siguiente:

1.  Ejecute el siguiente comando para comprobar que se configuró el registro de auditoría para los buzones de correo.
    
        Get-Mailbox | FL Name,AuditEnabled
    
    Un valor de `True` para la propiedad *AuditEnabled* comprueba que el registro de auditoría esté habilitado.

2.  Ejecute el siguiente comando para comprobar que se permiten datos adjuntos XML en Outlook Web App.
    
        Get-OwaMailboxPolicy | Select-Object -ExpandProperty AllowedFileTypes
    
    Compruebe que `.xml` esté incluido en la lista de tipos de archivos permitidos.

3.  Ejecute el siguiente comando para comprobar que los datos adjuntos XML se han quitado de la lista de archivos bloqueados en Outlook Web App.
    
        Get-OwaMailboxPolicy | Select-Object -ExpandProperty BlockedFileTypes
    
    Compruebe que `.xml` no esté incluido en la lista de tipos de archivos bloqueados.

Volver al principio

## Exportación del registro de auditoría de buzones de correo

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Registro de auditoría de administrador de sólo vista" en el tema [Permisos de infraestructura de la Shell y de Exchange](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

1.  En el Centro de Administración de Exchange (EAC), vaya a **Administración de cumplimiento** \> **Auditoría**.

2.  Haga clic en **Exportar registros de auditoría de buzones de correo**.

3.  Configure los siguientes criterios de búsqueda para exportar las entradas del informe de auditoría de buzones de correo:
    
      - **Fechas de inicio y finalización**   Seleccione el intervalo de fechas de las entradas que se incluirán en el archivo exportado.
    
      - **Buzones de correo de los que se buscará el registro de auditoría**   Seleccione los buzones de correo de los que se recuperarán las entradas de registro de auditoría.
    
      - **Tipo de acceso no propietario**   Seleccione una de las siguientes opciones para definir el tipo de acceso no propietario del que se recuperarán las entradas:
        
          - **Todos los usuarios que no son propietarios**   Búsqueda de acceso por parte de administradores y usuarios delegados dentro de la organización y por parte de los administradores del centro de datos de Microsoft en Exchange Online.
        
          - **Usuarios externos**   Se busca el acceso por parte de los administradores del centro de datos de Microsoft.
        
          - **Administradores y usuarios delegados**   Se busca el acceso por parte de administradores y usuarios delegados de la organización.
        
          - **Administradores**   Se busca el acceso por parte de los administradores de la organización.
    
      - **Destinatarios**   Seleccione los usuarios a los que se enviará el registro de auditoría de buzones de correo.

4.  Haga clic en **Export** (Exportar).
    
    Microsoft Exchange recupera las entradas del registro de auditoría de buzones de correo que cumplen con los criterios de búsqueda, los guarda en un archivo denominado SearchResult.xml y, a continuación, adjunta el archivo XML a un mensaje de correo electrónico enviado a los destinatarios que especificó.

## ¿Cómo saber si el proceso se ha completado correctamente?

Inicie sesión en el buzón al que se envió el registro de auditoría de buzones de correo. Si exportó correctamente el registro de auditoría, recibirá un mensaje de Exchange. En Exchange Online, puede tardar unos días en recibir este mensaje. El registro de auditoría de buzones (llamado SearchResult.xml) se adjuntará a este mensaje. Si ha configurado correctamente Outlook Web App para permitir datos adjuntos XML, puede descargar el archivo XML adjunto.

Volver al principio

## Consulta del registro de auditoría de buzones de correo

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Registro de auditoría de administrador de sólo vista" en el tema [Permisos de infraestructura de la Shell y de Exchange](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

Para guardar y ver el archivo SearchResult.xml:

1.  Inicie sesión en el buzón al que se envió el registro de auditoría de buzones de correo.

2.  En la bandeja de entrada, abra los datos adjuntos de XML enviados por Microsoft Exchange. Observe que el cuerpo del mensaje de correo electrónico contiene los criterios de búsqueda.

3.  Haga clic en el archivo adjunto y seleccione la opción de descargar el archivo XML.

4.  Abra el archivo SearchResult.xml en Microsoft Excel.

Volver al principio

## Más información

  - **Entradas del registro de auditoría de buzones**   En el ejemplo siguiente se muestra una entrada del registro de auditoría de buzones incluida en el archivo SearchResult.xml. Cada entrada va precedida por una etiqueta XML **\<Event\>** y termina con la etiqueta XML **\</Event\>**. Esta entrada muestra que el administrador purgó el mensaje con el asunto "**Notification of litigation hold**" de la carpeta Elementos recuperables en el buzón de correo de David el 30 de abril de 2010.
    
        <Event MailboxGuid="6d4fbdae-e3ae-4530-8d0b-f62a14687939" 
          Owner="PPLNSL-dom\david50001-1363917750" 
          LastAccessed="2010-04-30T11:01:55.140625-07:00" 
          Operation="HardDelete" 
          OperationResult="Succeeded" 
          LogonType="Admin"
         FolderId="0000000073098C3277988F4CB882F5B82EBF64610100A7C317F68C24304BBD18ABE1F185E79B00000026BD4F0000"
          FolderPathName="\Recoverable Items\Deletions"
          ClientInfoString="Client=OWA;Action=ViaProxy" 
          ClientIPAddress="10.196.241.168" 
          InternalLogonType="Owner"
          MailboxOwnerUPN="david@contoso.com"
          MailboxOwnerSid="S-1-5-21-290112810-296651436-1966561949-1151" 
          CrossMailboxOperation="false" 
          LogonUserDN="Administrator"
          LogonUserSid="S-1-5-21-290112810-296651436-1966561949-1149">
          <SourceItems>
           <ItemId="0000000073098C3277988F4CB882F5B82EBF64610700A7C317F68C24304BBD18ABE1F185E79B00000026BD4F0000A7C317F68C24304BBD18ABE1F185E79B00000026BD540"
            Subject="Notification of litigation hold"
            FolderPathName="\Recoverable Items\Deletions" /> 
          </SourceItems>
        </Event>

  - **Campos útiles en el registro de auditoría de buzones**   Esta es una descripción de los campos útiles del registro de auditoría de buzones. Pueden ayudarle a identificar la información concreta acerca de cada instancia de acceso de no propietario a un buzón de correo.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Campo</th>
    <th>Descripción</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Owner</strong></p></td>
    <td><p>El propietario del buzón al que obtuvo acceso un usuario que no es el propietario.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>LastAccessed</strong></p></td>
    <td><p>La fecha y hora en que se obtuvo acceso al buzón de correo.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Operation</strong></p></td>
    <td><p>La acción que realizó el usuario no propietario. Para obtener más información, vea la sección &quot;¿Qué se almacena en el registro de auditoría de buzones de correo?&quot; en <a href="https://technet.microsoft.com/es-es/library/jj156300(v=exchg.150)">Obtenga más información acerca de cómo ejecutar un informe de acceso al buzón de correo del que no se es propietario</a>.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OperationResult</strong></p></td>
    <td><p>Si la acción que realizó el usuario no propietario se efectuó correctamente o no.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>LogonType</strong></p></td>
    <td><p>El tipo de acceso no propietario. Los valores son: administrator, delegate y external.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>FolderPathName</strong></p></td>
    <td><p>El nombre de la carpeta que contenía el mensaje afectado por el usuario no propietario.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>ClientInfoString</strong></p></td>
    <td><p>Información acerca del cliente de correo usado por el usuario no propietario para tener acceso al buzón de correo.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ClientIPAddress</strong></p></td>
    <td><p>Dirección IP del equipo que usó el usuario no propietario para tener acceso al buzón.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>InternalLogonType</strong></p></td>
    <td><p>El tipo de inicio de sesión de la cuenta que usó el usuario no propietario para tener acceso a este buzón de correo.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>MailboxOwnerUPN</strong></p></td>
    <td><p>Dirección de correo electrónico del propietario del buzón de correo.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>LogonUserDN</strong></p></td>
    <td><p>Nombre para mostrar del usuario no propietario.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Subject</strong></p></td>
    <td><p>Línea de asunto del mensaje de correo electrónico afectado por el usuario que no es propietario.</p></td>
    </tr>
    </tbody>
    </table>
    
    Volver al principio

