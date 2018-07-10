---
title: 'Escriba un nombre de empresa: Exchange 2013 Help'
TOCTitle: Escriba un nombre de empresa
ms:assetid: a0e7cb24-0f55-442d-8ae2-21b177940b78
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee423549(v=EXCHG.150)
ms:contentKeyID: 50556828
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Escriba un nombre de empresa

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-04-19_

Puede escribir el nombre de su empresa en el cuadro **Nombre de la empresa** en un operador automático de mensajería unificada. De manera predeterminada, no se indica ningún nombre de empresa. Si escribe un nombre de empresa, se reproducirá un mensaje de bienvenida personalizado con el nombre de la empresa a las personas que llamen en el operador automático de mensajería unificada.

Para otras tareas relacionadas con los operadores automáticos de mensajería unificada, consulte [Procedimientos operador automático de mensajería unificada](um-auto-attendant-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el contenido "Operadores automáticos de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un operador automático de MU. Para conocer los pasos detallados, consulte [Crear un operador automático de mensajería unificada](create-a-um-auto-attendant-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para configurar un nombre de empresa

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Operadores automáticos de mensajería unificada**, seleccione el operador automático de mensajería unificada en el que desea ajustar el nombre de la empresa, y, a continuación, en la barra de herramientas, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Operador automático de mensajería unificada**, \> **General**, en **Nombre de empresa**, escriba el nombre de la empresa.

4.  Haga clic en **Guardar**.

## Uso del Shell para configurar un nombre de empresa

En este ejemplo, se establece el nombre de empresa en un operador automático de mensajería unificada denominado `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessName "Northwind Traders"

