---
title: 'Certificados digitales y SSL: Exchange 2013 Help'
TOCTitle: Certificados digitales y SSL
ms:assetid: a9e2e08c-d46a-4135-a387-eb653212b676
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd351044(v=EXCHG.150)
ms:contentKeyID: 48268535
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Certificados digitales y SSL

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2013-08-26_

Capa de sockets seguros (SSL) es un método para proteger la comunicación entre un cliente y un servidor. Para Exchange Server 2013, se usa SSL para ayudar a asegurar las comunicaciones entre el servidor y los clientes. Los clientes pueden ser teléfonos móviles, equipos de la red de una organización y equipos situados fuera de la red de una organización.

De manera predeterminada, al instalar Exchange 2013, las comunicaciones del cliente se cifran con SSL cuando se usa Outlook Web App, Exchange ActiveSync y Outlook Anywhere.

SSL requiere el uso de certificados digitales. En este tema se ofrece una breve descripción de los distintos tipos de certificados digitales, así como información sobre el modo de configurar Exchange 2013 para que use este tipo de certificados digitales.

**Contenido**

Introducción a los certificados digitales

Certificados digitales y conexiones proxy

Prácticas recomendadas con los certificados digitales

## Introducción a los certificados digitales

Los certificados digitales son archivos electrónicos que funcionan como una contraseña en línea para comprobar la identidad de un usuario o equipo. Sirven para crear el canal cifrado de SSL, que a su vez se usa para las comunicaciones del cliente. Un certificado es una declaración digital emitida por una entidad de certificación (CA) que garantiza la identidad del poseedor del certificado y permite que las partes se comuniquen de forma segura mediante el cifrado.

Los certificados digitales hacen lo siguiente:

  - Dan fe de que sus poseedores (personas, sitios web e incluso recursos de red como enrutadores) son de verdad quien dicen ser.

  - Protegen los datos que se intercambian en línea de posibles manipulaciones o robos.

Los certificados digitales pueden ser emitidos por una entidad de certificación de terceros o por una infraestructura de clave pública de Windows de confianza, mediante el uso de los servicios de servidor de certificados, o también se pueden autofirmar. Cada tipo de certificado tiene sus ventajas y desventajas. Todos los tipos de certificado digital están protegidos contra las manipulaciones y no se pueden falsificar.

Se pueden emitir certificados para varios usos. Por ejemplo, autenticación de usuario web, autenticación de servidor web, extensiones seguras multipropósito al correo de Internet (S/MIME), protocolo de seguridad de Internet (IPsec), seguridad de nivel de transporte (TLS) y firmas de código.

Un certificado contiene y vincula una clave pública con la identidad de la persona, el equipo o el servicio que posee la clave privada correspondiente. Tanto el cliente como el servidor usan las claves públicas y privadas para cifrar los datos antes de transmitirlos. En los usuarios, equipos y servicios basados en Windows, la confianza en una CA se establece cuando hay una copia del certificado raíz en el almacén de certificados raíz de confianza y el certificado contiene una ruta de certificación válida. Para que el certificado sea válido, no se tiene que haber revocado y su período de validez no tiene que haber expirado.

## Tipos de certificados

Se suelen usar tres tipos de certificados digitales principales: certificados autofirmados, certificados generados por una infraestructura de clave pública (PKI) de Windows y certificados emitidos por terceros.

## Certificados autofirmados

Cuando instala Exchange 2013, se configura de manera automática un certificado autofirmado en los servidores de buzones de correo. La aplicación que creó este certificado autofirmado es la que lo firma. El asunto y el nombre del certificado son iguales. El emisor y el asunto se definen en el certificado. Este certificado autofirmado se usa para cifrar comunicaciones entre el servidor de acceso de cliente y el servidor de buzones de correo. El servidor de acceso de cliente confía en el certificado autofirmado del servidor de buzones de correo automáticamente, así que no es necesario un certificado de terceros en el servidor de buzones de correo. Cuando instala Exchange 2013, también se crea un certificado autofirmado en los servidores de acceso de cliente. Este certificado autofirmado permitirá que algunos protocolos de cliente usen SSL para sus comunicaciones. Exchange ActiveSync y Outlook Web App pueden establecer una conexión SSL usando un certificado autofirmado. Outlook en cualquier lugar no funciona con un certificado autofirmado en el servidor de acceso de cliente. Los certificados autofirmados se tienen que copiar manualmente en el almacén de certificados de raíz de confianza del equipo o dispositivo móvil del cliente. Cuando un cliente se conecta a un servidor mediante SSL y el servidor presenta un certificado autofirmado, se le solicitará al cliente que compruebe que el certificado haya sido emitido por una autoridad de confianza. El cliente debe hacer explícita su confianza en la entidad de certificación. Si el cliente confirma su confianza, las comunicaciones SSL podrán seguir su curso.


