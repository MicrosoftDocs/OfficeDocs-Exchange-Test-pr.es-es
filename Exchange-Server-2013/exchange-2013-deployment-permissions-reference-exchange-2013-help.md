---
title: 'Referencia de permisos de implementación de Exchange 2013: Exchange 2013 Help'
TOCTitle: Referencia de permisos de implementación de Exchange 2013
ms:assetid: b13412d0-0cc4-4c1d-bf31-cae3d3e211a9
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee681663(v=EXCHG.150)
ms:contentKeyID: 59637138
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Referencia de permisos de implementación de Exchange 2013

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

En este tema, se describen los permisos necesarios para configurar una organización de Microsoft Exchange Server 2013. Los grupos de seguridad universal (USG) que están asociados con los grupos de funciones de administración y otros grupos de seguridad de Windows y entidades de seguridad, se agregan a las listas de control de acceso (ACL) de varios objetos Active Directory. Las ACL controlan qué operaciones se pueden realizar en cada objeto. Al comprender qué permisos se otorgan a cada grupo de roles, grupo de seguridad o entidad de seguridad, puede determinar los permisos mínimos requeridos para instalar Exchange 2013.

En algunos casos, la lista de control de acceso no se aplica en la propiedad habitual, **ntSecurityDescriptor**, sino en otra propiedad, como **msExchMailboxSecurityDescriptor**. El servicio de directorio no puede aplicar seguridad que no esté especificada en el descriptor de seguridad de Windows. En la mayoría de casos, estas ACL se replican para que el servicio de almacenamiento las almacene en objetos adecuados. Lamentablemente, no existe ninguna herramienta para ver estas ACL que no sea como datos binarios sin procesar.

Las columnas de cada tabla de permisos incluyen la siguiente información:

  - **Cuenta**   La entidad de seguridad ha concedido o denegado los permisos.

  - **Tipo de ACE**   Tipo de entrada de control de acceso (ACE)
    
      - **ACE de permiso**   Permite al usuario o grupo asociado con la ACE tener acceso a un elemento.
    
      - **ACE de denegación**   Evita que el usuario o grupo asociado con la ACE tenga acceso a un elemento.

  - **Herencia**   El tipo de herencia usada para objetos secundarios.
    
      - **Todos** indica que los permisos se aplican al objeto y a todos los subobjetos.
    
      - **Descripción** indica que los permisos se aplican a la clase de objeto enumerada en la fila En la propiedad/se aplica a.
    
      - **Ninguno** indica que dichos permisos sólo se aplican al objeto.

  - **Permisos**   Los permisos concedidos a la cuenta.

  - **En la propiedad/se aplica a**   En algunos casos, los permisos sólo se aplican a una determinada propiedad, a un conjunto de propiedades o a una clase de objeto. Estos permisos limitados se especifican aquí.

  - **Comentarios**   Si corresponde, esta columna explica por qué los permisos son necesarios o proporciona otra información acerca de los permisos.

Los permisos normalmente se enumeran en la tabla de la página de propiedades de **Seguridad** del Editor de interfaces ADSI (AdsiEdit.msc) Active Directory, en la vista **Avanzada** de la ficha **Ver/Editar**. La página de propiedades de **Seguridad** del Editor ADSI muestra una vista mucho más condensada de los permisos. La herramienta LDP (Ldp.exe) muestra la máscara de acceso directamente como un valor numérico. El código de instalación se refiere a los permisos con constantes predefinidas.

En la siguiente tabla se muestran las relaciones entre estos valores.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Página de resumen del Editor ADSI</th>
<th>Vista avanzada del Editor ADSI, ficha Ver/Editar</th>
<th>Entradas ACL aplicadas a un objeto determinado</th>
<th>Valor binario (máscara de acceso en LDP)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Control total</p></td>
<td><p>Control total</p></td>
<td><p><code>WRITE_OWNER | WRITE_DAC | READ_CONTROL | DELETE | ACTRL_DS_CONTROL_ACCESS | ACTRL_DS_LIST_OBJECT | ACTRL_DS_DELETE_TREE | ACTRL_DS_WRITE_PROP | ACTRL_DS_READ_PROP | ACTRL_DS_SELF | ACTRL_DS_LIST | ACTRL_DS_DELETE_CHILD | ACTRL_DS_CREATE_CHILD</code></p></td>
<td><p><code>0x000F01FF</code></p></td>
</tr>
<tr class="even">
<td><p>Leer</p></td>
<td><p>Mostrar contenido + Leer todas las propiedades + Permisos de lectura</p></td>
<td><p><code>ACTRL_DS_LIST | ACTRL_DS_READ_PROP | READ_CONTROL</code></p></td>
<td><p><code>0x00020014</code></p></td>
</tr>
<tr class="odd">
<td><p>Escribir</p></td>
<td><p>Escribir todas las propiedades + Todas las escrituras validadas</p></td>
<td><p><code>ACTRL_DS_WRITE_PROP | ACTRL_DS_SELF</code></p></td>
<td><p><code>0x00000028</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Mostrar contenidos</p></td>
<td><p><code>ACTRL_DS_LIST</code></p></td>
<td><p><code>0x00000004</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Leer todas las propiedades</p></td>
<td><p><code>ACTRL_DS_READ_PROP</code></p></td>
<td><p><code>0x00000010</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Escribir todas las propiedades</p></td>
<td><p><code>ACTRL_DS_WRITE_PROP</code></p></td>
<td><p><code>0x00000020</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Eliminar</p></td>
<td><p><code>DELETE</code></p></td>
<td><p><code>0x00010000</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Eliminar subárbol</p></td>
<td><p><code>ACTRL_DS_DELETE_TREE</code></p></td>
<td><p><code>0x00000040</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Permisos de lectura</p></td>
<td><p><code>READ_CONTROL</code></p></td>
<td><p><code>0x00020000</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Modificar permisos</p></td>
<td><p><code>WRITE_DAC</code></p></td>
<td><p><code>0x00040000</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Modificar propietario</p></td>
<td><p><code>WRITE_OWNER</code></p></td>
<td><p><code>0x00080000</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Todas las escrituras validadas</p></td>
<td><p><code>ACTRL_DS_SELF</code></p></td>
<td><p><code>0x00000008</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Todos los derechos extendidos</p></td>
<td><p><code>ACTRL_DS_CONTROL_ACCESS</code></p></td>
<td><p><code>0x00000100</code></p></td>
</tr>
<tr class="even">
<td><p>Crear todos los objetos secundarios</p></td>
<td><p>Crear todos los objetos secundarios</p></td>
<td><p><code>ACTRL_DS_CREATE_CHILD</code></p></td>
<td><p><code>0x00000001</code></p></td>
</tr>
<tr class="odd">
<td><p>Eliminar todos los objetos secundarios</p></td>
<td><p>Eliminar todos los objetos secundarios</p></td>
<td><p><code>ACTRL_DS_DELETE_CHILD</code></p></td>
<td><p><code>0x00000002</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p></p></td>
<td><p><code>ACTRL_DS_LIST_OBJECT</code></p></td>
<td><p><code>0x00000080</code></p></td>
</tr>
</tbody>
</table>


