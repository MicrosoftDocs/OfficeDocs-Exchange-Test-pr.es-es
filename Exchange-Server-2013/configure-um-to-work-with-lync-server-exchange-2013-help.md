---
title: 'Configurar la mensajería unificada para que funcione con Lync Server: Exchange 2013 Help'
TOCTitle: Configurar la mensajería unificada para que funcione con Lync Server
ms:assetid: 29bdddbf-75d5-4c92-988e-c8506ecc7a1c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ966276(v=EXCHG.150)
ms:contentKeyID: 52062012
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar la mensajería unificada para que funcione con Lync Server

 

_**Se aplica a:**Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2013-06-11_

Al integrar Microsoft Lync Server con la mensajería unificada de Exchange (MU), debe ejecutar el script ExchUcUtil.ps1 en el Shell. El script ExchUcUtil.ps1 hace lo siguiente:

  - Crea una puerta de enlace IP de mensajería unificada para cada agrupación de Lync Server.
    

    > [!IMPORTANT]
    > El script ExchUcUtil.ps1 crea una o más puertas de enlace IP de Mensajería unificada. Debe deshabilitar las llamadas salientes en todas las puertas de enlace IP de Mensajería unificada excepto una puerta de enlace que creó la secuencia de comandos. Esto incluye deshabilitar las llamadas salientes de las puertas de enlace IP de Mensajería unificada que se crearon antes de ejecutar el script. Para deshabilitar las llamadas salientes en una puerta de enlace IP de Mensajería unificada, consulte <A href="disable-outgoing-calls-on-um-ip-gateways-exchange-2013-help.md">Deshabilitar las llamadas salientes de puertas de enlace IP de mensajería unificada</A>.



  - Crea un grupo de extensiones de mensajería unificada para cada puerta de enlace IP de MU. El identificador de piloto de cada grupo de extensiones especifica el plan de marcado URI de SIP de la mensajería unificada que utiliza la agrupación front-end de Lync Server o del servidor de Standard Edition asociados a la puerta de enlace IP de la mensajería unificada.

  - Da permiso a Lync Server para leer los objetos del contenedor de mensajería unificada de Active Directory como los planes de marcado de mensajería unificada, los operadores automáticos, las puertas de enlace IP de mensajería unificada y los grupos de extensiones de mensajería unificada.


> [!IMPORTANT]
> Cada bosque de mensajería unificada debe estar configurado para confiar en el bosque en el que está implementado Lync Server 2013. Del mismo modo, dicho bosque debe estar configurado para confiar en cada bosque de la mensajería unificada. Si la mensajería unificada de Exchange está instalada en varios bosques, los pasos de integración de Exchange Server deben realizarse en cada bosque de mensajería unificada o tendrá que especificar el dominio de Lync Server. Por ejemplo, <EM>ExchUcUtil.ps1 –Forest:&lt;lync-domain-controller-fqdn&gt;</EM>.



Para obtener información sobre las tareas de administración adicionales para integrar Lync Server y la mensajería unificada, consulte [Resumen de implementación de Mensajería unificada de Exchange 2013 y Lync Server](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  2 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Cmdlets de permisos" en el tema [Cmdlets de Exchange 2013](https://technet.microsoft.com/es-es/library/bb124413\(v=exchg.150\)).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Usar el Shell para ejecutar el script ExchUcUtil.ps1

Ejecute el script ExchUcUtil.ps1 en todos los servidores Exchange de la organización que estén en la misma topología que Microsoft Lync Server. Puede ejecutar el script desde un servidor de buzones de correo con el Shell, o bien ejecutarlo con el Windows PowerShell remoto en un servidor de acceso de cliente. Si ejecuta el script en un servidor de acceso de cliente de su organización, dicho servidor transferirá por proxy la sesión de Remote Windows PowerShell a un servidor de buzones de la organización.


> [!IMPORTANT]
> El script ExchUcUtil.ps1 crea una o más puertas de enlace IP de Mensajería unificada. Debe deshabilitar las llamadas salientes en todas las puertas de enlace IP de Mensajería unificada excepto una puerta de enlace que creó la secuencia de comandos. Esto incluye deshabilitar las llamadas salientes de las puertas de enlace IP de Mensajería unificada que se crearon antes de ejecutar el script. Para deshabilitar las llamadas salientes en una puerta de enlace IP de Mensajería unificada, consulte <A href="disable-outgoing-calls-on-um-ip-gateways-exchange-2013-help.md">Deshabilitar las llamadas salientes de puertas de enlace IP de mensajería unificada</A>.




> [!IMPORTANT]
> Para ejecutar el script, debe tener los permisos del rol de administración de la organización de Exchange o ser miembro del grupo de seguridad de administradores de organización de Exchange.



1.  Abra el Shell de administración de Exchange.

2.  En el mensaje `C:\Windows\System32`, escriba **cd \&quot;\<drive letter\>\\Program Files\\Microsoft\\Exchange Server\\V15\\Scripts\>.ExchUcUtil.ps1\&quot;** y pulse la tecla Entrar.

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que el script ExchUcUtul.ps1 se ha completado correctamente, haga lo siguiente:

  - Use el cmdlet **Get-UMIPGateway** o el EAC para ver la nueva puerta o puertas de enlace IP de la mensajería unificada que se han creado.

  - Use el cmdlet **Get-UMHuntGroup** o el EAC para ver el nuevo grupo o grupos de extensiones de la mensajería unificada que se han creado.