> [!NOTE]
> De manera predeterminada, el certificado digital que se instala en el servidor o servidores de buzones de correo es un certificado autofirmado. No es necesario sustituir el certificado autofirmado en los servidores de buzones de correo de su organización por un certificado de terceros de confianza. El servidor de acceso de cliente confía automáticamente en el certificado autofirmado del servidor de buzones de correo, así que no es necesaria ninguna otra configuración para los certificados en el servidor de buzones de correo.



Es frecuente que organizaciones pequeñas decidan no usar certificados de terceros o no instalar su propia PKI para emitir certificados. Esta decisión puede deberse a que las soluciones son demasiado caras, a que sus administradores carezcan de la experiencia y los conocimientos necesarios para crear una jerarquía de certificados o a ambas razones. El uso de certificados autofirmados tiene un costo mínimo y una configuración muy sencilla. Sin embargo, establecer una infraestructura para la administración del ciclo de vida, la renovación, la administración de la confianza y la revocación de los certificados es mucho más difícil con los certificados autofirmados.

## Certificados de infraestructura de clave pública de Windows

El segundo tipo de certificado son los certificados generados por una PKI de Windows. Una infraestructura de clave pública (PKI) es un sistema de certificados digitales, entidades de certificación (CA) y entidades de registro (RA), que comprueban y autentican la validez de cada parte implicada en una transacción electrónica mediante el uso de criptografía con claves públicas. Al implementar una PKI en una organización que usa Active Directory, se proporciona una infraestructura para la administración del ciclo de vida, la renovación, la administración de la confianza y la revocación de los certificados. Todo esto, sin embargo, lleva un costo asociado al tener que implementar servidores e infraestructuras adicionales para crear y administrar certificados generados por una PKI de Windows.

Los servicios de servidor de certificados son necesarios para implementar una PKI de Windows y se pueden instalar desde **Agregar o quitar programas**, en el Panel de control. Los Servicios de servidor de certificados se pueden instalar en cualquier servidor del dominio.

Si obtiene certificados de una CA de Windows unida a un dominio, puede usar la CA para solicitar o firmar certificados que emitirá a sus propios servidores o equipos de la red. Esto le permite usar una PKI como si se tratara de un proveedor externo de certificados, pero con menor costo. Los certificados de PKI no pueden utilizarse públicamente como otros tipos de certificado. Sin embargo, cuando una CA de PKI firma el certificado del solicitante usando la clave privada, se verifica el solicitante. La clave pública de esta CA es parte del propio certificado de la CA. Un servidor que tenga este certificado en el almacén de certificados de raíz de confianza puede usar esa clave pública para autenticar al solicitante y descifrar su certificado.

Los pasos para implementar un certificado generado por PKI se parecen a los que se deben seguir para implementar un certificado autofirmado. Aún tiene que instalar una copia del certificado raíz de confianza desde la PKI al almacén de certificados de raíz de confianza de los equipos o dispositivos móviles con los que quiere establecer una conexión SSL a Microsoft Exchange.

Una PKI de Windows permite a las organizaciones publicar sus propios certificados. Los clientes pueden solicitar y recibir certificados de una PKI de Windows en la red interna. La PKI de Windows puede renovar o revocar certificados.

## Certificados de terceros de confianza

Los certificados comerciales o de terceros son certificados generados por una CA externa o comercial, adquiridos para usarlos en sus servidores de red. Uno de los problemas de los certificados autofirmados o basados en PKI es que, debido a que la confianza del certificado no se realiza de manera automática por el equipo o dispositivo móvil del cliente, debe asegurarse de importarlo en el almacén de certificados raíz de confianza de los dispositivos y los equipos del cliente. Los certificados comerciales o de terceros no tienen este problema. La mayoría de los certificados de CA comerciales son de confianza porque el certificado ya reside en el almacén de certificados raíz de confianza. Dado que el emisor es de confianza, el certificado también lo es. El uso de certificados de terceros simplifica notablemente la implementación.

Para las organizaciones de mayor tamaño o las que deben implementar certificados de forma pública, el uso de certificados comerciales o de terceros es la mejor solución, a pesar del costo que llevan asociado. Los certificados comerciales pueden no ser la mejor solución para las organizaciones de pequeño o mediano tamaño, para las que puede preferir usar alguna de las otras opciones de certificados que hay disponibles.

Volver al principio

