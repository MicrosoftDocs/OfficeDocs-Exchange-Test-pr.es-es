---
title: 'Crear una regla de protección de Outlook: Exchange 2013 Help'
TOCTitle: Crear una regla de protección de Outlook
ms:assetid: da64750d-faaf-44de-ad8c-888eba7fbdbf
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd638196(v=EXCHG.150)
ms:contentKeyID: 49895952
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Crear una regla de protección de Outlook

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

Con las reglas de protección de Microsoft Outlook, podrá proteger los mensajes con Information Rights Management (IRM) mediante la aplicación de una plantilla Rights Management Services (AD RMS) de Active Directory en Outlook 2010 antes de que se envíen los mensajes.

Para otras tareas de administración relacionadas con IRM, consulte [Procedimientos de Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Protección de derechos" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Debe tener implementado un servidor [AD RMS](https://technet.microsoft.com/es-es/library/hh831364.aspx) en el mismo bosque de Active Directory que el servidor que ejecuta Microsoft Exchange Server 2013.

  - Si configura reglas de protección de Outlook en mensajes protegidos por IRM, considere la posibilidad de habilitar el descifrado de transporte para permitir que los agentes de transporte, incluido el agente de reglas de transporte, descifren y obtengan acceso al mensaje. Si usa diarios, también debe considerar la posibilidad de habilitar el descifrado de informes de diarios para permitir que el agente de registro de diario guarde una copia no cifrada del mensaje en el informe del diario. Para obtener más información, consulte [Descifrado de informe de diarios](journal-report-decryption-exchange-2013-help.md).

  - No se puede usar el Centro de Administración de Exchange (EAC) para crear reglas de protección de Outlook. Debe usar el Shell.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Usar el Shell para crear una regla de protección de Outlook

En este ejemplo se crea la regla de protección de Outlook Proyecto Contoso. La regla protege los mensajes que se envían al grupo de distribución ContosoPMs con la plantilla AD RMS Business Critical.

    New-OutlookProtectionRule -Name "Project Contoso" -SentTo "DL-ContosoPMs@contoso.com" -ApplyRightsProtectionTemplate "Business Critical"


> [!NOTE]
> Cuando usa el predicado <CODE>SentTo</CODE> para una protección de Outlook y especifica un grupo de distribución, solo los mensajes dirigidos al grupo de distribución en los campos Para, CC o CCO está protegidos por IRM. La protección IRM no se aplica a los mensajes dirigidos a miembros individuales del grupo de distribución.



También puede usar los predicados `FromDepartment` y `SentToScope` para aplicar reglas de protección IRM a mensajes enviados a un departamento específico o a mensajes enviados al ámbito especificado (`InOrganization` para mensajes internos y `All` para todos los destinatarios).

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [New-OutlookProtectionRule](https://technet.microsoft.com/es-es/library/dd298182\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que ha creado correctamente una regla de protección de Outlook, siga estos pasos:

  - Ejecute el cmdlet [Get-OutlookProtectionRule](https://technet.microsoft.com/es-es/library/dd298004\(v=exchg.150\)) para asegurarse de que la regla ha sido creada y para ver las propiedades de la regla. Para ver un ejemplo de cómo crear una regla de protección de Outlook, consulte [Examples](https://technet.microsoft.com/es-es/dd298004\(exchg.150\)#examples) en **Get-OutlookProtectionRule**.

  - Use Outlook 2010 para crear un mensaje de prueba que cumpla la condición de la regla y asegúrese de que la regla se activa en el cliente.
    

    > [!NOTE]
    > Puede llevar tiempo que una regla de protección de Outlook esté disponible en Outlook.


