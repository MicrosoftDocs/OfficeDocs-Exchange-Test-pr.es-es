---
title: 'Poner todos los buzones en retención: Exchange 2013 Help'
TOCTitle: Poner todos los buzones en retención
ms:assetid: 4c141604-3210-44cc-b98e-f3e0f15613b8
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn767952(v=EXCHG.150)
ms:contentKeyID: 62486288
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Poner todos los buzones en retención

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2017-01-18_


> [!NOTE]
> Hemos pospuesto la fecha límite del 1 de julio de 2017 para crear nuevas conservaciones locales en Exchange Online (en los planes independientes de Office 365 y Exchange Online). Pero más tarde este año o a principios del año que viene no podrá crear nuevas conservaciones locales en Exchange Online. Como alternativa al uso de conservaciones locales, puede usar <A href="https://go.microsoft.com/fwlink/?linkid=780738">casos de eDiscovery</A> o <A href="https://go.microsoft.com/fwlink/?linkid=827811">directivas de retención</A> en el Centro de seguridad y cumplimiento de Office 365. Después de retirar las nuevas conservaciones locales, podrá seguir modificando las conservaciones locales existentes y se admitirá la creación de conservaciones locales en las implementaciones híbridas de Exchange Server 2013 y de Exchange. También podrá seguir colocando los buzones de correo en retención por juicio.