## Elección de un tipo de certificado

En el momento de elegir el tipo de certificado que se va a instalar, se deben tener en cuenta varios factores. El certificado debe estar firmado para ser válido. Se puede autofirmar o lo puede firmar una CA. Un certificado autofirmado tiene algunas limitaciones. Por ejemplo, no todos los dispositivos móviles permiten a un usuario instalar un certificado digital en el almacén de certificados raíz de confianza. La posibilidad de instalar certificados en un dispositivo móvil depende del fabricante del dispositivo móvil y del proveedor del servicio móvil. Algunos fabricantes y proveedores de servicio móvil deshabilitan el acceso al almacén de certificados raíz de confianza. En tal caso, no se pueden instalar en el dispositivo móvil ni un certificado autofirmado ni un certificado de una CA de PKI de Windows.

## Certificados de Exchange predeterminados

De manera predeterminada, Exchange instala un certificado autofirmado en el servidor de acceso de cliente y en el servidor de buzones de correo para cifrar todas las comunicaciones de red. A este respecto, para que todas las comunicaciones de la red se cifren es necesario que cada servidor de Exchange posea un certificado X.509 que pueda usar. El certificado autofirmado se debe sustituir en el servidor de acceso de cliente por uno en el que los clientes confíen automáticamente.

“Autofirmado” significa que ha sido el propio servidor de Exchange el que ha creado y firmado el certificado. Al no haber sido creado ni firmado por una entidad de certificación de confianza general, el certificado autofirmado y predeterminado no será de confianza para ningún software, salvo para otros servidores de Exchange de la misma organización. El certificado predeterminado está habilitado para todos los servicios de Exchange. Tiene un nombre alternativo de asunto (SAN) que corresponde al nombre del servidor de Exchange en el que está instalado. También tiene una lista de SAN que incluye el nombre del servidor y el nombre de dominio completo (FQDN) del servidor.

Si bien el resto de servidores de Exchange de la organización de Exchange confían en este certificado automáticamente, no sucederá lo mismo con clientes como los exploradores web, los clientes de Outlook, los teléfonos móviles, otros clientes de correo electrónico y los servidores de correo electrónico externos. Por lo tanto, plantéese sustituir este certificado por un certificado de terceros de confianza en sus servidores de acceso de cliente de Exchange. En caso de que posea su propia PKI interna y todos los clientes confíen en ella, también puede usar certificados de emisión propia.

## Requisitos de certificado por servicio

Los certificados se usan para varias cosas en Exchange. De igual modo, la mayoría de los clientes usa los certificados en más de un servidor de Exchange. Por lo general, cuanto menor sea el número de certificados existente, más sencillo será administrarlos.

## IIS

Todos los servicios siguientes de Exchange usan el mismo certificado en un servidor de acceso de cliente de Exchange determinado:

  - Outlook Web App

  - Centro de administración (EAC) de Exchange

  - Servicios Web Exchange

  - Exchange ActiveSync

  - Outlook en cualquier lugar

  - Detección automática

  - Distribución de la Libreta de direcciones de Outlook

Dado que solo se puede asociar un certificado a un sitio web y que, de manera predeterminada, todos estos servicios se suministran en un único sitio web, el certificado en cuestión deberá contener todos los nombres que los clientes de estos servicios usen (o bien incluirlos en un nombre comodín).

## POP/IMAP

Los certificados usados para POP o IMAP pueden especificarse independientemente del certificado usado para IIS. Sin embargo, para simplificar la administración, recomendamos incluir el nombre del servicio POP o IMAP en el certificado IIS y usar un único certificado para todos los servicios.

## SMTP

Se puede usar un certificado independiente para cada conector de recepción que configure. Dicho certificado deberá incluir el nombre que los clientes SMTP (u otros servidores SMTP) usan para llegar al conector. Para que la administración de certificados sea más sencilla, considere la posibilidad de incluir en un solo certificado todos los nombres para los que es necesario el tráfico TLS.

## Certificados digitales y conexiones proxy

Una conexión proxy es el método por el cual un servidor envía conexiones de cliente a otro servidor. En el caso de Exchange 2013, esto se produce cuando el servidor de acceso de cliente realiza una conexión proxy con una solicitud de cliente entrante en el servidor de buzones de correo que contiene la copia activa del buzón de correo del cliente.

Cuando los servidores de acceso de cliente envían solicitudes mediante proxy, se usa SSL para cifrarlas, pero no para autenticarlas. El certificado autofirmado en el servidor de buzones de correo cifra el tráfico entre el servidor de acceso de cliente y el servidor de buzones de correo.

