---
title: 'Crear una directiva de buzón de mensajería unificada: Exchange 2013 Help'
TOCTitle: Crear una directiva de buzón de mensajería unificada
ms:assetid: 7f20874b-c46c-4505-9a78-f63eacb578ff
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb123510(v=EXCHG.150)
ms:contentKeyID: 50556831
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.CreateUMMailboxPolicyWizardForm.CreateUMMailboxPolicyWizardPage
ms.translationtype: HT
---

# Crear una directiva de buzón de mensajería unificada

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-03-08_

Puede crear una directiva de buzones de mensajería unificada (MU) para aplicar un conjunto común de opciones de directiva de mensajería unificada, como opciones de directiva del NIP o restricciones de marcado, para una serie de buzones con mensajería unificada habilitada. Las directivas de buzones de mensajería unificada vinculan a un usuario habilitado para mensajería unificada con un plan de conmutación de llamadas de mensajería unificada y aplican una configuración de seguridad o conjunto de directivas común a una colección de buzones habilitados para mensajería unificada. Las directivas de buzones de mensajería unificada resultan útiles para aplicar y estandarizar la configuración de la mensajería unificada para los usuarios habilitados para ella.

De forma predeterminada, al crear un plan de conmutación de llamadas de mensajería unificada, también se crea una directiva de buzones de mensajería unificada. Puede que tenga que crear directivas de buzón de correo de mensajería unificada adicionales o modificar las directivas de buzón de correo de mensajería unificada existentes tras implementar mensajería unificada en su organización.

Para otras tareas de administración relacionadas con las directivas de buzón de correo de mensajería unificada, consulte [Procedimientos de políticas de buzón de mensajería unificada](um-mailbox-policy-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 3 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el el contenido "Directivas de buzón de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para crear una directiva de buzón de correo de mensajería unificada

1.  
    
    En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea modificar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Directivas de buzón de mensajería unificada**, haga clic en **Nuevo**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

3.  En la página **Nueva directiva de buzón de mensajería unificada**, en el cuadro de texto **Nombre**, escriba el nombre de la nueva directiva de buzón de correo de mensajería unificada.
    
    Use este cuadro para especificar un nombre único para la directiva de buzón de correo de mensajería unificada. Se trata de un nombre para mostrar que aparecerá en la Consola de administración de Exchange. Si necesita cambiar el nombre para mostrar de la directiva de buzón de correo de mensajería unificada después de haberla creado, primero debe eliminar la directiva existente y, a continuación, crear otra con el nombre adecuado. No puede eliminar una directiva de buzón de mensajería unificada si algún usuario habilitado para mensajería unificada está asociado a ella.
    
    El nombre de la directiva de buzón de correo de mensajería unificada es obligatorio, pero sólo se usa para mostrarlo. Se recomienda usar nombres con un significado concreto para las directivas de buzones de mensajería unificada, ya que la organización puede usar varias directivas de este tipo. La longitud máxima de un nombre de directiva de buzones de mensajería unificada es de 64 caracteres y puede incluir espacios. No obstante, no puede incluir ninguno de los caracteres siguientes: " / \\ \[ \] : ; | = , + \* ? \< \>.

4.  Haga clic en **Guardar** para guardar la nueva directiva de buzón de mensajería unificada. Cuando guarda la directiva de buzón de mensajería unificada, se habilitan todas las opciones de configuración predeterminadas, incluida la configuración de las directivas de PIN, las características de buzón de voz y el correo de voz protegido. Si desea personalizar o cambiar alguna opción predeterminada, use el cmdlet **Set-UMMailbox** para cambiar la configuración de la directiva de buzón de mensajería unificada que acaba de crear.

## Uso de Shell para crear una directiva de buzón de mensajería unificada

En este ejemplo se crea una nueva directiva de buzón de MU llamada `MyUMMailboxPolicy` asociada con un plan de marcado de MU llamado `MyUMDialPlan`.

    New-UMMailboxPolicy -Name MyUMMailboxPolicy -UMDialPlan MyUMDialPlan

