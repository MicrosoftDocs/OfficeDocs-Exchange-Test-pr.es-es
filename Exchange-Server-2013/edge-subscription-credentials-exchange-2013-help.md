---
title: 'Credenciales de suscripción perimetral: Exchange 2013 Help'
TOCTitle: Credenciales de suscripción perimetral
ms:assetid: 1d291bc1-9c00-4d1b-8da0-cb81f63d8305
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb266959(v=EXCHG.150)
ms:contentKeyID: 61183322
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Credenciales de suscripción perimetral

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

En este tema se explica cómo el proceso de suscripción perimetral establece las credenciales utilizadas para ayudar a proteger el proceso de sincronización de EdgeSync y cómo EdgeSync usa esas credenciales para establecer una conexión de LDAP segura entre un servidor de buzones de correo de Exchange 2013 y un servidor Transporte perimetral. Para obtener más información acerca del proceso de suscripciones perimetrales, vea [Suscripciones perimetrales](edge-subscriptions-exchange-2013-help.md).

**Contenido**

Proceso de suscripción perimetral

Cuentas de replicación de EdgeSync

Autenticación de replicación inicial

Autenticación de sesiones de sincronización programadas

Renovación de cuentas de replicación de EdgeSync

## Proceso de suscripción perimetral

El servidor Transporte perimetral se suscribe a un sitio de Active Directory para establecer una relación de sincronización entre los servidores de buzones de correo en un sitio de Active Directory y el servidor Transporte perimetral suscrito. Las credenciales que se establecen en el proceso de suscripción perimetral se usan para proteger la conexión LDAP entre un servidor de buzones de correo y un servidor Transporte perimetral de la red perimetral.

Cuando se ejecuta el cmdlet **New-EdgeSubscription** en un servidor Transporte perimetral, las credenciales de la cuenta de replicación de inicio de EdgeSync (ESBRA) se crean en el directorio de Active Directory Lightweight Directory Services (AD LDS) del servidor local y, a continuación, se escriben en el archivo de suscripción perimetral. Dichas credenciales únicamente se usan para establecer la sincronización inicial y expiran 24 horas después de haberse creado el archivo de suscripción perimetral. Si el proceso de suscripción perimetral no se ha completado en un plazo de 24 horas, tendrá que volver a ejecutar el cmdlet **New-EdgeSubscription** para crear un nuevo archivo de suscripción perimetral. El archivo XML de suscripción perimetral almacena datos de configuración para la suscripción perimetral.

El archivo XML de suscripción perimetral contiene los datos que se muestran en la siguiente tabla.

