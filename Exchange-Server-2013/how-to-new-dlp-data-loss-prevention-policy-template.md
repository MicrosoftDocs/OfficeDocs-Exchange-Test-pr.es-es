---
title: 'Cómo: Nueva plantilla de directiva de DLP (prevención de pérdida de datos)'
TOCTitle: Crear una directiva DLP a partir de una plantilla
ms:assetid: 4432ef8b-6108-48d3-b2af-43ef5b40d2bc
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150515(v=EXCHG.150)
ms:contentKeyID: 48267642
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Crear una directiva DLP a partir de una plantilla

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2015-01-14_

En Microsoft Exchange Server 2013, puede usar las plantillas de directivas de prevención de pérdida de datos (DLP) para ayudar a cumplir con las necesidades de cumplimiento y directivas de mensajería de su organización. Estas plantillas incluyen conjuntos de reglas predefinidas que pueden ayudarle a administrar los datos del mensaje asociados con varios requisitos normativos y legales comunes. Para ver una lista de todas las plantillas suministradas por Microsoft, consulte [Plantillas de directivas de DLP suministradas en Exchange](dlp-policy-templates-supplied-in-exchange-exchange-2013-help.md). Las plantillas de DLP que se suministran pueden ayudarle a administrar:

  - Datos de la ley Gramm-Leach-Bliley (GLBA)

  - Estándar de seguridad de datos de la industria de las tarjetas de pago (PCI DSS)

  - Información de identificación personal de Estados Unidos (PII de EE.UU.)

Puede personalizar cualquiera de las plantillas de DLP o usarlas como están. Las plantillas de directivas de DLP se crean sobre la base de las reglas de transporte que incluyen nuevas condiciones o predicados y acciones. Las directivas de DLP admiten el rango completo de reglas de transporte y se pueden agregar reglas adicionales cuando se haya establecido una directiva de DLP. Para obtener más información acerca de las plantillas de directivas, consulte [Plantillas de directiva de DLP](dlp-policy-templates-exchange-2013-help.md). Para obtener más información acerca de las funciones de las reglas de transporte, consulte [Reglas de transporte o de flujo de correo](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange Server 2013) o [Reglas de flujo de correo (reglas de transporte) en Exchange Online](https://technet.microsoft.com/es-es/library/jj919238\(v=exchg.150\)) (Exchange Online). Una vez que haya empezado a aplicar una directiva, puede obtener información sobre cómo observar los resultados revisando los siguientes temas:

Exchange 2013: [Ver informes de detección de directivas de DLP](view-dlp-policy-detection-reports-exchange-2013-help.md)

Exchange Online: [Ver informes de detección de directivas de DLP](https://technet.microsoft.com/es-es/library/dn904484\(v=exchg.150\))


> [!WARNING]
> Debe habilitar sus directivas de DLP en modo de prueba antes de ejecutarlo en su entorno de producción. Durante dichas pruebas, se recomienda que configure buzones de usuarios de ejemplo y envíe mensajes de prueba que invoquen las directivas de prueba para confirmar los resultados.



Para tareas de administración adicionales relacionadas con la creación de una directiva de DLP a partir de una plantilla, consulte [Procedimientos de DLP](dlp-procedures-exchange-2013-help.md) (Exchange Server 2013) o [Procedimientos de DLP](https://technet.microsoft.com/es-es/library/jj938003\(v=exchg.150\)) (Exchange Online).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 30 minutos

  - Asegúrese de que Exchange 2013 se haya configurado tal y como se describe en [Planificación e implementación](planning-and-deployment-for-exchange-2013-installation-instructions.md).

  - Configure las cuentas de usuario y administrador dentro de su organización y valide el flujo de correo básico.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Prevención de pérdida de datos (DLP)" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md)

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Use el EAC para configurar una directiva de DLP desde una plantilla

1.  En el EAC, vaya a **Administración de cumplimiento** \> **Prevención contra la pérdida de datos** y, a continuación, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").
    

    > [!NOTE]
    > También puede seleccionar esta acción si hace clic en la flecha situada al lado del icono <STRONG>Agregar</STRONG><IMG title="Agregar icono" alt="Agregar icono" src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif"> y selecciona <STRONG>Nueva directiva DLP desde una plantilla</STRONG> del menú desplegable.



2.  En la página **Crear nueva directiva de DLP a partir de una plantilla**, complete los campos siguientes:
    
    1.  **Nombre**   Agregue un nombre que distinga esta directiva de las demás.
    
    2.  **Descripción**   Agregue una descripción opcional que resuma esta directiva.
    
    3.  **Elige una plantilla**   Seleccione la plantilla adecuada para empezar a crear una nueva directiva.
    
    4.  **Más opciones**   Seleccione el modo o el estado. La nueva directiva no estará completamente habilitada hasta que especifique que debe estarlo. El modo predeterminado para una directiva es de prueba sin notificaciones.
    
    5.  Haga clic en **Guardar** para finalizar la creación de la directiva.


> [!NOTE]
> Además de las reglas dentro de una directiva específica, la organización puede tener directivas de la empresa o expectativas adicionales que se aplican a datos regulados dentro de su entorno de mensajería. Exchange&nbsp;2013 facilita el cambio de la plantilla básica a fin de agregar acciones de modo que su entorno de mensajería de Exchange cumpla con sus propios requisitos.



Puede modificar las directivas al editar las reglas dentro de estas una vez que se haya guardado la directiva dentro del entorno de Exchange 2013. Un ejemplo de cambio de regla podría incluir realizar exenciones de personas específicas de una directiva o enviar una notificación y bloquear la entrega de mensajes si se detecta que un mensaje tiene contenido confidencial. Para obtener más información sobre la edición de directivas y reglas, consulte [Administrar directivas de DLP](manage-dlp-policies-exchange-2013-help.md).

Debe navegar hasta el conjunto de reglas de directiva específicas en la página **Editar directiva de DLP** y usar las herramientas disponibles en dicha página para cambiar una directiva de DLP que haya creado previamente en Exchange 2013.

Algunas directivas permiten agregar reglas que invocan RMS para mensajes. Debe tener configurado RMS en el servidor de Exchange antes de agregar las acciones para usar este tipo de reglas.

Para cualquiera de las directivas de DLP, puede cambiar las reglas, las acciones, las excepciones, el periodo de la aplicación o si se aplicarán otras reglas dentro de la directiva y puede agregar sus propias condiciones personalizadas para cada una.

## Más información

[Prevención de pérdida de datos](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Plantillas de directiva de DLP](dlp-policy-templates-exchange-2013-help.md)

