---
title: 'Crear un operador automático de mensajería unificada: Exchange 2013 Help'
TOCTitle: Crear un operador automático de mensajería unificada
ms:assetid: 773f53fb-d80f-4a79-8bd3-bd753942489f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998875(v=EXCHG.150)
ms:contentKeyID: 49895724
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.UnifiedMessaging.CreateAutoAttendantWizardForm.CreateAutoAttendantWizardPage
ms.translationtype: HT
---

# Crear un operador automático de mensajería unificada

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-03-08_

Al crear un operador automático de Mensajería unificada (MU), éste contesta las llamadas entrantes a un número de teléfono externo, que, normalmente, contestaría un operador humano. A diferencia de otros componentes de mensajería unificada, tales como los planes de marcado y las puertas de enlace IP de mensajería unificada, no es necesario crear operadores automáticos de mensajería unificada. Sin embargo, los operadores automáticos ayudan a quienes realizan llamadas, tanto internas como externas, a buscar a los usuarios o departamentos que están en una organización y a transferir llamadas a estos.

Para conocer tareas de administración adicionales relacionadas con los operadores automáticos de mensajería unificada, consulte [Procedimientos operador automático de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/um-auto-attendant-procedures).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  3 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el contenido "Operadores automáticos de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para crear un operador automático de mensajería unificada

1.  
    
    En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**, seleccione el plan de marcado de mensajería unificada para el cual desea agregar un operador automático y, luego, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de MU**, en **Operadores automáticos MU**, haga clic en **Nuevo**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

3.  En la página **Nuevo operador automático de MU**, escriba la siguiente información:
    
      - **Nombre**   Use esta casilla para crear el nombre para mostrar del operador automático de mensajería unificada. El nombre de un operador automático de mensajería unificada es necesario y debe ser exclusivo. Sin embargo, se usa solamente para la visualización en el EAC y en el Shell.
        
        Si tiene que cambiar el nombre para mostrar del operador automático después de haberlo creado, primero, deberá eliminar el operador automático de mensajería unificada existente y crear otro operador automático que tenga el nombre apropiado. Si su organización usa varios operadores automáticos de mensajería unificada, es recomendable usar nombres significativos para los operadores automáticos de mensajería unificada. La longitud máxima del nombre de un operador automático de mensajería unificada es de 64 caracteres y puede contener espacios.
        
        Aunque puede asignar un nombre que contenga espacios a un nuevo operador automático de mensajería unificada, si integra la mensajería unificada en Office Communications Server 2007 R2 o Microsoft Lync Server, el nombre del operador automático no podrá contener espacios. Por lo tanto, si ha creado un operador automático con espacios en el nombre para mostrar y está integrándolo con Office Communications Server 2007 R2 o Lync Server, primero tendrá que eliminar el operador automático y, a continuación, crear otro que no incluya espacios en el nombre para mostrar.
    
      - **Crear operador automático como habilitado**   Active esta casilla para habilitar el operador automático para responder llamadas entrantes una vez que el Asistente para nuevo operador automático de mensajería unificada haya finalizado. De forma predeterminada, los nuevos operadores automáticos se crean como deshabilitados.
        
        Si decide crear el operador automático de MU como deshabilitado, puede usar el EAC o el Shell para habilitar el operador automático después de finalizar el asistente.
    
      - **Configurar el operador automático para responder a los comandos de voz**    Active esta casilla para habilitar el operador automático de mensajería unificada para voz. Si se habilita el operador automático para voz, las personas que llamen podrán responder con entradas de voz o marcación por tonos a los mensajes de asistencia por voz personalizados o del sistema que use el operador automático de mensajería unificada. De forma predeterminada, cuando los operadores automáticos se crean, no están habilitados para voz.
        
        Para que las personas que llaman usen un operador automático habilitado para voz, debe instalar el paquete de idioma de MU apropiado que contiene compatibilidad con el reconocimiento de voz automático (ASR) y configurar las propiedades del operador automático para que use este idioma.
    
      - **Números de acceso**   Use este cuadro para escribir el número de extensión o los números de teléfono que usarán los autores de llamadas para establecer contacto con el operador automático. Escriba un número de extensión o un número telefónico en el cuadro y, a continuación, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para agregar el número a la lista. El número de dígitos del número de extensión o de teléfono que proporcione no tiene que coincidir con el número de dígitos de un número de extensión configurado en el plan de marcado de mensajería unificada asociado. El motivo es que se permiten las llamadas directas a los operadores automáticos de mensajería unificada.
        
        La cantidad de números de extensión o de teléfono que se especifican es ilimitada. En cualquier caso, puede crear un operador automático nuevo sin indicar un número de extensión. No es necesario un número de extensión o de teléfono.
        
        Puede editar o quitar un número de extensión o de teléfono existente. Para editar un número de extensión existente o un número telefónico, haga clic en **Editar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). Para quitar un número de extensión existente o un número telefónico de la lista, haga clic en **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar").

4.  Haga clic en **Guardar**.

## Use el Shell para crear un operador automático de MU

En este ejemplo, se crea un operador automático de MU denominado `MyUMAutoAttendant` que acepta llamadas entrantes, pero no está habilitado para voz.

    New-UMAutoAttendant -Name MyUMAutoAttendant -UMDialPlan MyUMDialPlan -PilotIdentifierList 55000 -Enabled $false

En este ejemplo, se crea un operador automático de MU habilitado para voz denominado `MyUMAutoAttendant`.

    New-UMAutoAttendant -Name MyUMAutoAttendant -UMDialPlan MyUMDialPlan -PilotIdentifierList 56000,56100 -SpeechEnabled $true

