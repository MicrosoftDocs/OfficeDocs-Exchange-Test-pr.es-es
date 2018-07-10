---
title: 'Instalación de la herramienta para la solución de problemas de Mensajería unificada de Exchange: Exchange 2013 Help'
TOCTitle: Instalación de la herramienta para la solución de problemas de Mensajería unificada de Exchange
ms:assetid: 84223af0-a717-49ee-add6-86313bb30d17
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ff844714(v=EXCHG.150)
ms:contentKeyID: 56271502
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Instalación de la herramienta para la solución de problemas de Mensajería unificada de Exchange

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2016-12-09_

La herramienta de solución de problemas de mensajería unificada de Microsoft Exchange 2010 es un cmdlet del Shell de administración de Exchange denominado **Test-ExchangeUMCallFlow**. Puede usarlo para diagnosticar errores de configuración específicos de los escenarios de central de llamadas y para comprobar si el correo de voz funciona correctamente en las implementaciones locales o entre las instalaciones de mensajería unificada de Microsoft Exchange Server 2010 Service Pack 1 (SP1) o posterior. Puede usar este cmdlet con implementaciones de Microsoft Office, Microsoft Lync Server 2010 o posterior, o en implementaciones de mensajería unificada con puertas de enlace IP, IP PBX o controladores de borde de sesión (SBC).

La herramienta para la solución de problemas de Mensajería unificada se puede instalar en un servidor de Mensajería unificada local, en un servidor de buzones de correo de Exchange 2013 o en otro PC de 64 bits.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 3 minutos

  - Antes de instalar la herramienta para la solución de problemas de Mensajería unificada, tienen que estar instalados los siguientes componentes en un PC que ejecute Windows Vista, Windows 7, Windows 8 o la edición de 64 bits de Windows Server 2008 o Windows Server 2012:
    
      - .NET Framework 3.5 Service Pack 1 (SP1) de Microsoft vea [Microsoft.NET Framework 3.5 Service Pack 1](https://go.microsoft.com/fwlink/p/?linkid=152380).
    
      - Si la herramienta se ejecutará en un equipo Windows Vista o Windows Server 2008, consulte [actualización de la familia de Microsoft.NET Framework 3.5 para x64, de Windows Vista y Windows Server 2008 x64](https://go.microsoft.com/fwlink/p/?linkid=178998).
    
      - Administración remota de Windows (WinRM) 2.0 y Windows PowerShell V2 (Windows6.0-KB968930.msu). Consulte el artículo 968930 de Microsoft Knowledge Base, [Paquete de Windows Management Framework Core (Windows PowerShell 2.0 y WinRM 2.0)](http://go.microsoft.com/fwlink/?linkid=3052&kbid=968930).
    
      - Microsoft Unified Communications API administrada 2.0 Core Runtime (UcmaRuntimeWebDownloadX64.msi). Ver [comunicaciones unificadas Managed API 2.0 Core en tiempo de ejecución (64 bits)](https://go.microsoft.com/fwlink/p/?linkid=198175).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Instalar la herramienta para la solución de problemas de MU

1.  Descargar la mensajería de solución de problemas herramienta unificada desde el [Centro de descarga de Microsoft](https://go.microsoft.com/fwlink/p/?linkid=182625)y, a continuación, haga doble clic en la carpeta de instalación MicrosoftExchange2010UMTroubleshootingTool.msi.

2.  En la página **Este es el Asistente para la instalación de la herramienta de solución de problemas de mensajería unificada de Microsoft Exchange 2010**, haga clic en **Siguiente**.

3.  En la página **Contrato de licencia para el usuario final**, revise los términos de licencia de software y, si está de acuerdo, haga clic en **Acepto los términos del contrato de licencia** y, luego, haga clic en **Siguiente**.

4.  En la página **Seleccione la carpeta de instalación**, compruebe la ruta a la carpeta de instalación y haga clic en **Siguiente**.

5.  En la página **Confirme la instalación**, haga clic en **Siguiente** para iniciar la instalación.

6.  En la página **Instalación completa**, haga clic en **Cerrar**.