Su organización puede necesitar que todos los datos de buzones se conserven durante un período determinado. Puede utilizar la retención por juicio o la conservación local para cumplir este requisito. Después de poner un buzón en retención por juicio o en conservación local, todos los elementos del buzón que se modifiquen o que se eliminen permanentemente se conservan en la carpeta Elementos recuperables. Para obtener más información, vea [Conservación local y retención por juicio](https://technet.microsoft.com/es-es/library/ff637980(v=exchg.150)).

Antes de poner todos los buzones de una organización en retención por juicio o en conservación local, tenga en cuenta lo siguiente:

  - Al colocar buzones en retención, el contenido de buzón de archivo del usuario (si está habilitada) también se coloca en retención.

  - Poner todos los buzones de una organización en retención puede afectar significativamente al tamaño de los buzones. En una implementación de Exchange Server 2013, planee el almacenamiento adecuado para satisfacer los requisitos de conservación de su organización. En Exchange Online, [los límites de almacenamiento de los buzones](https://go.microsoft.com/fwlink/?linkid=403645) de sus usuarios dependen de la licencia de suscripción del usuario.

  - Conservar los datos de buzón durante mucho tiempo dará lugar al crecimiento de la carpeta Elementos recuperables en el buzón primario y el buzón de archivo de un usuario. La carpeta Elementos recuperables tiene su propio límite de almacenamiento, por lo que los elementos de la carpeta no se tienen en cuenta para el límite de almacenamiento del buzón. En Exchange Server 2013 y Exchange Online, el límite de almacenamiento predeterminado para la carpeta Elementos recuperables es de 30 GB.
    
      - En Exchange Online, la cuota para la carpeta Elementos recuperables aumenta automáticamente a 100 GB al colocar un buzón de correo en retención.
    
      - En Exchange Server 2013, se recomienda supervisar periódicamente el tamaño de esta carpeta para asegurarse de que no llegue al límite. Para obtener más información, vea [Carpeta Elementos recuperables](recoverable-items-folder-exchange-2013-help.md).

## Elegir entre retención por juicio y conservación local

Estos son algunos de los factores que hay que tener en cuenta al decidir la característica de retención que se debe usar para poner todos los buzones de la organización en retención.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Si quiere...</th>
<th>Usar la retención por juicio</th>
<th>Usar la conservación local</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Usar el EAC</p></td>
<td><p>Sí</p>
<p>Para establecer la retención por juicio, el EAC es lo más adecuado para las acciones ocasionales rápidas en unos pocos buzones. Se recomienda usar el Shell para establecer la retención por juicio para todos los usuarios de su organización.</p></td>
<td><p>Sí</p>
<p>Sin embargo, no puede seleccionar más de 500 buzones de origen en el EAC.</p></td>
</tr>
<tr class="even">
<td><p>Usar el Shell</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p>Poner más de 10.000 buzones de correo en retención</p></td>
<td><p>Sí</p>
<p>La retención por juicio es una propiedad del buzón. Puede poner todos los buzones de una organización en retención con el cmdlet <strong>Set-Mailbox</strong>.</p></td>
<td><p>Sí. Use varias conservaciones locales.</p>
<p>Puede usar grupos de distribución para especificar un máximo de 10.000 buzones en una sola conservación local. Para poner más buzones en retención, debe crear retenciones locales adicionales. Esto provocará una carga administrativa adicional. Es más sencillo usar una retención por juicio para poner en retención grandes cantidades de buzones.</p></td>
</tr>
<tr class="even">
<td><p>Poner muchos buzones diferentes en retención durante distintos períodos.</p></td>
<td><p>Sí</p>
<p>La retención por juicio es una propiedad del buzón. Puede poner en retención cada buzón (o conjuntos de buzones) con una duración diferente.</p>
<p>Vea la sección Más información para más ejemplos de cómo usar las propiedades de destinatarios en un filtro para poner en retención por juicio un subconjunto de buzones de correo.</p></td>
<td><p>Sí</p>
<p>Si va a aplicar retenciones individuales en miles de buzones de correo, se recomienda usar la retención por juicio. Si va a crear retenciones para eventos específicos que implican a varios usuarios, use una sola conservación local para el grupo de usuarios.</p>
<p>No se recomienda crear conservaciones locales independientes para cada buzón porque se crearían muchas consultas de conservación local que serán más difíciles de administrar que las retenciones por juicio. Si hay un gran número de objetos de conservación local se puede ralentizar el rendimiento en el EAC al actualizar, crear o modificar objetos de retención.</p></td>
</tr>
<tr class="odd">
<td><p>Poner automáticamente nuevos buzones en retención</p></td>
<td><p>No</p>
<p>Debe poner un buzón nuevo en retención por juicio después de crearlo. Puede programar el comando o script que se ejecutará con la frecuencia necesaria para lograr el mismo efecto.</p></td>
<td><p>No</p>
<p>Debe agregar un nuevo buzón a una conservación local aunque haya especificado un grupo de distribución cuando creó la conservación local. También puede programar el comando o script que se ejecutará con la frecuencia necesaria para lograr el mismo efecto. Se recomienda que el script compruebe si una conservación local ya ha alcanzado el límite de 10.000 buzones de correo, y que cree después una nueva conservación local si es necesario.</p></td>
</tr>
<tr class="even">
<td><p>Poner todas las carpetas públicas en retención</p></td>
<td><p>No</p>
<p>En Exchange Online, no se permite crear una retención por juicio en buzones de carpetas públicas. Tiene que usar la conservación local.</p></td>
<td><p>Sí</p></td>
</tr>
</tbody>
</table>


## Ponga todos los buzones en retención por juicio

Use el Shell para poner todos los buzones en retención indefinidamente o durante un tiempo especificado, fácil y rápidamente. Este comando pone todos los buzones en retención durante 2555 días (aproximadamente siete años).

```powershell
Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -eq "UserMailbox"} | Set-Mailbox -LitigationHoldEnabled $true -LitigationHoldDuration 2555
```

En el ejemplo se usa el cmdlet [Get-Mailbox](https://technet.microsoft.com/es-es/library/bb123685\(v=exchg.150\)) y un filtro de destinatarios para recuperar todos los buzones de usuario de la organización y, después, canaliza la lista de buzones al cmdlet [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)) para habilitar la retención por juicio y especificar la duración de la retención. Para obtener más información, vea [Poner un buzón en retención por juicio](place-a-mailbox-on-litigation-hold-exchange-2013-help.md).

## Poner todos los buzones en conservación local

Puede usar el EAC para seleccionar hasta 500 buzones y ponerlos en retención. Para obtener información detallada, vea [Crear o quitar una conservación local](https://technet.microsoft.com/es-es/library/dd979797(v=exchg.150)).


> [!TIP]
> Para poner más de 500 usuarios en conservación local, use el Shell. Vea <A href="https://technet.microsoft.com/es-es/library/dd298064(v=exchg.150)">New-MailboxSearch</A>.



## Más información

  - Al poner todos los buzones de la organización en retención, solo se ponen el retención los buzones que existen en el momento en que se ejecuta el comando. Si crea nuevos buzones más adelante, ejecute el comando de nuevo para ponerlos en retención. Si crea nuevos buzones con frecuencia, puede ejecutar el comando como una tarea programada con la frecuencia que necesite.

  - Colocar buzones en retención conserva los datos e impide su eliminación antes del período especificado y guarda la versión original de un mensaje antes de modificarlo. No elimina automáticamente los mensajes tras el período especificado. Combine la retención por juicio o la conservación local con una directiva de retención, que puede eliminar automáticamente los mensajes tras el período especificado, para satisfacer los requisitos de retención de correo electrónico de su organización. Vea [Etiquetas de retención y directivas de retención](https://technet.microsoft.com/es-es/library/dd297955(v=exchg.150)) para obtener más información.

  - El comando de PowerShell que se usa en este tema para poner todos los buzones en retención por juicio usa un filtro de destinatarios que devuelve todos los buzones de usuario. Puede usar otras propiedades de destinatarios para devolver una lista de buzones específicos que puede canalizar después al cmdlet **Set-Mailbox** para poner esos buzones en retención por juicio.
    
    Estos son algunos ejemplos de cómo usar los cmdlets **Get-Mailbox** y **Get-Recipient** para obtener un subconjunto de buzones en función de propiedades de usuarios o buzones. En estos ejemplos se da por hecho que las propiedades de buzón relevantes (como *CustomAttributeN* o *Department*) se han rellenado.
    
    ```powershell
        Get-Mailbox -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'CustomAttribute15 -eq "OneYearLitigationHold"'
    ```

    ```powershell
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'Department -eq "HR"'
    ```

    ```powershell
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'PostalCode -eq "98052"'
    ```

    ```powershell
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'StateOrProvince -eq "WA"'
    ```

    ```powershell
        Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -ne "DiscoveryMailbox"}
    ```
    
    Puede usar otras propiedades de buzón de usuario en un filtro para incluir o excluir buzones de correo. Para obtener información detallada, vea [Propiedades a las que se puede aplicar un filtro para el parámetro -Filter](https://technet.microsoft.com/es-es/library/bb738155\(v=exchg.150\)).