### Contenidos del archivo de suscripción perimetral

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Datos de suscripción</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Nombre del servidor perimetral</strong></p></td>
<td><p>Nombre NetBIOS del servidor de transporte perimetral. El nombre de la suscripción perimetral de Active Directory coincidirá con este nombre.</p></td>
</tr>
<tr class="even">
<td><p><strong>FQDN del servidor perimetral</strong></p></td>
<td><p>El nombre completo de dominio (FQDN) del servidor de transporte perimetral. Los servidores de buzones de correo del sitio de Active Directory suscrito deben poder localizar el servidor Transporte perimetral mediante DNS para resolver el FQDN.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Blob del certificado perimetral</strong></p></td>
<td><p>La clave pública del certificado autofirmado del servidor de transporte perimetral.</p></td>
</tr>
<tr class="even">
<td><p><strong>Nombre de usuario de ESRA</strong></p></td>
<td><p>El nombre asignado a la ESBRA. La cuenta ESBRA tiene el siguiente formato: ESRA.<em>Nombre del servidor de transporte perimetral</em>. ESRA significa cuenta de replicación de EdgeSync; tenga en cuenta la diferencia entre ESBRA (cuenta de replicación de inicio de EdgeSync) y ESRA.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Contraseña de ESRA</strong></p></td>
<td><p>La contraseña asignada a la ESBRA. La contraseña se genera mediante un generador de número aleatorio y se almacena en el archivo de suscripción perimetral como texto no cifrado.</p></td>
</tr>
<tr class="even">
<td><p><strong>Fecha de vigencia</strong></p></td>
<td><p>Fecha de creación del archivo de suscripción perimetral.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Duración</strong></p></td>
<td><p>Periodo de tiempo en que estas credenciales permanecerán vigentes. La cuenta ESBRA solo es válida durante un periodo de 24 horas.</p></td>
</tr>
<tr class="even">
<td><p><strong>Puerto SSL de AD/AM</strong></p></td>
<td><p>El puerto LDAP seguro al que enlaza el servicio EdgeSync cuando se sincronizan datos desde Active Directory a AD LDS. De manera predeterminada, es el puerto TCP 50636.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Id. del producto</strong></p></td>
<td><p>La información de licencias del servidor de transporte perimetral. Debe autorizar el servidor Transporte perimetral antes de crear la suscripción perimetral.</p></td>
</tr>
<tr class="even">
<td><p><strong>Número de versión</strong></p></td>
<td><p>Número de versión del archivo de suscripción perimetral.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Número de serie</strong></p></td>
<td><p>Versión de Exchange del servidor Transporte perimetral.</p></td>
</tr>
</tbody>
</table>



> [!IMPORTANT]
> Las credenciales ESBRA se escriben en el archivo de suscripción perimetral como texto no cifrado. Debe proteger este archivo durante todo el proceso de suscripción. Después de que el archivo de suscripción perimetral se importa a su organización de Exchange, debe eliminar de inmediato el archivo de suscripción perimetral del servidor de transporte perimetral, el recurso compartido de red que usó para importar el archivo a su organización de Exchange&nbsp;y todos los medios extraíbles.



Volver al principio

## Cuentas de replicación de EdgeSync

Las cuentas de replicación de EdgeSync (ESRA) son una parte importante de la seguridad de EdgeSync. La autenticación y autorización de ESRA son los mecanismos que se emplean para proteger la conexión entre un servidor de transporte perimetral y un servidor de buzones de correo.

La ESBRA que contiene el archivo de suscripción perimetral se usa para establecer una conexión LDAP segura durante la sincronización inicial. Después de importar el archivo de suscripción perimetral a un servidor de buzones de correo en el sitio de Active Directory al que se está suscribiendo el servidor Transporte perimetral, se crean cuentas ESRA adicionales en Active Directory para cada par de servidores de transporte conformado por un servidor de buzones de correo y un servidor Transporte perimetral. Durante la sincronización inicial, las credenciales ESRA que se acaban de crear se replican en AD LDS. Dichas credenciales ESRA se usan para la protección en sesiones de sincronización posteriores.

A cada cuenta de replicación de EdgeSync se le asignan las propiedades que se muestran en la tabla siguiente.

### Propiedades de Ms-Exch-EdgeSyncCredential

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nombre de la propiedad</th>
<th>Tipo</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>TargetServerFQDN</strong></p></td>
<td><p>Cadena</p></td>
<td><p>El servidor Transporte perimetral que acepta estas credenciales.</p></td>
</tr>
<tr class="even">
<td><p><strong>SourceServerFQDN</strong></p></td>
<td><p>String</p></td>
<td><p>El servidor de buzones de correo que presenta estas credenciales. Este valor está vacío si se trata de la credencial de inicio.</p></td>
</tr>
<tr class="odd">
<td><p><strong>EffectiveTime</strong></p></td>
<td><p>DateTime (UTC)</p></td>
<td><p>Cuándo empezar a usar esta credencial.</p></td>
</tr>
<tr class="even">
<td><p><strong>ExpirationTime</strong></p></td>
<td><p>DateTime (UTC)</p></td>
<td><p>Cuándo dejar de usar esta credencial.</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserName</strong></p></td>
<td><p>String</p></td>
<td><p>El nombre de usuario que se usa para autenticarse.</p></td>
</tr>
<tr class="even">
<td><p><strong>Password</strong></p></td>
<td><p>Byte</p></td>
<td><p>La contraseña que se usa para autenticarse. La contraseña se cifra mediante <strong>ms-Exch-EdgeSync-Certificate</strong>.</p></td>
</tr>
</tbody>
</table>


