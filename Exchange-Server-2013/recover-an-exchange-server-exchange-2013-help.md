---
title: 'Recuperar un servidor de Exchange: Exchange 2013 Help'
TOCTitle: Recuperar un servidor de Exchange
ms:assetid: 46e9a1cf-b64c-43c3-a898-6171176da761
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd876880(v=EXCHG.150)
ms:contentKeyID: 48268074
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Recuperar un servidor de Exchange

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Puede recuperar un servidor perdido mediante el conmutador **Setup /m:RecoverServer** en Microsoft Exchange Server 2013. La mayoría de las opciones de configuración para un equipo que ejecuta Exchange 2013 se almacena en Active Directory. El conmutador */m:RecoverServer* reconstruye un servidor de Exchange con el mismo nombre con la configuración y otra información almacenada en Active Directory.

A menudo, se puede recuperar un servidor de Exchange perdido por medio de hardware nuevo. Sin embargo, también puede usar un servidor existente.

En este tema se muestra cómo recuperar un servidor de Exchange 2013 perdido que no es miembro del grupo de disponibilidad de base de datos (DAG). Para obtener pasos detallados acerca de cómo recuperar un servidor que pertenecía a un DAG, consulte [Recuperar un servidor miembro de un grupo de disponibilidad de base de datos](recover-a-database-availability-group-member-server-exchange-2013-help.md).


> [!NOTE]
> Si se instala Exchange en una ubicación que no sea la predeterminada, debe usar el conmutador de instalación <EM>/TargetDir</EM> para especificar la ubicación de los archivos binarios de Exchange. Si no usa el conmutador <EM>/TargetDir</EM>, los archivos de Exchange se instalarán en la ubicación predeterminada (%programfiles%\Microsoft\Exchange Server\V15).<BR>Para determinar la ubicación de la instalación, siga estos pasos: 
> <OL>
> <LI>
> <P>Abra ADSIEDIT.MSC o LDP.EXE.</P>
> <LI>
> <P>Desplácese a la siguiente ubicación: <STRONG>CN=ExServerName,CN=Servidores,CN=Primer grupo administrativo,CN=Grupos administrativos,CN=ExOrg Name,CN=Microsoft Exchange,CN=Servicios,CN=Configuración,DC=NombreDeDominio,CN=Com</STRONG></P>
> <LI>
> <P>Haga clic con el botón secundario en el objeto de servidor de Exchange y, a continuación, haga clic en <STRONG>Propiedades</STRONG>.</P>
> <LI>
> <P>Localice el atributo <STRONG>msExchInstallPath</STRONG>. Este atributo almacena la ruta de instalación actual.</P></LI></OL>



¿Está buscando otras tareas de administración relacionadas con copias de seguridad y restauración de datos? Consulte [Copia de seguridad, restauración y recuperación ante desastres](backup-restore-and-disaster-recovery-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 20 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Sección "Permisos de infraestructura de Exchange" en el tema [Permisos de infraestructura de la Shell y de Exchange](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - El servidor sobre el cual se realiza la recuperación debe ejecutar el mismo sistema operativo que el servidor perdido. Por ejemplo, no se puede recuperar un servidor que ejecutaba Exchange 2013 y Windows Server 2008 R2 en un servidor que ejecuta Windows Server 2012, o viceversa. Del mismo modo, no se puede recuperar un servidor que ejecutaba Exchange 2013 y Windows Server 2012 en un servidor que ejecuta Windows Server 2012 R2, o viceversa.

  - Las mismas letras de las unidades de disco del servidor con errores para bases de datos montadas deben existir en el servidor en que se está ejecutando la recuperación.

  - El servidor en el que se realiza la recuperación debe tener las mismas características de rendimiento y la misma configuración de hardware que el servidor perdido.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Recuperar un servidor Exchange perdido

1.  Restablezca la cuenta de equipo del servidor perdido. Vea los pasos detallados en [Restablecer una cuenta de equipo](https://go.microsoft.com/fwlink/p/?linkid=165388).

2.  Instale el sistema operativo correcto y otorgue al servidor nuevo el mismo nombre que tenía el servidor perdido. La recuperación no se realizará si el servidor en el cual se ejecuta la recuperación no tiene el mismo nombre que tenía el servidor perdido.

3.  Unir el servidor al mismo dominio que el servidor perdido.

4.  Instale los requisitos previos y los componentes de sistema necesarios. Para obtener información detallada, consulte [Requisitos del sistema para Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md) y [Requisitos previos de Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).

5.  Inicie sesión en el servidor que se va a recuperar y abra un símbolo del sistema.

6.  Desplácese a los archivos de instalación de Exchange 2013 y ejecute el siguiente comando.
    
        Setup /m:RecoverServer /IAcceptExchangeServerLicenseTerms

7.  Después de completar la instalación y antes de poner al servidor recuperado en funcionamiento, vuelva a configurar cualquier parámetro personalizado que tenía el servidor y, luego, reinicie el servidor.

## ¿Cómo saber si el proceso se ha completado correctamente?

La finalización correcta de la instalación será el principal indicador de que la recuperación se realizó correctamente. Para comprobar que haya recuperado un servidor perdido correctamente, siga estos pasos:

  - Abra la herramienta Windows Services (services.msc) y compruebe que los servicios de Microsoft Exchange se hayan instalado y se estén ejecutando.

