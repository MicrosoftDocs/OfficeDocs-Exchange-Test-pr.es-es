---
title: 'Asignar certificado a servicios UM y llamar enrutador UM: Exchange 2013 Help'
TOCTitle: Asignar un certificado a los servicios de mensajería unificada y llamar al enrutador de mensajería unificada
ms:assetid: 8a900e5f-9779-4213-92d7-ec157b15fbc5
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn205140(v=EXCHG.150)
ms:contentKeyID: 54652445
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Asignar un certificado a los servicios de mensajería unificada y llamar al enrutador de mensajería unificada

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-04-29_

Puede usar el EAC o el Shell para asignar un certificado comercial de terceros o de infraestructura de clave pública (PKI) autofirmado para servicios de Exchange específicos. Cuando use el cmdlet **New-ExchangeCertificate** para asignar el certificado a servicios de Exchange con el parámetro *Services*, se le pedirá que asigne el certificado a servicios de Exchange. Si utiliza el EAC para crear un certificado, el Asistente para nuevo certificado de Exchange no le pedirá que asigne el certificado a servicios de Exchange. Tiene que editar las propiedades del certificado y asignarlo seleccionando qué servicios desea asignarle.

Cada servicio tiene requisitos de certificado diferentes. Por ejemplo, algunos servicios solamente requieren un nombre de servidor en los campos **Nombre de sujeto** o **Nombre alternativo del firmante** de un certificado y otros servicios pueden requerir un nombre de dominio completo (FQDN). Asegúrese de que el nombre del certificado es compatible con los usos necesarios para los servicios para los que se habilita.


> [!WARNING]
> Los certificados autofirmados no se pueden utilizar al integrar la mensajería unificada (UM) con Microsoft Lync Server.



Para otras tareas de administración relacionadas con la administración de certificados para mensajería unificada, consulte [Implementación de certificados para los procedimientos de mensajería unificada](deploying-certificates-for-um-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Administración de certificados" en el tema [Permisos de infraestructura de la Shell y de Exchange](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md) y la entrada "Servicio de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md). También debe iniciar sesión con una cuenta que pertenezca al grupo de administradores locales del equipo.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para asignar un certificado a los servicios de mensajería unificada y de enrutador de llamadas de mensajería unificada

1.  En el EAC, vaya a **Servidores** \> **Certificados**.

2.  En la vista de lista, seleccione el certificado que desea asignar a los servicios de mensajería unificada y de enrutador de llamadas de mensajería unificada y, después, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página *\<Nombre del certificado\>*, seleccione **Servicios** y, luego, seleccione **Mensajería unificada (UM)** y **Enrutador de llamadas de mensajería unificada**.

4.  Haga clic en **Guardar**.

## Usar el Shell para asignar un certificado a los servicios de mensajería unificada y de enrutador de llamadas de mensajería unificada

En este ejemplo se asigna un certificado a los servicios de mensajería unificada y de enrutador de llamadas de mensajería unificada.

    Enable-ExchangeCertificate -Thumbprint 5113ae0233a72fccb75b1d0198628675333d010e -Services 'UM, UMCallRouter'

