---
title: 'Suscripciones perimetrales: Exchange 2013 Help'
TOCTitle: Suscripciones perimetrales
ms:assetid: 3addd71a-4165-401f-a009-002bcd8baba6
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997438(v=EXCHG.150)
ms:contentKeyID: 61183325
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Suscripciones perimetrales

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Los servidores de transporte perimetral minimizan la superficie expuesta a ataques controlando todo el flujo de correo de Internet y proporcionando retransmisión SMTP y servicios de host inteligente para la organización de Exchange. Una serie de agentes que se ejecutan en el servidor Transporte perimetral de la red perimetral de la organización proporcionan niveles adicionales de protección de mensajes y seguridad. Dichos agentes son compatibles con las características que ofrecen protección frente a virus y correo no deseado, y aplican reglas de transporte para controlar el flujo de correo.

Las suscripciones perimetrales se usan para rellenar la instancia de Active Directory Lightweight Directory Services (AD LDS) en el rol de servidor Transporte perimetral con datos de Active Directory. Aunque la creación de una suscripción perimetral sea opcional, la suscripción de un servidor de transporte perimetral a la organización de Exchange proporciona una experiencia administrativa más sencilla y mejora las características contra el correo electrónico no deseado. Es necesario crear una suscripción perimetral si se desea usar la búsqueda de destinatarios o agregación de listas seguras, o bien si se desea proteger las comunicaciones SMTP con dominios asociados a través de Seguridad de la capa transporte mutua (MTLS) .

**Contenido**

Proceso de suscripción perimetral

Servicio EdgeSync de Microsoft Exchange

Administración de suscripciones perimetrales

## Proceso de suscripción perimetral

Un servidor de transporte perimetral no tiene acceso directo a Active Directory. Toda la información de configuración y de destinatarios que usa el servidor Transporte perimetral para procesar mensajes está almacenada localmente en AD LDS. La creación de una suscripción perimetral establece una replicación automática y segura de la información de Active Directory en AD LDS. Con el proceso de suscripción perimetral se especifican las credenciales que se usan para establecer una conexión segura de LDAP entre los servidores de buzones de correo de Exchange 2013 y un servidor de transporte perimetral con suscripción. El servicio EdgeSync de Microsoft Exchange que se ejecuta en los servidores de buzones de correo realiza una sincronización unidireccional periódica para transferir datos actualizados a AD LDS. Esto reduce las tareas de administración que se realizan en la red perimetral permitiendo que se configure el servidor de buzones de correo y después se sincronice dicha información con el servidor Transporte perimetral.

Puede suscribir un servidor Transporte perimetral al sitio de Active Directory que contiene los servidores de buzones de correo responsables de transferir mensajes hacia y desde los servidores de transporte perimetral. El proceso de suscripción perimetral crea una afiliación de pertenencia al sitio de Active Directory en el servidor de transporte perimetral. La afiliación al sitio permite a los servidores de buzones de correo de la organización de Exchange transmitir mensajes al servidor Transporte perimetral para su entrega en Internet sin necesidad de configurar conectores de envío.

Uno o varios servidores de transporte perimetral se pueden suscribir a un solo sitio de Active Directory. Sin embargo, un servidor de transporte perimetral no se puede suscribir a más de un sitio de Active Directory. Si tiene más de un servidor de transporte perimetral implementado, cada servidor se puede suscribir a un sitio de Active Directory diferente. Cada servidor de transporte perimetral requiere una suscripción perimetral independiente.

Para implementar un servidor de transporte perimetral y suscribirlo a un sitio de Active Directory, siga estos pasos:

1.  Instale la función del servidor Transporte perimetral.

2.  Compruebe que los servidores de transporte de buzones y el servidor de transporte perimetral se pueden comunicar entre sí mediante una resolución de nombres DNS.

3.  En el servidor de buzones de correo, configure los objetos y opciones que se van a replicar en el servidor de transporte perimetral.

4.  En el servidor de transporte perimetral, cree y exporte el archivo de suscripción perimetral.

