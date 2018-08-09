---
title: 'Configurar uso compartido federado entre organizaciones de Exchange'
TOCTitle: Configuración del uso compartido federado entre organizaciones de Exchange
ms:assetid: 94e31454-b027-4757-b52f-d3c2ead6d916
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ657473(v=EXCHG.150)
ms:contentKeyID: 49895790
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuración del uso compartido federado entre organizaciones de Exchange

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Con el uso compartido federado, los usuarios de la organización de Exchange local pueden compartir información de calendario de disponibilidad con los destinatarios de otras organizaciones de Exchange que también están configurados para un uso compartido federado. El uso compartido de la información de disponibilidad se puede habilitar entre dos organizaciones que ejecutan Exchange 2013 y también entre organizaciones que tienen una implementación de Exchange mixta. Para obtener más información acerca del uso compartido federado, consulte [Uso compartido](sharing-exchange-2013-help.md).

En este tema se resumen los requisitos y los pasos de configuración necesarios para habilitar el uso compartido de disponibilidad entre las diversas implementaciones de Exchange habituales:

  - Dos organizaciones Exchange 2013.

  - Una organización de Exchange 2013 y una organización de Exchange 2010 SP2.

  - Una organización de Exchange 2007 (o una organización mixta de Exchange 2007 y Exchange 2010 SP2) y una organización de Exchange 2013.

  - Una organización de Exchange 2003 (o una organización mixta de Exchange 2003 y Exchange 2010 SP2) y una organización de Exchange 2013.

Para otras tareas de administración relacionadas con el uso compartido federado, consulte [Procedimientos de la Federación](federation-procedures-exchange-2013-help.md).


> [!IMPORTANT]
> Esta característica de Exchange Server 2013 no es totalmente compatible con Office 365 operado por 21Vianet en China y pueden aplicarse ciertas limitaciones en las características. Para obtener más información, consulte <A href="https://go.microsoft.com/fwlink/?linkid=313640">Acerca de Office 365 operado por 21Vianet</A>.



## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 2 horas.

  - Los procedimientos descritos en este tema requieren permisos específicos. Vea cada procedimiento para ver la información de permisos.

  - Antes de realizar los procedimientos que aparecen en el tema, asegúrese de que entiende las limitaciones asociadas al uso compartido de información de disponibilidad entre organizaciones de Exchange. Para obtener información más detallada, consulte [Limitations of free/busy sharing](sharing-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## ¿Qué desea hacer?

## Configurar el uso compartido de información de disponibilidad entre organizaciones de Exchange 2013

Complete los pasos de [Configuración del uso compartido federado](configure-federated-sharing-exchange-2013-help.md) para ambas organizaciones.

## Configurar el uso compartido de información de disponibilidad entre organizaciones de Exchange 2013 y Exchange 2010 SP2

  - Configurar el uso compartido federado de la organización de Exchange 2013. Complete los pasos de [Configuración del uso compartido federado](configure-federated-sharing-exchange-2013-help.md).

  - Configure la delegación federada (nombre anterior que denominaba el uso compartido federado) de la organización de Exchange 2010 SP2. Complete los pasos de [Caso: Configuración del uso compartido de información de disponibilidad entre usuarios](https://go.microsoft.com/fwlink/p/?linkid=268410).

## Configurar el uso compartido de información de disponibilidad entre organizaciones de Exchange 2013 y Exchange 2007

  - Configurar el uso compartido federado de la organización de Exchange 2013. Complete los pasos de [Configuración del uso compartido federado](configure-federated-sharing-exchange-2013-help.md).

  - Complete los siguientes pasos en la organización de Exchange 2007:
    
    1.  **Agregar un servidor de Exchange 2010 SP2**
        
        Se debe instalar un servidor Exchange 2010 SP2 con el rol de servidor Acceso de clientes en la organización de Exchange 2007. Si tiene otros servidores Exchange 2010, también deben actualizarse a Exchange 2010 SP2. Para obtener más información sobre la instalación de Exchange 2010 en una organización de Exchange 2007, consulte [Exchange 2007 - Guía de planeamiento para la actualización y coexistencia](https://go.microsoft.com/fwlink/p/?linkid=268411).
    
    2.  **Configurar la delegación federada**
        
        Configure la delegación federada para la organización de Exchange 2007. En un servidor Exchange 2010 SP2 de la organización de Exchange 2007, siga los pasos descritos [Caso: Configuración del uso compartido de información de disponibilidad entre usuarios](https://go.microsoft.com/fwlink/p/?linkid=268410).
    
    3.  **Configurar la sincronización de Active Directory**
        
        La sincronización de Active Directory debe configurarse para todos los usuarios que necesiten compartir información de disponibilidad entre las organizaciones. Puede configurar la sincronización de Active Directory manualmente o usar un servicio de sincronización automatizado de Active Directory. Para configurar la sincronización con Active Directory, consulte los siguientes pasos:
        
          - **Requisitos previos**   Asegúrese de que la organización cumpla los requisitos de instalación de la sincronización de Active Directory.
            
            Para obtener más información, consulte [Prepare la sincronización de Active Directory](https://go.microsoft.com/fwlink/p/?linkid=247302)
        
          - **Planifique**   Asegúrese de comprender la Herramienta de sincronización de directorios de Microsoft Online Services y la guía básica de instalación.
            
            Para obtener más información, consulte [Sincronización de Active Directory: Guía básica](http://go.microsoft.com/fwlink/p/?linkid=203007)
        
          - **Instale y configure**   Configure la sincronización de Active Directory entre la organización local y la organización de servicio arrendatario de Office 365.
            
            Para obtener más información, consulte [Instalar y actualizar la herramienta de sincronización de directorios de Microsoft Online Services](https://go.microsoft.com/fwlink/p/?linkid=247303)
    
    4.  **Crear un espacio de direcciones de disponibilidad**
        
        Cree un espacio de direcciones de disponibilidad para la organización remota de Exchange 2013 que dirija las solicitudes de disponibilidad de los usuarios de buzones de Exchange 2007 al servidor de acceso de clientes de Exchange 2010 SP2 en la organización de Exchange 2007. Esta configuración habilita las solicitudes de disponibilidad de los usuarios de Exchange 2007 en los usuarios de la organización remota de Exchange 2013 que debe ponerse en proxy mediante el servidor de acceso de cliente de Exchange 2010 en la organización de Exchange 2007. El servidor de acceso de cliente de Exchange 2010 en la organización de Exchange 2007 emplea la confianza de federación y la relación de organización para enviar las solicitudes de disponibilidad al punto final de disponibilidad de bosque de la organización remota de Exchange 2013.
        
        Para configurar el espacio de direcciones de disponibilidad, en el servidor de acceso de cliente de Exchange 2010 de la organización de Exchange 2007, ejecute el comando siguiente en el Shell de administración de Exchange:
        
            Add-AvailabilityAddressSpace -AccessMethod InternalProxy -ProxyUrl https://<Exchange 2010 CAS server name>/ews/exchange.asmx -ForestName <SMTP domain of the remote Exchange organization> -UseServiceAccount $True
        
        Para obtener información detallada sobre parámetros y sintaxis, consulte [Add-AvailabilityAddressSpace](https://go.microsoft.com/fwlink/p/?linkid=268413).

## Configurar el uso compartido de información de disponibilidad entre organizaciones de Exchange 2013 y Exchange 2003

  - Configurar el uso compartido federado de la organización de Exchange 2013. Complete los pasos de [Configuración del uso compartido federado](configure-federated-sharing-exchange-2013-help.md).

  - Complete los siguientes pasos en la organización de Exchange 2003:
    
    1.  **Agregue el servidor de Exchange 2010 SP2**.
        
        Se debe instalar un servidor Exchange 2010 SP2 con el rol de servidor Acceso de clientes en la organización de Exchange 2003. Si tiene otros servidores Exchange 2010, también deben actualizarse a Exchange 2010 SP2. Para obtener más información sobre la instalación de Exchange 2010 en una organización de Exchange 2003, consulte [Exchange 2003 - Guía de planeamiento para la actualización y coexistencia](https://go.microsoft.com/fwlink/?linkid=268414)
        

        > [!WARNING]
        > Para que el uso compartido de información de disponibilidad funcione correctamente entre organizaciones de Exchange 2013 y Exchange 2003, la carpeta pública <STRONG>OU=EXTERNA (FYDIBOHF25SPDLT)</STRONG> debe existir en la jerarquía de carpetas públicas. Esta carpeta se crea automáticamente en el servidor de buzones de correo de Exchange 2010 de la organización de Exchange 2003 únicamente si selecciona la opción para crear carpetas públicas como parte de la configuración de los parámetros de cliente para soporte de Outlook 2003 durante la configuración de Exchange 2010. Asimismo, esta opción solamente se presenta durante el proceso de configuración si el servidor de buzones de Exchange 2010 es el primer servidor de buzones instalado en la organización. Si no se creó la carpeta pública <STRONG>OU=EXTERNA (FYDIBOHF25SPDLT)</STRONG> durante la instalación, deberá crearla manualmente. Paras obtener información acerca de cómo crear esta carpeta pública, consulte el artículo sobre <A href="http://go.microsoft.com/fwlink/p/?linkid=3052">cómo solucionar problemas de disponibilidad al utilizar la federación de Exchange en Microsoft Office 365 para empresas</A>.

    
    2.  **Configurar la delegación federada**.
        
        Configure la delegación federada para la organización de Exchange 2003. En un servidor Exchange 2010 SP2 de la organización de Exchange 2003, siga los pasos descritos [Caso: Configuración del uso compartido de información de disponibilidad entre usuarios](https://go.microsoft.com/fwlink/p/?linkid=268410).
    
    3.  **Configurar la sincronización de Active Directory**.
        
        La sincronización de Active Directory debe configurarse para todos los usuarios que necesiten compartir información de disponibilidad entre las organizaciones. Puede configurar la sincronización de Active Directory manualmente o usar un servicio de sincronización automatizado de Active Directory. Para obtener más información sobre la sincronización de Active Directory, consulte el artículo sobre [Forefront Identity Management](https://go.microsoft.com/fwlink/?linkid=294645).
        
          - **Requisitos previos**   Asegúrese de que la organización cumpla los requisitos de instalación de la sincronización de Active Directory.
            
            Para obtener más información, consulte [Prepare la sincronización de Active Directory](https://go.microsoft.com/fwlink/p/?linkid=247302)
        
          - **Planifique**   Asegúrese de comprender la Herramienta de sincronización de directorios de Microsoft Online Services y la guía básica de instalación.
            
            Para obtener más información, consulte [Sincronización de Active Directory: Guía básica](http://go.microsoft.com/fwlink/p/?linkid=203007)
        
          - **Instale y configure**   Configure la sincronización de Active Directory entre la organización local y la organización de servicio arrendatario de Office 365.
            
            Para obtener más información, consulte [Instalar y actualizar la herramienta de sincronización de directorios de Microsoft Online Services](https://go.microsoft.com/fwlink/p/?linkid=247303)
    
    4.  **Configure carpetas públicas para el uso compartido de la información de disponibilidad en su organización de Exchange 2003.**
        
        Complete los pasos siguientes en un servidor de Exchange 2003:
        
          - En el Administrador del sistema de Exchange, en el árbol de consola, vaya a **Grupos administrativos** \> **Primer grupo administrativo** \> **Servidores**.
        
          - Seleccione el servidor de Exchange 2003 y, a continuación, vaya a **Primer grupo de almacenamiento** \> **Almacén de carpetas públicas** \> **Carpetas públicas** \> **DISPONIBILIDAD de Schedule+**
        
          - En el panel de acciones, seleccione la carpeta **UO=EXTERNA (FYDIBOHF25SPDLT)** para el **Primer grupo administrativo**.
        
          - Haga clic con el botón secundario en la carpeta **UO=EXTERNA (FYDIBOHF25SPDLT)** y haga clic en **Propiedades**.
        
          - En **Propiedades de UO=EXTERNA (FYDIBOHF25SPDLT)**, seleccione la ficha **Replicación**.
        
          - Para replicar la carpeta **UO=EXTERNA (FYDIBOHF25SPDLT)** en el servidor de acceso de cliente/buzones de Exchange 2010, haga clic en **Agregar**.
        
          - En **Seleccionar un almacén de carpetas públicas**, seleccione la **Base de datos de carpetas públicas** para el servidor de acceso de cliente/buzones de Exchange 2010 y, a continuación, haga clic en **Aceptar**
            

            > [!NOTE]
            > De forma predeterminada, usa la programación de replicación establecida en la base de datos de carpetas públicas.

        
          - Haga clic en **Aceptar** para cerrar **Propiedades de UO=EXTERNA (FYDIBOHF25SPDLT)** y guardar los cambios.
        
          - Realice los mismos pasos para la carpeta **UO=Grupo administrativo de Exchange (FYDIBOHF23SPDLT)**.
            

            > [!WARNING]
            > En función del tamaño de las carpetas públicas, esta replicación podría tardar varias horas en finalizar.

        
          - Una vez replicadas las carpetas públicas **OU=EXTERNA (FYDIBOHF25SPDLT)** y **OU=Grupo administrativo de Exchange (FYDIBOHF23SPDLT)** en el servidor de acceso de cliente/buzones de Exchange 2010, deberá quitar las réplicas de estas carpetas públicas en el servidor de Exchange 2003.
    
    5.  **Modificar el parámetro LegacyExchangeDN**
        
        Modifique el parámetro *LegacyExchangeDN* en todos los objetos con correo habilitado de la organización de Exchange 2003 que hagan referencia a la organización remota de Exchange 2013. Cambie el valor de la unidad organizativa (OU) existente para el objeto con correo habilitado a **Externa (FYDIBOHF25SPDLT)**. Por ejemplo, **LegacyExchangeDN=/o=Primera organización/ou=Externa (FYDIBOHF25SPDLT)/cn=Destinatarios/cn=Nombre de usuario**.
        
        Para modificar los objetos habilitados para correo en la organización de Exchange 2003, puede usar el [Editor de interfaces del servicio de Active Directory (Editor ADSI)](https://go.microsoft.com/fwlink/?linkid=294644) o la [Utilidad Microsoft Exchange Server LegacyDN](http://go.microsoft.com/fwlink/?linkid=294643).

