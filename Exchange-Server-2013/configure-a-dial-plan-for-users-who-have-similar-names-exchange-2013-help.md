---
title: 'Configurar plan marcado para usuarios con nombres parecidos Exchange 2013 Help | Microsoft Docs'
TOCTitle: Configurar un plan de marcado para los usuarios con nombres parecidos
ms:assetid: 14783f45-95f5-49de-8215-0a3aef7dc034
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb266943(v=EXCHG.150)
ms:contentKeyID: 51406476
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar un plan de marcado para los usuarios con nombres parecidos

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-21_

Puede configurar un plan de marcado de Mensajería unificada (UM) para especificar la información que dan los llamadores cuando los usuarios tienen nombres iguales o parecidos. La mensajería unificada usa esta configuración para diferenciar entre los usuarios que tienen nombres iguales o parecidos y da esta información a los autores de llamadas. Cuando una persona que llama o un usuario de Outlook Voice Access debe introducir letras para encontrar a un usuario determinado, a veces, más de un nombre coincide con las letras introducidas. Puede usar una de las opciones disponibles para ofrecer a la persona que llama más información que le ayude a encontrar al usuario con el que intenta ponerse en contacto.

Puede definir esta configuración en los planes de marcado y los operadores automáticos de Mensajería unificada. Cuando se crea un operador automático de Mensajería unificada, este hereda esta configuración del plan de marcado que esté asociado al operador automático. De forma predeterminada, esta configuración no está definida para los planes de marcado, de forma que no se dará información adicional a los autores de llamadas para ayudarles a encontrar al usuario correcto.


> [!NOTE]
> Para que la información que se incluye sobre los usuarios con nombres parecidos funcione correctamente, hay que escribir la información del título, departamento y ubicación para los destinatarios de la organización de Microsoft Exchange.



Para otras tareas de administración relacionadas con los planes de marcado de mensajería unificada, consulte [Procedimientos de plan de marcado de mensajería unificada](um-dial-plan-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Planes de marcado de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para configurar planes de marcado de Mensajería unificada para usuarios con nombres parecidos

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, haga clic en **Configurar** \> **Transferir y buscar**, y luego, en **Información a incluir para usuarios con el mismo nombre**, seleccione una de las opciones siguientes:
    
      - **Título** El plan de marcado incluye el título de cada usuario cuando busca dos o más usuarios con nombres parecidos.
    
      - **Departamento** El plan de marcado incluye el departamento de cada usuario cuando encuentra dos o más usuarios con nombres parecidos.
    
      - **Ubicación** El plan de marcado incluye la ubicación de cada usuario cuando encuentra dos o más usuarios con nombres parecidos.
    
      - **Ninguno** El plan de marcado no incluirá ninguna información adicional cuando los usuarios tengan nombres similares. Pese a que esta es la configuración predeterminada, se recomienda incluir una de las opciones disponibles para los autores de llamadas. Si no lo hace, los autores de llamadas no podrán saber la diferencia entre dos o más usuarios con nombres parecidos.
    
      - **Pedir el alias** El plan de marcado pide al autor de la llamada el alias del usuario. Un alias es la parte de la dirección de correo o SMTP del usuario que está antes del símbolo (@).

3.  Haga clic en **Guardar**.

## Usar el Shell para configurar planes de marcado de Mensajería unificada para usuarios con nombres parecidos

En este ejemplo se establece la información a incluir con usuarios con nombres parecidos para que se pida el alias del usuario en un plan de marcado de UM denominado `MyDialPlan`.

    Set-UMDialplan -Identity MyDialPlan -MatchedNameSelectionMethod PromptForAlias

En este ejemplo se establece la información a incluir sobre departamento con usuarios con nombres parecidos en un plan de marcado de UM denominado `MyDialPlan`.

    Set-UMDialplan -Identity MyDialPlan -MatchedNameSelectionMethod Department

En este ejemplo se establece la información a incluir sobre ubicación con usuarios con nombres parecidos en un plan de marcado de UM denominado `MyDialPlan`.

    Set-UMDialplan -Identity MyDialPlan -MatchedNameSelectionMethod Location

