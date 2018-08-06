---
title: 'Ejecutar herramienta solucionar problemas UM de Exchange Windows 7 Windows 8 | Microsoft Docs'
TOCTitle: Ejecución de la herramienta para la solución de problemas de Mensajería unificada de Exchange en Windows 7 o Windows 8
ms:assetid: 98d6869d-ee4a-4088-849d-ef75b0f5d932
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ff851872(v=EXCHG.150)
ms:contentKeyID: 56271503
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ejecución de la herramienta para la solución de problemas de Mensajería unificada de Exchange en Windows 7 o Windows 8

 

_**Se aplica a:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2016-12-09_

La herramienta de solución de problemas de mensajería unificada de Microsoft Exchange 2010 es un cmdlet del Shell de administración de Exchange denominado **Test-ExchangeUMCallFlow**. Puede usarlo para diagnosticar errores de configuración específicos de los escenarios de central de llamadas y para comprobar si el correo de voz funciona correctamente en las implementaciones locales o entre las instalaciones de mensajería unificada de Microsoft Exchange Server 2010 Service Pack 1 (SP1) o posterior. Puede usar este cmdlet con implementaciones de Microsoft Office, Microsoft Lync Server 2010 o posterior, o en implementaciones de mensajería unificada con puertas de enlace IP, IP PBX o controladores de borde de sesión (SBC).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 3 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el entrada \&quot;Servidor de Mensajería unificada\&quot; o \&quot;Servicios de Mensajería unificada\&quot; en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Compruebe que la organización de Exchange 2010 o Exchange 2013 cumple los siguientes requisitos:
    
      - Se ha creado un plan de marcado de mensajería unificada. Para obtener información acerca de los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).
    
      - Se ha creado una directiva de buzón de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).
    
      - Se ha creado una puerta de enlace IP de mensajería unificada. Para conocer los pasos detallados, consulte [Cree una puerta de enlace IP de mensajería unificada](create-a-um-ip-gateway-exchange-2013-help.md).
    
      - Un servidor de mensajería UNIFICADA de Exchange 2010 se agregó al plan de marcado de mensajería UNIFICADA. Si está utilizando Exchange 2013 con Lync Server, agregue todos los servidores de buzón y acceso de cliente a los planes de marcado de URI de SIP. Para ver pasos detallados, consulte [Agregar un servidor de mensajería UNIFICADA a un Plan de marcado](https://go.microsoft.com/fwlink/p/?linkid=313051) o [Agregar servidores de acceso de cliente y buzón a un plan de marcado de URI de SIP](add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md).

  - Si ejecuta la herramienta para la solución de problemas de Mensajería unificada en un servidor de Mensajería unificada local con Exchange 2010 SP1 o posterior en un servidor de buzones de correo de Exchange 2013, es posible que no tenga que instalar todos los requisitos previos que aparecen en la lista de abajo. Es posible que ya se hayan instalado junto con el rol de servidor Mensajería unificada. No obstante, si está instalado la herramienta de solución de problemas de mensajería unificada en un equipo de 64 bits que no sea un servidor que ejecuta el rol de servidor Mensajería unificada, deberá instalar los siguientes componentes:
    
      - Microsoft .NET Framework 3.5 Service Pack 1 (SP1). Consulte [Microsoft.NET Framework 3.5 Service Pack 1](https://go.microsoft.com/fwlink/p/?linkid=152380).
    
      - Si la herramienta se ejecutará en un equipo Vista o Windows Server 2008 de Windows, consulte [actualización de la familia de Microsoft.NET Framework 3.5 para x64, de Windows Vista y Windows Server 2008 x64](https://go.microsoft.com/fwlink/p/?linkid=178998).
    
      - Administración remota de Windows (WinRM) 2.0 y Windows PowerShell V2 (Windows6.0-KB968930.msu). Consulte el artículo 968930 de Microsoft Knowledge Base, [Paquete de Windows Management Framework Core (Windows PowerShell 2.0 y WinRM 2.0)](http://go.microsoft.com/fwlink/?linkid=3052&kbid=968930).
    
      - Microsoft Unified Communications API administrada 2.0 Core Runtime (UcmaRuntimeWebDownloadX64.msi). Ver [comunicaciones unificadas Managed API 2.0 Core en tiempo de ejecución (64 bits)](https://go.microsoft.com/fwlink/p/?linkid=198175).

  - Descargue e instale la herramienta de solución de problemas de mensajería unificada.
    
      - Descargue la [herramienta de solución de problemas de la mensajería unificada](https://go.microsoft.com/fwlink/p/?linkid=182625) desde el centro de descarga de Microsoft.
    
      - Instale la herramienta. Para obtener información más detallada, consulte [Instalación de la herramienta para la solución de problemas de Mensajería unificada de Exchange](install-the-exchange-um-troubleshooting-tool-exchange-2013-help.md).
        

        > [!IMPORTANT]
        > Si va a utilizar la herramienta de solución de problemas en mensajería UNIFICADA en el modo de <CODE>SIPClient</CODE> , hay varios Office Communications Server 2007 R2 o Microsoft Lync Server y otros requisitos de requisitos previos que deben cumplirse. Para obtener más información, consulte <A href="https://go.microsoft.com/fwlink/p/?linkid=311961">lista de comprobación: implementar Office Communications Server 2007 R2 y la mensajería unificada de Exchange 2010</A>.



  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Ejecución de la herramienta para la solución de problemas de Mensajería unificada en Windows Vista, Windows 7 o Windows 8

1.  Haga clic en **Inicio** \> **Todos los programas** \> **Accesorios** \> **Windows PowerShell**.

2.  Haga clic con el botón secundario del mouse en **Windows PowerShell** y, en el menú emergente, seleccione **Ejecutar como administrador**.

3.  En el símbolo del sistema de Windows PowerShell, vaya a la carpeta en la que se instaló la herramienta para la solución de problemas de Mensajería unificada y ejecute lo siguiente.
    
        C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe -psconsolefile .\Microsoft.Exchange.UM.TroubleshootingToolsnapin.psc1 -noexit -command ". '.\Microsoft.Exchange.UM.TroubleshootingTool.ps1' "

4.  Si ejecuta la herramienta para la solución de problemas de Mensajería unificada en Windows Vista, Windows 7 o Windows 8, en el símbolo del sistema de Windows PowerShell, ejecute lo siguiente.
    
        Set-ExecutionPolicy RemoteSigned

5.  Desde el menú **Inicio**, abra la **herramienta para la solución de problemas de Mensajería unificada de Microsoft Exchange 2010**.

6.  En la ventana **Herramienta de solución de problemas de mensajería unificada de Microsoft Exchange 2010**, en el mensaje, escriba lo siguiente y presione Entrar.
    
        $cred=Get-Credential

7.  En la ventana **Solicitud de credenciales para Windows PowerShell**, escriba el dominio\\nombre de usuario y contraseña y, luego, haga clic en **Aceptar**.

8.  En la ventana **Herramienta de solución de problemas de mensajería unificada de Microsoft Exchange 2010**, especifique los parámetros necesarios del cmdlet para comprobar el flujo de llamadas. Por ejemplo:
    
        Test-ExchangeUMCallFlow -Mode SIPClient -CallingParty tonysmith@contoso.com - CalledParty jamiestark@contoso.com NextHop ocsfe.contoso.com -Credential $cred

