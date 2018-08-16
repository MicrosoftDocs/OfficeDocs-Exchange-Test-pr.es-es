---
title: 'Asociado conjunto servidor fax URI permitir envío faxes Exchange 2013 Help'
TOCTitle: El asociado del conjunto de servidor de fax URI para permitir el envío de faxes
ms:assetid: 77a9013b-d76b-4af2-8b2c-cef435cf67af
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ650873(v=EXCHG.150)
ms:contentKeyID: 52061877
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# El asociado del conjunto de servidor de fax URI para permitir el envío de faxes

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2016-12-09_

Puede habilitar y deshabilitar los faxes entrantes para usuarios que estén asociados con una directiva de buzón de mensajería unificada. De manera predeterminada, cuando habilita usuarios para mensajería unificada, los usuarios no pueden recibir mensajes de fax hasta que habilite los faxes entrantes en la directiva de buzones de mensajería unificada y especifique el URI para el servidor de fax del socio. Si los URI están configurados en la directiva de buzones de mensajería unificada pero la opción para permitir faxes entrantes está deshabilitada en el plan de marcado de mensajería unificada o para un usuario determinado, los usuarios habilitados para mensajería unificada vinculados con dicha directiva aún seguirán sin poder recibir faxes.

Para obtener más información acerca de los partners de fax, consulte [Microsoft PinPoint para asociados de negocios de Fax](https://go.microsoft.com/fwlink/?linkid=190238).

Para otras tareas de administración relacionadas con los faxes, consulte [Procedimientos de envío de faxes](faxing-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el el contenido "Directivas de buzón de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Utilice el EAC para establecer el URI del socio de fax

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea modificar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Directivas de buzones de mensajería unificada**, seleccione la directiva que desea cambiar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Directiva de buzones de mensajería unificada** \> **General**, en el cuadro **URI del servidor de fax del socio**, escriba el URI TCP o TLS. Por ejemplo: *sip:faxserver1.contoso.com:5060;transport=tcp* o *sip:faxserver2.contoso.com:5061;transport=tls*
    

    > [!NOTE]
    > Aunque el cuadro puede contener más de un URI de servidor de fax, sólo se utilizará uno. Si escribe dos URI, se utilizará sólo el primero.



4.  Haga clic en **Guardar** para guardar los cambios.

## Usar el Shell para establecer el URI del socio de fax

En este ejemplo se habilita a los usuarios vinculados con la directiva de buzones de mensajería unificada `UMDialPlan Default Policy` para que usen TCP con el puerto 5060 para el servidor de fax de socio `faxserver1`.

    Set-UMMailboxPolicy "UMDialPlan Default Policy" -FaxServerURI sip:faxserver1.contoso.com:5060;transport=tcp

En este ejemplo se habilita a los usuarios vinculados con la directiva de buzones de mensajería unificada `UMDialPlan Default Policy` para que usen TLS con el puerto 5061 para el servidor de fax de socio `faxserver2`.

    Set-UMMailboxPolicy "UMDialPlan Default Policy" -FaxServerURI sip:faxserver2.contoso.com:5061;transport=tls