5.  Copie el archivo de suscripción perimetral en el servidor de buzones de correo o en un recurso compartido de archivos al que se pueda tener acceso desde el sitio de Active Directory que tiene los servidores de buzones de correo.

6.  Importe el archivo de suscripción perimetral a un sitio de Active Directory.

## Qué sucede cuando se crea una nueva suscripción perimetral

Cuando se crea un archivo de suscripción perimetral (ejecutando el cmdlet **New-EdgeSubscription** en el servidor Transporte perimetral), tienen lugar las siguientes acciones:

  - Se crea una cuenta AD LDS llamada cuenta de replicación de inicio de EdgeSync (ESBRA). Estas credenciales ESBRA se usan para autenticar la primera conexión de EdgeSync a un servidor Transporte perimetral. Esta cuenta se configura para que expire 24 horas después de su creación. Por lo tanto, es necesario completar el proceso de suscripción de seis pasos que se describe en la sección anterior en un plazo de 24 horas. Si la cuenta ESBRA expira antes de que se haya completado el proceso de suscripción perimetral, tendrá que volver a ejecutar el cmdlet **New-EdgeSubscription** para crear un nuevo archivo de suscripción perimetral.

  - Las credenciales de la ESBRA se recuperan desde AD LDS y se escriben en el archivo de suscripción perimetral. La clave pública del certificado autofirmado del servidor de transporte perimetral también se exporta al archivo de suscripción perimetral. Las credenciales que se escriben en el archivo de suscripción perimetral son específicas del servidor desde el que se exporta el archivo.

  - Cualquier objeto de configuración creado anteriormente en un servidor Transporte perimetral que ahora se va a replicar en AD LDS desde Active Directory se eliminará de AD LDS. Asimismo, los cmdlets del Shell de administración de Exchange que se usaron para configurar dichos objetos quedarán deshabilitados. Sin embargo, todavía puede usar los cmdlets **Get-\*** para ver dichos objetos. La ejecución del cmdlet **New-EdgeSubscription** deshabilita los siguientes cmdlets en el servidor Transporte perimetral:
    
      - **Set-SendConnector**
    
      - **New-SendConnector**
    
      - **Remove-SendConnector**
    
      - **New-AcceptedDomain**
    
      - **Set-AcceptedDomain**
    
      - **Remove-AcceptedDomain**
    
      - **New-MessageClassification**
    
      - **Set-MessageClassification**
    
      - **Remove-MessageClassification**
    
      - **New-RemoteDomain**
    
      - **Set-RemoteDomain**
    
      - **Remove-RemoteDomain**

Cuando importa el archivo de suscripción perimetral al servidor de buzones de correo ejecutando el cmdlet **New-EdgeSubscription** en el buzón de servidores:

  - Se crea la suscripción perimetral, uniendo un servidor Transporte perimetral a una organización de Exchange. EdgeSync propagará datos de configuración a este servidor Transporte perimetral, creando un objeto de configuración perimetral en Active Directory.

  - Todos los servidores de buzones de correo del sitio de Active Directory reciben una notificación de Active Directory que informa de que se ha suscrito un nuevo servidor Transporte perimetral. El servidor de buzones de correo recupera la ESBRA desde el archivo de suscripción perimetral. El servidor de buzones de correo cifra entonces la cuenta ESBRA mediante la clave pública del certificado autofirmado del servidor Transporte perimetral. A continuación, las credenciales cifradas se escriben en el objeto de configuración perimetral.

  - Cada servidor de buzones de correo cifra también la cuenta ESBRA mediante su propia clave pública y, a continuación, almacena las credenciales en su propio objeto de configuración.

  - Las cuentas de replicación de EdgeSync (ESRA) se crean en Active Directory para cada par de servidores Transporte perimetral y de buzones. Cada servidor de buzones de correo almacena sus credenciales de ESRA como un atributo del objeto de configuración del servidor de buzones de correo.

  - Se crean automáticamente conectores de envío para transmitir mensajes salientes desde el servidor de transporte perimetral a Internet y mensajes entrantes desde dicho servidor a la organización de Exchange.

  - El servicio EdgeSync de Microsoft Exchange que se ejecuta en los servidores de buzones de correo usa las credenciales de ESBRA para establecer una conexión LDAP segura entre un servidor de buzones de correo y el servidor Transporte perimetral, y realiza la replicación inicial de datos. Los siguientes datos se replican en AD LDS:
    
      - Datos de topología
    
      - Datos de configuración
    
      - Datos de destinatario
    
      - Credenciales de ESRA

  - El servicio de credenciales de Microsoft Exchange que se ejecuta en el servidor Transporte perimetral instala las credenciales de ESRA. Dichas credenciales se usan para autenticar y proteger posteriores conexiones de sincronización.

  - Se establece la programación de sincronización de EdgeSync.

