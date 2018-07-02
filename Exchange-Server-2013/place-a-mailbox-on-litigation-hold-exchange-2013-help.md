---
title: 'Poner un buzón en retención por juicio: Exchange 2013 Help'
TOCTitle: Poner un buzón en retención por juicio
ms:assetid: adee4621-3626-4aec-aa53-00b35ff0d0b0
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn743673(v=EXCHG.150)
ms:contentKeyID: 62269034
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Poner un buzón en retención por juicio

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2016-10-18_

Coloque un buzón en retención por juicio para conservar todo el contenido del buzón, incluidos los elementos eliminados y las versiones originales de los elementos modificados. Al colocar el buzón de correo de un usuario en retención por juicio, el contenido del buzón de archivo del usuario (si está habilitado) también se coloca en retención. Los elementos eliminados y modificados se conservan durante un período especificado o hasta que se elimina la retención por juicio del buzón. Todos los elementos del buzón de correo se devuelven en una búsqueda de [Exhibición de documentos electrónicos en contexto](in-place-ediscovery-exchange-2013-help.md).


> [!IMPORTANT]
> La retención por juicio conserva los elementos de la carpeta Elementos recuperables en el buzón del usuario. Según el número y el tamaño de los elementos eliminados o modificados, el tamaño de la carpeta Elementos recuperables del buzón puede aumentar rápidamente. De forma predeterminada, la carpeta Elementos recuperables está configurada con una cuota alta. En Exchange Online, esta cuota se incrementará automáticamente al colocar un buzón en retención por juicio. En Exchange Server 2013, se recomienda supervisar semanalmente los buzones que se colocan en retención por juicio para asegurarse de que no alcanzan los límites de las cuotas de Elementos recuperables.



