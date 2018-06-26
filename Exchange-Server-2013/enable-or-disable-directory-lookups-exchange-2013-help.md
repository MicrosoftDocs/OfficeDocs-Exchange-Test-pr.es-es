---
title: 'Habilitar o deshabilitar las búsquedas de directorio: Exchange 2013 Help'
TOCTitle: Habilitar o deshabilitar las búsquedas de directorio
ms:assetid: c0768815-8578-4385-8d4c-7d1e40304cec
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee423557(v=EXCHG.150)
ms:contentKeyID: 52061933
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar o deshabilitar las búsquedas de directorio

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2016-05-10_

Puede habilitar búsquedas en el directorio para que los autores de las llamadas de un operador automático de mensajería unificada puedan buscar nombres en el directorio con el teclado numérico del teléfono, pero no puedan realizar búsquedas en el directorio con entradas de voz. Esta opción está habilitada de manera predeterminada. Si esta configuración está deshabilitada, las personas que llaman no podrán buscar en el directorio a una persona específica que use entradas de teclado o comandos de voz.

Para conocer tareas de administración adicionales relacionadas con los operadores automáticos de mensajería unificada, consulte [Procedimientos operador automático de mensajería unificada](um-auto-attendant-procedures-exchange-2013-help.md).


> [!NOTE]
> Los usuarios no pueden usar reconocimiento de voz automático (ASR) o entradas de voz para localizar usuarios en el directorio de Outlook Voice Access, pueden utilizar sólo entradas de tonos o DTMF.



## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el contenido "Operadores automáticos de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un operador automático de MU. Para conocer los pasos detallados, consulte [Crear un operador automático de mensajería unificada](create-a-um-auto-attendant-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para habilitar o deshabilitar las búsquedas en el directorio

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Operadores automáticos de mensajería unificada**, seleccione el operador automático de mensajería unificada en el que desea habilitar o deshabilitar las búsquedas en el directorio, y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Operador automático de mensajería unificada** \> **Libreta de direcciones y acceso de operador**, en **Opciones para las búsquedas en la libreta de direcciones**, active la casilla al lado de **Permitir a los autores de llamadas buscar usuarios por nombre o alias** para permitir que los autores de llamada busquen usuarios. Desactive esta casilla si desea impedir que los autores de llamada busquen usuarios.

4.  Haga clic en **Guardar**.

## Uso del Shell para habilitar o deshabilitar las búsquedas de directorio

En este ejemplo se deshabilitan las búsquedas de directorio en un operador automático de Mensajería unificada`MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -NameLookupEnabled $false

