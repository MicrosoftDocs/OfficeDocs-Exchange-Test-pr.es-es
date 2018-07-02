---
title: 'Implementaciones híbridas de Exchange Server: Exchange 2013 Help'
TOCTitle: '@NoTitle'
ms:assetid: 59e32000-4fcf-417f-a491-f1d8f9aeef9b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ200581(v=EXCHG.150)
ms:contentKeyID: 48268931
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Implementaciones híbridas de Exchange Server

 

_<strong>Se aplica a:</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>Última modificación del tema:</strong>2018-04-16_

**Resumen:**   Lo que necesita saber para planear una implementación híbrida de Exchange.

Una implementación híbrida ofrece a las organizaciones la capacidad de extender la experiencia enriquecida de características y el control administrativo de la organización local existente de Microsoft Exchange a la nube. Una implementación híbrida proporciona una apariencia de integración perfecta de una única organización de Exchange entre una organización de Exchange local y Exchange Online en Microsoft Office 365. Asimismo, una implementación híbrida puede funcionar como paso intermedio para pasar completamente a una organización de Exchange Online.

**Contenido**

Características de una implementación híbrida de Exchange

Consideraciones sobre la implementación híbrida de Exchange

Componentes de una implementación híbrida de Exchange

Ejemplo de una implementación híbrida de Exchange

Aspectos a tener en cuenta antes de configurar una implementación híbrida de Exchange

Terminología básica

Documentación de implementación híbrida de Exchange

## Características de una implementación híbrida de Exchange