Las siguientes secciones describen el modo en que se especifican las credenciales ESRA durante el proceso de sincronización de EdgeSync.

## Especificación de la cuenta de replicación de inicio de EdgeSync

Cuando el cmdlet **New-EdgeSubscription** se ejecuta en el servidor de transporte perimetral, la ESBRA se especifica de la siguiente manera:

  - Se crea un certificado autofirmado (Edge-Cert) en el servidor de transporte perimetral. La clave privada se almacena en el almacén del equipo local y la clave pública se escribe en el archivo de suscripción perimetral.

  - Se crea la cuenta de ESBRA en AD LDS y se escriben las credenciales en el archivo de suscripción perimetral.

  - El archivo de suscripción perimetral se exporta al copiarlo a un medio extraíble (como el servidor perimetral no está en Active Directory, no se puede usar una carpeta compartida para exportar el archivo). El archivo está ahora preparado para importarse a un servidor de buzones de correo.

## Especificación de las cuentas de replicación de EdgeSync en Active Directory

Cuando el archivo de suscripción perimetral se importa a un servidor de buzones de correo, se realizan los siguientes pasos para establecer un registro de la suscripción perimetral en Active Directory y para especificar credenciales ESRA adicionales:

1.  Se crea un objeto de configuración del servidor Transporte perimetral en Active Directory. El certificado Edge-Cert se escribe en dicho objeto como un atributo.

2.  Todos los servidores de buzones de correo del sitio de Active Directory suscrito reciben una notificación de Active Directory que informa de que se ha registrado una nueva suscripción perimetral. En cuanto se recibe dicha notificación, cada servidor de buzones de correo recupera la cuenta ESRA.edge y la cifra mediante la clave pública Edge-Cert. La cuenta ESRA.edge cifrada se escribe en el objeto de configuración del servidor Transporte perimetral.

3.  Cada servidor de buzones de correo crea un certificado autofirmado (TransportService-Cert). La clave privada se almacena en el almacén del equipo local y la clave pública se almacena en el objeto de configuración del servidor de buzones de correo de Active Directory.

4.  Cada servidor de buzones de correo cifra la cuenta ESRA.edge mediante la clave pública de su propio certificado TransportService y, a continuación, la almacena en su propio objeto de configuración.

