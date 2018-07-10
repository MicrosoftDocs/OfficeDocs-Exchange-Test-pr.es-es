---
title: 'Preparar Active Directory y los dominios: Exchange 2013 Help'
TOCTitle: Preparar Active Directory y los dominios
ms:assetid: f895e1ce-d766-4352-ac46-ec959c9954a9
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb125224(v=EXCHG.150)
ms:contentKeyID: 48268899
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Preparar Active Directory y los dominios

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Antes de instalar Microsoft Exchange Server 2013, debe prepararse el bosque de Active Directory y sus dominios. Exchange necesita preparar Active Directory para poder almacenar información sobre los buzones de los usuarios y la configuración de los servidores de Exchange de la organización. Si no está familiarizado con los dominios o los bosques de Active Directory, vea [Introducción a los Servicios de dominio de Active Directory](https://go.microsoft.com/fwlink/p/?linkid=399226).


> [!NOTE]
> Tanto si se trata de la primera instalación de Exchange en su entorno como si ya tiene versiones anteriores de Exchange Server ejecutándose, necesita preparar Active Directory para Exchange 2013. Puede ver <A href="exchange-2013-active-directory-schema-changes-exchange-2013-help.md">Cambios en el esquema de Active Directory de Exchange&nbsp;2013</A> para obtener detalles sobre las nuevas clases de esquema y atributos que Exchange 2013 agrega a Active Directory, incluidos los que se realizan mediante Service Packs (SP) y actualizaciones acumulativas (CU).



Puede preparar Active Directory para Exchange con un par de procedimientos. El primero consiste en delegar en el asistente para la instalación de Exchange 2013. Si la implementación de Active Directory no es muy extensa y no cuenta con un equipo independiente para administrar Active Directory, se recomienda usar el asistente. Deberá usar una cuenta que sea miembro de los grupos de seguridad Administradores de esquema y Administradores de empresa. Para más información sobre cómo usar el asistente para la instalación, vea [Instalar Exchange 2013 utilizando el asistente de configuración](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md).

Si la implementación de Active Directory es extensa o un equipo independiente administra Active Directory, este es su tema. Siga los pasos de este tema para controlar mejor las distintas fases de preparación y obtener información sobre quién puede realizar cada paso. Por ejemplo, tal vez los administradores de Exchange no dispongan de los permisos necesarios para extender el esquema de Active Directory.

¿Qué necesita saber antes de comenzar?

1\. Extender el esquema de Active Directory

2\. Preparar Active Directory

3\. Preparar los dominios de Active Directory

¿Cómo saber si el proceso se ha completado correctamente?

¿Le interesa saber lo que sucede cuando Active Directory se prepara para Exchange? Vea [¿Qué cambia en Active Directory cuando Exchange 2013 está instalado?](what-changes-in-active-directory-when-exchange-2013-is-installed-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: De 10 a 15 minutos o más (sin incluir la replicación de Active Directory), según el tamaño de la organización y el número de dominios secundarios

  - El equipo que use para ejecutar estos pasos debe cumplir los [Requisitos del sistema para Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md). Además, el bosque de Active Directory debe cumplir los requisitos de la sección "Servidores de directorios y redes" de [Requisitos del sistema para Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

  - Si la organización cuenta con varios dominios de Active Directory, se recomienda lo siguiente:
    
      - Realizar los pasos que se citan a continuación desde un sitio de Active Directory que disponga de un servidor de Active Directory de cada dominio.
    
      - Instalar el primer servidor de Exchange en un sitio de Active Directory con un servidor de catálogo global grabable de cada dominio.


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 1\. Extender el esquema de Active Directory

El primer paso al preparar una organización para Exchange 2013 es extender el esquema de Active Directory. Exchange almacena mucha información en Active Directory, pero para poder hacerlo deben agregarse y actualizarse clases, atributos y otros elementos. Si le interesa saber lo que ha cambiado al extender el esquema, vea [Cambios en el esquema de Active Directory de Exchange 2013](exchange-2013-active-directory-schema-changes-exchange-2013-help.md).

Antes de extender el esquema, tenga en cuenta lo siguiente:

  - La cuenta con la que inicie sesión debe ser miembro de los grupos de seguridad Administradores de esquema y Administradores de empresa.

  - El equipo donde ejecute el comando para ampliar el esquema debe encontrarse en el mismo sitio y el mismo dominio de Active Directory que el maestro de esquema.

  - Si usa el parámetro *DomainController*, asegúrese de especificar el nombre del controlador de dominio que actúa como maestro de esquema.

  - Solo se puede extender el esquema de Exchange con los pasos de este tema o mediante el programa de instalación de Exchange 2013. No existen otros procedimientos compatibles para extender el esquema.


> [!TIP]
> Si no cuenta con un equipo independiente que administre el esquema de Active Directory, puede omitir este paso y acceder directamente a Preparar Active Directory. Si no se extiende el esquema en el paso 1, los comandos del paso 2 lo harán por usted. Aunque decida omitir el paso 1, deberá tener en cuenta igualmente las consideraciones anteriores.



Cuando esté listo, haga lo siguiente para ampliar el esquema de Active Directory. Si dispone de varios bosques de Active Directory, asegúrese de iniciar sesión en el bosque correcto.

1.  Compruebe que el equipo está listo para ejecutar el programa de instalación de Exchange 2013. Para más información sobre los requisitos necesarios para ejecutar el programa de instalación, vea la sección [Active Directory preparation](exchange-2013-prerequisites-exchange-2013-help.md) de [Requisitos previos de Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).

2.  Abra una ventana del símbolo del sistema de Windows y vaya a la ubicación donde descargó los archivos de instalación de Exchange.

3.  Para extender el esquema, ejecute el comando siguiente.
    
        Setup.exe /PrepareSchema /IAcceptExchangeServerLicenseTerms

Cuando el programa de instalación termine de extender el esquema, deberá esperar mientras Active Directory replica los cambios a todos los controladores de dominio. Si quiere comprobar el estado de la replicación, puede usar la herramienta `repadmin`. `Repadmin` forma parte de la característica Herramientas de los Servicios de dominio de Active Directory en Windows Server 2012 R2, Windows Server 2012 y Windows Server 2008 R2. Para obtener más información sobre cómo usarla, vea [Repadmin](https://go.microsoft.com/fwlink/p/?linkid=257879).

## 2\. Preparar Active Directory

Una vez extendido el esquema de Active Directory, ya puede preparar otros elementos de Active Directory para Exchange 2013. Durante este paso, Exchange creará contenedores, objetos y otros elementos de Active Directory donde se almacenará la información. La colección de todos los contenedores, objetos, atributos, etc., de Exchange se conoce como *organización de Exchange*.

Antes de preparar Active Directory para Exchange, tenga en cuenta lo siguiente:

  - La cuenta con la que inicie sesión debe ser miembro del grupo de seguridad Administradores de empresa. Si ha omitido el paso 1 para que el comando *PrepareAD* extienda el esquema, la cuenta que use también debe ser miembro del grupo de seguridad Administradores de esquema.

  - El equipo donde ejecute el comando debe encontrarse en el mismo sitio y el mismo dominio de Active Directory que el maestro de esquema. También deberá ponerse en contacto con todos los dominios del bosque en el puerto TCP 389.

  - Antes de realizar este paso, espere hasta que Active Directory replique los cambios del paso 1 a todos los controladores de dominio.

Al ejecutar el comando siguiente para preparar Active Directory para Exchange, necesitará asignar un nombre a la organización de Exchange. Este nombre se usa de forma interna en Exchange y, por lo general, resulta visible para los usuarios. Es frecuente usar como nombre de organización el nombre de la compañía donde se está instalando Exchange. El nombre que use no afectará a la funcionalidad de Exchange ni determinará qué puede usar o no para las direcciones de correo electrónico. Puede asignar el nombre que desee, pero tenga en cuenta lo siguiente:

  - Puede usar todas las letras mayúsculas o minúsculas de la A a la Z.

  - Puede usar los números del 0 al 9.

  - El nombre puede contener espacios, siempre que no se sitúen al principio o al final de este.

  - Puede usar guiones.

  - El nombre puede contener hasta un máximo de 64 caracteres y no puede estar vacío.

  - Una vez se establece, el nombre no se puede cambiar.

Cuando esté listo, haga lo siguiente para preparar Active Directory para Exchange. Si el nombre de organización que desea usar contiene espacios, escríbalo entre comillas (").

1.  Abra una ventana del símbolo del sistema de Windows y vaya a la ubicación donde descargó los archivos de instalación de Exchange.

2.  Ejecute el comando siguiente:
    
        Setup.exe /PrepareAD /OrganizationName:"<organization name>" /IAcceptExchangeServerLicenseTerms

Cuando el programa de instalación termine de preparar Active Directory para Exchange, deberá esperar mientras Active Directory replica los cambios a todos los controladores de dominio. Si quiere comprobar el estado de la replicación, puede usar la herramienta `repadmin`. `repadmin` forma parte de la característica Herramientas de los Servicios de dominio de Active Directory en Windows Server 2012 R2, Windows Server 2012 y Windows Server 2008 R2. Para obtener más información sobre cómo usarla, vea [Repadmin](https://go.microsoft.com/fwlink/p/?linkid=257879).

## 3\. Preparar los dominios de Active Directory

El último paso para dejar Active Directory listo para Exchange consiste en preparar los distintos dominios de Active Directory en la ubicación donde se instalará Exchange, o donde se encontrarán los usuarios habilitados para correo. Este paso crea grupos de seguridad y contenedores adicionales y establece los permisos para que Exchange pueda acceder a ellos.

Si dispone de varios dominios en el bosque de Active Directory, puede elegir entre un par de procedimientos para prepararlos. Seleccione la opción que satisfaga sus necesidades. Si solo dispone de un dominio, puede omitir este paso porque el comando *PrepareAD* del paso 2 preparó el dominio por usted.

## Preparar todos los dominios del bosque de Active Directory

Para preparar todos los dominios de Active Directory, use el parámetro *PrepareAllDomains* al ejecutar el programa de instalación. El programa preparará por usted todos los dominios para Exchange en el bosque de Active Directory.

Antes de preparar todos los dominios en el bosque de Active Directory, tenga en cuenta lo siguiente:

  - La cuenta que use debe ser miembro del grupo de seguridad Administradores de empresa.

  - Espere hasta que Active Directory replique los cambios del paso 2 a todos los controladores de dominio. De no hacerlo así, podría generarse un error cuando intente preparar el dominio.

Cuando esté listo, haga lo siguiente para preparar todos los dominios en el bosque de Active Directory para Exchange.

1.  Abra una ventana del símbolo del sistema de Windows y vaya a la ubicación donde descargó los archivos de instalación de Exchange.

2.  Ejecute el comando siguiente:
    
        Setup.exe /PrepareAllDomains /IAcceptExchangeServerLicenseTerms

## Elegir los dominios de Active Directory que deben prepararse

Si desea elegir los dominios de Active Directory que desea preparar, use el parámetro *PrepareDomain* al ejecutar el programa de instalación. Si usa el parámetro *PrepareDomain*, incluya el nombre de dominio completo (FQDN) del dominio que desee preparar.

Antes de preparar los dominios en el bosque de Active Directory, tenga en cuenta lo siguiente:

  - La cuenta que use deberá disponer de unos permisos u otros dependiendo de la fecha de creación del dominio.
    
      - **El dominio se creó antes de ejecutar PrepareAD**   Si el dominio se creó **antes** de ejecutar el comando *PrepareAD* del paso 2, la cuenta que use debe ser miembro del grupo Admins. del dominio en el dominio que desea preparar.
    
      - **El dominio se creó después de ejecutar PrepareAD**   Si el dominio se creó **después** de ejecutar el comando *PrepareAD* del paso 2, la cuenta que use debe ser miembro del grupo de roles Administración de la organización y del grupo Admins. del dominio en el dominio que desea preparar.

  - Espere hasta que Active Directory replique los cambios del paso 2 a todos los controladores de dominio. De no hacerlo así, podría generarse un error cuando intente preparar el dominio.

  - Debe preparar todos los dominios en los que se instalará un servidor de Exchange. También necesitará preparar todos los dominios que contengan usuarios habilitados para correo (aunque no contengan servidores de Exchange).

  - No es necesario ejecutar el comando *PrepareDomain* en el dominio donde se ejecutó el comando *PrepareAD*. El comando *PrepareAD* prepara ese dominio automáticamente.

Cuando esté listo, haga lo siguiente para preparar un dominio individual en el bosque de Active Directory para Exchange.

1.  Abra una ventana del símbolo del sistema de Windows y vaya a la ubicación donde descargó los archivos de instalación de Exchange.

2.  Ejecute el comando siguiente. Incluya el FQDN del dominio que desea preparar (no lo incluya si desea preparar el dominio en el que está ejecutando el comando).
    
        Setup.exe /PrepareDomain:<FQDN of the domain you want to prepare> /IAcceptExchangeServerLicenseTerms

3.  Repita los pasos para cada dominio de Active Directory donde desee instalar un servidor de Exchange o donde se ubicarán los usuarios habilitados para correo.

## ¿Cómo saber si el proceso se ha completado correctamente?

Tras realizar todos los pasos anteriores, puede comprobar que todas las operaciones se han realizado correctamente. Para ello, use una herramienta denominada editor de interfaces del servicio de Active Directory (Editor ADSI). El Editor ADSI forma parte de la característica Herramientas de los Servicios de dominio de Active Directory en Windows Server 2012 R2, Windows Server 2012 y Windows Server 2008 R2. Para obtener más información sobre esta herramienta, vea [ADSI Edit (adsiedit.msc)](https://go.microsoft.com/fwlink/p/?linkid=294644).


> [!WARNING]
> Nunca cambie valores en el Editor ADSI a menos que así se le indique desde el soporte técnico de Microsoft. Si cambia estos valores, puede causar un daño irreparable en Active Directory y en la organización de Exchange.



Después de que Exchange amplía el esquema de Active Directory y prepara Active Directory para Exchange, se actualizan varias propiedades para mostrar que la preparación está completa. Revise la información de la lista siguiente para asegurarse de que estas propiedades tienen los valores correctos. Cada propiedad debe coincidir con el valor en la tabla siguiente para la versión de Exchange 2013 que va a instalar.

  - En el contexto de nomenclatura **Esquema**, compruebe que la propiedad **rangeUpper** en **ms-Exch-Schema-Verision-Pt** tiene el valor que se muestra en la tabla de Versiones de Active Directory de Exchange 2013 para su versión de Exchange 2013.
    
     

  - En el contexto de nomenclatura **Configuración**, compruebe que la propiedad **objectVersion** en el contenedor CN=\<*your organization*\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<*domain*\> tiene el valor que se muestra en la tabla de Versiones de Active Directory de Exchange 2013 para su versión de Exchange 2013.
    
     

  - En el contexto de nomenclatura **Predeterminado**, compruebe que la propiedad **objectVersion** en el contenedor **Objetos de sistema de Microsoft Exchange** de DC=\<*root domain* tiene el valor que se muestra en la tabla de Versiones de Active Directory de Exchange 2013 para su versión de Exchange 2013.
    
     

También puede consultar el registro de instalación de Exchange para comprobar que la preparación de Active Directory se ha completado correctamente. Para obtener más información, consulte [Comprobar una instalación de Exchange 2013](verify-an-exchange-2013-installation-exchange-2013-help.md). No podrá usar el cmdlet **Get-ExchangeServer** mencionado en el tema [Comprobar una instalación de Exchange 2013](verify-an-exchange-2013-installation-exchange-2013-help.md) hasta que haya completado la instalación de, al menos, un rol de servidor de Buzón de correo y otro de Acceso de clientes en un sitio de Active Directory.

## Versiones de Active Directory de Exchange 2013

La tabla siguiente muestra los objetos de Exchange 2013 en Active Directory que se actualizan cada vez que se instala una versión nueva de Exchange 2013. Puede comparar las versiones de los objetos que aparecen con los valores de la tabla siguiente para comprobar que la versión de Exchange 2013 que ha instalado ha actualizado correctamente Active Directory durante la instalación.


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
<th> </th>
<th>Versión de Exchange</th>
<th>rangeUpper</th>
<th>objectVersion</th>
<th>objectVersion</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Contexto de nomenclatura</strong></p></td>
<td><p> </p></td>
<td><p>Schema</p></td>
<td><p>Default</p></td>
<td><p>Configuration</p></td>
</tr>
<tr class="even">
<td><p><strong>Contenedor</strong></p></td>
<td><p> </p></td>
<td><p>ms-Exch-Schema-Version-Pt</p></td>
<td><p>Objetos de sistema de Microsoft Exchange</p></td>
<td><p>CN=&lt;<em>your organization</em>&gt;, CN=Microsoft Exchange, CN=Services, CN=Configuration, DC=&lt;<em>domain</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Exchange 2013 CU10 y posterior</p></td>
<td><p>15312</p></td>
<td><p>13236</p></td>
<td><p>16130</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Exchange 2013 CU9</p></td>
<td><p>15312</p></td>
<td><p>13236</p></td>
<td><p>15965</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Exchange 2013 CU8</p></td>
<td><p>15312</p></td>
<td><p>13236</p></td>
<td><p>15965</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Exchange 2013 CU7</p></td>
<td><p>15312</p></td>
<td><p>13236</p></td>
<td><p>15965</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Exchange 2013 CU6</p></td>
<td><p>15303</p></td>
<td><p>13236</p></td>
<td><p>15965</p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Exchange 2013 CU5</p></td>
<td><p>15300</p></td>
<td><p>13236</p></td>
<td><p>15870</p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Exchange 2013 SP1</p></td>
<td><p>15292</p></td>
<td><p>13236</p></td>
<td><p>15844</p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Exchange 2013 CU3</p></td>
<td><p>15283</p></td>
<td><p>13236</p></td>
<td><p>15763</p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Exchange 2013 CU2</p></td>
<td><p>15281</p></td>
<td><p>13236</p></td>
<td><p>15688</p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Exchange 2013 CU1</p></td>
<td><p>15254</p></td>
<td><p>13236</p></td>
<td><p>15614</p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Exchange 2013 RTM</p></td>
<td><p>15137</p></td>
<td><p>13236</p></td>
<td><p>15449</p></td>
</tr>
</tbody>
</table>

