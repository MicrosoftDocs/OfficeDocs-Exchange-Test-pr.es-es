---
title: 'Configurar un dominio aceptado para una unidad de negocio con buzones de correo fuera de la organización de Exchange: Exchange 2013 Help'
TOCTitle: Configurar un dominio aceptado para una unidad de negocio con buzones de correo fuera de la organización de Exchange
ms:assetid: ff46310b-5392-4eac-97bc-d39d397e1ce1
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ657737(v=EXCHG.150)
ms:contentKeyID: 49896043
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar un dominio aceptado para una unidad de negocio con buzones de correo fuera de la organización de Exchange

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-08-06_

En algunos casos, quizá deba configurar un dominio aceptado para una unidad de negocios en la cual algunos o todos los destinatarios del dominio no tienen buzones en la organización de Exchange. Esto puede suceder, por ejemplo, cuando una organización comparte el mismo espacio de direcciones SMTP entre dos o más sistemas de correo electrónico diferentes. Para esos escenarios, puede configurar un dominio aceptado como un dominio de retransmisión interna.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Dominios aceptados" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Si tiene un servidor Transporte perimetral con suscripción en la red perimetral, puede configurar dominios aceptados en un servidor de buzones de la organización de Exchange. La configuración de los dominios aceptados se replica al servidor Transporte perimetral durante la sincronización de EdgeSync. Para obtener más información, consulte [Suscripciones perimetrales](edge-subscriptions-exchange-2013-help.md).

  - Antes de configurar un dominio aceptado, debe comprobar que existe un registro de recursos MX del sistema de nombres de dominio (DNS) público para ese espacio de nombres SMTP, y que el registro de recursos MX haga referencia a un nombre de servidor y una dirección IP asociada a la organización de Exchange.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Usar el EAC para configurar un dominio aceptado como un dominio de retransmisión interna

1.  En el EAC, desplácese hasta **Flujo de correo** \> **Dominios aceptados**, seleccione el dominio que desea configurar y, luego, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En el campo **Nombre**, escriba el nombre para mostrar del dominio aceptado. Cada dominio aceptado para su organización debe tener un nombre único. Puede ser diferente del nombre del dominio aceptado. Por ejemplo, el dominio Contoso.com puede tener el nombre para mostrar Contoso Local Accepted Domain.

3.  Seleccione **Dominio de retransmisión interna**.

4.  Haga clic en **Guardar**.

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que configuró correctamente un dominio aceptado como un dominio de retransmisión interna, envíe un mensaje desde el dominio de retransmisión interna a un buzón de la organización de Exchange y compruebe que se recibió.

