---
title: 'Crear una directiva de uso compartido: Exchange 2013 Help'
TOCTitle: Crear una directiva de uso compartido
ms:assetid: cae8cab0-6265-448b-8add-5202cdb20678
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ657494(v=EXCHG.150)
ms:contentKeyID: 49895918
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Crear una directiva de uso compartido

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-04-07_

Las directivas de uso compartido permiten controlar la forma en que los usuarios de una organización de Exchange comparten la información de calendario con los usuarios que se encuentran fuera de la organización. Compartir directivas permite compartir información de calendario establecida por los usuarios de persona a persona con diferentes tipos de usuarios externos. Admiten el uso compartido de información de calendario con organizaciones externas federadas (como Office 365 u otra organización de Exchange local), organizaciones externas no federadas y personas con acceso a Internet. Para aplicar una directiva de uso compartido específica a los usuarios, vea [Aplicar una directiva de uso compartida a los buzones](apply-a-sharing-policy-to-mailboxes-exchange-2013-help.md).


> [!IMPORTANT]
> La creación de una directiva de uso compartido es uno de los varios pasos que debe realizar para configurar el uso compartido en su organización de Exchange. Primero tiene que configurar una confianza de federación con el sistema de autenticación de Azure Active Directory para la organización de Exchange local, para poder compartir la información de calendario con otras organizaciones de Exchange federadas. No se necesita una confianza de federación para las directivas de uso compartido de Internet.



Para obtener más información acerca del uso compartido federado, consulte [Uso compartido](sharing-exchange-2013-help.md).

