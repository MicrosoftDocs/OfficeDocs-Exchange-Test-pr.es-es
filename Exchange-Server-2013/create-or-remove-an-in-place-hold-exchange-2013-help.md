---
title: 'Crear o quitar una conservación local: Exchange 2013 Help'
TOCTitle: Crear o quitar una conservación local
ms:assetid: 9d5d8d37-a053-4830-9cb1-6e1ede25e963
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd979797(v=EXCHG.150)
ms:contentKeyID: 48268484
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Crear o quitar una conservación local

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2017-01-18_


> [!NOTE]
> Hemos pospuesto la fecha límite del 1 de julio de 2017 para crear nuevas conservaciones locales en Exchange Online (en los planes independientes de Office 365 y Exchange Online). Pero más tarde este año o a principios del año que viene no podrá crear nuevas conservaciones locales en Exchange Online. Como alternativa al uso de conservaciones locales, puede usar <A href="https://go.microsoft.com/fwlink/?linkid=780738">casos de eDiscovery</A> o <A href="https://go.microsoft.com/fwlink/?linkid=827811">directivas de retención</A> en el Centro de seguridad y cumplimiento de Office 365. Después de retirar las nuevas conservaciones locales, podrá seguir modificando las conservaciones locales existentes y se admitirá la creación de conservaciones locales en las implementaciones híbridas de Exchange Server 2013 y de Exchange. También podrá seguir colocando los buzones de correo en retención por juicio.



