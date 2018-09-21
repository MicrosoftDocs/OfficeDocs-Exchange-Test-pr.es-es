---
title: 'Establecer credenciales usar con herramienta solucionar problemas UM Exchange'
TOCTitle: Establecer las credenciales para usar con la herramienta para la solución de problemas de Mensajería unificada de Exchange
ms:assetid: 542b7718-9345-40cc-bcb2-e307e70a1fa2
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ff630916(v=EXCHG.150)
ms:contentKeyID: 56271499
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Establecer las credenciales para usar con la herramienta para la solución de problemas de Mensajería unificada de Exchange

 

_**Se aplica a:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2016-12-09_

La herramienta de solución de problemas de mensajería unificada de Microsoft Exchange 2010 es un cmdlet del Shell de administración de Exchange denominado **Test-ExchangeUMCallFlow**. Puede usarlo para diagnosticar errores de configuración específicos de los escenarios de central de llamadas y para comprobar si el correo de voz funciona correctamente en las implementaciones locales o entre las instalaciones de mensajería unificada de Microsoft Exchange Server 2010 Service Pack 1 (SP1) o posterior. Puede usar este cmdlet con implementaciones de Microsoft Office, Microsoft Lync Server 2010 o posterior, o en implementaciones de mensajería unificada con puertas de enlace IP, IP PBX o controladores de borde de sesión (SBC).

De forma predeterminada, cuando se ejecuta la herramienta para la solución de problemas de MU, usa las credenciales usadas al iniciar sesión en el equipo. Las credenciales usadas son las que se han especificado para la parte que realiza la llamada. Debe establecer o especificar las credenciales que se deben usar al ejecutar la herramienta para la solución de problemas de MU en el modo`SIPClient`. Sin embargo, no es necesario establecer las credenciales al ejecutar la herramienta para la solución de problemas de MU en el modo `Gateway`.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 3 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el entrada \&quot;Servidor de Mensajería unificada\&quot; o \&quot;Servicios de Mensajería unificada\&quot; en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Compruebe que la organización de Exchange 2010 o Exchange 2013 cumple los siguientes requisitos:
    
      - Se ha creado un plan de marcado de mensajería unificada. Para obtener información acerca de los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).
    
      - Se ha creado una directiva de buzones de correo de Mensajería unificada. Para ver los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-voice-mail/create-um-mailbox-policy).
    
      - Se ha creado una puerta de enlace IP de mensajería unificada. Para conocer los pasos detallados, consulte [Cree una puerta de enlace IP de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-ip-gateway).
    
      - Un servidor de mensajería UNIFICADA de Exchange 2010 se agregó al plan de marcado de mensajería UNIFICADA. Si está utilizando Exchange 2013 con Lync Server, agregue todos los servidores de buzón y acceso de cliente a los planes de marcado de URI de SIP. Para ver pasos detallados, consulte [Agregar un servidor de mensajería UNIFICADA a un Plan de marcado](https://go.microsoft.com/fwlink/p/?linkid=313051) o [Agregar servidores de acceso de cliente y buzón a un plan de marcado de URI de SIP](add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md).

  - Instale la herramienta para la solución de problemas de MU. Para conocer los pasos detallados, consulte [Instalación de la herramienta para la solución de problemas de Mensajería unificada de Exchange](install-the-exchange-um-troubleshooting-tool-exchange-2013-help.md).
    

    > [!IMPORTANT]
    > Si va a utilizar la herramienta de solución de problemas en mensajería UNIFICADA en el modo de <CODE>SIPClient</CODE> , hay varios otros Office Communications Server 2007 R2 o Microsoft Lync Server requisitos y requisitos previos. Para obtener más información, consulte <A href="https://go.microsoft.com/fwlink/p/?linkid=311961">lista de comprobación: implementar Office Communications Server 2007 R2 y la mensajería unificada de Exchange 2010</A> o <A href="checklist-integrate-exchange-2013-um-with-lync-server-exchange-2013-help.md">Lista de comprobación: Integrar mensajería unificada de Exchange 2013 con Lync Server</A>.



  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Establecer las credenciales para usar con la herramienta para la solución de problemas de MU

1.  Desde el menú **Inicio**, abra la **herramienta para la solución de problemas de Mensajería unificada de Microsoft Exchange 2010**.

2.  En la ventana **Herramienta para la solución de problemas de Mensajería unificada de Microsoft Exchange 2010**, en el aviso, escriba lo siguiente y presione Entrar.
    
        $cred=Get-Credential

3.  En la ventana **Solicitud de credenciales para Windows PowerShell**, escriba el dominio\\nombre de usuario y contraseña y, luego, haga clic en **Aceptar**.

4.  En la ventana **Herramienta de solución de problemas de mensajería unificada de Microsoft Exchange 2010**, especifique los parámetros necesarios del cmdlet para comprobar el flujo de llamadas. Por ejemplo:
    
        Test-ExchangeUMCallFlow -Mode SIPClient -CallingParty tonysmith@contoso.com - CalledParty jamiestark@contoso.com NextHop ocsfe.contoso.com -Credential $cred