## ¿Qué debe saber antes de comenzar?

  - Tiempo estimado para finalizar: 5 minutos

  - La configuración de la retención por juicio puede tardar hasta 60 minutos en surtir efecto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el entrada "Conservación local" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Para colocar un buzón de Exchange Online en retención por juicio, este debe tener asignada una licencia de Exchange Online (plan 2). Si un buzón tiene asignada una licencia de Exchange Online (plan 1), deberá asignarle una licencia independiente de Archivado de Exchange Online para aplicarle la conservación.

  - Como se ha explicado anteriormente, cuando se coloca el buzón de un usuario en retención por juicio, el contenido del buzón de archivo del usuario también se coloca en retención. Si coloca un buzón principal local en retención por juicio en una implementación híbrida de Exchange, el buzón de archivo basado en la nube (si está habilitado) también se coloca en retención.

  - En Exchange Online, la cuota para la carpeta Elementos recuperables aumenta automáticamente a 100 GB al colocar un buzón de correo en retención por juicio. El tamaño predeterminado de esta carpeta es de 30 GB.

  - La retención por juicio conserva los elementos eliminados y también conserva las versiones originales de los elementos modificados hasta que se elimine la retención. También puede especificar la duración de una retención para conservar un elemento del buzón durante el período de tiempo especificado. Si especifica el período de duración de una retención, se calcula desde la fecha en que se recibe un mensaje o se crea un elemento del buzón. Para conservar los elementos que cumplen los criterios especificados, use una conservación local para crear una retención *basada en consultas*. Para obtener información detallada, consulte [Crear o quitar una conservación local](create-or-remove-an-in-place-hold-exchange-2013-help.md).

  - Para colocar un buzón de Exchange Online en retención con el Shell, tiene que utilizar Exchange Online PowerShell. Para más información, vea [Conectarse a Exchange Online mediante PowerShell remoto](https://technet.microsoft.com/es-es/library/jj984289\(v=exchg.150\)).

  - No se admite la creación de una retención por juicio en un buzón de carpeta pública. Tendrá que usar la conservación local para crear una retención en las carpetas públicas.

## Usar el EMC para colocar un buzón en retención por juicio

1.  Vaya a **Destinatarios** \> **Buzones de correo**.

2.  En la lista de buzones de usuarios, haga clic en el buzón que quiere colocar en retención por juicio y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades de buzones, haga clic en **Características de buzón**.

4.  En **Retención por juicio: Deshabilitado**, haga clic en **Habilitar** para colocar el buzón en Retención por juicio.

5.  En la página **Retención por juicio**, especifique la siguiente información opcional:
    
      - **Duración de retención por juicio (días):**    Utilice este cuadro para especificar cuánto tiempo se conservarán los elementos del buzón cuando este se ponga en retención por juicio. La duración se calcula desde la fecha en que un elemento de buzón se recibe o se crea. Si deja este cuadro en blanco, los elementos se conservan indefinidamente o hasta que se elimine la retención. Use días para especificar la duración.
    
      - **Nota**   Utilice este cuadro para informar al usuario de que su buzón está en retención por juicio. La nota aparecerá en el buzón del usuario si está usando Outlook 2010 o versiones posteriores.
    
      - **Dirección URL**   Utilice este cuadro para dirigir al usuario a un sitio web con más información acerca de la retención por juicio. Esta dirección URL aparece en el buzón del usuario si está usando Outlook 2010 o versiones posteriores.

6.  Haga clic en **Guardar** en la página **Retención por juicio** y, después, haga clic en **Guardar** en la página de propiedades del buzón.

Volver al principio

## Usar el Shell para colocar un buzón en retención por juicio indefinidamente

En este ejemplo, se coloca el buzón bsuneja@contoso.com en retención por juicio. Los elementos del buzón se conservan indefinidamente o hasta que se elimine la retención.

    Set-Mailbox bsuneja@contoso.com -LitigationHoldEnabled $true


> [!NOTE]
> Al colocar un buzón en retención por juicio indefinidamente (sin especificar una duración), el valor de la propiedad <EM>LitigationHoldDuration</EM> del buzón se establece en <CODE>Unlimited</CODE>.



## Usar el Shell para colocar un buzón en retención por juicio y conservar los elementos durante un tiempo especificado

Este ejemplo coloca el buzón bsuneja@contoso.com en retención por juicio y conserva los elementos durante 2555 días (aproximadamente 7 años).

    Set-Mailbox bsuneja@contoso.com -LitigationHoldEnabled $true -LitigationHoldDuration 2555

## Usar el Shell para colocar todos los buzones en retención por juicio durante un tiempo especificado

Su organización puede necesitar que los datos de todos los buzones se conserven durante un período determinado. Antes de colocar todos los buzones de una organización en retención por juicio, tenga en cuenta lo siguiente:

En este ejemplo todos los buzones de usuario de la organización se colocan en retención por juicio durante un año (365 días).

    Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -eq "UserMailbox"} | Set-Mailbox -LitigationHoldEnabled $true -LitigationHoldDuration 365

El ejemplo usa el cmdlet [Get-Mailbox](https://technet.microsoft.com/es-es/library/bb123685\(v=exchg.150\)) para recuperar todos los buzones de la organización, especifica un filtro de destinatarios para incluir todos los buzones de usuario y, después, canaliza la lista de buzones al cmdlet [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)) para habilitar la retención por juicio y la duración de la retención.

Para colocar todos los buzones de usuario en una retención indefinida, ejecute el comando anterior pero no incluya el parámetro *LitigationHoldDuration*.

Consulte la sección Más información para ver ejemplos de cómo usar otras propiedades de destinatarios en un filtro para incluir o excluir uno o más buzones.

## Usar el Shell para quitar un buzón de la retención por juicio

En este ejemplo, se quita el buzón de correo bsuneja@contoso.com de la retención por juicio.

    Set-Mailbox bsuneja@contoso.com -LitigationHoldEnabled $false

Volver al principio

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que un buzón se ha colocado correctamente en retención por juicio, realice unas de estas acciones:

  - En el EAC:
    
    1.  Vaya a **Destinatarios** \> **Buzones de correo**.
    
    2.  En la lista de buzones de usuario, haga clic en el buzón cuya configuración de retención por juicio quiere comprobar y, después, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").
    
    3.  En la página de propiedades de buzones, haga clic en **Características de buzón**.
    
    4.  En **Retención por juicio**, compruebe que la retención está habilitada.
    
    5.  Haga clic en **Ver detalles** para comprobar cuándo se colocó el buzón en retención por juicio y quién lo hizo. También puede comprobar o cambiar los valores de las casillas opcionales **Duración de retención por juicio (días)**, **Nota** y **Dirección URL**.

  - En el Shell, ejecute uno de los siguientes comandos:
    
        Get-Mailbox <name of mailbox> | FL LitigationHold*
    
    o
    
        Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -eq "UserMailbox"} | FL Name,LitigationHold*
    
    Si un buzón se coloca en retención por juicio indefinidamente, el valor de la propiedad del buzón *LitigationHoldDuration* se establece en `Unlimited`.

