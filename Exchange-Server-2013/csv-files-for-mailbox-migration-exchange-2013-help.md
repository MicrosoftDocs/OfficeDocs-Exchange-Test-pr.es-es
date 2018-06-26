---
title: 'Archivos CSV para la migración de buzones: Exchange 2013 Help'
TOCTitle: Archivos CSV para la migración de buzones
ms:assetid: e67b3455-3946-4335-b80c-97823c76ac54
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn170437(v=EXCHG.150)
ms:contentKeyID: 54652425
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Archivos CSV para la migración de buzones

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2017-11-16_

Puede usar un archivo CSV para migrar en bloque una gran cantidad de buzones de correo de usuario. Puede especificar un archivo CSV cuando usa el Centro de administración de Exchange (EAC) o el cmdlet **New-MigrationBatch** en el Shell de administración de Exchange para crear un lote de migración. El uso de un archivo CSV para especificar varios usuarios para migrarlos en un lote de migración se admite en los siguientes escenarios de migración:

  - **Movimientos en organizaciones locales de Exchange**
    
      - **Movimiento local:** el movimiento local consiste en mover los buzones de correo de una base datos de buzones a otra. Se produce un movimiento local dentro de un solo bosque.
    
      - **Movimiento de empresas entre bosques:** en el movimiento de empresas entre bosques, los buzones de correo se mueven a otro bosque. Los movimientos entre bosques se inician desde el bosque de destino, que es el bosque al que se van a mover los buzones, o desde el bosque de origen, que es el que hospeda los buzones actualmente.

  - **Carga y descarga en Exchange Online**
    
      - **Migración de movimientos remotos de carga:** en una implementación híbrida de Exchange, puede mover los buzones de correo desde una organización de Exchange local hacia Exchange Online. Esto también se conoce como migración de movimientos remotos de *carga* porque los buzones se incorporan a Exchange Online.
    
      - **Migración de movimientos remotos de descarga:** también puede ejecutar una migración de movimientos remotos de *descarga*, en la que los buzones de Exchange Online se migran a la organización local de Exchange.
        

        > [!NOTE]
        > Tanto las migraciones de movimientos remotos de carga como de descarga se inician en la organización de Exchange Online.

    
      - **Migración preconfigurada de Exchange:** también puede migrar un subconjunto de buzones de correo desde una organización local de Exchange hacia Exchange Online. Es otro tipo de migración de carga. Solo puede migrar buzones de correo de Exchange 2003 y Exchange 2007 con una migración preconfigurada de Exchange. No se pueden migrar buzones de Exchange 2010 y Exchange 2013 con una migración preconfigurada. Antes de ejecutar una migración preconfigurada, debe usar una sincronización de directorio o cualquier otro método para aprovisionar los usuarios de correo de la organización de Exchange Online.
    
      - **Migración del IMAP:** este tipo de migración de carga migra datos del buzón de correo desde un servidor IMAP (incluyendo Exchange) hacia Exchange Online. En la migración del IMAP, primero debe aprovisionar los buzones de correo en Exchange Online para poder migrar los datos del buzón de correo.


> [!NOTE]
> Una migración de traslado Exchange no admite un utilizando un archivo CSV porque todos los buzones de usuario local se migran a Exchange Online en un único lote.



## Atributos compatibles con archivos CSV para movimientos o migraciones en bloque

La primera fila, o la fila de encabezado, de un archivo CSV que se usa para migrar usuarios enumera los nombres de los atributos, o campos, especificados en las filas que siguen. Los nombres de atributo se separan con una coma. Cada fila que se encuentra debajo de la fila de encabezado representa a un usuario individual y proporciona la información requerida para la migración. Los atributos de cada fila de usuario individual deben seguir el mismo orden que los nombres de atributo de la fila de encabezado. Los valores de atributo se separan con una coma. Si el valor de atributo de un registro en concreto es nulo, no escriba nada. Pero asegúrese de incluir la coma que separa el valor nulo del siguiente atributo.

