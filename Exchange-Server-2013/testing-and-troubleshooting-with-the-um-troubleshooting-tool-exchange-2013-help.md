---
title: 'Pruebas y solución de problemas con la herramienta para la solución de problemas de UM: Exchange 2013 Help'
TOCTitle: Pruebas y solución de problemas con la herramienta para la solución de problemas de UM
ms:assetid: 1fab2e52-bd2d-4e46-b222-53fee9d34cba
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg621148(v=EXCHG.150)
ms:contentKeyID: 56271496
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Pruebas y solución de problemas con la herramienta para la solución de problemas de UM

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2016-12-09_

La herramienta de solución de problemas de mensajería unificada de Microsoft Exchange 2010 es un cmdlet del Shell de administración de Exchange denominado **Test-ExchangeUMCallFlow**. Puede usarlo para diagnosticar errores de configuración específicos de los escenarios de central de llamadas y para comprobar si el correo de voz funciona correctamente en las implementaciones locales o entre las instalaciones de mensajería unificada de Microsoft Exchange Server 2010 Service Pack 1 (SP1) o posterior. Puede usar este cmdlet con implementaciones de Microsoft Office, Microsoft Lync Server 2010 o posterior, o en implementaciones de mensajería unificada con puertas de enlace IP, IP PBX o controladores de borde de sesión (SBC).

## Introducción

Este cmdlet emula llamadas y ejecuta una serie de pruebas de diagnóstico que ayudan a los administradores locales a identificar los errores de configuración en equipos de telefonía, configuraciones de Mensajería unificada de Exchange 2010 SP1 o posterior y problemas de conectividad entre implementaciones locales e implementaciones entre locales de Mensajería unificada de Exchange 2010 SP1 o posterior.

Al ejecutar el cmdlet, indica el motivo y las posibles soluciones de los problemas detectados. También da como resultado métricas generales de calidad del audio para diagnosticar problemas de calidad del audio relacionados con la conectividad de red, como vibración o pérdida de paquetes promedio. El cmdlet **Test-ExchangeUMCallFlow** admite las pruebas de componentes de mensajería unificada en llamadas `Secured`, `SIP Secured` y `Unsecured` y se puede ejecutar en los modos `Gateway` o `SIPClient`.

De forma predeterminada, cuando ejecuta la herramienta para la solución de problemas de Mensajería unificada, la herramienta usa las credenciales que se usaron al iniciar sesión en el PC. Las credenciales que se usan son las que se especificaron para la persona que llama. Debe establecer o especificar las credenciales que se deben usar al ejecutar la herramienta para la solución de problemas de Mensajería unificada en el modo `SIPClient`. Sin embargo, no es necesario establecer las credenciales al ejecutar la herramienta para la solución de problemas de Mensajería unificada en el modo `Gateway`. Para usar la herramienta de solución de problemas de Mensajería unificada en el modo `SIPClient`, se deben cumplir varios requisitos y requisitos previos de Office Communications Server 2007 R2 o Lync Server. Para más información, consulte [Lista de comprobación: implementación de la mensajería unificada de Exchange y Office Communications Server 2007](https://go.microsoft.com/fwlink/p/?linkid=311961) o [Lista de comprobación: Integrar mensajería unificada de Exchange 2013 con Lync Server](checklist-integrate-exchange-2013-um-with-lync-server-exchange-2013-help.md).


> [!IMPORTANT]
> El cmdlet <STRONG>Test-ExchangeUMCallFlow</STRONG> solo se debe usar para comprobar la funcionalidad de correo de voz de un servidor de Mensajería unificada de Microsoft Exchange Server 2010 que tenga instalado el Service Pack 1 (SP1) de Exchange 2010 o Microsoft Exchange 2013.



El cmdlet **Test-ExchangeUMCallFlow** se puede instalar en un servidor local de Mensajería unificada de Exchange 2010, en un servidor de buzones de Exchange 2013 o en otro PC de 64 bits que ejecute:

  - El sistema operativo Windows 7 o Windows 8

  - El sistema operativo Windows Server 2008 o Windows Server 2008 R2

  - El sistema operativo Windows Server 2012 o Windows Server 2012 R2

El cmdlet **Test-ExchangeUMCallFlow** requiere que estén instalados los siguientes componentes en un PC con Windows 7, Windows 8, Windows Server 2008 o Windows Server 2012 de 64 bits antes de instalar el cmdlet:

  - Microsoft .NET Framework 3.5 Service Pack 1 (SP1). Para descargar el Service Pack, consulte [Microsoft .NET Framework 3.5 Service Pack 1](https://go.microsoft.com/fwlink/?linkid=152380).

  - Las actualizaciones Microsoft .NET Framework 3.5 Family Update para Windows Vista x64 y Windows Server 2008 x64, si la herramienta se ejecutará en un PC con Windows Vista o Windows Server 2008. Para descargar la actualización, consulte [Microsoft .NET Framework 3.5 Family Update para Windows Vista x64 y Windows Server 2008 x64](https://go.microsoft.com/fwlink/?linkid=178998).

  - Administración remota de Windows (WinRM) 2.0 y Windows PowerShell V2 (Windows6.0-KB968930.msu). Para más información, consulte el artículo 968930 de Microsoft Knowledge Base, [Paquete básico de Windows Management Framework (Windows PowerShell 2.0 y WinRM 2.0)](http://go.microsoft.com/fwlink/?linkid=3052%26kbid=968930).

  - API 2.0 administrada de comunicaciones unificadas, Core Runtime (64 bits). Para descargar el archivo del programa UcmaRuntimeWebDownloadX64.msi, consulte [API 2.0 administrada de comunicaciones unificadas, Core Runtime (64 bits)](https://go.microsoft.com/fwlink/p/?linkid=198175).

El cmdlet **Test-ExchangeUMCallFlow** no está incluido en el DVD de Exchange 2010 SP1, en la descarga exclusiva de Exchange 2010 SP1 ni en los medios de instalación de Exchange 2013. Sin embargo, puede descargar el cmdlet del [Centro de descarga de Microsoft](https://go.microsoft.com/fwlink/p/?linkid=182625).

Para más información sobre sintaxis y parámetros, consulte [Test-ExchangeUMCallFlow](https://technet.microsoft.com/es-es/library/ff630913\(v=exchg.150\)).

