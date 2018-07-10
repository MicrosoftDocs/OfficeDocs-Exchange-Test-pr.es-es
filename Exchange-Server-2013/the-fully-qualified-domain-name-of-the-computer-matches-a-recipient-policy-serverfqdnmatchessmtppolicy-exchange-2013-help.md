---
title: 'El nombre de dominio completo del equipo coincide con un destinatario policy_ServerFQDNMatchesSMTPPolicy: Exchange 2013 Help'
TOCTitle: El nombre de dominio completo del equipo coincide con un destinatario policy_ServerFQDNMatchesSMTPPolicy
ms:assetid: f3ea61f8-1788-4cbf-814e-f7c088c1ac47
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.serverfqdnmatchessmtppolicy(v=EXCHG.150)
ms:contentKeyID: 48268861
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# El nombre de dominio completo del equipo coincide con un destinatario policy\_ServerFQDNMatchesSMTPPolicy

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2016-12-09_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La instalación de Microsoft® Exchange Server 2007 no puede continuar porque el Nombre de dominio completo (FQDN) del equipo local coincide con la dirección del Protocolo simple de transferencia de correo (SMTP) de una directiva de destinatario.

La instalación de Microsoft Exchange requiere que el FQDN de los servidores de una organización de Exchange no coincidan con ninguna dirección SMTP de directivas de destinatario de la misma organización de Exchange.

Si el FQDN de un equipo coincide con la dirección SMTP de una directiva de destinatarios, esta coincidencia puede hacer que falle el correo por el SMTP y se detenga en las colas MTA.

Para resolver este problema, cambie el nombre del equipo local o elimine o cambie el nombre de la directiva de destinatarios y vuelva a ejecutar la instalación de Microsoft Exchange.

Para cambiar el nombre del equipo local

1.  Abra **Sistema** en el **Panel de control**.

2.  En la ficha **Nombre del equipo**, haga clic en **Cambiar**

3.  En **Nombre de equipo**, escriba un nuevo nombre para el equipo, y después haga clic en **Aceptar**. Se le solicitará que proporcione un nombre de usuario y una contraseña de usuario para cambiar el nombre del equipo en el dominio.

4.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Propiedades del sistema**. Se le solicitará que reinicie su equipo para aplicar los cambios.


> [!IMPORTANT]
> Si el equipo que va a cambiar es un controlador de dominio, consulte "Cambiar el nombre de un controlador de dominio" (<A href="https://go.microsoft.com/fwlink/?linkid=66828">https://go.microsoft.com/fwlink/?LinkId=66828</A>).



Para modificar la dirección SMTP de la directiva de destinatarios

1.  Inicie el Administrador del sistema de Exchange.

2.  Haga clic en **Organización**, **Destinatarios** y, a continuación, en **Directivas de destinatarios**.

3.  Haga doble clic en la directiva que desea cambiar.

4.  Haga clic en la ficha **Direcciones de correo electrónico**, y después cambie la dirección SMTP adecuada.

Para obtener más información sobre problemas de registro de Directivas de destinatarios, consulte el artículo 288175 de Microsoft Knowledge Base, "XCON: Directiva de destinatario no coincide con el FQDN de un servidor en la organización, 5.4.8 NDR" ([http://go.microsoft.com/fwlink/?linkid=3052\&kbid=288175](http://go.microsoft.com/fwlink/?linkid=3052&kbid=288175)).