5.  Cada servidor de buzones de correo genera una cuenta ESRA para cada objeto de configuración de servidor Transporte perimetral en Active Directory (ESRA.edge. *Mailboxname.\#*).
    
    Ejemplo: ESRA.edge.Example.0
    
    La contraseña para ESRA.edge se genera mediante un generador de número aleatorio y se cifra mediante la clave pública del certificado TransportService-Cert. La contraseña que se genera tiene la longitud máxima permitida por Windows Server.

6.  Cada cuenta ESRA.edge. *Mailboxname.\#* se cifra mediante la clave pública del certificado Edge-Cert y se almacena en el objeto de configuración del servidor Transporte perimetral de Active Directory.

En las siguientes secciones se explica cómo se usan estas cuentas durante la sincronización de EdgeSync.

Volver al principio

## Autenticación de replicación inicial

La cuenta inicial de ESBRA se usa solo cuando se establece la sincronización inicial. Durante la primera sesión de sincronización de EdgeSync, las cuentas de ESRA adicionales, ESRA.edge.*Mailboxname.\#*, se replican en AD LDS. Estas cuentas se usan para autenticar sesiones de sincronización de EdgeSync posteriores.

El servidor de buzones de correo que lleva a cabo la replicación inicial se determina de manera aleatoria. El primer servidor de buzones de correo del sitio de Active Directory en realizar una exploración topológica y detectar la nueva suscripción perimetral realiza la réplica inicial. Como esta detección se basa en el momento de la exploración topológica, cualquier servidor de buzones de correo del sitio puede realizar la réplica inicial.

EdgeSync inicia una sesión segura de LDAP desde el servidor de buzones de correo al servidor Transporte perimetral. El servidor Transporte perimetral presenta su certificado autofirmado y el servidor de buzones de correo comprueba que dicho certificado coincide con el que está almacenado en el objeto de configuración del servidor Transporte perimetral de Active Directory. Una vez comprobada la identidad del servidor Transporte perimetral, el servidor de buzones de correo proporciona las credenciales de la cuenta ESRA.edge.*Mailboxname.\#* al servidor Transporte perimetral. El servidor Transporte perimetral comprueba las credenciales en la cuenta almacenada en AD LDS.

Después, el servicio EdgeSync del servidor de buzones de correo envía la topología, la configuración y los datos de destinatarios desde Active Directory a AD LDS. El cambio en el objeto de configuración del servidor Transporte perimetral de Active Directory se replica en AD LDS. AD LDS recibe las entradas ESRA.edge.*Mailboxname.\#* recién agregadas y el Servicio de credenciales de Microsoft Exchange crea la cuenta AD‎ LDS correspondiente. Estas cuentas están ya disponibles para autenticar sesiones programadas de sincronización de EdgeSync posteriores.

## Servicio de credenciales de Microsoft Exchange

El Servicio de credenciales de Microsoft Exchange forma parte de proceso de suscripción perimetral. El Servicio de credenciales únicamente se ejecuta en el servidor Transporte perimetral. Este servicio crea las cuentas ESRA recíprocas de AD LDS para que un servidor de buzones de correo pueda autenticarse en un servidor Transporte perimetral a fin de realizar la sincronización de EdgeSync. El servicio EdgeSync no se comunica directamente con el Servicio de credenciales de Microsoft Exchange. El Servicio de credenciales de Microsoft Exchange se comunica con AD LDS e instala las credenciales ESRA cuando el servidor de buzones de correo las actualiza.

Volver al principio

## Autenticación de sesiones de sincronización programadas

Cuando termina la sincronización de EdgeSync inicial, se establece la programación para la sincronización de EdgeSync, y los datos de Active Directory que han cambiado se actualizan de manera periódica en AD LDS. Un servidor de buzones de correo inicia una sesión LDAP segura con la instancia AD LDS del servidor Transporte perimetral. AD LDS demuestra su identidad ante este servidor de buzones de correo presentándole su certificado autofirmado. El servidor de buzones de correo presenta sus credenciales de ESRA.edge a AD LDS. La contraseña de ESRA.edge se cifra mediante la clave pública del certificado autofirmado del servidor de buzones de correo. Solo ese servidor de buzones de correo en concreto puede usar dichas credenciales para autenticarse en AD LDS.

Volver al principio

## Renovación de cuentas de replicación de EdgeSync

La contraseña de la cuenta ESRA debe ajustarse a la directiva de contraseñas del servidor local. Para evitar que el proceso de renovación de contraseñas produzca errores temporales de autenticación, se crea una segunda cuenta ESRA.edge siete días antes de que expire la primera cuenta ESRA.edge. Dicha segunda cuenta entra en vigencia tres días antes de que expire la primera cuenta ESRA. En cuanto entra en vigor la segunda cuenta ESRA.edge, EdgeSync deja de usar la primera cuenta e inicia el uso de la segunda. Cuando caduca la primera cuenta, las credenciales de la ESRA se eliminan. El proceso de renovación continúa hasta que la suscripción perimetral se quita.

Volver al principio

