---
title: 'Crear una regla de protección de transporte: Exchange 2013 Help'
TOCTitle: Crear una regla de protección de transporte
ms:assetid: 3a857185-ee16-4ee7-9e57-8be95f7e753a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd302432(v=EXCHG.150)
ms:contentKeyID: 49895578
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Crear una regla de protección de transporte

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

Puede usar las reglas de protección de transporte para aplicar una protección de derechos constante a los mensajes, en función de las propiedades de los mensajes, como remitente, destinatario, asunto y contenido.


> [!WARNING]
> Antes de crear reglas de transporte en su entorno de producción, recomendamos que los cree en un entorno de prueba y los pruebe exhaustivamente. Las reglas de transporte creadas en este tema son ejemplos. Puede crear reglas de transporte usando los predicados y valores correspondientes, en función de los requerimientos.



Para ver tareas de administración adicionales relacionadas con la Configuración de Information Rights Management (IRM), consulte [Procedimientos de Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 2-5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el el contenido "Reglas de transporte" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Un servidor que ejecuta [Información general sobre Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/es-es/library/hh831364.aspx) debe estar disponible en su organización y tener plantillas de RMS existentes.

  - Si configura reglas de protección de mensajes con IRM, y también usa el registro en diario, plantéese habilitar el descifrado de informes diarios para permitir al agente de registro diario guardar una copia cifrada del mensaje en el informe de diario. Para obtener más información, consulte [Descifrado de informe de diarios](journal-report-decryption-exchange-2013-help.md).

  - Después de crear una regla de protección de transporte, si la regla no se puede aplicar al mensaje porque un servidor AD RMS no está disponible, el servicio de transporte colocará a los mensajes en cola en servidores de buzones de correo. En función del volumen de estos mensajes, puede que se consuma espacio de disco adicional en los servidores de buzones de correo. Exchange intentará la protección de IRM del mensaje tres veces. Después de estos intentos, si no se puede tener acceso al servidor de AD RMS o el mensaje no se puede proteger con IRM, se enviará un informe de no entrega (NDR) al remitente.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Uso de EAC para crear una regla de protección de transporte

1.  Vaya a **Flujo de correo** \> **Reglas**.

2.  En la vista de lista, haga clic en **Nuevo**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

3.  En **Nueva regla** , primero haga clic en **Más opciones** y, a continuación, complete los siguientes campos:
    
      - **Nombre**   Escriba un nombre para la regla de transporte.
    
      - **Aplicar esta regla si**   Seleccione una condición e introduzca los valores necesarios para la condición. Para agregar más condiciones, haga clic en **Agregar condición**.
        

        > [!IMPORTANT]
        > Si no selecciona ninguna condición al crear una regla de protección de transporte, todos los mensajes que gestionan los servidores Exchange 2013 con el servicio de transporte de la organización estarán protegidos con IRM. Proteger todos los mensajes con IRM requiere más recursos. Por lo tanto, le recomendamos que planifique su servidor de buzones de correo e implementación de AD&nbsp;RMS en consecuencia.

    
      - **Haz lo siguiente**    Seleccione **Aplicar la protección de derechos al mensaje con** y, a continuación, use el cuadro de diálogo **Seleccionar plantilla RMS** para seleccionar una plantilla.
    
      - **Excepto si**   (Opcional) Haga clic en **Agregar excepción** para especificar una excepción a la regla.

4.  Haga clic en **Guardar** para crear una regla de transporte.

## Usar el Shell para crear una regla de protección de transporte

  - Para crear una regla de protección de transporte, debe tener plantillas RMS existentes en su implementación AD RMS. En este ejemplo, se recuperan las plantillas disponibles desde el clúster de AD RMS.
    
        Get-RMSTemplate | format-list
    
    Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-RMSTemplate](https://technet.microsoft.com/es-es/library/dd297960\(v=exchg.150\)).

  - En este ejemplo, se crea la regla de protección de transporte Protect-BusinessCriticalProject. La regla protege con IRM los mensajes que contienen la frase "Crucial para la empresa" en el campo Asunto mediante la plantilla **No reenviar**.
    

    > [!NOTE]
    > En este ejemplo se usa el predicado <CODE>SubjectContainsWords</CODE>. Puede usar cualquier combinación de predicados de reglas de transporte para formar las condiciones y excepciones de la regla. Para obtener información acerca de los predicados disponibles, consulte <A href="mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md">Condiciones de las reglas de transporte (predicados)</A>.

    
        New-TransportRule -Name "Protect-BusinessCriticalProject" -SubjectContainsWords "Business Critical" -ApplyRightsProtectionTemplate "Do Not Forward"
    
    Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-TransportRule](https://technet.microsoft.com/es-es/library/bb125138\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si creó una regla de protección de transporte correctamente, siga uno de estos procedimientos:

  - Use el EAC para comprobar que se ha creado la regla y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar") para ver las propiedades de la regla.

  - Use el cmdlet [Get-TransportRule](https://technet.microsoft.com/es-es/library/aa998585\(v=exchg.150\)) para recuperar la regla. Para ver un ejemplo de cómo recuperar una regla, consulte [Examples](https://technet.microsoft.com/es-es/aa998585\(exchg.150\)#examples) en **Get-TransportRule**.

  - Usando Outlook, Outlook Web App o un dispositivo móvil, envíe un mensaje de prueba que cumpla con las condiciones de la regla y compruebe si el mensaje que recibe el destinatario está protegido con IRM.

