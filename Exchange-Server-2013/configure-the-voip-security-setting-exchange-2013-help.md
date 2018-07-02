---
title: 'Establecer la configuración de seguridad de VoIP: Exchange 2013 Help'
TOCTitle: Establecer la configuración de seguridad de VoIP
ms:assetid: b5335654-c766-4f3f-883c-f31263e1d9c1
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb201721(v=EXCHG.150)
ms:contentKeyID: 49895854
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Establecer la configuración de seguridad de VoIP

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2014-10-16_

Puede habilitar la seguridad de voz sobre IP (VoIP) para un plan de marcado de Mensajería unificada. De forma predeterminada, cuando se crea un plan de marcado de mensajería unificada, se usará el modo no protegido o sin cifrado. Los servidores Exchange pueden responder a llamadas de uno o de varios planes de marcado de mensajería unificada, y pueden responder a llamadas de planes de marcado con diferentes configuraciones de seguridad de VoIP. En Office 365 y Exchange Online, el modo protegido es obligatorio y no se puede deshabilitar.

Cuando configure el plan de marcado de mensajería unificada para usar el modo Protegido con SIP (Protocolo de inicio de sesión) o Protegido, los servidores Exchange que contestan llamadas del plan de marcado de mensajería unificada cifrarán el tráfico de señalización SIP (para el modo protegido con SIP) o los canales de medios de Protocolo de transporte en tiempo real (RTP) y el tráfico de señalización SIP (para el modo protegido).


> [!IMPORTANT]
> Para las implementaciones locales e híbridas, al configurar los valores de SipTCPListeningPort, SipTLSListeningPort o UMStartUpMode en un servidor de acceso de clientes que ejecute el servicio de enrutador de llamadas de mensajería unificada de Microsoft Exchange o un servidor de buzones de correo que ejecute el servicio de mensajería unificada de Microsoft Exchange, deberá configurar las reglas del Firewall de Windows correctamente para permitir el tráfico de red RTP y SIP.



Para otras tareas de administración relacionadas con los planes de marcado de mensajería unificada, consulte [Procedimientos de plan de marcado de mensajería unificada](um-dial-plan-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Planes de marcado de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Utilice la EAC para configurar la seguridad VoIP en un plan de marcado de mensajería unificada

1.  En la EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**, seleccione el plan de marcado de mensajería unificada al que quiere cambiar la seguridad VoIP y luego haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, haga clic en **Configurar**.

3.  En **General**, en el **Modo de seguridad VoIP**, seleccione una de las siguientes opciones:
    
      - **Protegido con SIP**
    
      - **No protegido** (valor predeterminado)
    
      - **Protegido**

4.  Haga clic en **Guardar**.

## Uso del Shell para configurar la seguridad de VoIP de un plan de marcado de Mensajería unificada

En este ejemplo se configura un plan de marcado de Mensajería unificada con el nombre de `MySecureDialPlan` para cifrar el tráfico de SIP y RTP.

    Set-UMDialPlan -identity MySecureDialPlan -VoIPSecurity Secured

En este ejemplo se configura un plan de marcado de Mensajería unificada con el nombre de `MySecureDialPlan` para cifrar el tráfico de SIP y RTP.

    Set-UMDialPlan -identity MySecureDialPlan -VoIPSecurity SIPsecured

En este ejemplo se configura un plan de marcado de Mensajería unificada con el nombre de `MySecureDialPlan` para no cifrar el tráfico de SIP y RTP.

    Set-UMDialPlan -identity MySecureDialPlan -VoIPSecurity Unsecured

