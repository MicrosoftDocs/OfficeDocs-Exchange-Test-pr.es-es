---
title: 'Crear certificados para mensajería unificada (UM): Exchange 2013 Help'
TOCTitle: Crear certificados para mensajería unificada (UM)
ms:assetid: 66807ee7-3d3f-482d-a3ac-d4e9baca3271
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn205141(v=EXCHG.150)
ms:contentKeyID: 54652434
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Crear certificados para mensajería unificada (UM)

 

_**Se aplica a:**Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2013-04-29_

Puede usar el Asistente de nuevo certificado de intercambio en el EAC o el Shell para crear certificados autofirmados o solicitudes de certificado para un certificado interno de infraestructura de clave pública (PKI). Para la mensajería unificada (UM), puede utilizar uno de estos certificados para el servicio de mensajería unificada de Microsoft Exchange y el servicio de enrutamiento de llamadas de mensajería unificada de Microsoft Exchange. Puede utilizar el mismo certificado para ambos servicios, o bien un certificado distinto para cada uno. También puede comprar e importar un certificado comercial de otros fabricantes para servicios de mensajería unificada (UM). Si usa un certificado autofirmado para mensajería unificada (UM), es posible que necesite incluir el nombre de los servidores de acceso de cliente y de buzón en el nombre alternativo del firmante (SAN).

De manera predeterminada, cuando instala Exchange Server 2013, se crean dos certificados autofirmados: **certificado de autenticación de Microsoft Exchange Server** y **Microsoft Exchange**. El certificado autofirmado de **Microsoft Exchange** puede usarse para que la mensajería unificada cifre datos, pero usted debe asignar el certificado a los servicios de enrutador de llamadas de mensajería unificada y de mensajería unificada. Después de asignar el certificado a los servicios de mensajería unificada, puede copiarse e importarse a las puertas de enlace VoIP, IP-PBX y PBX habilitadas para SIP. Sin embargo, en vez de usar los certificados autofirmados predeterminados, es posible que necesite crear uno específicamente para mensajería unificada.


> [!WARNING]
> No se pueden usar certificados autofirmados cuando integra mensajería unificada (UM) con Microsoft Lync Server.



Para otras tareas de administración relacionadas con la administración de certificados para la mensajería unificada, consulte [Implementación de certificados para los procedimientos de mensajería unificada](deploying-certificates-for-um-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Administración de certificados" en el tema [Permisos de infraestructura de la Shell y de Exchange](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md) y entrada "Servicio de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md). También debe iniciar sesión con una cuenta que pertenezca al grupo de administradores locales del equipo.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para crear una solicitud de certificado para mensajería unificada (UM)

1.  En el EAC, vaya a **Servidores** \> **Certificados** y, a continuación, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

2.  En la página **Nuevo certificado de intercambio**, seleccione **Crear una solicitud para un certificado desde una entidad de certificación** y, a continuación, haga clic en **Siguiente**.

3.  Escriba un nombre descriptivo para el certificado y luego haga clic en **Siguiente**.

4.  Si no necesita un certificado comodín, haga clic en **Siguiente**. Si necesita un certificado comodín, seleccione **Solicitar un certificado comodín. Un certificado comodín puede usarse para proteger todos los subdominios dentro del dominio raíz con un solo certificado**, escriba el nombre del dominio raíz y haga clic en **Siguiente**.

5.  Dentro de **Almacenar solicitud de certificado en este servidor**, haga clic en **Examinar** para ir a la ubicación donde desea almacenar el archivo. Puede almacenar la solicitud de certificado en cualquier servidor de acceso de cliente o de buzón de la organización de Exchange. Seleccione la ubicación, haga clic en **Aceptar** y en **Siguiente**.

6.  Si solicitó un certificado comodín, avance directamente al paso 9.

7.  Si no solicitó un certificado comodín, necesitará especificar los dominios que desea incluir en el certificado. Si desea editar un dominio, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar") y en **Siguiente**.

