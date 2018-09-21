---
title: 'Crear una relación de organización: Exchange 2013 Help'
TOCTitle: Crear una relación de organización
ms:assetid: 5ea61b96-c8ca-44fc-b8b5-ca4341af36a6
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ657451(v=EXCHG.150)
ms:contentKeyID: 49895660
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Crear una relación de organización

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-04-07_

Configure una relación de organización para compartir la información de calendario con un socio de negocio externo. Puede configurar una relación de organización entre dos organizaciones federadas de Exchange 2013 o entre una organización federada de Exchange 2013 y organizaciones federadas de Exchange 2010. También puede configurar una relación de organización entre la organización de Exchange local y una organización de Office 365.


> [!IMPORTANT]
> La creación de una relación de organización representa uno de los pasos de la configuración del uso compartido federado de la organización de Exchange, y requiere configurar una confianza de federación para la organización local de Exchange.



Para obtener más información acerca del uso compartido federado, consulte [Uso compartido](sharing-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  15 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el sección “Permisos de calendario y uso compartido” del tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Se debe configurar una confianza de federación activa para la organización de Exchange local. Para obtener información más detallada, consulte [Configurar una confianza de federación](configure-a-federation-trust-exchange-2013-help.md).

  - La organización externa que quiere configurar en la relación de organización debe tener también una confianza de federación establecida con el sistema de autenticación de Azure AD. Al configurar la relación de organización se usa el dominio federado principal para la organización externa de Exchange.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## ¿Qué desea hacer?

## Usar el EAC para crear una relación de organización

1.  En un servidor de Exchange 2013 de la organización local, vaya a **organización** \> **uso compartido**.

2.  En **Uso compartido de la organización**, haga clic en **Nuevo**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

3.  En el cuadro **Nombre de la relación** de **nueva relación de organización**, escriba un nombre descriptivo para la relación de organización.

4.  En el cuadro **Dominios para compartir**, escriba el dominio federado o el subdominio federado para la organización de Office 365 o Exchange local a la que desea permitir que vea sus calendarios. Si necesita especificar varios dominios para la organización externa, separe los dominios con una coma. Por ejemplo, **contoso.com, service.contoso.com**.

5.  Active la casilla **Habilitar el uso compartido de la información de disponibilidad de calendario** para activar el uso compartido de calendario con los dominios que especifique. Establezca el nivel de uso compartido de la información de disponibilidad de calendario y defina qué usuarios pueden compartir esta información.
    
    Para configurar el nivel de acceso a la información de disponibilidad, seleccione una de las siguientes opciones:
    
      - **Información de disponibilidad de calendario solo con hora**
    
      - **Disponibilidad de calendario con hora, asunto y ubicación**
    
    Para especificar los usuarios que van a compartir la información de disponibilidad de calendario, seleccione una de las siguientes opciones:
    
      - **Todos en su organización**
    
      - **Un grupo de seguridad especificado**
        
        Para especificar un grupo de seguridad, haga clic en **Examinar**.

6.  Haga clic en **guardar** para crear la relación de organización.

## Uso del Shell para crear una relación de organización

En este ejemplo se crea una relación entre organizaciones con Contoso, Ltd con las condiciones siguientes:

  - La relación de la organización está habilitada para contoso.com, northamerica.contoso.com y europe.contoso.com.

  - El acceso de disponibilidad está habilitado.

  - La organización solicitante recibe la información de la fecha de disponibilidad, el asunto y la ubicación de la organización de destino.

<!-- end list -->

    New-OrganizationRelationship -Name "Contoso" -DomainNames "contoso.com","northamerica.contoso.com","europe.contoso.com" -FreeBusyAccessEnabled $true -FreeBusyAccessLevel LimitedDetails

En este ejemplo se intenta descubrir automáticamente la información de configuración de la organización externa de Exchange Contoso.com mediante el uso de los nombres de dominio que se proporcionan en el cmdlet **Get-FederationInformation**. Si usa este método para crear una relación de organización, primero debe asegurarse de haber creado un identificador de la organización mediante el cmdlet **Set-FederatedOrganizationIdentifier**.

    Get-FederationInformation -DomainName Contoso.com | New-OrganizationRelationship -Name "Contoso" -FreeBusyAccessEnabled $true -FreeBusyAccessLevel -LimitedDetails

Para obtener más información acerca de la sintaxis y los parámetros, consulte [Get-FederationInformation](https://technet.microsoft.com/es-es/library/dd351221\(v=exchg.150\)) y [New-OrganizationRelationship](https://technet.microsoft.com/es-es/library/ee332357\(v=exchg.150\)).

En este ejemplo se crea una relación entre organizaciones con Fourth Coffee. En este ejemplo, se proporciona la configuración de conexión con la organización externa de Exchange. Se aplican las condiciones siguientes:

  - La relación de organización se establece con el dominio fourthcoffee.com, un dominio federado de Fourth Coffee.

  - La dirección URL de la aplicación de los servicios Web Exchange es mail.fourthcoffee.com.

  - La dirección URL de detección automática es https://mail.fourthcoffee.com/autodiscover/autodiscover.svc/wssecurity.

  - El acceso de disponibilidad está habilitado.

  - La organización solicitante solo recibe información de disponibilidad con la hora.

<!-- end list -->

    New-OrganizationRelationship -Name "Fourth Coffee" -DomainNames "fourthcoffee.com" -FreeBusyAccessEnabled $true -FreeBusyAccessLevel -AvailabilityOnly -TargetAutodiscoverEpr "https://mail.fourthcoffee.com/autodiscover/autodiscover.svc/wssecurity" -TargetApplicationUri "mail.fourthcoffee.com"

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-OrganizationRelationship](https://technet.microsoft.com/es-es/library/ee332357\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

La finalización correcta del asistente para **nueva relación organizativa** representa el primer indicio de que la creación de la relación de organización se completó tal y como se esperaba.

Para comprobar con más detalle si la relación de organización se creó correctamente, ejecute el siguiente comando del Shell y verifique la información de relación:

```powershell
Get-OrganizationRelationship | format-list
```


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