El servicio EdgeSync de Microsoft Exchange que se está ejecutando en los servidores de buzones de correo del sitio de Active Directory con suscripción realiza una replicación unidireccional de datos desde Active Directory a AD LDS de forma periódica. También puede usar el cmdlet **Start-EdgeSynchronization** para invalidar la programación de sincronización EdgeSync e iniciar inmediatamente la sincronización.

Para obtener más información acerca de las cuentas ESRA y cómo se usan para proteger el proceso de sincronización de EdgeSync, vea [Credenciales de suscripción perimetral](edge-subscription-credentials-exchange-2013-help.md).

En este ejemplo se suscribe un servidor Transporte perimetral al sitio especificado y se crea el conector de envío de Internet y el conector de envío desde el servidor Transporte perimetral a los servidores de buzones de correo.

```powershell
New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "C:\EdgeSubscriptionInfo.xml" -Encoding Byte -ReadCount 0)) -CreateInternetSendConnector $true -CreateInboundSendConnector $true -Site "Default-First-Site-Name" 
```

> [!NOTE]  
> Si los valores de los parámetros <EM>CreateInternetSendConnector</EM> y <EM>CreateInboundSendConnector</EM> son <CODE>$true</CODE>: Se muestran a continuación solo para fines de demostración.

En este ejemplo, se exporta un archivo de suscripción perimetral.

```powershell
New-EdgeSubscription -FileName "C:\EdgeSubscriptionInfo.xml"
```


> [!NOTE]  
> Al ejecutar el cmdlet <STRONG>New-EdgeSubscription</STRONG> en el servidor Transporte perimetral, se recibe un mensaje para confirmar los comandos que se deshabilitarán y la configuración que se sobrescribirá en el servidor Transporte perimetral. Para omitir esta confirmación, debe utilizar el parámetro <EM>Force</EM>. Este parámetro resulta útil en scripts con el cmdlet <STRONG>New-EdgeSubscription</STRONG>. El parámetro <EM>Force</EM> también se utiliza para sobrescribir un archivo que tenga el mismo nombre que el archivo que se crea al volver a suscribirse en un servidor Transporte perimetral.



