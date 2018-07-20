---
title: 'Configurar la zona horaria: Exchange 2013 Help'
TOCTitle: Configurar la zona horaria
ms:assetid: 30d769e1-3657-4622-bc9a-643c63cf46d9
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997162(v=EXCHG.150)
ms:contentKeyID: 50556764
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar la zona horaria

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2012-11-17_

De manera predeterminada, el operador automático de mensajería unificada usa la zona horaria del servidor de buzones en la que se creó. Sin embargo, en algunas situaciones deberá cambiar la zona horaria a otra diferente para un operador automático de mensajería unificada. Por ejemplo, si tiene dos planes de marcado de MU y cada plan de marcado representa una zona horaria diferente, debe configurar un operador automático de MU para que tenga la misma zona horaria que el servidor de buzones y el otro, para que tenga una zona horaria diferente.

Para conocer tareas de administración adicionales relacionadas con los operadores automáticos de mensajería unificada, consulte [Procedimientos operador automático de mensajería unificada](um-auto-attendant-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el contenido "Operadores automáticos de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un operador automático de MU. Para conocer los pasos detallados, consulte [Crear un operador automático de mensajería unificada](create-a-um-auto-attendant-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso del Centro de Administración de Exchange para configurar la zona horaria

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de MU**, en **Operadores automáticos de mensajería unificada**, seleccione el operador automático de mensajería unificada en el que desea ajustar la zona horaria, y, a continuación, pulse en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Operador automático de mensajería unificada**, haga clic en **Horario comercial** y, luego, en **Zona horaria**, seleccione la zona horaria de la lista desplegable.

4.  Para guardar sus cambios, haga clic en **Aceptar** y, a continuación, en **Guardar**.

## Usar el Shell para configurar la zona horaria

En este ejemplo, se configura la zona horaria a la zona horaria del Pacífico en un operador de mensajería unificada llamado `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -TimeZoneName Pacific

