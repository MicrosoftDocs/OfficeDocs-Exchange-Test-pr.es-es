---
title: 'Sensibilidad de errores de consultas DNS: Exchange 2013 Help'
TOCTitle: Sensibilidad de errores de consultas DNS
ms:assetid: a3c3980c-20ca-4b54-a2e6-76d49af620b4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb676467(v=EXCHG.150)
ms:contentKeyID: 52062053
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Sensibilidad de errores de consultas DNS

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2014-12-02_

En Microsoft Exchange Server 2013, el grado de sensibilidad de consulta DNS se puede ajustar para lograr que los mensajes se entreguen un poco más rápido cuando se produzcan errores DNS en relación con el dominio de destino. No obstante, en función de los errores DNS, este ajuste podría provocar errores en la entrega si se dan determinadas circunstancias.

## Consultas DNS y entrega de mensajes remota

El servidor Exchange responsable de la entrega de mensajes a los destinatarios externos debe poder encontrar un servidor de mensajería de destino que acepte correo para los destinatarios externos. En función del destino, los mensaje se ponen en una o más colas de entrega remotas mientras esperan la entrega a los destinatarios remotos. Para obtener más información acerca de las colas de entrega, vea [Colas](queues-exchange-2013-help.md) .

El servidor Exchange consulta los servidores DNS configurados de modo que encuentren los registros DNS necesarios para entregar el mensaje. Los servidores DNS son necesarios en el orden en que aparecen en la lista. Si uno de los servidores DNS no está disponible, la consulta pasa al siguiente servidor DNS en la lista. Los servidores DNS se consultan para obtener la información siguiente:

  - **Registros Mail eXchange (MX) para la parte del dominio del destinatario externo**   El registro MX contiene el nombre de dominio completo (FQDN) del servidor de mensajería que es el responsable de aceptar los mensajes para el dominio, así como un valor de preferencia para el servidor de mensajería. Un valor de preferencia inferior indica un servidor de mensajería preferido. El valor de preferencia es importante si el dominio tiene más de un registro MX. Para optimizar la tolerancia a errores, la mayoría de las organizaciones utilizan varios servidores de mensajería y varios registros MX con valores de preferencia distintos.

  - **Registros de dirección (A) para los servidores de mensajería de destino**   Cada servidor de mensajería utilizado en un registro MX debería tener un registro A correspondiente. El registro A se utiliza para buscar la dirección IP del servidor de mensajería de destino. El servidor Transporte perimetral suscrito utiliza la dirección IP para abrir una conexión SMTP con el servidor de mensajería de destino. A pesar de que técnicamente se puede utilizar el FQDN de un registro de nombre canónico (CNAME) en un registro MX, esta práctica incumple RFC 974, RFC 1034, RFC 1912 y RFC 2181 y, en consecuencia, la mayoría de servidores de mensajería no la admiten.
    
    La combinación necesaria de consultas DNS iterativas y consultas DNS recursivas que se inician con un servidor DNS raíz se utiliza para resolver el FQDN del servidor de mensajería que hay en el registro MX en una dirección IP.

En Exchange 2013 hay un límite de consulta DNS de 5 segundos para cada servidor DNS. Este límite no se puede configurar. Además, existe un límite de un minuto para toda la consulta DNS.

## Posibles problemas de DNS

Aunque la configuración DNS en el servidor Exchange se haya realizado correctamente, puede seguir habiendo problemas con los registros DNS de un dominio concreto o con cualquier servidor DNS utilizado para buscar el servidor DNS de autorización para un dominio específico. Normalmente, no podrá controlar estos problemas y los deberán resolver los propietarios de dichos servidores DNS. Estos errores relacionados con DNS pueden estar causados por una o varias de las siguientes condiciones:

  - Registros DNS no válidos para el dominio de destino

  - Problemas con la utilización del servidor DNS

  - Problemas con la replicación del servidor DNS

En Exchange 2013, cuando una consulta DNS da lugar a errores, la consulta pasa al siguiente servidor DNS sólo si dicho servidor DNS no ha devuelto aún ningún error para la consulta actual.

Puede controlar la sensibilidad de los errores de consultas DNS modificando el archivo de configuración de la aplicación XML `%ExchangeInstallPath%bin\EdgeTransport.exe.config`. Este archivo está asociado con el servicio de transporte de Microsoft Exchange. Los cambios que guarde en este archivo se aplican después de reiniciar el servicio de transporte de Microsoft Exchange. Al reiniciar este servicio, el flujo de correo del servidor se interrumpe temporalmente. La sensibilidad de los errores de consultas DNS la controla la clave *DnsFaultTolerance* en el archivo EdgeTransport.exe.config. Esta clave usa los valores siguientes:

  - **Indulgente**   Cuando la consulta DNS se encuentra con una combinación de registros MX válidos y no válidos, continúa hasta que se alcanza el límite de tiempo de espera de DNS, que es de un minuto. Se desechan los registros MX no válidos y se utiliza el registro MX válido que tiene el valor de preferencia más bajo para entregar el mensaje al servidor de mensajería de destino. Es el valor predeterminado.

  - **Normal**   Cuando la consulta DNS se encuentra por primera vez con un registro MX no válido, inmediatamente se desechan los registros MX resueltos que tienen un valor de preferencia superior o igual al de los registros MX no válidos. De entre los registros MX restantes, se utiliza el que tenga un valor de preferencia más bajo para entregar el mensaje al servidor de mensajería de destino sin esperar a que finalice el tiempo de espera de toda la consulta DNS. Si bien este comportamiento podría redundar en una entrega más rápida de los mensajes, el posible inconveniente es que la consulta DNS podría carecer de registros MX válidos si las condiciones siguientes son verdaderas:
    
      - El registro MX no válido es el primer registro MX para el dominio de destino.
    
      - Los registros MX válidos tienen el mismo valor de preferencia que los registros MX no válidos.

Tanto en modo `Normal` como en modo `Lenient`, los resultados de la consulta DNS en el caso de un registro MX no válido no se almacenan en la memoria caché. La próxima vez que se ejecuta una consulta DNS, ésta intentará resolver los registros MX para el dominio de destino.


> [!NOTE]
> Las configuraciones personalizadas referentes al servidor que lleve a cabo en los archivos de configuración de la aplicación XML de Exchange, por ejemplo, los archivos web.config en los servidores de acceso de cliente o el archivo EdgeTransport.exe.config en los servidores de buzones de correo, se sobrescribirán al instalar la actualización acumulativa o el Service Pack de Exchange. Asegúrese de guardar esta información para que pueda volver a configurar fácilmente su servidor tras la instalación. Vuelva a establecer estas configuraciones después de instalar una actualización acumulativa de Exchange.


