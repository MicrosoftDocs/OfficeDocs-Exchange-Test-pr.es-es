---
title: 'Implementar Exchange 2013 en una topología entre bosques: Exchange 2013 Help'
TOCTitle: Implementar Exchange 2013 en una topología entre bosques
ms:assetid: 65be650f-d435-4f60-9ff0-5cb88a726abb
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998597(v=EXCHG.150)
ms:contentKeyID: 51406508
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Implementar Exchange 2013 en una topología entre bosques

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Este tema explica cómo implementar Exchange 2013 en una topología entre bosques usando Forefront Identity Manager 2010 R2 SP1. Para implementar Exchange 2013 en una topología entre bosques, primero tiene que instalar Exchange 2013 en cada bosque y, a continuación, conectar los bosques para que los usuarios puedan ver los datos de dirección y disponibilidad de los boques.

La siguiente figura ilustra la sincronización de usuarios entre dos bosques de Exchange 2013.

**Ejemplo de sincronización entre bosques de Exchange 2013**

![Ejemplo de varios bosques de Exchange 2010](images/Aa998597.df0ba5dd-cb96-4542-98bd-2a425defe317(EXCHG.150).gif "Ejemplo de varios bosques de Exchange 2010")

Este tema *no* describe cómo implementar Exchange 2013 en una topología de bosque (o bosque de recursos) dedicado de Exchange. Para obtener más información acerca de cómo implementar Exchange 2013 en una topología de bosque de recursos, consulte [Implementación de Exchange 2013 en una topología de bosques de recursos de Exchange](deploy-exchange-2013-in-an-exchange-resource-forest-topology-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

Para llevar a cabo el siguiente procedimiento en Exchange 2013, confirme los siguientes aspectos:

  - Ha configurado correctamente el Sistema de nombres de dominio (DNS) para la resolución de nombres a través de distintos bosques en la organización. Para comprobar que DNS está configurado correctamente, use la herramienta de ping para comprobar la conectividad en cada uno de los bosques desde los demás bosques de la organización y desde el servidor en que piensa ejecutar el agente GALSync.

  - El agente de administración GALSync (MA) se comunica con el bosque de Exchange 2013 mediante Windows PowerShell V2.0 RTM. Para asegurarse de que Windows PowerShell v1.0 no está instalado en este equipo, vaya al Panel de control y haga clic en Programas y características.

  - Asegúrese de que no se haya instalado la administración remota de Windows mediante WindowsUpdate.

  - Instale Windows PowerShell y la administración remota de Windows. Para obtener detalles, consulte el artículo 968930 de Microsoft Knowledge Base, el [paquete Windows Management Framework Core (Windows PowerShell 2.0 y WinRM 2.0)](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=968930).

  - Descargue Forefront Identity Manager 2010 R2 SP1. Consulte [Descargar Microsoft Forefront Identity Manager 2010 R2 SP1](https://go.microsoft.com/fwlink/p/?linkid=279868).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Implementar Exchange 2013 en una topología entre bosques con Forefront Identity Manager 2010 R2 SP1

1.  En cada bosque, instale Exchange 2013 por separado. Para instalar Exchange 2013, siga los mismos pasos que realizaría si estuviera instalando Exchange 2013 en una topología de bosque único. Para obtener instrucciones detalladas, consulte uno de los siguientes temas:
    
      - [Implementar una nueva instalación de Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)
    
      - [Instalar Exchange 2013 utilizando el asistente de configuración](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)
        

        > [!NOTE]
        > En este tema se asume que no tiene una topología existente de Exchange 2007 o de Exchange 2010. Si tiene una topología existente de Exchange y quiere actualizarla, vea <A href="upgrade-from-exchange-2010-to-exchange-2013-exchange-2013-help.md">Actualizar de Exchange&nbsp;2010 a Exchange&nbsp;2013</A> o <A href="upgrade-from-exchange-2007-to-exchange-2013-exchange-2013-help.md">Actualizar de Exchange&nbsp;2007 a Exchange&nbsp;2013</A>.



2.  En cada bosque, utilice Usuarios y equipos de Active Directory para crear un contenedor en el que FIM 2010 R2 SP1 creará contactos para cada buzón del otro bosque. Lo más recomendable es que denomine este contenedor **FromFIM**. Para crear el contenedor, seleccione el dominio en el que desea crearlo, haga clic con el botón secundario en el dominio, seleccione **Nuevo** \> **Unidad organizativa**. En **Nuevo objeto: unidad organizativa**, escriba **FromFIM** y, a continuación, haga clic en **Aceptar**.

3.  Cree un agente de administración GALSync para cada bosque usando Forefront Identity Manager. De este modo podrá sincronizar los usuarios en cada bosque y crear una GAL común. Para obtener más detalles, consulte los recursos siguientes:
    
      - [Configurar la sincronización de listas de direcciones globales (GAL) con Forefront Identity Manager (FIM) 2010](https://go.microsoft.com/fwlink/p/?linkid=279869)
    
      - [Trabajar con agentes de administración](https://go.microsoft.com/fwlink/p/?linkid=279870)
    
      - [Mapa de ruta de documentación de Forefront Identity Manager 2010 R2](https://go.microsoft.com/fwlink/p/?linkid=279871)
    

    > [!IMPORTANT]
    > Aunque los recursos se ocupan de Exchange 2010, Exchange&nbsp;2013 es compatible con FIM 2010 R2 SP1. Asegúrese de configurar <STRONG>Extensiones</STRONG> en FIM 2010 R2 SP1 para Exchange&nbsp;2013.

    
    1.  En la página **Configurar extensiones**, en **Configurar nombres de visualización de particiones**, junto a **Provisión para**, seleccione **Exchange 2013**. Verá el campo **URI de Exchange 2013 RPS**. Introduzca el URI de un servidor de acceso de clientes de Exchange 2013 para asegurarse de que la conexión de PowerShell remoto esté funcionando. El **URI de Exchange 2013 RPS** debe estar en el siguiente formato: http://CAS\_Server\_FQDN/Powershell. Haga clic en **Aceptar**.
        

        > [!NOTE]
        > Asegúrese de que las credenciales del administrador usadas para conectarse al bosque de Exchange&nbsp;2013&nbsp;también puedan establecer conexiones PowerShell remotas a ese bosque.<BR>La figura siguiente muestra cómo seleccionar el aprovisionamiento de Exchange&nbsp;2013.

        
        **Aprovisionamiento de agente de administración GalSync para Exchange 2013**
        
        ![Aprovisionamiento de Exchange 2010 del agente de administración](images/Aa998597.8f403cda-e5e4-4edf-887f-c1ed46cee3f5(EXCHG.150).gif "Aprovisionamiento de Exchange 2010 del agente de administración")  

4.  Cree un conector de envío SMTP en cada uno de los bosques. Para conocer los pasos detallados, consulte [Configurar un conector de envío entre bosques](configure-a-cross-forest-send-connector-exchange-2013-help.md).

5.  En cada bosque, habilite el servicio de disponibilidad para que los usuarios de cada bosque puedan ver los datos de disponibilidad de los usuarios de los otros bosques. Para obtener más información, consulte [Servicio de disponibilidad en Exchange 2013](availability-service-in-exchange-2013-exchange-2013-help.md).

6.  Si quiere retransmitir correo a través de algún bosque de la organización, debe configurar un dominio de ese bosque como dominio con autorización. Para conocer los pasos detallados, consulte [Configurar Exchange para aceptar correo de varios dominios autoritativos](configure-exchange-to-accept-mail-for-multiple-authoritative-domains-exchange-2013-help.md).

