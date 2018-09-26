---
title: 'Libretas de direcciones sin conexión: Exchange 2013 Help'
TOCTitle: Libretas de direcciones sin conexión
ms:assetid: a6bcb072-4ab9-400e-a5d0-c05264629097
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb232155(v=EXCHG.150)
ms:contentKeyID: 49895816
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Libretas de direcciones sin conexión

 

_**Se aplica a:** Exchange Server 2010, Exchange Server 2013_

_**Última modificación del tema:** 2014-11-16_

Una libreta de direcciones sin conexión (OAB) es una recopilación de una lista de direcciones que se ha descargado para que un usuario de Microsoft Outlook pueda obtener acceso a la libreta de direcciones cuando no tiene conexión con el servidor. Microsoft Exchange genera los archivos OAB nuevos y los comprime y los sitúa en un recurso compartido local. Puede decidir qué listas de direcciones estarán disponibles para los usuarios que trabajan sin conexión; también puede configurar el método de distribución de las mismas.

Para obtener más información acerca de las listas de direcciones, consulte [Listas de direcciones](https://docs.microsoft.com/es-es/exchange/address-books/address-lists/address-lists).


> [!IMPORTANT]
> Los datos OAB son producidos por el servicio Microsoft Exchange OABGen, que es un asistente de buzón de correo. Si utiliza el descriptor de seguridad para impedir que los usuarios vean ciertos destinatarios de Active Directory, los usuarios que descarguen la OAB podrán ver esos destinatarios ocultos. Por lo tanto, para ocultar un destinatario de una libreta de direcciones, ajuste el parámetro <EM>HiddenFromAddressListsEnabled</EM> en los cmdlets <A href="https://technet.microsoft.com/es-es/library/aa998596(v=exchg.150)">Set-PublicFolder</A>, <A href="https://technet.microsoft.com/es-es/library/aa995950(v=exchg.150)">Set-MailContact</A>, <A href="https://technet.microsoft.com/es-es/library/aa995971(v=exchg.150)">Set-MailUser</A>, <A href="https://technet.microsoft.com/es-es/library/bb123796(v=exchg.150)">Set-DynamicDistributionGroup</A>, <A href="https://technet.microsoft.com/es-es/library/bb123981(v=exchg.150)">Set-Mailbox</A> y <A href="https://technet.microsoft.com/es-es/library/bb124955(v=exchg.150)">Set-DistributionGroup</A>. Como alternativa, puede crear una nueva OAB predeterminada que no contenga los destinatarios ocultos. Para obtener información acerca de cómo agregar o quitar listas de direcciones de una OAB, consulte <A href="https://docs.microsoft.com/es-es/exchange/address-books/offline-address-books/add-or-remove-an-address-list">Agregar una lista de direcciones o quitar una lista de direcciones de la libretas de direcciones sin conexión</A>.



¿Está buscando las tareas de administración relacionadas OAB? Consulte [Procedimientos de libretas de direcciones sin conexión](https://docs.microsoft.com/es-es/exchange/address-books/offline-address-books/offline-address-book-procedures).

**Contenido**

Movimiento de OAB entre versiones de Exchange

OAB versión 4 y clientes de Outlook

Distribución basada en web

Aspectos que se deben tener en cuenta en relación con la OAB

## Movimiento de OAB entre versiones de Exchange

En Exchange 2007 y Exchange 2010, se usa el cmdlet **Move-OfflineAddressBook** para mover la generación de OAB a otro servidor de buzón de correo. Exchange 2013 solo admite OAB (versión 4). Se trata de la misma versión OAB que se encontraba por defecto en Exchange 2010. No se puede configurar Exchange 2013 para generar otras versiones de OAB y la generación de OAB se realiza en el servidor del buzón de correo en el que reside el buzón de correo de la organización. Por lo tanto, para mover la generación de OAB en Exchange 2013, deberá mover el buzón de correo de la organización. Solo puede mover la generación de una OAB a otra base de datos de buzón de correo Exchange 2013. No se puede mover la generación de una OAB a una versión anterior de Exchange. Para encontrar el buzón de Exchange 2013 OAB de la organización, ejecute el siguiente comando del Shell:

```powershell
  Get-Mailbox -Arbitration | where {$_.PersistedCapabilities -like "*oab*"}
```

Seguidamente, puede utilizar los cmdlets **MoveRequest** para mover el buzón.

## OAB versión 4 y clientes de Outlook

Exchange 2013 solo admite OAB versión 4. OAB versión 4 se presentó en el Exchange 2003 Service Pack 2 (SP2) y es admitida por Outlook 2007, Outlook 2010 y Outlook 2013. Esta OAB Unicode permite que los equipos del cliente reciban actualizaciones diferenciales en lugar de descargas OAB completas y un tamaño de archivo reducido.

## Clientes de Outlook que utilizan la versión 4 de OAB

Para los clientes de Outlook 2013, Outlook 2010, Outlook 2007 y clientes que emplean la versión 4 de OAB, si el tamaño de los archivos Changes.oab representa la mitad (o más) del tamaño de todos los archivos OAB completos, Outlook inicia una descarga de la OAB completa.

## Distribución basada en web

*Distribución basada en web* es el método de distribución mediante el cual los clientes de Outlook 2013, Outlook 2010, o Outlook 2007 que trabajan offline pueden acceder a una OAB.

Existen varias ventajas al utilizar la distribución basada en web, entre las que se incluyen:

  - Admisión de más equipos cliente simultáneos.

  - Reducción en el uso de ancho de banda.

  - Más control sobre los puntos de distribución OAB. Con la distribución basada en web, el punto de distribución es la dirección web HTTPS donde los equipos cliente pueden descargar la OAB.

Para beneficiarse al máximo de la distribución basada en web, los equipos cliente deben ejecutar Outlook 2013, Outlook 2010 o Outlook 2007.

Para su buen funcionamiento, la distribución basada en web depende de los siguientes componentes:

  - **Proceso de generación de OAB**   Es el proceso mediante el cual Exchange crea y actualiza la OAB. Para crear y actualizar una OAB, el servicio OABGen se ejecuta en el servidor Buzón de correo en el que se aloja el buzón de correo organizativo. Para admitir la distribución OAB, este debe ser un servidor de buzón de ejecuta Exchange.

  - **Distribución OAB**   Si un cliente inicia la petición de distribución OAB, la petición se dirigirá a través de un servidor de acceso de cliente. El servidor de acceso de clientes enruta la petición al servidor de buzón de correo que aloja los archivos OAB. Los archivos OAB se distribuyen directamente desde el servidor de buzón de correo al cliente.

  - **Directorio virtual de OAB**   El directorio virtual de OAB es el punto de distribución que utiliza el método de distribución basado en web. De forma predeterminada, cuando se instala Exchange, se crea un directorio virtual nuevo denominado **OAB** en el sitio web predeterminado en Internet Information Services (IIS). Si tiene usuarios de cliente que se conectan a Outlook desde fuera del firewall de la organización, puede agregar un sitio web externo. Como alternativa, al ejecutar el cmdlet **New-OABVirtualDirectory** en el Shell, se crea un directorio virtual nuevo denominado OAB en el sitio web predeterminado IIS en el servidor acceso de cliente Exchange local. Para obtener información, consulte [Crear un directorio virtual de la libreta de direcciones sin conexión]().

  - **Servicio de detección automática**   Esta es una característica disponible en Outlook 2013, Outlook 2010, Outlook 2007, y algunos dispositivos móviles que configura automáticamente los clientes para tener acceso a Exchange. El servicio se ejecuta en un servidor de acceso de cliente y devuelve la URL de OAB correcta para una conexión específica del cliente.

## Aspectos que se deben tener en cuenta en relación con la OAB

Como práctica recomendada, tanto si se utiliza una sola OAB como si se emplean varias, tenga en cuenta los factores siguientes cuando planifique e implemente su estrategia de OAB:

  - El tamaño de cada OAB de la organización. Para obtener más información, consulte Aspectos que se deben tener en cuenta en relación con el tamaño de una OAB más adelante en este tema.

  - El número de descargas de OAB.

  - La cantidad y la frecuencia de los cambios de nombre distintivo principal.

  - Los errores de coincidencia en direcciones SMTP.

  - Cantidad total de cambios efectuados en el directorio.

## Aspectos que se deben tener en cuenta en relación con el tamaño de una OAB

En algunas organizaciones, la OAB es un archivo pequeño que los usuarios remotos descargan en ocasiones. En el caso de estas organizaciones, la descarga de la OAB no suele ser un problema. Ahora bien, en algunas organizaciones grandes con grandes directorios o en organizaciones en las que se ha implementado Outlook 2003 en el modo Exchange en caché, sí podría suponer un problema, sobre todo si esas organizaciones tienen servidores de Exchange consolidados en un centro de datos regional.

Los tamaños de OAB pueden oscilar entre unos cuantos megabytes y varios cientos de megabytes. Los factores siguientes pueden influir en el tamaño de la OAB:

  - El uso de certificados en una empresa. Cuantos más certificados de infraestructura de claves públicas (PKI) haya, mayor será la OAB. Los certificados de PKI van desde 1 kilobyte (KB) a 3 KB. Son el factor individual que más contribuye al tamaño de la OAB.

  - El número de destinatarios de correo en Active Directory.

  - El número de grupos de distribución en Active Directory.

  - La información que una empresa agrega a Active Directory por cada objeto con buzón o correo habilitado. Por ejemplo, algunas organizaciones rellenan las propiedades de dirección de cada usuario, mientras que otras no.