Los valores del atributo del archivo CSV reemplazan el valor del parámetro correspondiente si ese mismo parámetro se usa cuando se crea un lote de migración con el EAC o el Shell de administración de Exchange. Para más información y ejemplos, vea la sección Los valores de atributo del archivo CSV reemplazan los valores para el lote de migración.


> [!TIP]
> Puede usar cualquier editor de texto para crear el archivo CSV, pero usar una aplicación como Microsoft&nbsp;Excel facilitará la importación de los datos y la configuración y la organización de los archivos CSV. Asegúrese de guardar los archivos CSV como archivos .csv o .txt.



Las secciones siguientes describen los atributos de la fila de encabezado de un archivo CSV para cada tipo de migración. Cada sección incluye una tabla que enumera los atributos admitidos, si se requiere, un ejemplo de un valor para el atributo y una descripción.


> [!NOTE]
> En las secciones siguientes, el <EM>entorno de origen</EM> indica la ubicación actual del buzón de correo de usuario o de una base de datos. El <EM>entorno de destino</EM> indica la ubicación a la que se migrará el buzón de correo o la base de datos a la que se moverá el buzón de correo.



## Movimientos locales

En la tabla que sigue se describen los atributos compatibles con un archivo CSV para movimientos locales. Para más información, vea [Administración de movimientos locales](manage-on-premises-moves-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Atributo</th>
<th>Obligatorio u opcional</th>
<th>Valores aceptados</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>Obligatorio</p></td>
<td><p>Dirección SMTP para el usuario</p></td>
<td><p>Especifica el usuario que se moverá.</p></td>
</tr>
<tr class="even">
<td><p>TargetDatabase</p></td>
<td><p>Opcional</p></td>
<td><p>Nombre de la base de datos</p></td>
<td><p>Especifica la base de datos de buzón que se moverá el buzón principal del usuario a. Puede especificar otra base de datos en las filas del archivo CSV, que le permite mover buzones en el mismo lote de migración a diversas bases de datos diferentes.</p></td>
</tr>
<tr class="odd">
<td><p>TargetArchiveDatabase</p></td>
<td><p>Opcional</p></td>
<td><p>Nombre de la base de datos</p></td>
<td><p>Especifica la base de datos de buzón que se moverá el buzón del usuario archivo (si existe) a. Puede especificar otra base de datos en las filas del archivo CSV, que le permite mover buzones de archivo en el mismo lote de migración a diversas bases de datos diferentes.</p>

> [!NOTE]
> Si no se especifica la base de datos de archivo, el buzón de archivo se mueve a la misma base de datos como el buzón principal.


</td>
</tr>
<tr class="even">
<td><p>BadItemLimit</p></td>
<td><p>Opcional</p></td>
<td><p><code>Unlimited</code> o un número entero no negativo de <code>0</code> (valor predeterminado) a un valor máximo de <code>2147483647</code></p></td>
<td><p>Especifica el número de elementos incorrectos que deben omitirse si el servicio de migración encuentra un elemento dañado en el buzón de correo. Si incluye este atributo en el archivo CSV, se reemplazará el valor predeterminado o el valor que especifique si incluye el parámetro <em>BadItemLimit</em> al crear el lote de migración mediante el EAC o el Shell de administración de Exchange.</p>

> [!TIP]
> Recomendamos usar el valor predeterminado de 0 y solo aumentar el límite de elementos incorrectos para un usuario en particular si no se puede realizar correctamente el movimiento o la migración de dicho usuario.


<p></p></td>
</tr>
<tr class="odd">
<td><p>MailboxType</p></td>
<td><p>Opcional</p></td>
<td><p>Use uno de los siguientes valores:</p>
<ul>
<li><p><code>PrimaryOnly</code></p></li>
<li><p><code>ArchiveOnly</code></p></li>
<li><p><code>PrimaryAndArchive</code> (el valor predeterminado)</p></li>
</ul></td>
<td><p>Especifica si se va a mover el buzón principal del usuario, buzón archivado o ambos.</p></td>
</tr>
</tbody>
</table>


## Migraciones de movimientos remotos de carga en una implementación híbrida

En una implementación híbrida, puede mover los buzones de correo desde una organización local de Exchange hacia Exchange Online. Cuando se cargan buzones de correo, el lote de migración se crea en la organización de Exchange Online y el administrador de Exchange Online es el encargado de iniciarla. Para más información, vea [Mover buzones de correo entre organizaciones locales y de Exchange Online en implementaciones híbridas](https://technet.microsoft.com/es-es/library/jj906432\(v=exchg.150\)).

En la tabla que sigue se describen los atributos compatibles con un archivo CSV para migraciones de movimientos remotos de carga.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Atributo</th>
<th>Obligatorio u opcional</th>
<th>Valores aceptados</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>Obligatorio</p></td>
<td><p>Dirección SMTP para el usuario</p></td>
<td><p>Especifica la dirección de correo electrónico para el usuario habilitado para correo en la organización de Exchange Online que corresponde al buzón de correo de usuario local que se migrará.</p></td>
</tr>
<tr class="even">
<td><p>BadItemLimit</p></td>
<td><p>Opcional</p></td>
<td><p><code>Unlimited</code> o un número entero no negativo de <code>0</code> (valor predeterminado) a un valor máximo de <code>2147483647</code></p></td>
<td><p>Especifica el número de elementos incorrectos que deben omitirse si el servicio de migración encuentra un elemento dañado en el buzón de correo. Si incluye este atributo en el archivo CSV, se reemplazará el valor predeterminado o el valor que especifique si incluye el parámetro <em>BadItemLimit</em> al crear el lote de migración mediante el EAC o el Shell de administración de Exchange.</p>

> [!TIP]
> Recomendamos usar el valor predeterminado de 0 y solo aumentar el límite de elementos incorrectos para un usuario en particular si no se puede realizar correctamente el movimiento o la migración de dicho usuario.


</td>
</tr>
<tr class="odd">
<td><p>LargeItemLimit</p></td>
<td><p>Opcional</p></td>
<td><p><code>Unlimited</code> o un número entero no negativo de <code>0</code> (valor predeterminado) a un valor máximo.</p></td>
<td><p>Especifica el número de elementos de gran tamaño en el buzón del usuario que se omitirán. Cuando el número de elementos de gran tamaño supera este valor, se produce un error en la migración del buzón.</p>
<p>El valor predeterminado es 0, lo que significa que se produce un error en la migración si el buzón de correo contiene algún elemento de gran tamaño.</p>
<p>Cuando se cargan buzones de correo en Exchange Online, se migrarán solo los elementos que tengan un tamaño máximo de 35 MB.</p></td>
</tr>
<tr class="even">
<td><p>MailboxType</p></td>
<td><p>Opcional</p></td>
<td><p>Use uno de los siguientes valores:</p>
<ul>
<li><p><code>PrimaryOnly</code></p></li>
<li><p><code>ArchiveOnly</code></p></li>
<li><p><code>PrimaryAndArchive</code> (el valor predeterminado)</p></li>
</ul></td>
<td><p>Especifica si se va a mover el buzón principal del usuario, buzón archivado o ambos.</p></td>
</tr>
</tbody>
</table>


## Movimientos de empresas entre bosques y migraciones de movimientos remotos de descarga en una implementación híbrida

Como se indicó anteriormente, los movimientos entre bosques se inician desde el bosque de destino o desde el bosque de origen. Las migraciones de movimientos remotos de descarga se inician desde la organización de Exchange Online. Para más información, vea:

  - [Preparar los buzones para las solicitudes de movimiento entre bosques](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md)

  - [Mover buzones de correo entre organizaciones locales y de Exchange Online en implementaciones híbridas](https://technet.microsoft.com/es-es/library/jj906432\(v=exchg.150\))

En la tabla siguiente se describen los atributos compatibles para un archivo CSV para movimientos empresariales entre bosques y para migraciones de movimientos remotos de descarga en una implementación híbrida de Exchange.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Atributo</th>
<th>Obligatorio u opcional</th>
<th>Valores aceptados</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>Obligatorio</p></td>
<td><p>Dirección SMTP para el usuario</p></td>
<td><p>Para los movimientos de empresas entre bosques, especifica el buzón de correo o el usuario habilitado para correo en el bosque de origen.</p>
<p>Para las migraciones de movimientos remotos de descarga, se especifica el buzón de correo de Exchange Online.</p></td>
</tr>
<tr class="even">
<td><p>TargetDatabase</p></td>
<td><p>Obligatorio para las migraciones de movimientos remotos de descarga y para los movimientos de empresas entre bosques que se inician desde el bosque de origen. De manera alternativa, este atributo puede especificarse al crear el lote de migración en el EAC o mediante el Shell de administración de Exchange.</p>
<p>Este atributo es opcional para los movimientos empresariales entre bosques que se inician desde el bosque de destino.</p></td>
<td><p>Nombre de la base de datos</p></td>
<td><p>Especifica la base de datos de buzón en el bosque de destino que se moverá el buzón principal del usuario a. Puede especificar otra base de datos en las filas del archivo CSV, que le permite mover buzones en el mismo lote de migración a diversas bases de datos diferentes.</p></td>
</tr>
<tr class="odd">
<td><p>TargetArchiveDatabase</p></td>
<td><p>Opcional</p></td>
<td><p>Nombre de la base de datos</p></td>
<td><p>Especifica la base de datos de buzón en el bosque de destino que se moverá el buzón del usuario archivo a. Puede especificar otra base de datos en las filas del archivo CSV, que le permite mover buzones de archivo en el mismo lote de migración a diversas bases de datos diferentes.</p></td>
</tr>
<tr class="even">
<td><p>BadItemLimit</p></td>
<td><p>Opcional</p></td>
<td><p><code>Unlimited</code> o un número entero no negativo de <code>0</code> (valor predeterminado) a un valor máximo de <code>2147483647</code></p></td>
<td><p>Especifica el número de elementos incorrectos que deben omitirse si el servicio de migración encuentra un elemento dañado en el buzón de correo. Si incluye este atributo en el archivo CSV, se reemplazará el valor predeterminado o el valor que especifique si incluye el parámetro <em>BadItemLimit</em> al crear el lote de migración mediante el EAC o el Shell de administración de Exchange.</p>

> [!TIP]
> Recomendamos usar el valor predeterminado de 0 y solo aumentar el límite de elementos incorrectos para un usuario en particular si no se puede realizar correctamente el movimiento o la migración de dicho usuario.


</td>
</tr>
<tr class="odd">
<td><p>LargeItemLimit</p></td>
<td><p>Opcional</p></td>
<td><p><code>Unlimited</code> o un número entero no negativo de <code>0</code> (valor predeterminado) a un valor máximo.</p></td>
<td><p>Especifica el número de elementos de gran tamaño en el buzón del usuario que se omitirán. Cuando el número de elementos de gran tamaño supera este valor, se produce un error en la migración del buzón.</p>
<p>El valor predeterminado es 0, lo que significa que se produce un error en la migración si el buzón de correo contiene algún elemento de gran tamaño.</p>
<p>Cuando se cargan buzones de correo en Exchange Online, se migrarán solo los elementos que tengan un tamaño máximo de 35 MB.</p></td>
</tr>
<tr class="even">
<td><p>MailboxType</p></td>
<td><p>Opcional</p></td>
<td><p>Use uno de los siguientes valores:</p>
<ul>
<li><p><code>PrimaryOnly</code></p></li>
<li><p><code>ArchiveOnly</code></p></li>
<li><p><code>PrimaryAndArchive</code> (el valor predeterminado)</p></li>
</ul></td>
<td><p>Especifica si se va a mover el buzón principal del usuario, buzón archivado o ambos.</p></td>
</tr>
</tbody>
</table>


## Migraciones preconfiguradas de Exchange

Debe usar un archivo CSV para identificar el grupo de usuarios para un lote de migración cuando quiere usar una migración preconfigurada de Exchange para migrar los buzones de correo locales de Exchange 2003 y Exchange 2007 a Exchange Online. No hay límites para la cantidad de buzones que pueden migrarse a la nube con una migración preconfigurada de Exchange. Sin embargo, el archivo CSV para un lote de migración puede contener un máximo de 1000 filas. Para migrar más de 1 000 buzones de correo, debe crear archivos CSV adicionales y, luego, usar cada uno para crear un nuevo lote de migración. Para más información sobre las migraciones preconfiguradas de Exchange, vea [Migrar buzones de correo a Exchange Online con una migración preconfigurada](https://technet.microsoft.com/es-es/library/jj874018\(v=exchg.150\)).

En la tabla que sigue se describen los atributos compatibles con un archivo CSV para una migración preconfigurada de Exchange.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Atributo</th>
<th>Obligatorio u opcional</th>
<th>Valores aceptados</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>Obligatorio</p></td>
<td><p>Dirección SMTP para el usuario</p></td>
<td><p>Especifica la dirección de correo electrónico para el usuario habilitado para correo (o un buzón si está reintentando la migración) de Exchange Online que corresponde al buzón del usuario local que se migrarán. Usuarios habilitados para correo se crean en Exchange Online como resultado de la sincronización de directorios u otro proceso de aprovisionamiento. La dirección de correo electrónico del usuario con correo habilitado debe coincidir con la propiedad <em>WindowsEmailAddress</em> para el buzón local correspondiente.</p></td>
</tr>
<tr class="even">
<td><p>Password</p></td>
<td><p>Opcional</p></td>
<td><p>Una contraseña debe tener una longitud mínima de ocho caracteres y satisfacer cualquier restricción de contraseña que se aplique en la organización de Office 365.</p></td>
<td><p>Esta contraseña se establece en la cuenta de usuario cuando el usuario habilitado para correo correspondiente en Exchange Online se convierte en un buzón de correo durante la migración.</p></td>
</tr>
<tr class="odd">
<td><p>ForceChangePassword</p></td>
<td><p>Opcional</p></td>
<td><p><code>True</code> o <code>False</code></p></td>
<td><p>Especifica si un usuario debe cambiar la contraseña la primera vez que inicia sesión en el buzón de correo de Exchange Online.</p>

> [!NOTE]
> Si ha implementado una solución de inicio de sesión único mediante la implementación de Active Directory Federation Services 2.0 (AD FS 2.0) de la organización local, debe utilizar <CODE>False</CODE> para el valor de este atributo.


</td>
</tr>
</tbody>
</table>


## Migraciones de IMAP

Un archivo CSV para un lote de migración de IMAP puede tener un máximo de 50 000 filas. Pero es aconsejable migrar a los usuarios en varios lotes más pequeños. Para más información sobre las migraciones de IMAP, vea los siguientes temas:

  - [Migrar correo desde un servidor IMAP a buzones de Exchange Online](https://technet.microsoft.com/es-es/library/jj874015\(v=exchg.150\))

  - [Archivos CSV para lotes de migración de IMAP](https://technet.microsoft.com/es-es/library/jj200730\(v=exchg.150\))

En la tabla que sigue se describen los atributos compatibles con un archivo CSV para una migración de IMAP.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Atributo</th>
<th>Obligatorio u opcional</th>
<th>Valores aceptados</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>Obligatorio</p></td>
<td><p>Dirección SMTP para el usuario.</p></td>
<td><p>Especifica el identificador de usuario del buzón de correo de Exchange Online del usuario.</p></td>
</tr>
<tr class="even">
<td><p>UserName</p></td>
<td><p>Obligatorio</p></td>
<td><p>Cadena que identifica al usuario en el sistema de mensajería IMAP, en un formato compatible con el servidor IMAP.</p></td>
<td><p>Especifica el nombre de inicio de sesión para la cuenta del usuario en el sistema de mensajería IMAP (el entorno de origen). Además del nombre de usuario, puede utilizar las credenciales de una cuenta que se ha asignado los permisos necesarios para tener acceso a buzones en el servidor IMAP. Para obtener más información, consulte <a href="https://technet.microsoft.com/es-es/library/jj200730(v=exchg.150)">Archivos CSV para lotes de migración de IMAP</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Password</p></td>
<td><p>Obligatorio</p></td>
<td><p>Cadena de contraseña.</p></td>
<td><p>Especifica la contraseña para la cuenta de usuario especificada por el atributo UserName.</p></td>
</tr>
</tbody>
</table>


## Los valores de atributo del archivo CSV reemplazan los valores para el lote de migración

Los valores del atributo del archivo CSV reemplazan el valor del parámetro correspondiente si ese mismo parámetro se usa cuando se crea un lote de migración con el EAC o el Shell de administración de Exchange. Si quiere que el valor de lote de migración se aplique a un usuario, debe dejar esa celda en blanco en el archivo CSV. Esto permite mezclar y hacer coincidir ciertos valores de atributos para los usuarios seleccionados en un lote de migración.

Por ejemplo, vamos a decir crear un lote en la Shell de administración de Exchange para el principal de una empresa entre bosques mover los usuarios y los buzones de archiving al bosque de destino con el siguiente comando de Shell de administración de Exchange.

    New-MigrationBatch -Name CrossForestBatch1 -SourceEndpoint ForestEndpoint1 -TargetDeliveryDomain forest2.contoso.com -TargetDatabases @(EXCH-MBX-02,EXCH-MBX-03) -TargetArchiveDatabases @(EXCH-MBX-A02,EXCH-MBX-A03) -CSVData ([System.IO.File]::ReadAllBytes("C:\Users\Administrator\Desktop\CrossForestBatch1.csv")) -AutoStart


> [!NOTE]
> Como el valor predeterminado es mover principal y archivar los buzones, no tienes que explícitamente se especifique en el comando Shell de administración de Exchange.



Una parte del archivo CrossForestBatch1.csv para este lote de migración tiene el siguiente aspecto:

    EmailAddress,TargetDatabase,TargetArchiveDatabase
    user1@contoso.com,EXCH-MBX-01,EXCH-MBX-A01
    user2@contoso.com,,
    user3@contoso.com,EXCH-MBX-01,
    ...

Debido a que los valores del archivo CSV reemplazan los valores del lote de migración, los buzones de correo principales y de archivo para user1 se mueven a EXCH-MBX-01 y EXCH-MBX-A01, respectivamente, en el bosque de destino. Los buzones de correo principales y de archivo para user2 se mueven a EXCH-MBX-02 o EXCH-MBX-03. El buzón de correo principal para user3 se mueve a EXCH-MBX-01 y el buzón de correo de archivo se mueve a EXCH-MBX-A02 o EXCH-MBX-A03.

En otro ejemplo, supongamos que se crea una sección para una migración de movimiento remoto de incorporación en una implementación híbrido para mover buzones de archiving a Exchange Online con el siguiente comando.

    New-MigrationBatch -Name OnBoarding1 -SourceEndpoint RemoteEndpoint1 -TargetDeliveryDomain cloud.contoso.com -CSVData ([System.IO.File]::ReadAllBytes("C:\Users\Administrator\Desktop\OnBoarding1.csv")) -MailboxType ArchiveOnly -AutoStart

Pero también quiere mover los buzones de correo principales para los usuarios seleccionados, de modo que una parte del archivo OnBoarding1.csv para este lote de migración tendría el siguiente aspecto:

    EmailAddress,MailboxType
    user1@contoso.com,
    user2@contoso.com,
    user3@cloud.contoso.com,PrimaryAndArchive
    user4@cloud.contoso.com,PrimaryAndArchive
    ...

Debido a que el valor del tipo de buzón de correo del archivo CSV reemplaza los valores del parámetro *MailboxType* en el comando para crear el lote, solo se migra a Exchange Online el buzón de correo de archivo para user1 y user2. Pero los buzones de correo principales y de archivo para user3 y user4 se mueven a Exchange Online.