## Certificados y proxy inverso

Muchas de las implementaciones de Exchange usan proxy inverso para publicar servicios de Exchange en Internet. Los proxy inversos se pueden configurar para terminar el cifrado SSL, examinar el tráfico a salvo en el servidor y, a continuación, abrir un nuevo canal de cifrado SSL que vaya de los servidores proxy inversos a los servidores de Exchange que hay detrás. Esto se conoce como protocolo de puente SSL. Otra forma de configurar los servidores proxy inversos consiste en dejar que las conexiones SSL atraviesen directamente los servidores de Exchange que hay tras los servidores proxy inversos. En cualquier caso, los clientes en Internet se conectan al servidor proxy inverso por medio de un nombre de host para el acceso de Exchange, como mail.contoso.com. Entonces, el servidor proxy inverso se conecta a Exchange con otro nombre de host distinto, como el nombre de equipo del servidor de acceso de cliente de Exchange. No es preciso incluir en el certificado el nombre de equipo del servidor de acceso de cliente de Exchange, ya que casi todos los servidores proxy inversos más habituales son capaces de relacionar el nombre de host que el cliente usa con el nombre de host interno del servidor de acceso de cliente de Exchange.

## SSL y DNS dividido

El DNS dividido es una tecnología que permite configurar varias direcciones IP para el mismo nombre de host en función de la procedencia de la solicitud de DNS de origen. Esto se conoce también como DNS de horizonte dividido, DNS de vista dividida o DNS de cerebro dividido. El DNS dividido contribuye a reducir el número de nombres de host que se debe administrar en Exchange, al permitir que los clientes se conecten a Exchange a través del mismo nombre de host, independientemente de si se conectan desde Internet o desde una intranet. Además, gracias al DNS dividido, las solicitudes procedentes de la intranet pueden obtener una dirección IP distinta de las solicitudes que provienen de Internet.

El DNS dividido no suele ser necesario en una implementación de Exchange a pequeña escala, ya que los usuarios pueden tener acceso al mismo extremo DNS, ya provengan de la intranet o de Internet. Sin embargo, en implementaciones de mayor envergadura, esta configuración derivará en una elevada carga tanto en el servidor proxy de Internet saliente como en el servidor proxy inverso. En estas implementaciones, configure el DNS dividido de tal modo, por ejemplo, que los usuarios externos obtengan acceso a mail.contoso.com y los internos, a internal.contoso.com. Si usa el DNS dividido de esta forma, los usuarios no tendrán que recordar distintos nombres de host en función de dónde se encuentren.

## Windows PowerShell remoto

La autenticación Kerberos y el cifrado Kerberos se utilizan para el acceso a Windows PowerShell remoto, tanto desde el Centro de administración (EAC) de Exchange como desde el Shell de administración de Exchange. Por lo tanto, no tendrá que configurar los certificados SSL para usarlos con Windows PowerShell remoto.

Volver al principio

## Prácticas recomendadas con los certificados digitales

Aunque la configuración de los certificados digitales de la organización variará en función de sus necesidades específicas, a continuación se incluye información sobre prácticas recomendadas que puede serle útil a la hora de elegir la configuración de certificados digitales más adecuada.

## Procedimiento recomendado: Usar un certificado de terceros de confianza

A fin de evitar que los clientes reciban errores relativos a certificados que no son de confianza, el certificado que el servidor de Exchange use debe proceder de alguien en quien el cliente confíe. Si bien la mayoría de los clientes se puede configurar de forma que confíe en cualquier certificado o emisor de certificado, resulta más sencillo usar un certificado de terceros de confianza en el servidor de Exchange. Esto es así porque casi todos los clientes ya confían en sus certificados raíz. Existen varios emisores de certificados de terceros que ofrecen certificados configurados expresamente para Exchange. Puede usar el EAC para generar solicitudes de certificado que sean aptos para la mayoría de los emisores de certificados.

## Cómo seleccionar una entidad de certificación