8.  Dentro de **De acuerdo con su selección, se incluirán los siguientes dominios en el certificado. Puede agregar dominios adicionales aquí o realizar cambios** puede agregar, editar, eliminar o comprobar el nombre de los dominios que aparecen dentro de **Dominio**. A continuación, haga clic en **Siguiente**.

9.  Dentro de **Especifique información sobre la organización. Este es un requisito de la entidad de certificación**, especifique la siguiente información:
    
      - **Nombre de la organización**
    
      - **Nombre del departamento**
    
      - **Ciudad o localidad**
    
      - **Estado o provincia**
    
      - **Nombre de país o región**   Para esta opción, use la lista desplegable y seleccione el país o la región.

10. Dentro de **Guardar la solicitud de certificado en el siguiente archivo**, escriba el nombre de archivo del certificado y haga clic en **Finalizar**.

## Usar el Shell para crear una solicitud de certificado para mensajería unificada (UM)

Este ejemplo crea una nueva solicitud de certificado de Exchange para un servidor de buzón denominado `MyMailboxServer` con un nombre descriptivo de `CertUM`.

    New-ExchangeCertificate -FriendlyName 'CertUM' -GenerateRequest -PrivateKeyExportable $true -KeySize '2048' -DomainName '*.northwindtraders.com' -SubjectName 'C=US,S=wa,L=redmond,O=northwindtraders,OU=servers,CN= northwindtraders.com' -Server 'MyMailboxServer'

## Usar el EAC para crear un certificado autofirmado para mensajería unificada (UM)

1.  En el EAC, vaya a **Servidores** \> **Certificados** y, a continuación, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

2.  En la página **Nuevo certificado de intercambio**, elija **Crear un certificado autofirmado** y seleccione **Siguiente**.

3.  Escriba un nombre descriptivo para el certificado y luego seleccione **Siguiente**.

4.  Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para seleccionar los servidores de Exchange a los que desee aplicar este certificado. A continuación, haga clic en **Siguiente**.

5.  Especifique los dominios que desee incluir en el certificado y, a continuación, seleccione **Siguiente**. Si desea agregar un dominio para un servicio, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

6.  Compruebe que los nombres de los dominios incluidos sean correctos y luego seleccione **Finalizar**.


> [!IMPORTANT]
> Cuando use el EAC para crear un certificado, no se le solicitará que habilite los servicios para el certificado. Tras la creación del certificado, puede usar el EAC o el cmdlet <STRONG>Enable-ExchangeCertificate</STRONG> en el Shell para habilitar los servicios de Exchange. Para obtener más información acerca de cómo asignar un certificado a servicios de mensajería unificada (UM), consulte <A href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">Asignar un certificado a los servicios de mensajería unificada y llamar al enrutador de mensajería unificada</A>.



## Usar el Shell para crear un certificado autofirmado para mensajería unificada (UM)

Este ejemplo crea un nuevo certificado autofirmado de Exchange para un servidor de buzón denominado `MyMailboxServer` con un nombre descriptivo de `UMCert`.

    New-ExchangeCertificate -Services 'UM, UMCallRouter' -DomainName '*.northwindtraders.com' -FriendlyName 'UMSelfSigned' -SubjectName 'C=US,S=WA,L=Redmond,O=Northwindtraders,OU=Servers,CN= Northwindtraders.com' -PrivateKeyExportable $true


> [!TIP]
> Cuando especifique los servicios que desea habilitar con el parámetro <EM>Services</EM>, se le solicitará que asigne esos servicios. En este ejemplo, se le solicitará que habilite el certificado para los servicios de enrutador de llamadas de mensajería unificada (UM) y la mensajería unificada (UM). Para obtener más información acerca de cómo habilitar un certificado para servicios, consulte <A href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">Asignar un certificado a los servicios de mensajería unificada y llamar al enrutador de mensajería unificada</A>.