Para información detallada sobre la sintaxis y los parámetros, véase [New-EdgeSubscription](https://technet.microsoft.com/es-es/library/bb123800\(v=exchg.150\)).

## Conectores de envío creados durante el proceso de suscripción perimetral

De forma predeterminada, al completar el proceso de suscripción perimetral recomendado importando el archivo de suscripción perimetral a un servidor de buzones de correo, se crean automáticamente los conectores de envío necesarios para permitir el flujo de correo de extremo a extremo entre Internet y la organización de Exchange, y se eliminan los conectores de envío existentes en el servidor Transporte perimetral. En algunos escenarios, puede optar por suprimir la creación automática de conectores de envío y configurarlos de forma manual. Para obtener más información acerca de la configuración manual de los conectores de envío, vea [Configurar manualmente el flujo de correo del servidor de transporte perimetral](manually-configure-edge-transport-server-mail-flow-exchange-2013-help.md) y [Configurar el flujo de correo de Internet a través de un servidor de transporte perimetral sin usar EdgeSync](configure-internet-mail-flow-through-an-edge-transport-server-without-using-edgesync-exchange-2013-help.md).

El proceso de suscripción perimetral facilita los siguientes conectores de envío:

  - Un conector de envío configurado para retransmitir mensajes de correo electrónico desde la organización de Exchange a Internet.

  - Un conector de envío configurado para retransmitir mensajes de correo electrónico desde el servidor Transporte perimetral a la organización de Exchange.

Además, la suscripción de un servidor Transporte perimetral a la organización de Exchange permite que los servidores de buzones de correo en el sitio de Active Directory con suscripción usen el conector de envío dentro de la organización para retransmitir mensajes a dicho servidor Transporte perimetral.

## Crear automáticamente un conector de envío entrante para recibir mensajes de Internet

De forma predeterminada, cuando se ejecuta el cmdlet **New-EdgeSubscription** en el servidor de buzones de correo, el parámetro del conector de envío entrante *CreateInboundSendConnector* se establece en el valor `$true`. Esto crea el conector de envío requerido para enviar mensajes a la organización de Exchange. La siguiente tabla muestra la configuración de este conector de envío.

### Configuración del conector de envío entrante automático

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Propiedad</th>
<th>Valor</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>EdgeSync - Entrante para &lt;<em>Nombre de sitio</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p><em>AddressSpaces</em></p></td>
<td><p><code>SMTP:--;1</code></p>
<p>El valor <code>--</code> en el espacio de direcciones representa todos los dominios aceptados con autorización y de retransmisión interna para la organización de Exchange. Cualquier mensaje que el servidor Transporte perimetral reciba de los dominios aceptados se enrutan a este conector de envío y se retransmiten a los hosts inteligentes.</p></td>
</tr>
<tr class="odd">
<td><p><em>SourceTransportServers</em></p></td>
<td><p>&lt;<em>Nombre de suscripción perimetral</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>True</p></td>
</tr>
<tr class="odd">
<td><p><em>DNSRoutingEnabled</em></p></td>
<td><p>False</p></td>
</tr>
<tr class="even">
<td><p><em>SmartHosts</em></p></td>
<td><p><code>--</code></p>
<p>El valor <code>--</code> en la lista de hosts inteligentes representa todos los buzones de servidores en el sitio de Active Directory suscrito. Los servidores de buzones de correo que se agreguen al sitio de Active Directory con suscripción tras establecer la suscripción perimetral no participan en el proceso de sincronización de EdgeSync. Sin embargo, se agregan automáticamente a la lista de hosts inteligentes para el conector de envío entrante creado automáticamente. Si hay más de un servidor de buzones de correo ubicado en el sitio de Active Directory con suscripción, las conexiones entrantes se cargarán equilibradas entre los hosts inteligentes.</p></td>
</tr>
</tbody>
</table>


No se puede modificar el espacio de direcciones ni la lista de hosts inteligentes durante su creación para el conector de envío entrante creado automáticamente. Sin embargo, puede establecer el parámetro *CreateInboundSendConnector* en el valor `$false` cuando crea una suscripción perimetral. Esto permite configurar de forma manual un conector de envío desde el servidor Transporte perimetral a la organización de Exchange.

## Crear automáticamente un conector de envío saliente para enviar mensajes a Internet

De forma predeterminada, cuando se ejecuta el cmdlet **New-EdgeSubscription** en el servidor de buzones de correo, el parámetro del conector de envío saliente *CreateInternetSendConnector* se establece en el valor `$true`. Esto crea el conector de envío requerido para enviar mensajes a Internet. La siguiente tabla muestra la configuración predeterminada de este conector de envío.

### Configuración del conector de envío automático a Internet

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Propiedad</th>
<th>Valor</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>EdgeSync - &lt;<em>Nombre de sitio</em>&gt; para Internet</p></td>
</tr>
<tr class="even">
<td><p><em>AddressSpaces</em></p></td>
<td><p><code>SMTP:*;100</code></p></td>
</tr>
<tr class="odd">
<td><p><em>SourceTransportServers</em></p></td>
<td><p>&lt;<em>Nombre de suscripción perimetral</em>&gt;</p>

> [!NOTE]  
> El nombre de la suscripción perimetral es el mismo que el del servidor de transporte perimetral con suscripción.


</td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>True</p></td>
</tr>
<tr class="odd">
<td><p><em>DNSRoutingEnabled</em></p></td>
<td><p>True</p></td>
</tr>
<tr class="even">
<td><p><em>DomainSecureEnabled</em></p></td>
<td><p>True</p></td>
</tr>
</tbody>
</table>


Si se suscribe más de un servidor Transporte perimetral para el mismo sitio de Active Directory, no se crean conectores de envío adicionales para Internet. En su lugar, todas las suscripciones perimetrales se agregan al mismo conector de envío como servidor de origen. Esto equilibra la carga de las conexiones salientes a Internet en los servidores de transporte perimetral con suscripción.

El conector de envío saliente se configura para enviar mensajes de correo electrónico desde la organización de Exchange a todos los dominios remotos de SMTP, mediante enrutamiento de DNS para resolver nombres de dominio en registros de recursos MX. Para obtener información detallada sobre la configuración manual de un conector, vea [Configurar manualmente el flujo de correo del servidor de transporte perimetral](manually-configure-edge-transport-server-mail-flow-exchange-2013-help.md).

## Servicio EdgeSync de Microsoft Exchange

Tras suscribir a un servidor Transporte perimetral a un sitio de Active Directory, EdgeSync replicará la configuración y los datos de destinatarios en los servidores de transporte perimetral. El servicio replica los siguientes datos de Active Directory en AD LDS:

  - Configuración de conector de envío

  - Dominios aceptados

  - Dominios remotos

  - Clasificaciones de mensajes

  - Listas de remitentes seguros

  - Listas de remitentes bloqueados

  - Destinatarios

  - Lista de dominios de envío y de recepción usada en las comunicaciones seguras de dominios con asociados

  - Lista de servidores SMTP que aparecen como internos en la configuración de transporte de su organización

  - Lista de servidores de buzones de correo en el sitio de Active Directory con suscripción

Para obtener información detallada sobre los datos que se replican en AD LDS y cómo se usan, vea [Datos de replicación de EdgeSync](edgesync-replication-data-exchange-2013-help.md).

EdgeSync usa un canal LDAP seguro mutuamente autenticado y autorizado para transferir datos desde el servidor de buzones de correo al servidor Transporte perimetral.

Para replicar datos en AD LDS, el servidor de buzones de correo se enlaza con un servidor de catálogo global para recuperar datos actualizados. El servicio EdgeSync inicia una sesión LDAP segura entre un servidor de buzones de correo y el servidor Transporte perimetral con suscripción mediante el puerto TCP 50636 no estándar.

Cuando se suscribe por primera vez un servidor de transporte perimetral en un sitio de Active Directory, la replicación inicial que completa AD LDS con los datos de Active Directory puede tardar cinco minutos o más, según la cantidad de datos del servicio de directorio. Después de la replicación inicial, EdgeSync solo sincroniza objetos nuevos y modificados, y quita los objetos eliminados.

## Programación de sincronización

Los distintos tipos de datos se sincronizan en distintas programaciones. La programación de sincronización de EdgeSync especifica el intervalo máximo entre sincronizaciones de EdgeSync. La sincronización de EdgeSync tiene lugar en los siguientes intervalos:

  - Datos de configuración: 3 minutos.

  - Datos de destinatario: 5 minutos.

  - Datos de topología: 5 minutos

Si quiere cambiar estos intervalos, use el cmdlet **Set-EdgeSyncServiceConfig**. El uso del cmdlet **Start-EdgeSynchronization** en el servidor de buzones de correo para forzar la sincronización de la suscripción perimetral invalida el temporizador de la siguiente sincronización de EdgeSync programada e inicia EdgeSync de inmediato.

## Selección de servidores de buzones de correo

Un servidor Transporte perimetral con suscripción se asocia con un sitio de Active Directory particular. Si existe más de un servidor de buzones de correo en el sitio, todos ellos pueden replicar datos a los servidores de transporte perimetral con suscripción. Para evitar la contención entre servidores de buzones de correo al sincronizar, el servidor de buzones de correo preferido se selecciona de la siguiente forma:

1.  El primer servidor de buzones de correo del sitio de Active Directory en realizar una exploración topológica y detectar la nueva suscripción perimetral realiza la réplica inicial. Como esta detección se basa en el momento de la exploración topológica, cualquier servidor de buzones de correo del sitio puede realizar la réplica inicial.

2.  El servidor de buzones de correo que realiza la réplica inicial establece una opción de concesión de EdgeSync y establece un bloqueo en la suscripción perimetral. La opción de concesión establece al servidor de buzones de correo como servidor preferido para proporcionar servicios de sincronización a dicho servidor Transporte perimetral. El bloqueo evita que el servicio EdgeSync que se ejecuta en otro servidor de buzones de correo asuma la opción de concesión.

3.  La opción de concesión de EdgeSync dura una hora. Durante esa hora, ningún otro servicio EdgeSync puede asumir la opción a menos que se inicie una sincronización manual antes de que termine la hora. Si el servidor de buzones de correo no está disponible para proporcionar el servicio EdgeSync cuando se inicia la sincronización manual, tras una espera de cinco minutos, el bloqueo se libera y otro servicio EdgeSync puede asumir la opción de concesión y realizar la sincronización.

4.  A menos que inicie la sincronización manual, se produce una sincronización basada en la programación de sincronización de EdgeSync. Si el servidor preferido no está disponible cuando se produce la programación de sincronización, pasada una espera de cinco minutos, el bloqueo se libera y otra tarea del servicio EdgeSync puede asumir la opción de concesión y realizar la sincronización.

Este método de bloqueo y concesión evita que más de una instancia del servicio EdgeSync envíe datos al mismo servidor Transporte perimetral al mismo tiempo.


> [!NOTE]  
> Si también tiene servidores de buzones de correo de Exchange 2010 o Exchange 2007 en el sitio de Active Directory con suscripción, los servidores de buzones de correo de Exchange&nbsp;2013 siempre tendrán prioridad y realizarán la replicación.




> [!NOTE]  
> Cuando se suscribe un servidor Transporte perimetral a un sitio de Active Directory, todos los servidores de buzones de correo instalados en ese sitio de Active Directory en ese momento pueden participar en el proceso de sincronización de EdgeSync. Si se elimina uno de estos servidores, el servicio EdgeSync que se ejecuta en los servidores de buzones de correo restantes continuará el proceso de sincronización de datos. Sin embargo, si más adelante instala nuevos servidores de buzones de correo en el sitio de Active Directory, no participarán automáticamente en la sincronización de EdgeSync. Si desea habilitar dichos servidores de buzones de correo nuevos para que participen en la sincronización de EdgeSync, tendrá que volver a suscribir el servidor Transporte perimetral.



En la siguiente tabla se enumeran las propiedades de EdgeSync relacionadas con el bloqueo y la concesión. Se puede usar el cmdlet **Set-EdgeSyncServiceConfig** para configurar estas propiedades.

### Propiedades de concesión de EdgeSync

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parámetro</th>
<th>Valor predeterminado</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>LockDuration</em></p></td>
<td><p><code>00:05:00</code> (5 minutos)</p></td>
<td><p>Esta opción determina cuanto tiempo adquirirá un bloqueo un servicio EdgeSync particular. Si el servicio EdgeSync en el servidor de buzones de correo que mantiene este bloqueo no responde, tras cinco minutos el servicio EdgeSync en otro servidor de buzones de correo asumirá la concesión. Forzar la sincronización inmediata de EdgeSync no anula este valor.</p></td>
</tr>
<tr class="even">
<td><p><em>OptionDuration</em></p></td>
<td><p><code>01:00:00</code> (1 hora)</p></td>
<td><p>Esta opción determina cuánto tiempo un servicio EdgeSync puede declarar una opción de concesión en un servidor Transporte perimetral. Si el servicio EdgeSync que mantiene la concesión no está disponible y no se reinicia durante este período de opción, ningún otro servicio EdgeSync de Exchange asumirá la opción de concesión, a no ser que fuerce la sincronización de EdgeSync.</p></td>
</tr>
<tr class="odd">
<td><p><em>LockRenewalDuration</em></p></td>
<td><p><code>00:01:00</code> (1 minuto)</p></td>
<td><p>Esta opción determina con qué frecuencia se actualiza el campo de bloqueo cuando un servicio EdgeSync ha adquirido un bloqueo en un servidor Transporte perimetral.</p></td>
</tr>
</tbody>
</table>


## Preparación para la ejecución del servicio EdgeSync

Antes de que pueda suscribir su servidor Transporte perimetral en la organización de Exchange, debe asegurarse de que su infraestructura y los servidores de buzones de correo estén preparados para el servicio EdgeSync. Para preparar la sincronización de EdgeSync, necesita:

  - Comprobar que el firewall perimetral de la red que separa el servidor Transporte perimetral de la organización de Exchange está configurado para habilitar las comunicaciones a través de los puertos correctos. El servidor de transporte perimetral usa puertos LDAP no estándar. Si el entorno requiere puertos específicos, puede modificar los puertos utilizados por AD LDS mediante el script ConfigureAdam.ps1 incluido en Exchange. Para obtener más información, vea [Modificar la configuración de AD LDS](modify-ad-lds-configuration-exchange-2013-help.md). Modifique los puertos antes de crear la suscripción perimetral. Si modifica los puertos después de haber creado la suscripción perimetral, deberá quitar la suscripción perimetral y crear una nueva suscripción perimetral. De forma predeterminada, los siguientes puertos LDAP se usan para tener acceso a AD LDS:
    
      - **LDAP** El puerto 50389/TCP se usa localmente para enlazar con la instancia de AD LDS. No es necesario que este puerto esté abierto en el firewall perimetral de la red.
    
      - **LDAP seguro**   El puerto 50636/TCP se usa para la sincronización de directorios de servidores de buzones de correo en AD LDS. Este puerto debe estar abierto en el firewall para que la sincronización de EdgeSync se realice correctamente.

  - Comprobar que la resolución de nombres de host de DNS se realice correctamente desde el servidor Transporte perimetral a los servidores de buzones de correo y viceversa.

  - Concesión de licencia al servidor de transporte perimetral. La información de licencia del servidor Transporte perimetral se captura cuando se crea la suscripción perimetral. Los servidores de transporte perimetral con suscripción necesitan suscribirse a la organización de Exchange después de que la clave de licencia se ha aplicado en el servidor Transporte perimetral. Si se aplica la clave de licencia en el servidor Transporte perimetral después de realizar el proceso de suscripción perimetral, la información de concesión de licencia no se actualiza en la organización de Exchange y deberá volverse a suscribir al servidor Transporte perimetral.

  - Configurar los siguientes valores de transporte para la propagación en servidor Transporte perimetral:
    
      - **Servidores SMTP internos**   Use el parámetro *InternalSMTPServers* en el cmdlet **Set-TransportConfig** para especificar una lista de direcciones IP de servidor SMTP interno o intervalos de direcciones IP que el identificador de remitente y los agentes de filtrado de conexión omitirán en el servidor Transporte perimetral.
    
      - **Dominios aceptados**   Configure todos los dominios con autorización, dominios de retransmisión internos y dominios de retransmisión externos.
    
      - **Dominios remotos**   Configure los valores de dominios remotos.

Volver al principio

## Administración de suscripciones perimetrales

Para ver instrucciones paso a paso sobre las tareas de administración de suscripción perimetral, vea [Manage Edge Subscriptions](manage-edge-subscriptions-exchange-2013-help.md).

