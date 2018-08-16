---
title: 'Modificar una búsqueda de eDiscovery local: Exchange 2013 Help'
TOCTitle: Modificar una búsqueda de exhibición de documentos electrónicos local
ms:assetid: 3162743c-cc12-4997-91e0-bcbfea8bcb17
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd335182(v=EXCHG.150)
ms:contentKeyID: 49895555
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modificar una búsqueda de exhibición de documentos electrónicos local

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-08-27_

Después de crear una búsqueda de Exhibición de documentos electrónicos en contexto, puede modificarla para cambiar los parámetros de la búsqueda. Por ejemplo, puede modificar los buzones de correo en los que buscar, los intervalos de fechas, las palabras clave y las opciones de registro, o puede especificar otro buzón de detección para almacenar resultados de búsqueda. Los cambios efectuados en las propiedades de la búsqueda se usarán al reanudar la búsqueda.


> [!WARNING]
> Si hay una búsqueda de Exhibición de documentos electrónicos en contexto ejecutándose, debe pararla antes de modificarla. Cuando reinicia la búsqueda, los resultados de la última vez en que se realizó la búsqueda se eliminan del buzón de detección. Sin embargo, los registros de las búsquedas anteriores se guardan.



## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 2-5 minutos.

  - Se ha creado una búsqueda de Exhibición de documentos electrónicos en contexto y no se está ejecutando.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Exhibición de documentos electrónicos en contexto" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## ¿Qué desea hacer?

## Usar el EAC para modificar una búsqueda de Exhibición de documentos electrónicos en contexto

1.  Vaya a **Administración del cumplimiento** \> **Conservación local y exhibición de documentos electrónicos en contexto**.

2.  En la vista de lista, seleccione la búsqueda de Exhibición de documentos electrónicos en contexto que quiera modificar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En **Conservación local y exhibición de documentos electrónicos en contexto**, puede modificar la siguiente configuración:
    
      - En la página **Nombre**, modifique el nombre de la búsqueda y la descripción opcional.
    
      - En la página **Buzones de correo**, modifique los buzones de correo en los que buscar. Puede buscar en todos los buzones o seleccionar buzones específicos para la búsqueda.
        

        > [!IMPORTANT]
        > No se puede usar la opción <STRONG>Buscar en todos los buzones</STRONG> para retener todos los buzones de los servidores de buzones de Exchange&nbsp;2013. Para crear una Conservación local, seleccione <STRONG>Especificar buzones en los que buscar</STRONG>. Para obtener más información, consulte <A href="create-or-remove-an-in-place-hold-exchange-2013-help.md">Crear o quitar una conservación local</A>.

    
      - En la página **Consulta de búsqueda**, modifique los campos siguientes:
        
          - **Incluir todo el contenido del buzón de correo del usuario**   Seleccione esta opción para retener todo el contenido de los buzones seleccionados.
        
          - **Filtrado basado en criterios**   Seleccione esta opción para especificar los criterios de búsqueda, incluyendo palabras clave, fechas de inicio y finalización, direcciones de remitente y destinatario, y tipos de mensaje.
    
      - En la página **Conservación local**, active la casilla **Pausar el contenido que coincida con la consulta de búsqueda en los buzones seleccionados** y seleccione una de las siguientes opciones para colocar elementos en Conservación local:
        
          - **Retener indefinidamente**   Seleccione esta opción para retener indefinidamente los elementos devueltos. Los elementos en espera se conservarán hasta que quite el buzón de correo de la búsqueda o la búsqueda.
        
          - **Especificar el número de días que se retendrán elementos con relación a su fecha de recepción** Use esta opción para retener elementos durante un período específico. Por ejemplo, puede usar esta opción si su organización necesita que todos los mensajes se conserven durante un mínimo de siete años. Puede usar una Conservación local *basada en tiempo* con una directiva de retención para asegurarse de que los elementos se eliminen a los siete años.
            

            > [!IMPORTANT]
            > Al colocar buzones o elementos en "Retención en contexto" por propósitos legales, normalmente se recomienda retener elementos de forma indefinida y eliminar la retención una vez completado el caso o la investigación.



4.  Haga clic en **Guardar**.

## Usar el Shell para modificar una búsqueda de Exhibición de documentos electrónicos en contexto

En este ejemplo se modifica la búsqueda de Exhibición de documentos electrónicos en contexto "Search-Project Contoso" para que se busque en buzones de correo que pertenezcan a los miembros del grupo de distribución "DG-ProjectManagers".

    Set-MailboxSearch -Identity "Search-Project Contoso" -SourceMailboxes "DG-ProjectManagers"

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si ha modificado correctamente una búsqueda de Exhibición de documentos electrónicos en contexto, siga uno de estos pasos:

  - Use el EAC para comprobar las propiedades de la búsqueda.

  - Use el cmdlet **Get-MailboxSearch** del Shell para comprobar las propiedades de la búsqueda. Para consultar ejemplos de cómo comprobar las propiedades de una búsqueda de buzones de correo, vea la sección "Ejemplos" de [Get-MailboxSearch](https://technet.microsoft.com/es-es/library/dd351021\(v=exchg.150\)).


> [!NOTE]
> Si usa <STRONG>Get-MailboxSearch</STRONG> en Exchange Online para recuperar información sobre una búsqueda de exhibición de documentos electrónicos, debe especificar el nombre de una búsqueda para devolver una lista completa de las propiedades de búsqueda; por ejemplo, <CODE>Get-MailboxSearch "Contoso Legal Case"</CODE>. Si ejecuta el cmdlet <STRONG>Get-MailboxSearch</STRONG> sin usar parámetros, no se devuelven las siguientes propiedades: 
> <UL>
> <LI>
> <P>SourceMailboxes</P>
> <LI>
> <P>Fuentes</P>
> <LI>
> <P>SearchQuery</P>
> <LI>
> <P>ResultsLink</P>
> <LI>
> <P>PreviewResultsLink</P>
> <LI>
> <P>Errores</P></LI></UL>El motivo es que requiere muchos recursos para devolver estas propiedades para todas las búsquedas de exhibición de documentos electrónicos en su organización.


