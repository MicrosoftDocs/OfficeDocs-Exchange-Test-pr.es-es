---
title: 'Configurar operador automático para usuarios que tienen nombres similares'
TOCTitle: Configurar a un operador automático para los usuarios que tienen nombres similares
ms:assetid: 2e7318a0-67f9-4d7b-8300-5f0ef77656a8
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997135(v=EXCHG.150)
ms:contentKeyID: 52061806
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar a un operador automático para los usuarios que tienen nombres similares

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2012-12-16_

Puede configurar el método que usará para los usuarios con nombres parecidos en las opciones **Libreta de direcciones y acceso del operador** de un operador automático, o bien dejar la configuración predeterminada del operador automático y definir esta configuración en el plan de marcado asociado al operador. De forma predeterminada, un operador automático puede desambiguar entre dos o más usuarios con nombres iguales o parecidos porque la configuración predeterminada del operador es **Heredar del plan de marcado**.


> [!NOTE]
> Para que la información que se incluye sobre los usuarios con nombres parecidos funcione correctamente, hay que escribir la información del título, departamento y ubicación para los destinatarios de la organización de Microsoft Exchange.



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

## Usar el EAC para configurar un operador automático de mensajería unificada para usuarios con nombres parecidos

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Operadores automáticos de mensajería unificada**, seleccione el operador automático de mensajería unificada que quiera configurar y luego haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Operador automático de mensajería unificada**, haga clic en **Libreta de direcciones y acceso de operador**. Luego, en **Información a incluir para usuarios con el mismo nombre**, seleccione una de las siguientes opciones:
    
      - **Puesto   **El operador automático incluirá el puesto de cada usuario cuando se enumeran las coincidencias.
    
      - **Departamento**   El operador automático incluirá el departamento de cada usuario cuando se enumeran las coincidencias.
    
      - **Ubicación**   El operador automático incluirá la ubicación de cada usuario cuando se enumeran las coincidencias.
    
      - **Ninguno**   El operador automático no incluirá información adicional cuando se enumeran las coincidencias.
    
      - **Solicitar el alias** El operador automático pedirá al autor de la llamada el alias de usuario.
    
      - **Heredar del plan de marcado**   El operador automático usará la configuración predeterminada del plan de marcado asociado con el operador automático.

4.  Haga clic en **Guardar**.

## Usar el EAC para configurar un operador automático de mensajería unificada para usuarios con nombres parecidos

En este ejemplo se establece la información que se incluirá para usuarios con nombres parecidos en "Solicitar el alias" para un operador automático de mensajería unificada denominado `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -MatchedNameSelectionMethod PromptForAlias

En este otro ejemplo se establece la información que se incluirá en el título de los usuarios con nombres parecidos, permite la búsqueda de nombres y permite a los llamadores que llaman al operador automático pulsar \* para oír el saludo de bienvenida de Outlook para un operador automático de mensajería unificada denominado `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -MatchedNameSelectionMethod Title -NameLookupEnabled $true -StarOutToDialPlanEnabled $true