## Más información

  - Si su organización requiere que los datos de todos los buzones se conserven durante un período de tiempo específico, considere lo siguiente antes de poner todos los buzones de una organización en retención por juicio.
    
      - Cuando se usa el comando anterior para aplicar una retención a todos los buzones de una organización (o a un subconjunto de buzones que coinciden con un filtro de destinatarios especificado), solo se retienen los buzones que existen en el momento en que se ejecuta el comando. Si crea nuevos buzones más adelante, tiene que ejecutar el comando de nuevo para poner los nuevos buzones en retención. Si crea nuevos buzones con frecuencia, puede ejecutar el comando como una tarea programada con la frecuencia que necesite.
    
      - Poner todos los buzones en retención por juicio puede afectar significativamente al tamaño de los buzones. En una organización de Exchange Server 2013, planee el almacenamiento adecuado para satisfacer los requisitos de conservación de su organización.
    
      - La carpeta Elementos recuperables tiene su propio límite de almacenamiento, por lo que los elementos de la carpeta no cuentan para el límite de almacenamiento del buzón. Como se explicó anteriormente, conservar los datos de buzón durante mucho tiempo dará lugar al crecimiento de la carpeta Elementos recuperables en el buzón y el archivo de un usuario. Para aceptar este crecimiento en Exchange Online, la cuota para la carpeta Elementos recuperables aumenta automáticamente de 30 GB a 100 GB al colocar un buzón de correo en retención por juicio.
        
        En Exchange Server 2013, el límite de almacenamiento predeterminado para la carpeta Elementos recuperables también es de 30 GB. Se recomienda supervisar periódicamente el tamaño de esta carpeta para asegurarse de que no llegue al límite. Para obtener más información, consulte [Carpeta Elementos recuperables](recoverable-items-folder-exchange-2013-help.md).

  - El comando anterior para colocar una retención en todos los buzones utiliza un filtro de destinatarios que devuelve todos los buzones de usuario. Puede usar otras propiedades de destinatarios para devolver una lista de buzones específicos que puede canalizar después al cmdlet **Set-Mailbox** para poner esos buzones en retención por juicio.
    
    Estos son algunos ejemplos de cómo usar los cmdlets **Get-Mailbox** y **Get-Recipient** para obtener un subconjunto de buzones en función de propiedades de usuarios o buzones. En estos ejemplos se da por hecho que las propiedades de buzón relevantes (como *CustomAttributeN* o *Department*) se han rellenado.
    
        Get-Mailbox -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'CustomAttribute15 -eq "OneYearLitigationHold"'
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'Department -eq "HR"'
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'PostalCode -eq "98052"'
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'StateOrProvince -eq "WA"'
    
        Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -ne "DiscoveryMailbox"}
    
    Puede usar otras propiedades de buzón de usuario en un filtro para incluir o excluir buzones de correo. Para obtener información detallada, consulte [Propiedades a las que se puede aplicar un filtro para el parámetro -Filter](https://technet.microsoft.com/es-es/library/bb738155\(v=exchg.150\)).

Volver al principio

