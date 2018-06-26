---
title: 'Personalizar las plantillas de detalles: Exchange 2013 Help'
TOCTitle: Personalizar las plantillas de detalles
ms:assetid: b4beeedd-e46f-442e-844a-e8575f95dca0
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.toolbox.detailstemplate(v=EXCHG.150)
ms:contentKeyID: 49116470
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Personalizar las plantillas de detalles

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2012-09-25_

Use el editor de plantilla de detalles para personalizar la presentación de la interfaz gráfica de usuario (GUI) de cliente de las propiedades de un objeto a las que se tiene acceso mediante las listas de direcciones de MicrosoftOutlook. Por ejemplo, cuando un usuario abre una lista de direcciones en Outlook, se presentan las propiedades de un determinado objeto según se define en la plantilla de detalles de la organización de Exchange. Es posible personalizar los objetos cambiando los tamaños del campo, agregando o quitando campos, agregando o quitando pestañas o reorganizando campos. El diseño de estas plantillas puede variar según el idioma.

## ¿Qué necesita saber antes de comenzar?

  - No existe la opción de deshacer en el editor de plantillas de detalles. Si comete un error, deberá volver a la versión anterior. Para obtener más información, consulte [Restaurar la configuración predeterminada de una plantilla de detalles](restore-a-details-template-to-the-default-configuration-exchange-2013-help.md).

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Plantillas de detalles" en el tema [Permisos de libreta de direcciones y dirección de correo electrónico](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Personalización de las plantillas de detalles

1.  En el **Cuadro de herramientas de Exchange** , haga clic en el **Editor de plantillas de detalles**, y en el panel de acciones, haga clic en **Abrir herramienta**.

2.  En el árbol de la consola del Editor de plantillas de detalles, haga clic en **Plantillas de detalles**.
    
    En el panel de detalles, se muestran las columnas siguientes:
    
      - **Idioma** Esta columna incluye el idioma en que se creó la plantilla.
    
      - **Tipo de plantilla** Esta columna incluye el tipo de plantilla que se puede personalizar.
    
      - **Identidad** Esta columna incluye la identidad única de la plantilla.
    
      - **Creación** Esta columna incluye la fecha y la hora de creación de la plantilla.
    
      - **Modificación** Esta columna incluye la fecha y hora de la última modificación de la plantilla.

3.  Para editar una plantilla, haga clic en la plantilla que desee y, a continuación, en el panel de acciones, haga clic en **Editar** Por ejemplo, la plantilla de detalles de contactos **Inglés (Estados Unidos)** se muestra en la figura siguiente.
    
    **Plantilla de detalles predeterminada al verla desde Outlook 2013**
    
    ![Plantilla de detalles predeterminada de Outlook 2007](images/JJ673049.a0af8aca-663d-4702-ab2f-9a342f481cdf(EXCHG.150).gif "Plantilla de detalles predeterminada de Outlook 2007")  

4.  Después de hacer clic en **Editar**, puede realizar varias tareas para personalizar una plantilla de detalles:
    
      - Para mover un objeto en el panel del diseñador, seleccione el objeto y arrástrelo a una nueva ubicación en la plantilla. Cuando mueva el objeto, verá las líneas de alineación.
    
      - Para cambiar el texto de una etiqueta, seleccione la etiqueta en el panel de diseño. En el panel de propiedades, escriba el nuevo texto en el cuadro **Texto**. Para crear métodos abreviados de teclado, puede usar el símbolo "y" comercial (&). Coloque el símbolo "y" comercial (&) antes de la letra que desea usar como método abreviado.
    
      - Para cambiar el tamaño de un objeto, seleccione el objeto y, a continuación, arrastre los controladores de tamaño hasta que el objeto tenga la forma y el tamaño deseados.
    
      - Para eliminar un objeto, seleccione el objeto y, a continuación, presione la tecla SUPR.
        

        > [!NOTE]
        > El Editor de plantillas de detalles no contiene un botón <STRONG>Deshacer</STRONG> ni le permite usar un método abreviado de teclado para deshacer una acción. Para deshacer una adición realizada a la plantilla, debe usar la tecla SUPR. Para deshacer una eliminación, debe volver a aplicar el ajuste. También es posible volver a la configuración original saliendo del Editor de plantillas de detalles sin guardar los cambios. Si desea deshacer los cambios una vez guardados, puede restaurar la plantilla. Al restaurar una plantilla, se pierden todas las personalizaciones y se restaura la configuración original de la plantilla. Para obtener más información acerca de cómo restaurar la plantilla de detalles, consulte <A href="restore-a-details-template-to-the-default-configuration-exchange-2013-help.md">Restaurar la configuración predeterminada de una plantilla de detalles</A>.

    
      - Para agregar un cuadro de texto Editar, listas de selección, cuadros desplegables con varios valores o cuadros de lista con varios valores, arrastre el objeto del panel de cuadro de herramientas al panel de diseño. Para establecer el atributo del objeto, haga clic en el cuadro desplegable de atributos del panel de propiedades y, a continuación, seleccione el atributo que usará Exchange.
        

        > [!NOTE]
        > Deberá vincular el objeto a un atributo para que lo use Exchange. Además, el atributo determina el contenido que se mostrará al usuario final en Outlook. Si no selecciona ningún atributo, se seleccionará automáticamente un atributo al azar.

    
      - Para agregar un cuadro de grupo, arrastre el objeto al panel de diseño. A continuación, en el panel de propiedades, escriba el nombre en el cuadro **Texto**. Use los cuadros de grupos para agrupar objetos similares.
    
      - Para agregar un tabulador a la plantilla, haga clic con el botón derecho en un tabulador existente y, a continuación, haga clic en **Agregar tabulador**. Aparecerá un tabulador en blanco. Para dar un nombre al tabulador, escriba el nombre en el cuadro **Texto** del panel de propiedades.
    
      - Para quitar un tabulador de la plantilla, haga clic en él con el botón derecho y, a continuación, haga clic en **Quitar tabulador**. Aparecerá una advertencia. Haga clic en **Aceptar** para confirmar que desea quitar el tabulador.
    
      - Para cambiar el orden de tabulación de los objetos de un tabulador de forma que los usuarios puedan usar la tecla TAB para ir a los objetos en el orden que deseen, seleccione el objeto en el panel de diseño. En el panel de propiedades, use el cuadro **TabIndex** para cambiar el orden.
        

        > [!NOTE]
        > Para garantizar que los usuarios no puedan usar la tecla TAB para obtener acceso a las etiquetas de un objeto (por ejemplo <STRONG>Nombre</STRONG> o <STRONG>Alias</STRONG>), cambie el orden de las etiquetas para que aparezcan al final en el orden de tabulación.



5.  Para guardar los cambios en la plantilla de detalles, en el menú **Archivo**, haga clic en **Guardar**.

6.  Para cerrar la plantilla, en el menú **Archivo**, haga clic en **Salir**.

