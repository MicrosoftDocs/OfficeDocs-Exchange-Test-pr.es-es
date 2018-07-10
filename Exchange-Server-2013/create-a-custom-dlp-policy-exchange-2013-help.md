---
title: 'Crear una nueva directiva de DLP personalizada: Exchange 2013 Help'
TOCTitle: Crear una nueva directiva de DLP personalizada
ms:assetid: b3299a39-9663-41e4-b76e-9d2f7879d486
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150550(v=EXCHG.150)
ms:contentKeyID: 48267713
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Crear una nueva directiva de DLP personalizada

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2016-03-18_

Una directiva de prevención contra la pérdida de datos (DLP) personalizada le permite establecer condiciones, reglas y acciones que ayuden a satisfacer las necesidades específicas de su organización y que no estén cubiertas en una de las plantillas de DLP preexistentes.

Las condiciones de la regla que están disponibles en una única directiva incluyen todas las reglas de transporte tradicionales además de los tipos de información confidencial presentados en [Qué buscan los tipos de información confidencial de Exchange](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md). Para obtener más información acerca de las reglas de transporte, consulte [Reglas de transporte o de flujo de correo](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange 2013) o [Reglas de flujo de correo (reglas de transporte) en Exchange Online](https://technet.microsoft.com/es-es/library/jj919238\(v=exchg.150\)) (Exchange Online).


> [!WARNING]
> Debe habilitar sus directivas de DLP en modo de prueba antes de ejecutarlo en su entorno de producción. Durante dichas pruebas, se recomienda que configure buzones de usuarios de ejemplo y envíe mensajes de prueba que invoquen las directivas de prueba para confirmar los resultados. Para obtener más información sobre las pruebas, consulte <A href="test-a-mail-flow-rule-exchange-2013-help.md">Probar una regla de flujo de correo</A>.



Para otras tareas adicionales relacionadas con la creación de una directiva de DLP personalizada, consulte [Procedimientos de DLP](dlp-procedures-exchange-2013-help.md) (Exchange 2013) o [Procedimientos de DLP](https://technet.microsoft.com/es-es/library/jj938003\(v=exchg.150\)) (Exchange Online).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 60 minutos

  - Entrada "Prevención contra la pérdida de datos (DLP)" Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Para crear una nueva directiva de DLP personalizada, debe seguir las instrucciones de instalación de Exchange 2013. Para obtener más información acerca de la implementación, consulte [Planificación e implementación](planning-and-deployment-for-exchange-2013-installation-instructions.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!NOTE]
> Debido a las variaciones en los entornos del cliente, los Servicios de soporte técnico de Microsoft (CSS) no pueden participar en el desarrollo o en las pruebas de scripts personalizados de expresiones regulares ("RegEx scripts"). Para el desarrollo, pruebas y depuración de scripts personalizados de RegEX, los clientes de Office 365 necesitarán contar con los recursos internos de TI. Como alternativa, los clientes de Office 365 pueden elegir usar un recurso externo de consultoría como los Servicios de consultoría de Microsoft (MCS). Independientemente de los recursos de desarrollo de scripts, los ingenieros de soporte técnico de CSS EXO y EOP no están disponibles para ayudar a los clientes con consultas acerca de los scripts de RegEx personalizados.




> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Utilice la EAC paa crear una directiva de DLP personalizada sin ningura regla existente

1.  En la EAC, desplácese hasta **Administración de cumplimiento** \> **Prevención contra la pérdida de datos**. Todas las directivas existentes que se hayan configurado se muestran en una lista.

2.  Haga clic en la flecha junto al icono **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono")y seleccione **Nueva directiva personalizada**.
    

    > [!IMPORTANT]
    > Si hace clic en el icono <STRONG>Agregar</STRONG><IMG title="Agregar icono" alt="Agregar icono" src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif">en lugar de la flecha, creará una nueva directiva basada en una plantilla. Para obtener más información acerca de la utilización de plantillas, consulte <A href="how-to-new-dlp-data-loss-prevention-policy-template.md">Crear una directiva DLP a partir de una plantilla</A>.



3.  En la página **Nueva directiva personalizada**, complete los siguientes campos:
    
    1.  **Nombre**   Agregue un nombre que distinguirá esta directiva de las demás.
    
    2.  **Descripción**   Agregue una descripción opcional que resuma esta directiva.
    
    3.  **Seleccione un estado**   Seleccione el modo o estado para esta directiva. La nueva directiva no estará completamente habilitada hasta que especifique que debe estarlo. El modo predeterminado para una directiva es de prueba sin notificaciones.

4.  Haga clic en **Guardar** para terminar de crear la nueva información de referencia de la directiva. La directiva se agrega a la lista de todas las directivas que haya configurado a pesar de que aún no hay reglas ni acciones asociadas con esta nueva directiva personalizada.

5.  Haga doble clic en la directiva que acaba de crear o selecciónela y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

6.  En la página **Modificar directiva de DLP**, haga clic en **Reglas**.
    
    Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono")para agregar una nueva regla en blanco. Puede establecer condiciones usando todas las reglas de transporte tradicionales además de los tipos de información confidencial.
    
    Para evitar confusiones, proporcione un nombre único para cada parte de su directiva o regla cuando tenga la opción de proporcionar su propia cadena de caracteres. Existen varias opciones adicionales disponibles para usted:
    
    1.  Haga clic en la flecha junto al icono **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para agregar una regla acerca de la notificación del remitente o concesión de reemplazos.
    
    2.  Para eliminar una regla, resáltela y haga clic en **Eliminar**![Eliminar icono](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Eliminar icono").
    
    3.  Haga clic en **Más opciones**![Icono Más opciones](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icono Más opciones") para agregar acciones y condiciones adicionales para esta regla incluidos los límites dependientes del tiempo de aplicación o efectos en otras reglas de esta directiva.

7.  Haga clic en **Guardar** para terminar de modificar la directiva y guardar los cambios.

Las plantillas de directivas de DLP son un tipo de característica en Microsoft Exchange que pueden ayudar a diseñar y aplicar una directiva sólida y un sistema de cumplimiento para su entorno de mensajería. Para obtener más información acerca de las características de cumplimiento, consulte [Directiva de mensajería y conformidad](messaging-policy-and-compliance-exchange-2013-help.md) (Exchange 2013) o [Seguridad y cumplimiento de Exchange Online](https://technet.microsoft.com/es-es/library/jj200706\(v=exchg.150\)).

## Más información

[Prevención de pérdida de datos](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Reglas de transporte o de flujo de correo](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)Exchange 2013

[Reglas de flujo de correo (reglas de transporte) en Exchange Online](https://technet.microsoft.com/es-es/library/jj919238\(v=exchg.150\))Exchange Online

[Integración de las reglas de información confidencial con las reglas de transporte](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)