Una implementación híbrida proporciona las características siguientes:

  - Enrutamiento de correo seguro entre las organizaciones locales y las de Exchange Online.

  - Enrutamiento de correo con un espacio de nombres de dominio compartido. Por ejemplo, las organizaciones locales y de Exchange Online usan el dominio SMTP @contoso.com.

  - Una lista global de direcciones (GAL) unificada, también llamada "libreta de direcciones compartida".

  - Disponibilidad y uso compartido de calendario entre las organizaciones locales y las de Exchange Online.

  - Control centralizado del flujo de correo entrante y saliente. Puede configurar los mensajes entrantes y salientes de Exchange Online para que se enruten a través de la organización local de Exchange.

  - Dirección URL de Outlook en la web única para las organizaciones locales y de Exchange Online.

  - Capacidad de desplazar buzones de correo locales existentes a la organización Exchange Online. Los buzones de Exchange Online también se pueden mover de vuelta a la organización local si es necesario.

  - Administración centralizada de buzones de correo mediante el Centro de administración de Exchange (EAC) local.

  - Seguimiento de mensajes, sugerencias de correo electrónico y búsqueda de varios buzones entre las organizaciones locales y las de Exchange Online.

  - Archivado de mensajes basados en la nube para buzones de Exchange locales. El archivado de Exchange Online se puede usar con una implementación híbrida. Obtenga más información sobre el archivado de Exchange Online en [Servicios adicionales de Microsoft Office 365](https://go.microsoft.com/fwlink/p/?linkid=233231).

## Consideraciones sobre la implementación híbrida de Exchange

Antes de realizar una implementación híbrida de Exchange, debería tener en cuenta lo siguiente:

  - **Requisitos para la implementación híbrida**: antes de configurar una implementación híbrida, debe asegurarse de que la organización local cumple todos los requisitos previos para una implementación correcta. Para obtener más información, consulte [Requisitos previos de implementación híbrida](hybrid-deployment-prerequisites-exchange-2013-help.md).

  - **Clientes de Exchange ActiveSync**: al mover un buzón de su organización local de Exchange a Exchange Online, todos los clientes que acceden al buzón deben actualizarse para poder usar Exchange Online. Esto incluye los dispositivos de Exchange ActiveSync. La mayoría de los clientes de Exchange ActiveSync se volverán a configurar automáticamente al mover el buzón a Exchange Online, pero algunos dispositivos antiguos podrían no actualizarse correctamente. Para obtener más información, vea [Configuración de un dispositivo de Exchange ActiveSync con implementaciones híbridas de Exchange](exchange-activesync-device-settings-with-exchange-hybrid-deployments-exchange-2013-help.md).

  - **Migración de permisos de buzones**: los permisos de buzones locales como Enviar como, Acceso total, Enviar en nombre de y los permisos de carpeta que se apliquen explícitamente al buzón se migran a Exchange Online. Los permisos de buzones (no explícitos) heredados y los permisos concedidos a objetos que no están habilitados para correo en Exchange Online no se migran. Debe asegurarse de que todos los permisos se conceden explícitamente y todos los objetos están habilitados para correo antes de la migración. Por lo tanto, tendrá que planificar la configuración de estos permisos en Office 365 si es aplicable para su organización. En el caso de los permisos Enviar como, si el usuario y el recurso que se intenta enviar como no se mueven al mismo tiempo, deberá agregar explícitamente el permiso Enviar como en Exchange Online con el cmdlet **Add-RecipientPermission**.

  - **Compatibilidad con los permisos de buzón entre locales**: las implementaciones híbridas de Exchange son compatibles con el uso de los permisos Acceso total y Enviar en nombre de entre buzones ubicados en una organización de Exchange local y buzones ubicados en Office 365. Es necesario realizar más pasos para los permisos Enviar como. Además, es posible que se requiera una configuración adicional para admitir permisos de buzón entre locales en función de la versión de Exchange instalada en la organización local. Para obtener más información, vea [Delegar permisos de buzón](permissions-in-exchange-hybrid-deployments-exchange-2013-help.md) en [Permisos en implementaciones híbridas de Exchange](permissions-in-exchange-hybrid-deployments-exchange-2013-help.md) y [Configurar Exchange para admitir permisos de buzón delegada en una implementación híbrida](configure-exchange-to-support-delegated-mailbox-permissions-in-a-hybrid-deployment-exchange-2013-help.md).
    

    > [!NOTE]
    > A partir de febrero de 2018, se está implementando la característica para admitir el acceso total, el envío en nombre de alguien y los derechos de carpeta entre bosques, y se espera que se complete en abril de 2018.



  - **Baja de servicios**  Como parte de la administración continuada de destinatarios, es posible que tenga la necesidad de mover los buzones de correo de Exchange Online de vuelta a su entorno local.
    
    Para obtener más información sobre cómo mover buzones de correo en una implementación híbrida basada en Exchange 2010, vea [Mover un buzón de Exchange Online a la organización local](https://technet.microsoft.com/es-es/library/hh882527\(v=exchg.150\)).
    
    Para obtener más información sobre cómo mover buzones de correo en implementaciones híbridas basadas en Exchange 2013 o versiones más recientes, vea [Mover buzones de correo entre organizaciones locales y de Exchange Online en implementaciones híbridas](move-mailboxes-between-on-premises-and-exchange-online-organizations-in-hybrid-deployments-exchange-2013-help.md).

  - **Configuración del reenvío de buzones** Los buzones se pueden configurar para reenviar automáticamente a otro buzón el correo que reciban. Aunque Exchange admite el reenvío de buzones, la configuración de reenvío no se copia en Exchange Online al migrar un buzón. Antes de migrar un buzón a Exchange Online, asegúrese de exportar la configuración de reenvío de cada buzón. La configuración de reenvío se guarda en las propiedades `DeliverToMailboxAndForward`, `ForwardingAddress` y `ForwardingSmtpAddress` de cada buzón.

## Componentes de una implementación híbrida de Exchange

Una implementación híbrida implica varios servicios y componentes distintos:

  - **Servidores de Exchange**  Al menos un servidor de Exchange debe estar configurado en su organización local si desea configurar una implementación híbrida. Si está ejecutando Exchange 2013 o una versión más antigua, debe instalar al menos un servidor que ejecute los roles de buzones de correo y acceso de cliente. Si está ejecutando Exchange 2016 o una versión más reciente, debe instalar al menos un servidor que ejecute el rol de buzones de correo. Si es necesario, los servidores de transporte perimetral de Exchange también se pueden instalar en una red perimetral y admitir el flujo de correo seguro con Office 365.
    

    > [!NOTE]
    > No se admite la instalación de servidores de Exchange que ejecuten los roles de servidor de buzones de correo o acceso de cliente en una red perimetral.



  - **Microsoft Office 365**   El servicio Office 365 incluye una organización de Exchange Online como parte del servicio de suscripción. Las organizaciones que van a configurar una implementación híbrida deben adquirir una licencia para cada buzón que se migre o se cree en la organización de Exchange Online.

  - **Asistente para la configuración híbrida**Exchange incluye el Asistente para la configuración híbrida que proporcionan un proceso eficaz para configurar una implementación híbrida entre organizaciones de Exchange locales y organizaciones de Exchange Online.
    
    Para obtener más información, vea [Asistente de configuración híbrida](hybrid-configuration-wizard-exchange-2013-help.md).

  - **Sistema de autenticación de Azure AD**   El sistema de autenticación de Azure Active Directory (AD) es un servicio en la nube gratuito que actúa como agente de confianza entre su organización de Exchange 2016 local y la organización de Exchange Online. Las organizaciones locales que configuran una implementación híbrida deben tener una confianza de federación con el sistema de autenticación de Azure AD. La confianza de federación se puede crear manualmente como parte de la configuración de las características de uso compartido federado entre una organización Exchange local y organizaciones Exchange federadas, o como parte de la configuración de una implementación híbrida con el Asistente para la configuración híbrida. La confianza de federación con el sistema de autenticación de Azure AD para el inquilino de Office 365 se configura automáticamente cuando se activa la cuenta de servicio de Office 365.
    
    Obtenga más información en: [Sistema de autenticación de Azure AD](https://go.microsoft.com/fwlink/p/?linkid=135986).

  - **Sincronización de Azure Active Directory**   La sincronización de Azure AD usa Azure AD Connect para replicar la información de Active Directory local para los objetos con correo habilitado en la organización de Office 365 para dar soporte a la lista de direcciones globales (GAL) unificadas y la autenticación de usuario. Configurar una implementación híbrida de las organizaciones necesitan implementar Azure Connect de AD en un servidor local independiente, para sincronizar su Active Directory local con Office 365.
    
    Obtenga más información en: [Introducción a Azure AD Connect](https://go.microsoft.com/fwlink/p/?linkid=203007).

Terminología básica

## Ejemplo de implementación híbrida

Observe el siguiente escenario. Es un ejemplo de topología que proporciona una descripción general de una implementación de Exchange 2016 típica. Contoso, Ltd. es una organización de un solo dominio y un solo bosque, con dos controladores de dominio y un servidor de Exchange 2016 instalado. Los usuarios remotos de Contoso usan Outlook en la web para conectar a Exchange 2016 en Internet para comprobar sus buzones de correo y acceder a su calendario de Outlook.

![La implementación de Exchange local antes de configurar la implementación híbrida con Office 365](images/JJ200581.dad133ae-d18a-42ec-8f0a-dd1de391200e(EXCHG.150).png "La implementación de Exchange local antes de configurar la implementación híbrida con Office 365")

Imaginemos que es el administrador de red de Contoso y está interesado en configurar una implementación híbrida. Entonces implementa y configura un servidor de Azure AD Connect obligatorio y también decide usar la característica de sincronización de contraseñas de Azure AD Connect, de modo que el usuario pueda usar las mismas credenciales para su cuenta de red local y su cuenta de Office 365. Después de completar los requisitos previos de la implementación híbrida con el Asistente para la configuración híbrida para seleccionar opciones para la implementación híbrida, su nueva topología tiene la siguiente configuración:

  - Los usuarios usarán el mismo nombre de usuario y contraseña para iniciar la sesión en la organización local y de Exchange Online (“inicio de sesión único”).

  - Los buzones de usuario ubicados en la organización local y en la organización de Exchange Online utilizarán el mismo dominio de dirección de correo electrónico. Por ejemplo, los buzones ubicados en el sistema local y los buzones ubicados en la organización de Exchange Online utilizarán @contoso.com en las direcciones de correo electrónico de usuario.

  - Todo el correo saliente se entrega en Internet por la organización local. La organización local controla todo el transporte de mensajería y sirve como retransmisor de la organización de Exchange Online (“transporte de correo centralizado”).

  - Los usuarios de la organización de Exchange Online local pueden compartir información de disponibilidad del calendario entre sí. Las relaciones entre organizaciones configuradas para ambas organizaciones también permiten realizar el seguimiento de mensajes entre instalaciones, sugerencias de correo electrónico y búsqueda de mensajes.

  - Los usuarios del sistema local y de Exchange Online usan la misma dirección URL para conectar a sus buzones en Internet.

![La implementación de Exchange local después de configurar la implementación híbrida con Office 365](images/JJ200581.e8681849-f15d-4d0e-b77e-6105b6096c4b(EXCHG.150).png "La implementación de Exchange local después de configurar la implementación híbrida con Office 365")

Si compara la configuración de organización existente de Contoso y la configuración de la implementación híbrida, observará que al configurar la implementación híbrida se han agregado servidores y servicios que admiten comunicaciones y características adicionales que se comparten entre la organización local y la de Exchange Online. Aquí tiene una descripción general de los cambios que la implementación híbrida ha supuesto en la organización de Exchange local inicial.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Configuración</th>
<th>Antes de configurar una implementación híbrida</th>
<th>Después configurar una implementación híbrida</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Ubicación de buzón</p></td>
<td><p>Sólo buzones locales.</p></td>
<td><p>Buzones locales y en Office 365.</p></td>
</tr>
<tr class="even">
<td><p>Transporte de mensajes</p></td>
<td><p>Los servidores de buzones de correo locales administran todo el enrutamiento de mensajes entrantes y salientes.</p></td>
<td><p>Los servidores de buzones de correo locales administran el enrutamiento de mensajes internos entre la organización local y la organización de Office 365.</p></td>
</tr>
<tr class="odd">
<td><p>Outlook en la web</p></td>
<td><p>Los servidores de buzones de correo locales reciben todas las solicitudes de Outlook en la web y muestran la información del buzón.</p></td>
<td><p>Los servidores de buzones de correo locales redirigen las solicitudes de Outlook en la web a los servidores de buzones de correo de Exchange 2016 locales o proporcionan un vínculo para iniciar sesión en Office 365.</p></td>
</tr>
<tr class="even">
<td><p>GAL unificado para ambas organizaciones</p></td>
<td><p>No aplicable; solo una organización.</p></td>
<td><p>El servidor de sincronización local de Active Directory replica información de Active Directory para los objetos con correo habilitado para Office 365.</p></td>
</tr>
<tr class="odd">
<td><p>Inicio de sesión único usado por ambas organizaciones</p></td>
<td><p>No aplicable; solo una organización.</p></td>
<td><p>La implementación de Active Directory local y Office 365 usan el mismo nombre de usuario y contraseña para los buzones ubicados en la implementación local o en Office 365.</p></td>
</tr>
<tr class="even">
<td><p>Relación de organización establecida y una confianza de federación con el sistema de autenticación de Azure AD</p></td>
<td><p>Se puede configurar una relación de confianza con el sistema de autenticación de Azure AD y relaciones de organización con otras organizaciones federadas de Exchange.</p></td>
<td><p>Se requiere una relación de confianza con el sistema de autenticación de Azure AD. Las relaciones de organización se establecen entre la implementación local y Office 365.</p></td>
</tr>
<tr class="odd">
<td><p>Uso compartido de disponibilidad</p></td>
<td><p>Uso compartido de la disponibilidad sólo entre usuarios locales.</p></td>
<td><p>Uso compartido de la disponibilidad entre los usuarios locales y los usuarios de Office 365.</p></td>
</tr>
</tbody>
</table>


## Aspectos a tener en cuenta antes de configurar una implementación híbrida

Ahora que ya está un poco más familiarizado con las implementaciones híbridas, debe tomar en consideración varios temas importantes. Configurar una implementación híbrida podría afectar a varias áreas de su red y organización de Exchange actuales.

## Sincronización de directorios e inicio de sesión único

La sincronización de Active Directory entre la organización local y la organización de Office 365, que lleva a cabo cada tres horas un servidor que ejecuta Azure Active Directory Connect, es un requisito para configurar una implementación híbrida. La sincronización de directorios permite que los destinatarios de ambas organizaciones se vean en la lista global de direcciones. También sincroniza los nombres de usuario y las contraseñas, lo que permite a los usuarios iniciar sesión con las mismas credenciales en la organización local y en Office 365.


> [!NOTE]
> Si decide configurar Azure AD Connect con AD&nbsp;FS, los nombres de usuario y las contraseñas de los usuarios locales seguirán sincronizándose en Office 365 de forma predeterminada. Sin embargo, los usuarios se autenticarán con su implementación de Active Directory local a través de AD&nbsp;FS como método principal de autenticación. En el caso de que AD&nbsp;FS no pueda conectarse a la implementación de Active Directory local por cualquier motivo, los clientes intentarán volver atrás y autenticarse con los nombres de usuario y las contraseñas sincronizados en Office 365.



Todos los clientes de Azure Active Directory y Office 365 tienen, de forma predeterminada, un límite de 50 000 objetos (usuarios, contactos habilitados para correo y grupos). Esté límite determina cuántos objetos se pueden crear en la organización de Office 365. Cuando se comprueba el primer dominio, este límite aumenta automáticamente a 300 000 objetos. Si ha comprobado un dominio y necesita sincronizar más de 300 000 objetos o no tiene dominios que comprobar y necesita sincronizar más de 50 000 objetos, deberá ponerse en contacto con el departamento de soporte técnico de Azure Active Directory para solicitar un aumento de su límite de cuota de objetos.

Además de un servidor con Azure AD Connect, también debe implementar un servidor proxy de aplicación web si decide configurar AD FS. Este servidor se debe colocar en la red perimetral y actuará como intermediario entre el servidor interno de Azure AD Connect e Internet. El servidor proxy de aplicación web debe aceptar conexiones de clientes y servidores en Internet mediante el puerto TCP 443.

## Administración de implementación híbrida

Gestione la implementación híbrida en Exchange 2016 mediante una única consola de administración unificada que le permite gestionar tanto su organización local como la organización de Exchange Online. El *Centro de administración de Exchange* (EAC), que reemplaza a la Consola de administración de Exchange y al Panel de control de Exchange, le permite conectar y configurar las características de ambas organizaciones. Cuando ejecuta el Asistente para la configuración híbrida por primera vez, se le solicitará que se conecte con su organización de Exchange Online. Debe usar una cuenta de Office 365 que sea miembro del grupo de roles de administración de la organización para conectar el EAC a su organización Exchange Online.

## Certificados

Los certificados digitales de Nivel de sockets seguro (SSL) juegan un papel importante en la configuración de una implementación híbrida. Aportan seguridad a las comunicaciones entre los servidores híbridos locales y la organización Exchange Online. Los certificados son un requisito para configurar varios tipos de servicios. Si ya se están usando certificados digitales en la organización de Exchange, quizá deba modificar los certificados para incluir dominios adicionales o bien adquirir certificados adicionales a una entidad emisora de certificados (CA) de confianza. Si todavía no se usan certificados, deberá adquirir uno o más a una entidad emisora de certificados de confianza.

Encontrará más información en: [Requisitos de certificados para implementaciones híbridas](certificate-requirements-for-hybrid-deployments-exchange-2013-help.md)

## Ancho de banda

La conexión de red a Internet afectará directamente al rendimiento de las comunicaciones entre la organización local y la de Office 365. Esto es especialmente cierto cuando se mueven buzones desde el servidor de Exchange 2016 local a la organización de Office 365. La cantidad de ancho de banda de red disponible, en combinación con el tamaño del buzón y el número de buzones que se mueven paralelamente, dará como resultado cantidades de tiempo diferentes de finalización de los movimientos de buzones. Además, otros servicios de Office 365, como SharePoint Server 2016 y Skype Empresarial, también pueden afectar al ancho de banda disponible para los servicios de mensajería.

Antes de mover los buzones a Office 365, debe:

  - Determinar el tamaño medio de los buzones de correo que se moverán a Office 365.

  - Determinar la media de conexión y velocidad de proceso de la conexión a Internet desde la organización local.

  - Calcular la velocidad de transferencia media esperada y planificar los movimientos de buzón en consecuencia.

Obtenga más información en: [Conexión de red](https://go.microsoft.com/fwlink/p/?linkid=280178).

## Mensajería unificada

La mensajería unificada (UM) es compatible en una implementación híbrida entre las organizaciones locales y de Office 365. La solución de telefonía local debe poder comunicarse con Office 365. Para esto, puede ser necesario comprar hardware y software adicionales.

Si desea mover los buzones desde su organización local a Office 365, y esos buzones están configurados para la mensajería unificada, debe configurar la mensajería unificada en su implementación híbrida antes de mover los buzones. Si mueve los buzones antes de configurar la mensajería unificada en su implementación híbrida, esos buzones ya no tendrán acceso a la funcionalidad de mensajería unificada.

Encontrará más información en: [Configuración de la coexistencia con la mensajería unificada](https://go.microsoft.com/fwlink/p/?linkid=842271)

## Information Rights Management

Information Rights Management (IRM) permite a los usuarios aplicar las plantillas de Active Directory Rights Management Services (AD RMS) a los mensajes que enviaron. Las plantillas AD RMS pueden ayudar a evitar la pérdida de información, ya que permiten a los usuarios controlar quién puede abrir el mensaje protegido por derechos y qué se puede hacer con el mensaje una vez abierto.

IRM en una implementación híbrida requiere planificación, configuración manual de la organización de Office 365 y una comprensión de cómo los clientes usan los servidores AD RMS según si el buzón está en la organización local o en la de Exchange Online.

Encontrará más información en: [IRM en implementaciones híbridas de Exchange](irm-in-exchange-hybrid-deployments-exchange-2013-help.md)

## Dispositivos móviles

En una implementación híbrida, los dispositivos móviles son compatibles. Si Exchange ActiveSync ya está habilitado en los servidores existentes, continuarán redirigiendo las solicitudes desde dispositivos móviles a buzones situados en el servidor de buzones de correo locales. En los dispositivos móviles que se conectan a los buzones existentes y que se mueven de la organización local a Office 365, los perfiles de Exchange ActiveSync se actualizarán automáticamente para que se conecten a Office 365 en la mayoría de los teléfonos. Todos los dispositivos móviles que admitan Exchange ActiveSync serán compatibles con una implementación híbrida.

Obtenga más información en: [Telefonía móvil](http://go.microsoft.com/fwlink/p/?linkid=206387).

## Requisitos del cliente

Se recomienda que los clientes usen Outlook 2016 o Outlook 2013 para obtener la mejor experiencia y rendimiento en la implementación híbrida. Los clientes anteriores a Outlook 2010 no son compatibles con las implementaciones híbridas o con Office 365.

## Licencias para Office 365

Para crear o mover buzones en Office 365, deberá registrarse en Office 365 para empresas y contar con licencias disponibles. Cuando se registre en Office 365, recibirá un número específico de licencias que podrá asignar a nuevos buzones o a buzones movidos desde la organización local. Cada buzón de correo en Office 365 debe tener una licencia.

## Servicios antivirus y contra correo no deseado

Los buzones que se han movido a Office 365 reciben automáticamente la protección antivirus y contra correo no deseado provista por Exchange Online Protection (EOP), un servicio proporcionado por Office 365. Es posible que deba adquirir licencias adicionales de EOP para sus usuarios locales si elige enrutar todo el correo entrante de Internet a través del servicio de EOP. Se recomienda evaluar detenidamente si su protección de EOP de Office 365 también es apropiada para satisfacer las necesidades de protección antivirus y contra correo no deseado de la organización local. Si ha establecido protección en la organización local, debe actualizar o configurar las soluciones locales antivirus y contra correo no deseado de manera que brinden la máxima protección en toda la organización.

Encontrará más información en: [Protección antimalware y contra correo electrónico no deseado](https://technet.microsoft.com/es-es/library/jj200731\(v=exchg.150\))

## Carpetas públicas

Office 365 admite carpetas públicas, y las carpetas públicas locales se pueden migrar a Office 365. Además, es posible mover las carpetas públicas de Office 365 a la organización de Exchange 2016 local. Tanto los usuarios locales como de Office 365 pueden acceder a las carpetas públicas situadas en cualquier organización con Outlook en la web, Outlook 2016, Outlook 2013, Outlook 2010 SP2 o versiones más recientes. La configuración de la carpeta pública local existente y el acceso para los buzones locales no cambia al configurar una implementación híbrida.

Encontrará más información en: [Carpetas públicas](https://technet.microsoft.com/es-es/library/jj150538\(v=exchg.150\))

## Accesibilidad

Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de esta lista de comprobación, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](https://technet.microsoft.com/es-es/library/jj150484\(v=exchg.150\)).

## Terminología básica

En la siguiente lista se muestran las definiciones de los componentes principales asociados a las implementaciones híbridas en Exchange 2013.

  - **transporte de correo centralizado**  
    Opción de configuración híbrida en la que los mensajes de Internet entrantes y salientes de Exchange Online se enrutan a través de la organización local de Exchange. Esta opción de enrutamiento se configura en el asistente de configuración híbrida. Para obtener más información, vea [Opciones de transporte en las implementaciones híbridas de Exchange](transport-options-in-exchange-hybrid-deployments-exchange-2013-help.md).

<!-- end list -->

  - **dominio de coexistencia**  
    Dominio aceptado que se agrega a la organización local para el flujo de correo híbrido y las solicitudes de detección automática del servicio de Office 365. Este dominio se agrega como un dominio proxy secundario a cualquier directiva de direcciones de correo electrónico que tenga plantillas *PrimarySmtpAddress* para los dominios seleccionados en el asistente de configuración híbrida. De manera predeterminada, es \<domain\>.mail.onmicrosoft.com.

<!-- end list -->

  - ***HybridConfiguration* Objeto de Active Directory**  
    Objeto de Active Directory en la organización local que contiene los parámetros de configuración de implementación híbrida deseados definidos por las opciones elegidas en el asistente de configuración híbrida. El motor de configuración híbrida usa estos parámetros al configurar los valores locales y de Exchange Online para habilitar las características híbridas. El contenido del objeto *HybridConfiguration* se restablece cada vez que se ejecuta el asistente de configuración híbrida.

<!-- end list -->

  - **motor de configuración híbrida**  
    El motor de configuración híbrida (HCE) ejecuta las acciones centrales necesarias para configurar y actualizar una implementación híbrida. El HCE compara el estado del objeto *HybridConfiguration* de Active Directory con los valores de configuración de Exchange local y Exchange Online y, después, ejecuta tareas para hacer coincidir los valores de configuración de la implementación con los parámetros definidos en el objeto *HybridConfiguration* de Active Directory. Para obtener más información, vea [Motor de configuración híbrida](hybrid-configuration-wizard-exchange-2013-help.md).

<!-- end list -->

  - **asistente de configuración híbrida (HCW)**  
    Herramienta adaptable incluida en Exchange que guía a los administradores por los pasos para configurar una implementación híbrida entre las organizaciones locales y de Exchange Online. El asistente define los parámetros de configuración de la implementación híbrida en el objeto *HybridConfiguration* e indica al motor de configuración híbrida que ejecute las tareas de configuración necesarias para habilitar las características híbridas definidas. Para obtener más información, vea [Asistente de configuración híbrida](hybrid-configuration-wizard-exchange-2013-help.md).

<!-- end list -->

  - **Implementación híbrida basada en Exchange 2010**  
    Implementación híbrida configurada con el Service Pack 3 (SP3) para los servidores locales de Exchange Server 2010 como el punto de conexión para los servicios de Office 365 y Exchange Online. Se trata de una opción de implementación híbrida para las organizaciones locales de Exchange 2010, Exchange Server 2007 y Exchange Server 2003.

<!-- end list -->

  - **Implementación híbrida basada en Exchange 2013**  
    Implementación híbrida configurada con los servidores locales de Exchange 2013 como el punto de conexión para los servicios de Office 365 y Exchange Online. Se trata de una opción de implementación híbrida para las organizaciones locales de Exchange 2013, Exchange 2010 y Exchange 2007.

<!-- end list -->

  - **Implementación híbrida basada en Exchange 2016**  
    Implementación híbrida configurada con los servidores locales de Exchange 2016 como el punto de conexión para los servicios de Office 365 y Exchange Online. Se trata de una opción de implementación híbrida para las organizaciones locales de Exchange 2016, Exchange 2013 y Exchange 2010.

<!-- end list -->

  - **transporte de correo seguro**  
    Característica de una implementación híbrida configurada automáticamente que habilita la mensajería segura entre organizaciones locales y de Exchange Online. Los mensajes se cifran y se autentican mediante la Seguridad de la capa de transporte (TLS) con un certificado seleccionado en el Asistente para la configuración híbrida. El inquilino de Office 365 es el punto de conexión para las conexiones de transporte híbrido que se originen desde la organización local y el origen de las conexiones de transporte híbrido hasta la organización local de Exchange Online.

Terminología básica

## Documentación de implementación híbrida de Exchange

La tabla a continuación contiene vínculos a temas que le ayudarán a saber más acerca de las implementaciones híbridas en Microsoft Exchange y de administrarlas.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tema</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="hybrid-configuration-wizard-exchange-2013-help.md">Asistente de configuración híbrida</a></p></td>
<td><p>Conozca cómo el asistente de la configuración híbrida y el motor de configuración híbrida configuran una implementación híbrida.</p></td>
</tr>
<tr class="even">
<td><p><a href="hybrid-deployment-prerequisites-exchange-2013-help.md">Requisitos previos de implementación híbrida</a></p></td>
<td><p>Obtenga más información sobre los prerrequisitos para una implementación híbrida, incluyendo las organizaciones con servidores Exchange compatibles, requisitos de Office 365 y otros requisitos de configuración local.</p></td>
</tr>
<tr class="odd">
<td><p><a href="certificate-requirements-for-hybrid-deployments-exchange-2013-help.md">Requisitos de certificados para implementaciones híbridas</a></p></td>
<td><p>Más información sobre los requisitos para certificados digitales en las implementaciones híbridas.</p></td>
</tr>
<tr class="even">
<td><p><a href="transport-options-in-exchange-hybrid-deployments-exchange-2013-help.md">Opciones de transporte en las implementaciones híbridas de Exchange</a></p></td>
<td><p>Obtengas más información sobre las opciones de transporte de mensajes entrantes y salientes en las implementaciones híbridas.</p></td>
</tr>
<tr class="odd">
<td><p><a href="transport-routing-in-exchange-hybrid-deployments-exchange-2013-help.md">Enrutamiento de transporte en las implementaciones híbridas de Exchange</a></p></td>
<td><p>Obtengas más información sobre las opciones de enrutamiento de mensajes entrantes y salientes en las implementaciones híbridas.</p></td>
</tr>
<tr class="even">
<td><p><a href="hybrid-management-in-exchange-hybrid-deployments-exchange-2013-help.md">Administración híbrida en las implementaciones híbridas de Exchange</a></p></td>
<td><p>Obtenga más información sobre la gestión de implementaciones híbridas con el Centro de administración de Exchange y el Shell de administración de Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><a href="shared-free-busy-in-exchange-hybrid-deployments-exchange-2013-help.md">Información de disponibilidad compartida en implementaciones híbridas de Exchange</a></p></td>
<td><p>Obtenga más información sobre la disponibilidad del calendario compartido entre las organizaciones Exchange locales y Online en una implementación híbrida.</p></td>
</tr>
<tr class="even">
<td><p><a href="server-roles-in-exchange-hybrid-deployments-exchange-2013-help.md">Roles de servidor en implementaciones híbridas de Exchange</a></p></td>
<td><p>Obtenga más información sobre el modo en el que funcionan los roles del servidor de Exchange en una implementación híbrida.</p></td>
</tr>
<tr class="odd">
<td><p><a href="irm-in-exchange-hybrid-deployments-exchange-2013-help.md">IRM en implementaciones híbridas de Exchange</a></p></td>
<td><p>Obtenga más información sobre cómo funciona Information Rights Management en una implementación híbrida.</p></td>
</tr>
<tr class="even">
<td><p><a href="permissions-in-exchange-hybrid-deployments-exchange-2013-help.md">Permisos en implementaciones híbridas de Exchange</a></p></td>
<td><p>Más información sobre cómo utiliza una implementación híbrida el control de acceso basado en roles (RBAC) para controlar los permisos.</p></td>
</tr>
<tr class="odd">
<td><p><a href="edge-transport-servers-with-hybrid-deployments-exchange-2013-help.md">Servidores de transporte perimetral con implementaciones híbridas</a></p></td>
<td><p>Obtenga más información sobre los servidores de Exchange de transporte perimetral y sobre cómo se implementan y operan en una implementación híbrida.</p></td>
</tr>
<tr class="even">
<td><p><a href="single-sign-on-with-hybrid-deployments-exchange-2013-help.md">Inicio de sesión único con implementaciones híbridas</a></p></td>
<td><p>Obtenga más información sobre el modo en el que funciona el inicio de sesión único mediante la sincronización de contraseña y AD FS en una implementación híbrida.</p></td>
</tr>
<tr class="odd">
<td><p><a href="hybrid-deployment-procedures-exchange-2013-help.md">Procedimientos de implementación híbrida</a></p></td>
<td><p>Explore los procedimientos para crear y modificar las implementaciones híbridas en sus organizaciones de Exchange locales y en sus organizaciones de Exchange Online.</p></td>
</tr>
<tr class="even">
<td><p><a href="hybrid-deployments-with-exchange-2013-and-exchange-2010-exchange-2013-help.md">Implementaciones híbridas con Exchange 2013 y Exchange 2010</a></p></td>
<td><p>Obtenga más información acerca de las implementaciones híbridas basadas en Exchange 2013 con organizaciones de Exchange 2010.</p></td>
</tr>
<tr class="odd">
<td><p><a href="hybrid-deployments-with-exchange-2013-and-exchange-2007-exchange-2013-help.md">Implementaciones híbridas con Exchange 2013 y Exchange 2007</a></p></td>
<td><p>Obtenga más información acerca de implementaciones híbridas basadas en Exchange 2013 con organizaciones de Exchange 2007.</p></td>
</tr>
</tbody>
</table>


## ¿Es la primera vez que usa Office 365?


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/Dn249373.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="Icono reducido de LinkedIn Learning" alt="Icono reducido de LinkedIn Learning" /> <strong>¿Es la primera vez que usa Office 365?</strong><br />
LinkedIn Learning pone a su disposición vídeos gratuitos de cursos de <a href="https://support.office.com/es-es/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a>.</p></td>
</tr>
</tbody>
</table>

