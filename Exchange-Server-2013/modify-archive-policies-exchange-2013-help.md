---
title: 'Modificar las directivas de archivo: Exchange 2013 Help'
TOCTitle: Modificar las directivas de archivo
ms:assetid: 1e3002c2-801a-43ea-ae00-52ab34d76b9c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Hh529919(v=EXCHG.150)
ms:contentKeyID: 49895508
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Modificar las directivas de archivo

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2016-02-01_

En Exchange Server 2013 y Exchange Online, puede usar directivas de archivo para mover automáticamente los elementos de los buzones a archivos personales (locales) o basados en la nube. Las directivas de archivo son etiquetas de retención que usan la acción de retención **Mover a archivo**.

La instalación de Exchange crea una directiva de retención denominada **Directiva de MRM predeterminada**. Esta directiva tiene asignada una etiqueta de directiva predeterminada (DPT) que mueve los elementos al buzón de archivo después de dos años. La directiva también incluye una cantidad de etiquetas personales que los usuarios pueden aplicar a elementos de carpetas o buzones para mover o eliminar mensajes automáticamente. Si un buzón no tiene una directiva de retención asignada cuando se habilita el archivo, Exchange aplica automáticamente la **Directiva de MRM predeterminada**. También puede crear sus propias directivas de retención y archivo y aplicarlas a los usuarios de buzón. Para obtener más información, consulte [Etiquetas de retención y directivas de retención](retention-tags-and-retention-policies-exchange-2013-help.md).

Puede modificar las etiquetas de retención incluidas en la directiva predeterminada para satisfacer sus requisitos comerciales. Por ejemplo, puede modificar el DPT de archivo para mover elementos al archivo después de tres años, en lugar de dos. También puede crear etiquetas personales adicionales y agregarlas a una directiva de retención, incluida la **Directiva de MRM predeterminada**, o permitir a los usuarios agregar etiquetas personales a sus buzones de correo desde las opciones de Outlook Web App.

Para ver otras tareas de administración relacionadas con los archivos, consulte:

  - **Exchange Server 2013:** [Administrar archivos locales en Exchange 2013](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md)

  - **Exchange Online:** [Habilitar o deshabilitar un buzón de archivo en Exchange Online](https://technet.microsoft.com/es-es/library/jj984357\(v=exchg.150\))


> [!NOTE]
> En una implementación híbrida de Exchange, puede habilitar un buzón de archivo basado en la nube para un buzón principal local. Si asigna una directiva de archivo a un buzón local, los elementos se mueven al archivo basado en la nube. Si un elemento se mueve al buzón de archivo, no se conserva una copia del elemento en el buzón local. Si el buzón local se coloca en retención, una directiva de archivo moverá igualmente los elementos al buzón de archivo basado en la nube, donde se conservarán durante el tiempo especificado por la retención.



## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Administración de registros de mensajes" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Usar el EAC para modificar la directiva de archivo predeterminada

1.  Vaya a **Administración de cumplimiento** y a \> **Etiquetas de retención**.

2.  En la vista de lista, seleccione la etiqueta **Mover al archivo después de 2 años predeterminado** y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").
    

    > [!TIP]
    > Puede hacer clic en la columna <STRONG>TIPO</STRONG> para clasificar las etiquetas de retención por tipo. La directiva de archivo predeterminada se muestra como tipo <STRONG>Predeterminado</STRONG> y tiene la acción de retención <STRONG>Archivo</STRONG>. Como alternativa, haga clic en <STRONG>NOMBRE</STRONG> para clasificar las etiquetas de retención por nombre.



3.  
    
    En **Etiqueta de retención**, vea o modifique las siguientes configuraciones y, a continuación, haga clic en **Guardar**:
    
      - **Nombre**   Use este cuadro situado en la parte superior de la página para ver o cambiar el nombre de la etiqueta.
    
      - **Tipo de etiqueta de retención**   Este campo de sólo lectura muestra el tipo de etiqueta.
    
      - **Acción de retención**   No modifique este campo de directivas de archivo.
    
      - **Período de retención** Seleccione una de las opciones siguientes:
        
          - **Nunca**   Haga clic en este botón para deshabilitar la etiqueta. Si se deshabilita la DPT, la etiqueta no se aplicará al buzón.
            

            > [!IMPORTANT]
            > El asistente de buzones no procesa los elementos que tienen aplicada una etiqueta de retención deshabilitada. Si quiere evitar que se aplique una determinada etiqueta a los elementos, le recomendamos que deshabilite la etiqueta en lugar de eliminarla. Al eliminar una etiqueta, la configuración de la etiqueta se elimina de Active Directory y el asistente de buzones procesa todos los mensajes para quitar la etiqueta eliminada.

            

            > [!NOTE]
            > Si un usuario aplica una etiqueta a un elemento porque cree que el elemento nunca se moverá, si se habilita la etiqueta más adelante, es posible que se muevan los elementos que el usuario quería conservar en el buzón principal.

        
          - **Cuando el elemento alcanza la siguiente antigüedad (en días)**   Haga clic en este botón para mover a un archivo después de un cierto período. De manera predeterminada, se establece esta configuración para mover los elementos al archivo después de dos años (730 días). Para modificar esta configuración, en el cuadro de texto que corresponda, escriba el número de días del período de retención. Los valores oscilan entre 1 y 24.855 días.
    
      - **Comentario**   Use este cuadro para escribir el comentario que se mostrará a los usuarios de Outlook y Outlook Web App.

## Usar el Shell para modificar las directivas de archivo

Este ejemplo modifica la etiqueta `Default 2 year move to archive` para mover los elementos después de 1095 días (3 años).

    Set-RetentionPolicyTag "Default 2 year move to archive" -Name "Default 3 year move to archive" -AgeLimitForRetention 1095

En este ejemplo, se deshabilita la etiqueta `Default 2 year move to archive`.

    Set-RetentionPolicyTag "Default 2 year move to archive" -RetentionEnabled $false

Este ejemplo recupera todos las DPT de archivo y las etiquetas personales y las deshabilita.

    Get-RetentionPolicyTag | ? {$_.RetentionAction -eq "MoveToArchive"} | Set-RetentionPolicyTag -RetentionEnabled $false

Para obtener más información acerca de la sintaxis y los parámetros, consulte [Set-RetentionPolicyTag](https://technet.microsoft.com/es-es/library/dd298042\(v=exchg.150\)) y [Get-RetentionPolicyTag](https://technet.microsoft.com/es-es/library/dd298009\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Use el cmdlet [Get-RetentionPolicyTag](https://technet.microsoft.com/es-es/library/dd298009\(v=exchg.150\)) para recuperar la configuración de la etiqueta de retención.

Este comando recupera las propiedades de la etiqueta de retención `Default 2 year move to archive` y canaliza los resultados al cmdlet **Format-List** para mostrar todas las propiedades en un formato de lista.

    Get-RetentionPolicyTag "Default 2 year move to archive" | Format-List