Los derechos extendidos son derechos personalizados especificados por aplicaciones individuales. Se especifican en la ACL. Sin embargo, carecen de sentido para Active Directory. La aplicación específica aplica todos los derechos extendidos. Son ejemplos de derechos extendidos de Exchange "Crear una carpeta pública" o "Crear propiedades con nombre en el almacén de información".

Para obtener información acerca de los permisos que se establecen durante la instalación de Exchange Server 2010 de Microsoft, vea [Referencia de permisos de implementación de Exchange 2010](https://go.microsoft.com/fwlink/p/?linkid=402924).

## Preparar permisos de Active Directory

Las tablas de permisos de esta sección muestran los permisos que se establecen al ejecutar el comando `Setup /PrepareAD`.


> [!NOTE]
> Los permisos descritos en esta sección son los permisos predeterminados que se configuran al implementar Exchange&nbsp;2013 con el modelo de permisos compartidos. Si ha implementado Exchange&nbsp;2013 con el modelo de permisos divididos de Active Directory, el permiso predeterminado es diferente. Para obtener más información acerca de los cambios en los permisos predeterminados al usar permisos divididos de Active Directory y los modelos de permisos compartidos y divididos en general, vea <A href="understanding-split-permissions-exchange-2013-help.md">Active Directory split permissions</A> en <A href="understanding-split-permissions-exchange-2013-help.md">Descripción de los permisos divididos</A>. Si decide no usar los permisos divididos de Active Directory al instalar Exchange, Exchange utilizará los permisos compartidos.



## Permisos de contenedor de Microsoft Exchange

En la siguiente tabla se muestran los permisos que se establecen en el contenedor de Microsoft Exchange dentro de la partición de configuración.

### Nombre distintivo del objeto: CN=Microsoft Exchange,CN=Servicios,CN=Configuración,DC=\<dominio\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuenta</th>
<th>Tipo de ACE</th>
<th>Herencia</th>
<th>Permisos</th>
<th>En la propiedad/se aplica a</th>
<th>Comentarios</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cuenta de instalación</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Control total</p></td>
<td><p></p></td>
<td><p>Es la cuenta que se usa para ejecutar <code>/PrepareAD</code>.</p></td>
</tr>
<tr class="even">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Control total</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Control total</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Leer</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Usuarios autenticados</p></td>
<td><p>ACE de permiso</p></td>
<td><p>None</p></td>
<td><p>Propiedad de lectura</p>
<p>Mostrar contenidos</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Modificar permisos</p></td>
<td><p>msExchSmtpRceiveConnector</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Administración de carpetas públicas</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Leer</p>
<p>Mostrar objeto</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Configuración delegada</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Leer</p>
<p>Mostrar objeto</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Permisos de contenedor de detección automática de Microsoft Exchange

En la siguiente tabla se muestran los permisos que se establecen en el contenedor de detección automática de Microsoft Exchange dentro de la partición de configuración.

### Nombre distintivo del objeto: CN=Detección automática de Exchange,CN=Servicios,CN=Configuración,DC=\<dominio\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuenta</th>
<th>Tipo de ACE</th>
<th>Herencia</th>
<th>Permisos</th>
<th>En la propiedad/se aplica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Leer</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Permisos de contenedor de organización de Microsoft Exchange

Las tablas de permisos de esta sección muestran los permisos que se establecen en la organización y los subcontenedores de Microsoft Exchange dentro de la partición de configuración.

### Nombre distintivo del objeto: CN=\<organización\>,CN=Microsoft Exchange,CN=Servicios,CN=Configuración,DC=\<dominio\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuenta(s)</th>
<th>Tipo de ACE</th>
<th>Herencia</th>
<th>Permisos</th>
<th>En la propiedad/se aplica a</th>
<th>Comentarios</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Administradores de la empresa</p>
<p>Administradores del dominio raíz</p>
<p>Cuenta de instalación</p>
<p>Administración de la organización</p></td>
<td><p>ACE de denegación</p></td>
<td><p>Todo</p></td>
<td><p>Enviar como</p>
<p>Recibir como</p></td>
<td><p></p></td>
<td><p>Los administradores de Windows no tienen permiso para abrir buzones de correo.</p></td>
</tr>
<tr class="even">
<td><p>Administradores de la empresa</p>
<p>Administradores del esquema</p>
<p>Administradores del dominio raíz</p>
<p>Cuenta de instalación</p>
<p>Administración de la organización</p></td>
<td><p>ACE de denegación</p></td>
<td><p>Todo</p></td>
<td><p>Suplantación de Servicios Web Exchange</p>
<p>Serialización de token de servicios Web Exchange</p></td>
<td><p></p></td>
<td><p>Derecho extendido</p></td>
</tr>
<tr class="odd">
<td><p>Administradores de la empresa</p>
<p>Administradores del esquema</p>
<p>Administradores del dominio raíz</p>
<p>Cuenta de instalación</p></td>
<td><p>ACE de denegación</p></td>
<td><p>Todo</p></td>
<td><p>Almacenar acceso de transporte</p>
<p>Almacenar delegación limitada</p>
<p>Almacenar acceso de lectura</p>
<p>Almacenar acceso de escritura y lectura</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Sistema local</p></td>
<td><p>Permitir</p></td>
<td><p>Todo</p></td>
<td><p>Todos los derechos extendidos</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Usuarios autenticados</p></td>
<td><p>ACE de denegación</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p></td>
<td><p><code>msExchAvailabilityUserPassword / msExchAvailabilityAddressSpace</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Usuarios autenticados</p></td>
<td><p>Permitir</p></td>
<td><p>Ninguno</p></td>
<td><p>Leer</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Permisos de lectura</p>
<p>Mostrar contenidos</p>
<p>Propiedad de lectura</p>
<p>Mostrar objeto</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Administración de carpetas públicas</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Permisos de lectura</p>
<p>Mostrar contenidos</p>
<p>Propiedad de lectura</p>
<p>Mostrar objeto</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>NT Authority\Network Service</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Leer</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de disponibilidad administrada</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Permisos de lectura</p>
<p>Mostrar contenidos</p>
<p>Propiedad de lectura</p>
<p>Mostrar objeto</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Todos los derechos extendidos</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>groupType</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchOwningServer</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchMailboxSecurityDescriptor</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchUMServerWritableFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchDatabaseCreated</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchUserCulture</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchMobileMailboxFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>siteFolderGUID</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>siteFolderServer</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchEDBOffline</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>userCertificate</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchUMDtmfMap</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchBlockedSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>Public Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchPatchMDB</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>publicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchUMSpokenName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchUMPinChecksum</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchSafeSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>thumbnailPhoto</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Crear carpeta pública de alto nivel</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Administración de carpetas públicas</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Crear carpeta pública de alto nivel</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Ver el estado del almacén de información</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Administración de carpetas públicas</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Ver el estado del almacén de información</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Administrar almacén de información</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Administración de carpetas públicas</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Administrar almacén de información</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Crear propiedades con nombre en el almacén de información</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Administración de carpetas públicas</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Crear propiedades con nombre en el almacén de información</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Modificar ACL de carpeta pública</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Administración de carpetas públicas</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Modificar ACL de carpeta pública</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Modificar cuotas de carpeta pública</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Administración de carpetas públicas</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Modificar cuotas de carpeta pública</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Modificar ACL de administración de carpetas públicas</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Administración de carpetas públicas</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Modificar ACL de administración de carpetas públicas</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Modificar expiración de carpeta pública</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Administración de carpetas públicas</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Modificar expiración de carpeta pública</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Modificar lista de réplicas de carpetas públicas</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Administración de carpetas públicas</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Modificar lista de réplicas de carpetas públicas</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Modificar retención de elementos eliminados en una carpeta pública</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Administración de carpetas públicas</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Modificar retención de elementos eliminados en una carpeta pública</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Crear una carpeta pública</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Administración de carpetas públicas</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Crear una carpeta pública</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Administración de carpetas públicas</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Carpeta pública habilitada para correo</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Todos</p>
<p>NT Authority\Anonymous Logon</p>
<p></p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Crear propiedades con nombre en el almacén de información</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Todos</p>
<p>NT Authority\Anonymous Logon</p>
<p></p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Crear una carpeta pública</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Todos</p>
<p>NT Authority\Anonymous Logon</p>
<p></p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Permisos de lectura</p>
<p>Mostrar contenidos</p>
<p>Propiedad de lectura</p>
<p>Mostrar objeto</p></td>
<td><p><code>/ msExchPrivateMDB</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Todos</p>
<p>NT Authority\Anonymous Logon</p>
<p></p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Permisos de lectura</p>
<p>Mostrar contenidos</p>
<p>Propiedad de lectura</p>
<p>Mostrar objeto</p></td>
<td><p><code>/ msExchPublicMDB</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Permisos de lectura</p>
<p>Mostrar contenidos</p>
<p>Propiedad de lectura</p>
<p>Mostrar objeto</p></td>
<td><p><code>/ siteAddressing</code></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nombre distintivo del objeto: CN=Todas las listas de direcciones,CN=Contenedor de listas de direcciones,CN=\<organización\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuenta</th>
<th>Tipo de ACE</th>
<th>Herencia</th>
<th>Permisos</th>
<th>En la propiedad/se aplica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Usuarios autenticados</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Mostrar contenidos</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchLastAppliedRecipientFilter</code></p>
<p><code>msExchRecipientFilterFlags</code></p></td>
</tr>
<tr class="odd">
<td><p>Administración de carpetas públicas</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchLastAppliedRecipientFilter</code></p>
<p><code>msExchRecipientFilterFlags</code></p></td>
</tr>
</tbody>
</table>


### Nombre distintivo del objeto: CN=Listas de direcciones sin conexión,CN=Contenedor de listas de direcciones, CN=\<organización\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuenta</th>
<th>Tipo de ACE</th>
<th>Herencia</th>
<th>Permisos</th>
<th>En la propiedad/se aplica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Usuarios autenticados</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Descargar la libreta de direcciones sin conexión</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nombre distintivo del objeto: CN=Direccionamiento,CN=\<organización\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuenta</th>
<th>Tipo de ACE</th>
<th>Herencia</th>
<th>Permisos</th>
<th>En la propiedad/se aplica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Usuarios autenticados</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Leer</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nombre distintivo del objeto: CN=Directivas de destinatarios,CN=\<organización\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuenta</th>
<th>Tipo de ACE</th>
<th>Herencia</th>
<th>Permisos</th>
<th>En la propiedad/se aplica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchLastAppliedRecipientFilter</code></p>
<p><code>msExchRecipientFilterFlags</code></p></td>
</tr>
<tr class="even">
<td><p>Administración de carpetas públicas</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchLastAppliedRecipientFilter</code></p>
<p><code>msExchRecipientFilterFlags</code></p></td>
</tr>
</tbody>
</table>


## Permisos de contenedor de partición de configuración

Las tablas de permisos de esta sección muestran los permisos que se establecen por el comando `Setup /PrepareAD` en varios contenedores dentro de la partición de configuración.

### Nombre distintivo del objeto: CN=Sitios,CN=Configuración,DC=\<dominio\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuenta</th>
<th>Tipo de ACE</th>
<th>Herencia</th>
<th>Permisos</th>
<th>En la propiedad/se aplica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Administración de la organización</p>
<p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchVersion / site</code></p></td>
</tr>
<tr class="even">
<td><p>Administración de la organización</p>
<p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchVersion / site-link</code></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p>
<p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchPartnerId / site</code></p></td>
</tr>
<tr class="even">
<td><p>Administración de la organización</p>
<p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchMinorPartnerId / site</code></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p>
<p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchResponsibleforSites / site</code></p></td>
</tr>
<tr class="even">
<td><p>Administración de la organización</p>
<p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p></p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchTransportSiteFlags / site</code></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p>
<p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchCost / site-link</code></p></td>
</tr>
<tr class="even">
<td><p>Administración de la organización</p>
<p>Subsistema de confianza de Exchange</p>
<p>Sistema local</p>
<p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Permisos de lectura</p>
<p>Mostrar contenidos</p>
<p>Propiedad de lectura</p>
<p>Mostrar objeto</p></td>
<td><p><code>/ msExchEdgeSyncEHFConnector</code></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p>
<p>Subsistema de confianza de Exchange</p>
<p>Sistema local</p>
<p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Permisos de lectura</p>
<p>Mostrar contenidos</p>
<p>Propiedad de lectura</p>
<p>Mostrar objeto</p></td>
<td><p><code>/ msExchEdgeSyncMservConnector</code></p></td>
</tr>
<tr class="even">
<td><p>Administración de la organización</p>
<p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Secundarios</p></td>
<td><p>Crear secundario</p>
<p>Eliminar secundario</p>
<p>Eliminar árbol</p></td>
<td><p><code>msExchEdgeSyncServiceConfig / site</code></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p>
<p>Subsistema de confianza de Exchange</p>
<p>Sistema local</p>
<p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Permisos de lectura</p>
<p>Mostrar contenidos</p>
<p>Propiedad de lectura</p>
<p>Mostrar objeto</p></td>
<td><p><code>/ msExchEdgeSyncServiceConfig</code></p></td>
</tr>
<tr class="even">
<td><p>Administración de la organización</p>
<p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Secundarios</p></td>
<td><p>Crear secundario</p>
<p>Eliminar secundario</p>
<p>Eliminar árbol</p></td>
<td><p><code>msExchEdgeSyncMservConnector / msExchEdgeSyncServiceConfig</code></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p>
<p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Secundarios</p></td>
<td><p>Crear secundario</p>
<p>Eliminar secundario</p>
<p>Eliminar árbol</p></td>
<td><p><code>msExchEdgeSyncEHFConnector / msExchEdgeSyncServiceConfig</code></p></td>
</tr>
</tbody>
</table>


### Nombre distintivo del objeto: CN=Objetos eliminados,CN=Configuración,DC=\<dominio\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuenta</th>
<th>Tipo de ACE</th>
<th>Herencia</th>
<th>Permisos</th>
<th>En la propiedad/se aplica a</th>
<th>Comentarios</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Mostrar contenidos</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Administración de organizaciones</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Leer</p>
<p>Mostrar objeto</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Cuenta de instalación</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Permiso de lectura</p>
<p>Permiso de escritura</p>
<p>Mostrar contenidos</p>
<p>Propiedad de lectura</p>
<p>Mostrar objeto</p></td>
<td><p></p></td>
<td><p>Es la cuenta que se usa para ejecutar <code>/PrepareAD</code>.</p></td>
</tr>
<tr class="even">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Leer</p>
<p>Mostrar objeto</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servicio de red</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Mostrar contenidos</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Permisos de grupo administrativo de Exchange

El comando `Setup /PrepareAD` también configura los siguientes permisos en grupos administrativos dentro de la organización.

### Nombre distintivo del objeto: CN=\<grupo administrativo\>,CN=Grupos administrativos,CN=\<organización\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuenta</th>
<th>Tipo de ACE</th>
<th>Herencia</th>
<th>Permisos</th>
<th>En la propiedad/se aplica a</th>
<th>Comentarios</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Servicio de actualización de acceso de destinatarios</p></td>
<td><p><code>msExchExchangeServer</code></p></td>
<td><p>Permite a los administradores de destinatarios de Exchange marcar a los destinatarios con información de la dirección del proxy.</p></td>
</tr>
<tr class="even">
<td><p>Sistema local</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Servicio de actualización de acceso de destinatarios</p></td>
<td><p><code>msExchExchangeServer</code></p></td>
<td><p>Permite a los servidores marcar a los destinatarios con información de la dirección del proxy.</p></td>
</tr>
<tr class="odd">
<td><p>Administración de carpetas públicas</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Servicio de actualización de acceso de destinatarios</p></td>
<td><p><code>msExchExchangeServer</code></p></td>
<td><p>Permite a los administradores de carpetas públicas de Exchange marcar a los destinatarios con información de la dirección del proxy.</p></td>
</tr>
</tbody>
</table>


### Nombre distintivo del objeto: CN=Configuración de seguridad avanzada,CN=\<grupo administrativo\>,CN=Grupos administrativos,CN=\<organización\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuenta</th>
<th>Tipo de ACE</th>
<th>Herencia</th>
<th>Permisos</th>
<th>En la propiedad/se aplica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Usuarios autenticados</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Ninguno</p></td>
<td><p>Mostrar contenidos</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nombre distintivo del objeto: CN=Cifrado,CN=Configuración de seguridad avanzada,CN=\<grupo administrativo\>,CN=Grupos administrativos,CN=\<organización\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuenta</th>
<th>Tipo de ACE</th>
<th>Herencia</th>
<th>Permisos</th>
<th>En la propiedad/se aplica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Usuarios autenticados</p></td>
<td><p>ACE de permiso</p></td>
<td><p>None</p></td>
<td><p>Propiedad de lectura</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nombre distintivo del objeto: CN=Matrices,CN=\<grupo administrativo\>,CN=Grupos administrativos,CN=\<organización\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuenta</th>
<th>Tipo de ACE</th>
<th>Herencia</th>
<th>Permisos</th>
<th>En la propiedad/se aplica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Usuarios autenticados</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Ninguno</p></td>
<td><p>Mostrar contenidos</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nombre distintivo del objeto: CN=Grupos de disponibilidad de base de datos,CN=\<grupo administrativo\>,CN=Grupos administrativos,CN=\<organización\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuenta</th>
<th>Tipo de ACE</th>
<th>Herencia</th>
<th>Permisos</th>
<th>En la propiedad/se aplica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Usuarios autenticados</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Ninguno</p></td>
<td><p>Mostrar contenidos</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nombre distintivo del objeto: CN=Bases de datos,CN=\<grupo administrativo\>,CN=Grupos administrativos,CN=\<organización\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuenta</th>
<th>Tipo de ACE</th>
<th>Herencia</th>
<th>Permisos</th>
<th>En la propiedad/se aplica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Usuarios autenticados</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Ninguno</p></td>
<td><p>Mostrar contenidos</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nombre distintivo del objeto: CN=Servidores,CN=\<grupo administrativo\>,CN=Grupos administrativos,CN=\<organización\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuenta</th>
<th>Tipo de ACE</th>
<th>Herencia</th>
<th>Permisos</th>
<th>En la propiedad/se aplica a</th>
<th>Comentarios</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de denegación</p></td>
<td><p>Todo</p></td>
<td><p>Recibir como</p></td>
<td><p></p></td>
<td><p>Los servidores Exchange no tienen permiso para abrir buzones de correo.</p></td>
</tr>
<tr class="even">
<td><p>Usuarios autenticados</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Ninguno</p></td>
<td><p>Mostrar contenidos</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Permisos de contenedor de grupos de seguridad de Microsoft Exchange

Las tablas de permisos de esta sección muestran los permisos que se establecen en el contenedor de los grupos de seguridad de Microsoft Exchange dentro de la partición de dominio raíz.

### Nombre distintivo del objeto: OU=Grupos de seguridad de Microsoft Exchange,DC=\<dominio raíz\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuenta</th>
<th>Tipo de ACE</th>
<th>Herencia</th>
<th>Permisos</th>
<th>En la propiedad/se aplica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Control total</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Crear secundario</p></td>
<td><p><code>/ Group</code></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Eliminar</p></td>
<td><p><code>/ group</code></p></td>
</tr>
<tr class="even">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>Member / group</code></p></td>
</tr>
</tbody>
</table>


### Nombre distintivo del objeto: CN=Administración de la organización,OU=Grupos de seguridad de Microsoft Exchange,DC=\<dominio raíz\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuenta</th>
<th>Tipo de ACE</th>
<th>Herencia</th>
<th>Permisos</th>
<th>En la propiedad/se aplica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Control total</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nombre distintivo del objeto: CN=Administración de carpetas públicas,OU=Grupos de seguridad de Microsoft Exchange,DC=\<dominio raíz\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuenta</th>
<th>Tipo de ACE</th>
<th>Herencia</th>
<th>Permisos</th>
<th>En la propiedad/se aplica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Control total</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nombre distintivo del objeto: CN=ExchangeLegacyInterop,OU=Grupos de seguridad de Microsoft Exchange,DC=\<dominio raíz\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuenta</th>
<th>Tipo de ACE</th>
<th>Herencia</th>
<th>Permisos</th>
<th>En la propiedad/se aplica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Control total</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nombre distintivo del objeto: CN=Servidores de Exchange,OU=Grupos de seguridad de Microsoft Exchange,DC=\<dominio raíz\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuenta</th>
<th>Tipo de ACE</th>
<th>Herencia</th>
<th>Permisos</th>
<th>En la propiedad/se aplica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Control total</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Administradores de dominio raíz</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Miembros de lectura</p>
<p>Miembros de escritura</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Administradores de dominios secundarios</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Miembros de lectura</p>
<p>Miembros de escritura</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Preparar dominio

Las siguientes tablas muestran los permisos que se establecen al ejecutar el comando `Setup /PrepareDomain`.


> [!NOTE]
> Los permisos descritos en esta sección son los permisos predeterminados que se configuran al implementar Exchange&nbsp;2013 con el modelo de permisos compartidos. Si ha implementado Exchange&nbsp;2013 con el modelo de permisos divididos de Active Directory, el permiso predeterminado es diferente. Para obtener más información acerca de los cambios en los permisos predeterminados al usar permisos divididos de Active Directory y los modelos de permisos compartidos y divididos en general, vea <A href="understanding-split-permissions-exchange-2013-help.md">Active Directory split permissions</A> en <A href="understanding-split-permissions-exchange-2013-help.md">Descripción de los permisos divididos</A>. Si decide no usar los permisos divididos de Active Directory al instalar Exchange, Exchange utilizará los permisos compartidos.



### Nombre distintivo del objeto: DC=\<dominio\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuenta</th>
<th>Tipo de ACE</th>
<th>Herencia</th>
<th>Permisos</th>
<th>En la propiedad/se aplica a</th>
<th>Comentarios</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Usuarios autenticados</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de lectura</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>NT AUTHORITY\NETWORK</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de lectura</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p>Otorga permisos de lectura del servicio de transporte</p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>groupType</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchMailboxSecurityDescriptor</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchUMServerWritableFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de lectura</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de lectura</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchUserCultulre</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de lectura</p></td>
<td><p><code>memberOf</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de lectura</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de lectura</p></td>
<td><p><code>userAccountControl</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de lectura</p></td>
<td><p><code>canonicalName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Sincronización de replicación</p></td>
<td><p></p></td>
<td><p>Derecho extendido</p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Crear secundario</p>
<p>Eliminar secundario</p>
<p>Mostrar secundarios</p></td>
<td><p><code>msExchActiveSyncDevices / User</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Crear secundario</p>
<p>Eliminar secundario</p>
<p>Mostrar secundarios</p></td>
<td><p><code>msExchActiveSyncDevices / inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchSafeSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchMobileMailboxFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchSafeRecipientsHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>userCertificate</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchUMDtmfMap</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchBlockedSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchUMSpokenName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchUMPinChecksum</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>thumbnailPhoto</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Leer</p>
<p>Mostrar objeto</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>textEncodedORAddress</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>proxyAddresses</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>mail</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>displayNamePrintable</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>showInAddressBook</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Control total</p></td>
<td><p><code>/ msExchDynamicDistributionList</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>adminDisplayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>displayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Leer</p>
<p>Mostrar objeto</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>displayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>Public Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>adminDisplayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Control total</p></td>
<td><p><code>/ msExchDynamicDistributionList</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>textEncodedORAddress</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>showInAddressBook</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>proxyAddresses</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>displayNamePrintable</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>mail</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Permisos de Windows de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>pwdLastSet</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Permisos de Windows de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>WriteDACL</p></td>
<td><p><code>/ user</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Permisos de Windows de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>WriteDACL</p>
<p></p></td>
<td><p><code>/ inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Permisos de Windows de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Eliminar árbol</p></td>
<td><p><code>/ user</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Permisos de Windows de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Eliminar árbol</p>
<p></p></td>
<td><p><code>/ inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Permisos de Windows de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>sAMAccountName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Permisos de Windows de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Crear secundario</p>
<p>Eliminar</p></td>
<td><p><code>/ contact</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Permisos de Windows de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Crear secundario</p>
<p>Eliminar</p></td>
<td><p><code>/ inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Permisos de Windows de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Crear secundario</p>
<p>Eliminar</p></td>
<td><p><code>/ user</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Permisos de Windows de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Crear secundario</p>
<p>Eliminar</p></td>
<td><p><code>/ organizationUnit</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Permisos de Windows de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Crear secundario</p>
<p>Eliminar</p></td>
<td><p><code>/ group</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Permisos de Windows de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Crear secundario</p>
<p>Eliminar secundario</p></td>
<td><p><code>/ computer</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Permisos de Windows de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>Member</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Permisos de Windows de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>wwwHomePage</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Permisos de Windows de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>countryCode</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Permisos de Windows de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>userAccountControl</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Permisos de Windows de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>managedBy</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Permisos de Windows de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Restablecer la contraseña en el siguiente inicio de sesión</p></td>
<td><p></p></td>
<td><p>Derecho extendido</p></td>
</tr>
<tr class="even">
<td><p>Permisos de Windows de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Cambiar contraseña</p></td>
<td><p><code> / user</code></p></td>
<td><p>Derecho extendido</p></td>
</tr>
<tr class="odd">
<td><p>Configuración delegada</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de lectura</p></td>
<td><p><code>User Account Restrictions</code></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nombre distintivo del objeto: CN=AdminSDHolder,CN=Sistema,DC=\<dominio\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuenta</th>
<th>Tipo de ACE</th>
<th>Herencia</th>
<th>Permisos</th>
<th>En la propiedad/se aplica a</th>
<th>Comentarios</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Usuarios autenticados</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de lectura</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>NT AUTHORITY\NETWORK</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de lectura</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p>Otorga permisos de lectura del servicio de transporte</p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>groupType</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchMailboxSecurityDescriptor</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchUMServerWritableFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de lectura</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de lectura</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchUserCultulre</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de lectura</p></td>
<td><p><code>memberOf</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de lectura</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de lectura</p></td>
<td><p><code>userAccountControl</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de lectura</p></td>
<td><p><code>canonicalName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Sincronización de replicación</p></td>
<td><p></p></td>
<td><p>Derecho extendido</p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Crear secundario</p>
<p>Eliminar secundario</p>
<p>Mostrar secundarios</p></td>
<td><p><code>msExchActiveSyncDevices / User</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Crear secundario</p>
<p>Eliminar secundario</p>
<p>Mostrar secundarios</p></td>
<td><p><code>msExchActiveSyncDevices / inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchSafeSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchMobileMailboxFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchSafeRecipientsHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>userCertificate</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchUMDtmfMap</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchBlockedSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchUMSpokenName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchUMPinChecksum</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>thumbnailPhoto</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Leer</p>
<p>Mostrar objeto</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>textEncodedORAddress</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>proxyAddresses</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>mail</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>displayNamePrintable</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>showInAddressBook</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Control total</p></td>
<td><p><code>/ msExchDynamicDistributionList</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>adminDisplayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>displayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Leer</p>
<p>Mostrar objeto</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>displayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>Public Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>adminDisplayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Control total</p></td>
<td><p><code>/ msExchDynamicDistributionList</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>textEncodedORAddress</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>showInAddressBook</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>proxyAddresses</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>displayNamePrintable</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>mail</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Permisos de Windows de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>pwdLastSet</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Permisos de Windows de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>sAMAccountName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Permisos de Windows de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>Member</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Permisos de Windows de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>wwwHomePage</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Permisos de Windows de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>countryCode</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Permisos de Windows de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>userAccountControl</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Permisos de Windows de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>managedBy</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Configuración delegada</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de lectura</p></td>
<td><p><code>User Account Restrictions</code></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nombre distintivo del objeto: CN=Objetos eliminados,DC=\<dominio\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuenta</th>
<th>Tipo de ACE</th>
<th>Herencia</th>
<th>Permisos</th>
<th>En la propiedad/se aplica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Mostrar contenidos</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nombre distintivo del objeto: CN=Objetos de sistema de Microsoft Exchange,DC=\<dominio\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuenta</th>
<th>Tipo de ACE</th>
<th>Herencia</th>
<th>Permisos</th>
<th>En la propiedad/se aplica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NT AUTHORITY\NETWORK</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de lectura</p>
<p>Mostrar contenidos</p>
<p>Permisos de lectura</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Usuarios autenticados</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Permisos de lectura</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Usuarios autenticados</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de lectura</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
</tr>
<tr class="even">
<td><p>Usuarios autenticados</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de lectura</p></td>
<td><p><code>adminDisplayName</code></p></td>
</tr>
<tr class="odd">
<td><p>Usuarios autenticados</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de lectura</p></td>
<td><p><code>modifyTimeStamp</code></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de denegación</p></td>
<td><p>Todo</p></td>
<td><p>Eliminar árbol</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Permisos de lectura</p>
<p>Mostrar contenidos</p>
<p>Leer árbol PropertyDelete</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Crear secundario</p>
<p></p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Crear secundario</p>
<p>Eliminar secundario</p></td>
<td><p><code>/ publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Crear secundario</p>
<p></p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Eliminar secundario</p>
<p></p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Eliminar secundario</p>
<p></p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>/ publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Cambiar contraseña</p>
<p>Restablecer la contraseña en el siguiente inicio de sesión</p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Permisos de lectura</p>
<p>Mostrar contenidos</p>
<p>Propiedad de lectura</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Crear secundario</p>
<p>Eliminar secundario</p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="even">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Crear secundario</p>
<p>Eliminar secundario</p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="even">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>mail / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>displayNamePrintable / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>displayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>textEncodedORAddress / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>proxyAddresses / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>cn / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>showInAddressBook / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>Exchange Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p>legacyExchangeDN / publicFolder</p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>Exchange Personal Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>msDSPhoneticDisplayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>msExchPFContacts / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>garbageCollPeriod / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>name / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>msExchPublicDelegates / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Administración de carpetas públicas</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Permisos de lectura</p>
<p>Mostrar contenidos</p>
<p>Propiedad de lectura</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Administración de carpetas públicas</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>mail / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Administración de carpetas públicas</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>displayNamePrintable / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Administración de carpetas públicas</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>displayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Administración de carpetas públicas</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>textEncodedORAddress / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Administración de carpetas públicas</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>proxyAddresses / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Administración de carpetas públicas</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>cn / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Administración de carpetas públicas</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>showInAddressBook / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Administración de carpetas públicas</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>Exchange Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Administración de carpetas públicas</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>legacyExchangeDN / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Administración de carpetas públicas</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>Exchange Personal Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Administración de carpetas públicas</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>msDSPhoneticDisplayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Administración de carpetas públicas</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>msExchPFContacts / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Administración de carpetas públicas</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>garbageCollPeriod / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Administración de carpetas públicas</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>name / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Administración de carpetas públicas</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>msExchPublicDelegates / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Permisos de lectura</p>
<p>Mostrar contenidos</p>
<p>Propiedad de lectura</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>mail / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>displayNamePrintable / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>displayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>textEncodedORAddress / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>proxyAddresses / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>cn / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>showInAddressBook / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>Exchange Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>legacyExchangeDN / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>Exchange Personal Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>msDSPhoneticDisplayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>msExchPFContacts / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>garbageCollPeriod / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>name / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Subsistema de confianza de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p>
<p>Propiedad de escritura</p></td>
<td><p><code>msExchPublicDelegates / publicFolder</code></p></td>
</tr>
</tbody>
</table>


### Nombre distintivo del objeto: CN=Servidores de dominio de instalación de Exchange,CN=Objetos de sistema de Microsoft Exchange,DC=\<dominio\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuenta</th>
<th>Tipo de ACE</th>
<th>Herencia</th>
<th>Permisos</th>
<th>En la propiedad/se aplica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Control total</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Instalación de rol de servidor

Durante la instalación de los roles de servidor Buzón de correo y Acceso de cliente, el programa de instalación agrega el grupo de seguridad universal de administración de la organización al grupo de seguridad del administrador en el equipo local para que los miembros del grupo de roles de administración denominado Administración de la organización pueda administrar el servidor.

En la siguiente tabla de permisos se muestran los permisos que se establecen al instalar los roles de servidor Acceso de cliente o Buzón de correo.

### Nombre distintivo del objeto: CN=\<servidor\>,CN=Servidores,CN=\<grupo administrativo\>,CN=Grupos administrativos,CN=\<organización\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuenta</th>
<th>Tipo de ACE</th>
<th>Herencia</th>
<th>Permisos</th>
<th>En la propiedad/se aplica a</th>
<th>Comentarios</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MACHINE$</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Permisos de lectura</p>
<p>Mostrar contenidos</p>
<p>Propiedad de lectura</p>
<p>Mostrar objeto</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>MACHINE$</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Ninguno</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p><code>msExchServerSite</code></p>
<p><code>msExchEdgeSyncCredential</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Almacenar acceso de transporte</p>
<p>Almacenar delegación limitada</p>
<p>Almacenar acceso de sólo lectura</p>
<p>Almacenar acceso de escritura y lectura</p></td>
<td><p></p></td>
<td><p>Derechos extendidos</p></td>
</tr>
<tr class="even">
<td><p>NT AUTHORITY\NETWORK</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Serialización de token de servicios Web Exchange</p></td>
<td><p></p></td>
<td><p>Derecho extendido</p>
<p>Sólo se otorga en objetos del rol de servidor Buzón de correo.</p></td>
</tr>
<tr class="odd">
<td><p>NT AUTHORITY\NETWORK</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Permisos de lectura</p>
<p>Mostrar contenidos</p>
<p>Propiedad de lectura</p>
<p>Mostrar objeto</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Sistema local</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Permisos de lectura</p>
<p>Mostrar contenidos</p>
<p>Propiedad de lectura</p>
<p>Mostrar objeto</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Configuración delegada</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Control total</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Configuración delegada</p></td>
<td><p>ACE de denegación</p></td>
<td><p>Todo</p></td>
<td><p>Crear secundario</p>
<p>Eliminar secundario</p></td>
<td><p><code>/ msExchPublicMDB</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Usuarios autenticados</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de lectura</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Configuración delegada</p></td>
<td><p>ACE de denegación</p></td>
<td><p>Todo</p></td>
<td><p>Recibir como</p>
<p>Enviar como</p></td>
<td><p></p></td>
<td><p>Derecho extendido</p></td>
</tr>
</tbody>
</table>


## Grupos de disponibilidad de base de datos

Las tablas de permisos de esta sección muestran los permisos que se establecen en referencia a los grupos de disponibilidad de base de datos y sus miembros.

### Nombre distintivo del objeto: CN=\<DAGName\>,CN=Grupos de disponibilidad de base de datos,CN=\<grupo administrativo\>,CN=Grupos administrativos,CN=\<organización\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuenta</th>
<th>Tipo de ACE</th>
<th>Herencia</th>
<th>Permisos</th>
<th>En la propiedad/se aplica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Usuarios autenticados</p></td>
<td><p>ACE de permiso</p></td>
<td><p>None</p></td>
<td><p>Propiedad de lectura</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Transporte perimetral

Si instala un servidor Transporte perimetral y establece una suscripción perimetral con la organización de Exchange, los permisos de la siguiente tabla se adquieren al crear una instancia del servidor Transporte perimetral en la organización.

### Nombre distintivo del objeto: CN=\<servidor\>,CN=Servidores,CN=\<grupo administrativo\>,CN=Grupos administrativos,CN=\<organización\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuenta</th>
<th>Tipo de ACE</th>
<th>Herencia</th>
<th>Permisos</th>
<th>En la propiedad/se aplica a</th>
<th>Comentarios</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Propiedad de escritura</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Usuarios autenticados</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Ninguno</p></td>
<td><p>Propiedades de lectura</p></td>
<td><p></p></td>
<td><p>La ACE se define en el esquema para objetos de clase de <code>msExchExchangeServer</code><code>defaultSecurityDescriptor</code></p></td>
</tr>
</tbody>
</table>


## Instalación del servidor de Buzón de correo

Durante la instalación del primer servidor de buzones de correo, se crean los siguientes contenedores si aún no existen. La siguiente tabla de permisos muestra los permisos que se aplican.

### Nombre distintivo del objeto: CN=Configuración de disponibilidad,CN=\<organización\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuenta</th>
<th>Tipo de ACE</th>
<th>Herencia</th>
<th>Permisos</th>
<th>En la propiedad/se aplica a</th>
<th>Comentarios</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Descripción</p></td>
<td><p>Propiedad de lectura</p></td>
<td><p><code>msExchAvailabilityUserPassword / msExchAvailabilityAddressSpaceObjects</code></p></td>
<td><p>Derecho extendido</p></td>
</tr>
</tbody>
</table>


### Nombre distintivo del objeto: CN=Predeterminado\<Servidor\>,CN=Conectores de recepción SMTP,CN=Protocolos,CN=\<Servidor\>,CN=Servidores,CN=\<grupo administrativo\>,CN=\<organización\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuenta</th>
<th>Tipo de ACE</th>
<th>Herencia</th>
<th>Permisos</th>
<th>En la propiedad/se aplica a</th>
<th>Comentarios</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE de denegación</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar encabezados de bosque</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE de denegación</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar encabezados de organización</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar todos los remitentes</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar todos los remitentes</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar todos los remitentes</p></td>
<td><p></p></td>
<td><p>Es el conocido identificador de seguridad (SID) para los servidores de buzones de correo.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar todos los remitentes</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar todos los remitentes</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores protegidos externamente.</p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar EXCH50</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar EXCH50</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar EXCH50</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar EXCH50</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar EXCH50</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores protegidos externamente.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar mensajes a cualquier destinatario</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar mensajes a cualquier destinatario</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar mensajes a cualquier destinatario</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar mensajes a cualquier destinatario</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar mensajes a cualquier destinatario</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores protegidos externamente.</p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar XShadow</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar XShadow</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar encabezados de enrutamiento</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar encabezados de enrutamiento</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar encabezados de enrutamiento</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar encabezados de enrutamiento</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar encabezados de enrutamiento</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores protegidos externamente.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar XSessionParams</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar XSessionParams</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar XSessionParams</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar encabezados de bosque</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar encabezados de bosque</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar encabezados de bosque</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar xAttr</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar xAttr</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar xAttr</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Accept XProxyFrom</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar el bosque XProxyFrom</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar el bosque XProxyFrom</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar XSysProbe</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar el bosque XSysProbe</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar el bosque XSysProbe</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar propiedades extendidas de XMessageContext</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar propiedades extendidas de XMessageContext</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar propiedades extendidas de XMessageContext</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar el índice Fast XMessageContext</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar el índice Fast XMessageContext</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar el índice Fast XMessageContext</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar caché de destinatarios de AD de XMessageContext</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar caché de destinatarios de AD de XMessageContext</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar caché de destinatarios de AD de XMessageContext</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar el marcador de autenticación</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar el marcador de autenticación</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar el marcador de autenticación</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar el marcador de autenticación</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar el marcador de autenticación</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores protegidos externamente.</p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Omitir filtros contra correo no deseado</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Omitir filtros contra correo no deseado</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Omitir filtros contra correo no deseado</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Omitir filtros contra correo no deseado</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Omitir filtros contra correo no deseado</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores protegidos externamente.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Omitir tamaño límite de mensajes</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Omitir tamaño límite de mensajes</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Omitir tamaño límite de mensajes</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Omitir tamaño límite de mensajes</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Omitir tamaño límite de mensajes</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores protegidos externamente.</p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar encabezados de organización</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar encabezados de organización</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar encabezados de organización</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar mensajes al servidor</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar mensajes al servidor</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar mensajes al servidor</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar mensajes al servidor</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar mensajes al servidor</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores protegidos externamente.</p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar remitentes de dominios autoritativos</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar remitentes de dominios autoritativos</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar remitentes de dominios autoritativos</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar remitentes de dominios autoritativos</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar remitentes de dominios autoritativos</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores protegidos externamente.</p></td>
</tr>
<tr class="odd">
<td><p>Usuarios autenticados</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar mensajes a cualquier destinatario</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Usuarios autenticados</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar encabezados de enrutamiento</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Usuarios autenticados</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Omitir filtros contra correo no deseado</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Usuarios autenticados</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar mensajes al servidor</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nombre distintivo del objeto: CN=Cliente \<Servidor\>,CN=Conectores de recepción SMTP,CN=Protocolos,CN=\<Servidor\>,CN=Servidores,CN=\<grupo administrativo\>,CN=\<organización\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuenta</th>
<th>Tipo de ACE</th>
<th>Herencia</th>
<th>Permisos</th>
<th>En la propiedad/se aplica a</th>
<th>Comentarios</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Usuarios autenticados</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar mensajes a cualquier destinatario</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Usuarios autenticados</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar encabezados de enrutamiento</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Usuarios autenticados</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Omitir filtros contra correo no deseado</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Usuarios autenticados</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar mensajes al servidor</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar XSessionParams</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar XSessionParams</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar XSessionParams</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar todos los remitentes</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar todos los remitentes</p></td>
<td><p></p></td>
<td><p>Es el conocido identificador de seguridad (SID) para los servidores de buzones de correo.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar todos los remitentes</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar todos los remitentes</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores protegidos externamente.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar Exch50</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar Exch50</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar Exch50</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores protegidos externamente.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar Exch50</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar mensajes a cualquier destinatario</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar mensajes a cualquier destinatario</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar mensajes a cualquier destinatario</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar mensajes a cualquier destinatario</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar mensajes a cualquier destinatario</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores protegidos externamente.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar XShadow</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar XShadow</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar encabezados de enrutamiento</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar encabezados de enrutamiento</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar encabezados de enrutamiento</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar encabezados de enrutamiento</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar encabezados de enrutamiento</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores protegidos externamente.</p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar encabezados de bosque</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar encabezados de bosque</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar encabezados de bosque</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar xAttr</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar xAttr</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar xAttr</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Accept XProxyFrom</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar el bosque XProxyFrom</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar el bosque XProxyFrom</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar el marcador de autenticación</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar el marcador de autenticación</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar el marcador de autenticación</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar el marcador de autenticación</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores protegidos externamente.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar XSysProbe</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar el bosque XSysProbe</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar el bosque XSysProbe</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar el marcador de autenticación</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores protegidos externamente.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Omitir filtros contra correo no deseado</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Omitir filtros contra correo no deseado</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Omitir filtros contra correo no deseado</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Omitir filtros contra correo no deseado</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores protegidos externamente.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar propiedades extendidas de XMessageContext</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar propiedades extendidas de XMessageContext</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar propiedades extendidas de XMessageContext</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar el índice Fast XMessageContext</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar el índice Fast XMessageContext</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar el índice Fast XMessageContext</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Omitir tamaño límite de mensajes</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Omitir tamaño límite de mensajes</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Omitir tamaño límite de mensajes</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Omitir tamaño límite de mensajes</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores protegidos externamente.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar encabezados de organización</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar encabezados de organización</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar encabezados de organización</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar caché de destinatarios de AD de XMessageContext</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar caché de destinatarios de AD de XMessageContext</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar caché de destinatarios de AD de XMessageContext</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar mensajes al servidor</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar mensajes al servidor</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar mensajes al servidor</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar mensajes al servidor</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores protegidos externamente.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar remitentes de dominios autoritativos</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar remitentes de dominios autoritativos</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar remitentes de dominios autoritativos</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Aceptar remitentes de dominios autoritativos</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores protegidos externamente.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Creación de conector de envío SMTP

En la siguiente tabla se muestran los permisos que se establecen al crear conectores de envío.

### Nombre distintivo del objeto: CN=\<Nombre del conector\>,CN=Conexiones,CN=\<grupo de enrutamiento\>,CN=Grupos de enrutamiento, CN=\<grupo administrativo\>,CN=\<organización\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuenta</th>
<th>Tipo de ACE</th>
<th>Herencia</th>
<th>Permisos</th>
<th>En la propiedad/se aplica a</th>
<th>Comentarios</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NT AUTHORITY\ANONYMOUS LOGON</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar encabezados de enrutamiento</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar encabezados de organización</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar encabezados de organización</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar encabezados de organización</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar encabezados de bosque</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar encabezados de bosque</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar encabezados de bosque</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="even">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar XShadow</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar XShadow</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar XShadow</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar encabezados de enrutamiento</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-10</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar encabezados de enrutamiento</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores asociados.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar encabezados de enrutamiento</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar encabezados de enrutamiento</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar encabezados de enrutamiento</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores protegidos externamente.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-24</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar encabezados de enrutamiento</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de Exchange heredados.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores de Exchange</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar Exch50</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar Exch50</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de buzones de correo.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar Exch50</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores Transporte perimetral.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar Exch50</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores protegidos externamente.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-24</p></td>
<td><p>ACE de permiso</p></td>
<td><p>Todo</p></td>
<td><p>Enviar Exch50</p></td>
<td><p></p></td>
<td><p>Es el conocido SID para los servidores de Exchange heredados.</p></td>
</tr>
</tbody>
</table>

