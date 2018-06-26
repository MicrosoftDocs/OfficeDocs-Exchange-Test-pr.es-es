---
title: 'Crear un plan de marcado de mensajería unificada: Exchange 2013 Help'
TOCTitle: Crear un plan de marcado de mensajería unificada
ms:assetid: 963ff2e1-515d-439a-953a-664174e5e283
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb123819(v=EXCHG.150)
ms:contentKeyID: 49895791
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.CreateUMDialPlanWizardForm.CreateUMDialPlanWizardPage
ms.translationtype: HT
---

# Crear un plan de marcado de mensajería unificada

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2013-04-16_

Un plan de marcado de mensajería unificada (MU) contiene información de configuración relacionada con la red de telefonía. Un plan de marcado de mensajería unificada establece un vínculo desde el número de extensión telefónica de un usuario con correo de voz habilitado hasta su buzón de correo. Al crear un plan de marcado de mensajería unificada, puede configurar el número de dígitos de los números de extensión, el tipo de Identificador uniforme de recursos (URI) y los ajustes de seguridad VoIP para el plan de marcado.

Cada vez que crea un plan de marcado de la MU, también se crea una directiva de buzón de mensajería unificada. Esta directiva se denomina Directiva predeterminada \<*DialPlanName*\>.

Para otras tareas de administración relacionadas con los planes de marcado de mensajería unificada, consulte [Procedimientos de plan de marcado de mensajería unificada](um-dial-plan-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  3 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Planes de marcado de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para crear un plan de marcado de MU

1.  
    
    En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada** y, a continuación, haga clic en **Nuevo**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

2.  En la página **Nuevo plan de marcado de mensajería unificada**, complete los siguientes cuadros:
    
      - **Nombre**   Escriba el nombre del plan de marcado. El nombre de un plan de marcado de mensajería unificada es necesario y debe ser exclusivo. Sin embargo, se usa solamente para la visualización en el EAC y en el Shell. Si tiene que cambiar el nombre para mostrar del plan de marcado después de crearlo, antes debe eliminar el plan de marcado de mensajería unificada y, a continuación, crear otro plan de marcado con el nombre adecuado. Si la organización usa varios planes de marcado de mensajería unificada, es recomendable usar nombres significativos para los planes. La longitud máxima del nombre de un plan de marcado de MU es de 64 caracteres y puede incluir espacios. No obstante, no pueden incluirse ninguno de los caracteres siguientes: " / \\ \[ \] : ; | = , + \* ? \< \>.
        
        Aunque puede incluir espacios en un nombre para el plan de marcado de mensajería unificada, si integra la mensajería unificada con Office Communications Server 2007 R2 o Microsoft Lync Server, el nombre del plan de marcado no podrá contener espacios. Por lo tanto, si ha creado un plan de marcado con espacios en el nombre para mostrar y está integrándolo con Office Communications Server 2007 R2 o Lync Server, primero tendrá que eliminar el plan de marcado y, a continuación, crear otro plan de marcado que no incluya espacios en el nombre para mostrar.
        

        > [!IMPORTANT]
        > Aunque en el cuadro del nombre del plan de marcado se pueden escribir hasta 64 caracteres, el nombre no debe tener más de 49 caracteres. Si intenta crear un nombre de plan de marcado que contenga más de 49 caracteres, recibirá un mensaje de error. El mensaje le informará de que la directiva de buzón de correo de mensajería unificada no se pudo generar porque el nombre del plan de marcado de mensajería unificada es demasiado largo. Esta situación se produce porque, como se ha comentado anteriormente, al crear un plan de marcado, también se crea una directiva de buzón de correo de mensajería unificada predeterminada con el nombre Directiva predeterminada <EM>&lt;nombrePlanMarcado&gt;</EM>. Cuando los caracteres correspondientes a Directiva predeterminada se agregan al nombre del plan de marcado, el número total de caracteres supera el límite. El parámetro <EM>name</EM> tanto para el plan de marcado de MU como para la directiva de buzones de MU puede tener un máximo de 64 caracteres. No obstante, si el nombre del plan de marcado tiene 49 caracteres, el nombre de la directiva de buzones de MU tendrá más de 64 caracteres y el sistema no lo permitirá.

    
      - **Longitud de la extensión (dígitos)**   Escriba el número de dígitos para el plan de marcado. El número de dígitos para números de extensión se basa en el plan de marcado de telefonía que se crea en una central de conmutación (PBX) o en una IP PBX. Por ejemplo, si un usuario asociado con un plan de marcado de telefonía marca una extensión de 4 dígitos para llamar a otro usuario del mismo plan de marcado de telefonía, debe seleccionar 4 como el número de dígitos de la extensión.
        
        Este cuadro es obligatorio y tiene un intervalo de valores entre 1 y 20. La longitud típica oscila entre 3 y 7. Si el entorno de telefonía actual incluye números de extensión, deberá especificar un número de dígitos que coincida con el número de dígitos de dichas extensiones.
        
        Al crear un plan de marcado Protocolo de inicio de sesión (SIP) o E.164 y asociarlo a un usuario habilitado para MU, aún debe introducir un número de extensión para que lo use dicho usuario. Este número lo usan los usuarios de Outlook Voice Access para obtener acceso al buzón de correo.
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(Tipo UI\_URI)
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(Seguridad UI\_VoIP)
    
      - **Idioma del audio**   Use esta lista para especificar el idioma predeterminado que usarán los usuarios de Outlook Voice Access. Esta configuración no aplica a la configuración del idioma en un operador automático de mensajería unificada. Puede establecer que el idioma para Outlook Voice Access sea el mismo u otro diferente al idioma que se utiliza en un operador automático de mensajería unificada. Cuando un usuario realiza una llamada a un usuario vinculado a un plan de marcado, el idioma del audio es el idioma predeterminado que utiliza el operador grabado de voz. Las instrucciones del sistema que escuchan las personas que llaman también están grabadas en el mismo idioma. El idioma que se escoja en el plan de marcado de mensajería unificada se usará para leer el correo electrónico, los mensajes de voz y los elementos del calendario; decir el nombre del usuario si el saludo personal no se ha grabado, transcribir un mensaje de voz usando la característica Vista previa de mensaje de voz y habilitar el reconocimiento de voz automático (ASR) para trabajar correctamente.
    
      - **Código de país o región**   Use este cuadro para escribir el código de país o región que se usará para las llamadas salientes. Este número se antepondrá al número de teléfono que se marque. En este cuadro se pueden escribir de 1 a 4 dígitos. Por ejemplo, en Estados Unidos el código de país o región es 1. En el Reino Unido es 44.

3.  Haga clic en **Guardar**.

## Usar el Shell para crear un plan de marcado de MU

Este ejemplo crea un nuevo plan de marcado de MU denominado `MyUMDialPlan` que usa números de extensión de cuatro dígitos.

    New-UMDialplan -Name MyUMDialPlan -NumberofDigits 4

En este ejemplo se crea un nuevo plan de marcado de MU denominado `MyUMDialPlan` que usa números de extensión de cinco dígitos y admite URI de SIP.

    New-UMDialplan -Name MyUMDialPlan -UriType SIPName -NumberofDigits 5