Para otras tareas de administración relacionadas con la federación, consulte [Procedimientos de la Federación](federation-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  15 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el sección “Permisos de calendario y uso compartido” del tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Para las directivas de uso compartido entre organizaciones de Exchange federadas, debe cumplirse lo siguiente:
    
      - Debe existir un servidor Acceso de cliente de Exchange 2013 en cada organización de Exchange. Las directivas de uso compartido también se admiten entre las organizaciones de Exchange donde una organización tiene servidores de acceso de cliente Exchange 2013 y la otra organización tiene servidores de acceso de cliente Exchange 2010 SP3 o posterior.
    
      - Cada organización de Exchange ha creado una confianza de federación con el sistema de autenticación de Azure AD. Para obtener información más detallada, consulte [Configurar una confianza de federación](configure-a-federation-trust-exchange-2013-help.md).
    
      - Cada organización de Exchange ha configurado un identificador de organización federada. Se han agregado dominios usados para generar las direcciones de correo electrónico de los usuarios a los identificadores de organización.
    
      - Los buzones de correo de usuario están ubicados en los servidores de buzones de Exchange 2013 o Exchange 2010 en cada organización de Exchange.
    
      - Únicamente los usuarios de Outlook 2010 o superior y Outlook Web App pueden crear invitaciones de uso compartido.

  - Para las directivas de uso compartido con organizaciones de Exchange no federado o acceso individual, debe cumplirse lo siguiente:
    
      - Un servidor Acceso de cliente de Exchange 2013 existe en la organización de Exchange que comparte la información de calendario del usuario.
    
      - Los buzones de correo de usuario están ubicados en los servidores Buzón de correo de Exchange 2013 de la organización de Exchange que comparte la información de calendario del usuario.
    
      - El servidor Acceso de cliente Exchange 2013 debe estar habilitado para acceder a Outlook Web App.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## ¿Qué desea hacer?

## Uso de EAC para crear una directiva de uso compartido

1.  Vaya a **organización** \> **uso compartido**.

2.  En la vista de lista, en **Uso compartido individual**, haga clic en **Nuevo**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

3.  En **nueva directiva compartida**, escriba un nombre descriptivo para la directiva de uso compartido en el cuadro **Nombre de la directiva**.

4.  Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para especificar las reglas de uso compartido para la directiva de uso compartido.

5.  En **regla de uso compartido**, seleccione una de las siguientes opciones para especificar los dominios con los que desea compartir:
    
      - **Compartir con todos los dominios**
    
      - **Compartir con un dominio específico**

6.  Si selecciona **Compartir con un dominio específico**, escriba el dominio con el que desea compartir. Si necesita indicar más de un dominio para esta directiva de uso compartido, guarde la configuración del primer dominio y, después, cambie las reglas de uso compartido para agregar más dominios.

7.  Para definir los niveles de uso compartido del calendario que desea aplicar a la directiva, active la casilla **Compartir la carpeta de calendario** y, a continuación, seleccione una de las siguientes opciones:
    
      - **Información de disponibilidad de calendario solo con hora**
    
      - **Información de disponibilidad de calendario con hora, asunto y ubicación**
    
      - **Toda la información de citas de calendarios, incluidas la hora, el asunto, la ubicación y el título**

8.  Haga clic en **guardar** para configurar las reglas de la directiva de uso compartido.

9.  Si desea que esta directiva de uso compartido sea la directiva predeterminada para los usuarios de la organización de Exchange, seleccione la casilla de verificación **Hacer que esta sea mi directiva de uso compartido predeterminada**.

10. Haga clic en **guardar** para crear la directiva de uso compartido.

## Usar el EAC para permitir que todos los usuarios compartan información completa de calendario

Puede editar la directiva de uso compartido predeterminada para permitir que todos los usuarios compartan información completa de calendario con personas fuera de la organización.

1.  Vaya a **organización** \> **uso compartido**.

2.  En la vista de lista, en **Uso compartido individual**, seleccione **Directiva predeterminada de uso compartido** y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En el cuadro de diálogo **Directiva de uso compartido**, seleccione **Compartir con todos los dominios** y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

4.  En el cuadro de diálogo **Regla de uso compartido**, en **Especifica qué información quieres compartir**, seleccione **Toda la información de citas de calendarios, incluidas la hora, el asunto, la ubicación y el título** y, a continuación, haga clic en **Guardar**.

5.  En el cuadro de diálogo **Directiva de uso compartido**, haga clic en **Guardar** para establecer las reglas para la directiva de uso compartido.

## Uso del Shell para crear una directiva de uso compartido

  - En este ejemplo se crea la directiva de uso compartido Contoso para el dominio federado externo contoso.com. Esta directiva permite que los usuarios del dominio contoso.com vean la información detallada sobre la disponibilidad (disponible/no disponible) de su usuario. Esta directiva está habilitada de modo predeterminado.
    
        New-SharingPolicy -Name "Contoso" -Domains contoso.com: CalendarSharingFreeBusyDetail

  - En este ejemplo se crea la directiva de uso compartido ContosoWoodgrove para dos dominios federados distintos (contoso.com y woodgrovebank.com) con acciones de uso compartido diferentes configuradas para cada dominio. La directiva está deshabilitada.
    
        New-SharingPolicy -Name "ContosoWoodgrove" -Domains 'contoso.com: CalendarSharingFreeBusySimple', 'woodgrovebank.com: CalendarSharingFreeBusyDetail -Enabled $false

  - En este ejemplo se crea la directiva de uso compartido Anonymous para una organización de Exchange con el servidor de acceso de clientes CAS01 y el servidor de buzones de correo MAIL01, con la acción de uso compartido configurada para la información de disponibilidad de calendario limitada. Esta directiva permite a los usuarios de su organización de Exchange invitar a usuarios con acceso a Internet a ver la información de disponibilidad en el calendario enviándoles un vínculo. La directiva está habilitada.
    
    1.  Establezca la dirección URL del proxy web para MAIL01.
        
            Set-ExchangeServer -Identity "Mail01" -InternetWebProxy "<Webproxy URL>"
    
    2.  Habilite el directorio virtual de publicación en CAS01.
        
            Set-OwaVirtualDirectory -Identity "CAS01" -ExternalURL "<URL for CAS01>" -CalendarPublishingEnabled $true
    
    3.  Cree la directiva de uso compartida anónimo y configure el uso compartido de información de calendario limitado.
        
            New-SharingPolicy -Name "Anonymous" -Domains 'Anonymous: CalendarSharingFreeBusySimple' -Enabled $true

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte los siguientes temas:

  - [New-SharingPolicy](https://technet.microsoft.com/es-es/library/dd298186\(v=exchg.150\))

  - [Set-ExchangeServer](https://technet.microsoft.com/es-es/library/bb123716\(v=exchg.150\))

  - [Set-OwaVirtualDirectory](https://technet.microsoft.com/es-es/library/bb123515\(v=exchg.150\))

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la directiva de uso compartido se creó correctamente, ejecute el siguiente comando del Shell para comprobar la información de directiva de uso compartido.

    Get-SharingPolicy <policy name> | format-list


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