Una conservación local conserva todo el contenido de un buzón de correo, incluidos los elementos eliminados y las versiones originales de los elementos modificados. Todos esos elementos del buzón de correo se devuelven en una búsqueda de [Exhibición de documentos electrónicos en contexto](in-place-ediscovery-exchange-2013-help.md). Al colocar el buzón de un usuario en conservación local, el contenido del buzón de archivo correspondiente (si está habilitado) también se coloca en conservación local y se devuelve en una búsqueda de exhibición de documentos electrónicos.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la Entrada "Conservación local" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Para colocar un buzón de Exchange Online en conservación local, este debe tener asignada una licencia de Exchange Online (plan 2). Si un buzón tiene asignada una licencia de Exchange Online (plan 1), deberá asignarle una licencia independiente de Archivado de Exchange Online para aplicarle la conservación.

  - En función de la topología y la latencia de replicación de Active Directory, aplicar una Conservación local puede tardar hasta una hora.

  - Como se ha explicado anteriormente, cuando se coloca el buzón de un usuario en conservación local, el contenido del buzón de archivo del usuario también se coloca en conservación. Si coloca un buzón principal local en conservación en una implementación híbrida de Exchange, el buzón de archivo basado en la nube (si está habilitado) también se coloca en conservación.

  - Si un usuario se encuentra en varias conservaciones locales, se combinan las consultas de búsqueda de cualquier conservación basada en consultas (con operadores **OR**). En este caso, el número máximo de palabras clave en todas las conservaciones basadas en consulta de un buzón es de 500. Si hay más de 500 palabras clave, todo el contenido del buzón se coloca en conservación (y no solo el contenido que coincide con los criterios de búsqueda). Todo el contenido se conserva hasta que el número total de palabras clave es de 500 o menos.

  - En Exchange Online, la cuota para la carpeta Elementos recuperables aumenta automáticamente a 100 GB al colocar un buzón de correo en conservación local. El tamaño predeterminado de la carpeta Elementos recuperables es de 30 GB.

  - En Exchange Online puede poner grupos de Office 365 en conservación local. Cuando un grupo de Office 365 se pone en conservación local, también su buzón se pone en conservación local; por el contrario, los buzones de los miembros del grupo no se ponen en conservación local. Para obtener información sobre los grupos de Office 365, consulte [Obtenga más información sobre los grupos de Office 365](https://go.microsoft.com/fwlink/p/?linkid=724066).

## Crear una Conservación local

**Usar el EAC para crear una Conservación local**

1.  Desplácese a **Administración del cumplimiento** \> **Conservación y exhibición de documentos electrónicos en contexto**.

2.  Haga clic en **Nueva**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

3.  En **Conservación y exhibición de documentos electrónicos en contexto**, en la página **Nombre y descripción**, escriba un nombre para la búsqueda y una descripción opcional, y, a continuación, haga clic en **Siguiente**.

4.  En la página **Buzones y carpetas públicas**, elija las ubicaciones del contenido que desee colocar en espera y, a continuación, haga clic en **Siguiente**.
    
    ![Elegir las ubicaciones de contenido para colocar en suspensión](images/Dd979797.bbe76c50-a93b-4e5e-acd2-78e0d747ea19(EXCHG.150).png "Elegir las ubicaciones de contenido para colocar en suspensión")  
    
    1.  **Buscar en todos los buzones de correo**   No puede seleccionar esta opción para crear una conservación local. Puede seleccionar esta opción para las búsquedas de eDiscovery locales. Sin embargo, para crear una conservación local, deberá seleccionar los buzones de correo específicos que desee colocar en espera.
    
    2.  **No buscar en ningún buzón de correo**   Seleccione esta opción cuando esté creando una conservación local exclusivamente para carpetas públicas.
    
    3.  **Especificar buzones para buscar**   Seleccione esta opción y, a continuación, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para seleccionar los buzones de correo o los grupos de distribución que desee colocar en espera. En Exchange Online, también puede seleccionar grupos de Office 365 para colocarlos en espera.
    
    4.  **Buscar en todas las carpetas públicas**   En Exchange Online, puede seleccionar esta casilla para colocar todas las carpetas públicas de la organización en espera. Como se ha explicado anteriormente, para crear una conservación local únicamente para carpetas públicas, asegúrese de seleccionar la opción **No buscar en ningún buzón de correo**.

5.  En la página **Consulta de búsqueda**, rellene los siguientes campos y, a continuación, pulse en **Siguiente**:
    
      - **Incluir todo el contenido del buzón del usuario**   Haga clic en este botón para poner en espera todo el contenido de los buzones de correo que seleccione.
    
      - **Filtros basados en criterios**: haga clic en este botón para especificar los criterios de búsqueda, incluidas las palabras clave, las fechas de inicio y de finalización, las direcciones del remitente y del destinatario y los tipos de mensaje. Al crear una conservación basada en consulta, solo se conservarán los elementos que coincidan con los criterios de búsqueda.
        

        > [!TIP]
        > Al colocar carpetas públicas en un conservación local, también se conservarán los mensajes de correo electrónico relacionados con el proceso de sincronización de la jerarquía de carpetas públicas. Esto puede dar lugar a la conservación de miles de elementos de correo electrónico relacionados con la sincronización de la jerarquía. Estos mensajes pueden llenar la cuota de almacenamiento de la carpeta Elementos recuperables de los buzones de correo de las carpetas públicas. Para evitar esto, puede crear una conservación local basada en consulta y agregar el siguiente par de <CODE>property:value</CODE> a la consulta de búsqueda:<BR><CODE>NOT(subject:HierarchySync*)</CODE><BR>El resultado es que no se pondrá en espera ningún mensaje (relacionado con la sincronización de la jerarquía de carpetas públicas) que contenga la frase "HierarchySync" en la línea de asunto.



6.  En la página **Configuración de Conservación local**, seleccione la casilla de verificación **Pausar el contenido que coincida con la consulta de búsqueda en los buzones seleccionados** y, a continuación, seleccione una de las siguientes opciones:
    
      - **Retenido indefinidamente**   Pulse este botón para retener de manera indefinida los elementos que devuelva la búsqueda. Los elementos en espera se conservarán hasta que quite la búsqueda o quite el buzón de correo de la búsqueda.
    
      - **Especifique el número de días que se retendrán elementos en relación a su fecha de recepción**   Use este botón para conservar elementos durante un período específico. Por ejemplo, puede usar esta opción si su organización necesita que todos los mensajes se conserven durante un mínimo de siete años. Puede usar una Conservación local *basada en tiempo* junto con una directiva de retención para asegurarse de que los elementos se eliminan en siete años. Para obtener más información sobre las directivas de retención, consulte [Etiquetas de retención y directivas de retención](retention-tags-and-retention-policies-exchange-2013-help.md).

**Usar el Shell para crear una Conservación local**

En este ejemplo se crea una Conservación local con el nombre de Hold-CaseId012 y se agrega el buzón joe@contoso.com a la conservación.


> [!IMPORTANT]
> Si no especifica parámetros de búsqueda adicionales para una Conservación local, todos los elementos de los buzones de correo de origen especificados se colocan en espera. Si no especifica el parámetro <EM>ItemHoldPeriod</EM>, los elementos se colocarán en espera de forma indefinida o hasta que el buzón sea quitado de la retención o la retención se elimine.



    New-MailboxSearch "Hold-CaseId012"-SourceMailboxes "joe@contoso.com" -InPlaceHoldEnabled $true

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-MailboxSearch](https://technet.microsoft.com/es-es/library/dd298064\(v=exchg.150\)).

**¿Cómo saber si el proceso se ha completado correctamente?**

Para comprobar si ha creado una Conservación local correctamente, siga uno de estos procedimientos:

  - Use el EAC para comprobar que la Conservación local aparece en la vista de lista de la pestaña **Conservación y exhibición de documentos electrónicos en contexto**.

  - Use el cmdlet **Get-MailboxSearch** para recuperar la búsqueda de buzón de correo y compruebe los parámetros de búsqueda. Para ver un ejemplo de cómo recuperar una búsqueda de buzón, consulte los ejemplos de [Get-MailboxSearch](https://technet.microsoft.com/es-es/library/dd351021\(v=exchg.150\)).

Volver al principio

## Quitar una Conservación local


> [!IMPORTANT]
> En Exchange&nbsp;2013, las búsquedas de buzón pueden utilizarse para crear una Conservación local y una Exhibición de documentos electrónicos en contexto. No se puede quitar una búsqueda de buzón de correo que se utiliza para una Conservación local. Antes deberá desactivar la Conservación local desmarcando la casilla de verificación <STRONG>Pausar el contenido que coincida con la consulta de búsqueda en los buzones seleccionados</STRONG> en la página <STRONG>Configuración de Conservación local</STRONG> o configurando el parámetro <EM>InPlaceHoldEnabled</EM> a <CODE>$false</CODE> en el Shell. También puede eliminar un buzón usando el parámetro <EM>SourceMailboxes</EM> especificado en la búsqueda.



**Usar el EAC para quitar una Conservación local**

1.  Navegue a **Administración de cumplimiento** \> **Conservación y exhibición de documentos electrónicos en contexto**.

2.  En la vista de lista, seleccione la Conservación local que desea eliminar y, a continuación, pulse **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En propiedades de **Conservación y exhibición de documentos electrónicos en contexto**, en la página **Conservación local**, desmarque **Usar el contenido que coincida con la consulta de búsqueda en los buzones seleccionados**, y, a continuación, pulse en **Guardar**.

4.  Vuelva a seleccionar la Conservación local desde la vista de lista, y, a continuación, haga clic en **Eliminar**![Eliminar icono](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Eliminar icono").

5.  En la advertencia, haga clic en **Sí** para eliminar la búsqueda.

**Usar el Shell para quitar una Conservación local**

Este ejemplo deshabilita en primer lugar la Conservación local llamada Hold-CaseId012 y, a continuación, quita la búsqueda de buzón.

    Set-MailboxSearch "Hold-CaseId012"  -InPlaceHoldEnabled $false
    Remove-MailboxSearch "Hold-CaseId012"

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-MailboxSearch](https://technet.microsoft.com/es-es/library/dd335145\(v=exchg.150\)).

**¿Cómo saber si el proceso se ha completado correctamente?**

Para comprobar si ha eliminado una Conservación local correctamente, siga uno de estos procedimientos:

  - Use el EAC para comprobar que la Conservación local no aparece en la vista de lista de la pestaña **Conservación y exhibición de documentos electrónicos en contexto**.

  - Use el cmdlet **Get-MailboxSearch** para recuperar todas las búsquedas de buzón de correo y compruebe que la búsqueda que ha quitado ya no aparece en la lista. Para ver un ejemplo de cómo recuperar una búsqueda de buzón, consulte los ejemplos de [Get-MailboxSearch](https://technet.microsoft.com/es-es/library/dd351021\(v=exchg.150\)).

Volver al principio