Una entidad de certificación es una compañía que emite certificados y garantiza la validez de los mismos. El software cliente (por ejemplo, exploradores como Microsoft Internet Explorer o sistemas operativos como Windows o Mac OS) disponen de una lista integrada de entidades de certificación en las que confían. Normalmente, esta lista se puede configurar para agregar y quitar entidades, pero a menudo dicha configuración es en exceso engorrosa. Use los siguientes criterios a la hora de seleccionar una entidad de certificación para adquirir los certificados:

  - Asegúrese de que la entidad de certificación es de confianza para el software cliente (sistemas operativos, exploradores, teléfonos móviles) que se va a conectar a los servidores de Exchange.

  - Elija una entidad de certificación que admita, por ejemplo, “certificados de comunicaciones unificadas” para usar con el servidor de Exchange.

  - Asegúrese de que la entidad de certificación admite los tipos de certificado que va a usar. Considere la utilización de certificados de nombre alternativo de asunto (SAN). No todas las CA admiten certificados SAN, mientras que otras no admiten la cantidad de nombres de host que se pueden necesitar.

  - Asegúrese de que la licencia que adquiere para los certificados permite poner dicho certificado en el número de servidores que tiene previsto usar. Algunas entidades emisoras de certificados sólo permiten colocar un certificado en un servidor.

  - Compare los precios de certificado entre las distintas entidades de certificación.

## Procedimiento recomendado: Uso de certificados de SAN

En función de cómo configure los nombres del servicio en la implementación de Exchange, el servidor Exchange requerirá un certificado que puede representar varios nombres de dominio. Aunque un certificado comodín, como uno para \*.contoso.com, puede solucionar este tipo de problemas, muchos clientes no se sienten cómodos con las implicaciones de seguridad que supone conservar un certificado que se puede usar para cualquier subdominio. Una opción más segura es crear una lista con todos los dominios necesarios como nombres alternativos de sujeto en el certificado. De forma predeterminada, este método se usa cuando Exchange genera las solicitudes de certificado.

## Procedimiento recomendado: Usar el Asistente para certificados de Exchange para solicitar certificados

Muchos servicios en Exchange utilizan certificados. Un error común al solicitar certificados es hacer la solicitud sin incluir el conjunto correcto de nombres de servicios. El asistente para solicitar certificados del Centro de administración de Exchange le ayudará a incluir la lista de nombres apropiada en la solicitud del certificado. Con este asistente podrá especificar los servicios con los que el certificado va a funcionar y, según cuáles sean esos servicios, incluir los nombres que deben estar en el certificado para que, así, se pueda usar con dichos servicios. Ejecute el Asistente para certificados cuando haya implementado el conjunto inicial de servidores de Exchange 2013 y haya decidido cuáles van a ser los nombres de host que se van a usar para los distintos servicios de la implementación. En teoría, solo tendrá que ejecutar este asistente una vez por cada sitio de Active Directory en el que implemente Exchange.

En lugar de preocuparse por si se deja algún nombre de host de la lista de SAN del certificado adquirido, puede acudir a una entidad de certificación que ofrezca, sin cargo adicional alguno, un periodo de gracia durante el cual puede devolver un certificado y solicitarlo de nuevo con algunos nombres de host más.

## Procedimiento recomendado: Usar el menor número de nombres de host posible

Aparte de usar cuantos menos certificados posible, es igualmente aconsejable usar el menor número de nombres de host que pueda. De esta forma, se ahorrará dinero. Muchos proveedores de certificados tienen un recargo establecido en función de la cantidad de nombres de host que se agregan al certificado.

Lo que más le puede ayudar a reducir el número de nombres de host que necesita y, por ende, a simplificar la administración de los certificados, es no incluir nombres de host de servidor entre los nombres alternativos del sujeto del certificado.

Los nombres de host que debe incluir en los certificados de Exchange son aquéllos que las aplicaciones cliente usan para conectarse a Exchange. A continuación se enumeran los nombres de host habituales que se necesitarán para una compañía llamada Contoso:

  - **Mail.contoso.com**   Nombre de host que cubre la mayoría de las conexiones a Exchange, incluyendo MicrosoftOutlook, Outlook Web App, Outlook en cualquier lugar, la Libreta de direcciones sin conexión, los servicios web de Exchange, POP3, IMAP4, SMTP, el panel de control de Exchange y ActiveSync.

  - **Autodiscover.contoso.com**   Nombre de host que usan los clientes que admiten la detección automática, como Microsoft Office Outlook 2007 y versiones posteriores, Exchange ActiveSync y los clientes de los servicios web de Exchange.

  - **Legacy.contoso.com**   Nombre de host necesario en un escenario de coexistencia con Exchange 2007 y Exchange 2013. Si va a tener clientes con buzones de correo en Exchange 2007 y Exchange 2013, la configuración de un nombre de host heredado evitará que los usuarios se vean obligados a memorizar una segunda dirección URL durante el proceso de actualización.

## Descripción de los certificados comodín

Un certificado comodín está diseñado para admitir un dominio y varios subdominios. Por ejemplo, si configura un certificado comodín para \*.contoso.com, obtendrá un certificado que funciona en mail.contoso.com, web.contoso.com y autodiscover.contoso.com.

Volver al principio

