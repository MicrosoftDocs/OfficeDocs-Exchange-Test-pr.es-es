---
title: 'Modificadores WhatIf, Confirm y ValidateOnly: Exchange 2013 Help'
TOCTitle: Modificadores WhatIf, Confirm y ValidateOnly
ms:assetid: a850eea7-431e-49c5-b877-1ebde2a2b48f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124088(v=EXCHG.150)
ms:contentKeyID: 49116440
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modificadores WhatIf, Confirm y ValidateOnly

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2012-10-04_

Tanto los administradores y los autores de scripts experimentados, como los administradores nuevos en Exchange y scripting, se pueden beneficiar con los modificadores *WhatIf*, *Confirm* y *ValidateOnly*. Estos modificadores permiten controlar la forma en la que se ejecutan los comandos e indican qué hará exactamente un comando antes de afectar a los datos. Esta funcionalidad es muy importante en las transiciones del entorno de prueba al entorno de producción y cuando aplica nuevos comandos o scripts.

Los modificadores *WhatIf*, *Confirm* y *ValidateOnly* son especialmente útiles cuando se usan con comandos que modifican objetos que se devuelven al usar un filtro o un comando **Get** en un canal. Este tema describe cada modificador y también proporciona un comando de ejemplo para cada modificador.


> [!IMPORTANT]
> Si desea usar los modificadores <EM>WhatIf</EM>, <EM>Confirm</EM> y <EM>ValidateOnly</EM> con comandos en un script, debe agregar el modificador adecuado a cada comando en el script y no en la línea de comandos que llama al script.




> [!NOTE]
> <EM>WhatIf</EM>, <EM>Confirm</EM> y <EM>ValidateOnly</EM> se denominan parámetros de modificador. Para obtener más información acerca de los parámetros de modificador, consulte <A href="https://technet.microsoft.com/es-es/library/bb124388(v=exchg.150)">Parámetros</A>.



## Modificador WhatIf

El modificador *WhatIf* instruye al comando al que se aplica que se ejecute, pero solamente para mostrar los objetos que se verían afectados por la ejecución del comando y para mostrar qué cambios producirían en ellos. El modificador en realidad no cambia ninguno de esos objetos. Cuando usa el modificador *WhatIf*, puede ver si los cambios que se producirían en los objetos son los que esperaba, sin la preocupación de modificar los objetos.

Cuando ejecuta un comando junto al modificador *WhatIf*, el modificador *WhatIf* se coloca al final del comando, como se observa en el siguiente ejemplo:

    New-AcceptedDomain -Name "Contoso Domain" -DomainName "contoso.com" -WhatIf 

Cuando ejecuta este comando de ejemplo, el Shell devuelve el siguiente texto:

    What if: Creating Accepted Domain "Contoso Domain" with domain name "contoso.com".

## Modificador Confirm

El modificador *Confirm* instruye al comando al que se aplica que detenga el procesamiento antes de hacer cualquier cambio. De esta forma, el comando le pide que confirme cada acción antes de continuar. Cuando usa el modificador *Confirm*, puede escalonar los cambios en los objetos para asegurarse de que los cambios se hagan solamente en los objetos específicos que desea cambiar. Esta funcionalidad es útil cuando aplica cambios a muchos objetos y desea tener un control preciso del funcionamiento del Shell. Se muestra una solicitud de confirmación para cada objeto antes de que el Shell modifique el objeto.

De forma predeterminada, el Shell aplica automáticamente el modificador *Confirm* a los cmdlets que contengan los siguientes verbos:

  - **Clear**

  - **Disable**

  - **Dismount**

  - **Move**

  - **Remove**

  - **Stop**

  - **Suspend**

  - **Uninstall**

Cuando se ejecuta un cmdlet que contiene cualquiera de estos verbos, el Shell detiene automáticamente el comando y espera que lo confirme antes continuar el proceso.

Cuando aplique manualmente el modificador *Confirm* a un comando, incluya el modificador *Confirm* al final del comando, como se observa en el siguiente ejemplo:

    Get-JournalRule | Enable-JournalRule -Confirm

Cuando ejecuta este comando de ejemplo, el Shell devuelve la siguiente solicitud de confirmación:

    Confirm
    Are you sure you want to perform this action?
    Enabling journal rule "Litigation Journal Rule".
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
    (default is "Y"):

La solicitud de confirmación ofrece las siguientes opciones:

  - **\[Y\] Yes**   Escriba **Y** para instruir al comando que continúe la operación. La siguiente operación presentará otra solicitud de confirmación. `[Y] Yes` es la opción predeterminada.

  - **\[A\] Sí a todol**   Escriba **A** para instruir al comando que continúe la operación y todas las operaciones posteriores. Tras haber elegido esta opción no recibirá más solicitudes de confirmación en relación a este comando.

  - **\[N\] No**   Escriba **N** para instruir al comando que omita esta operación y continúe con la siguiente. La siguiente operación presentará otra solicitud de confirmación.

  - **\[L\] No a todol**   Escriba **L** para instruir al comando que omita esta operación y todas las operaciones posteriores.

  - **\[S\] Suspend**   Escriba **S** para detener el canal actual y volver a la línea de comandos. Escriba **Exit** para reanudar el canal.

  - **\[?\] Help**   Escriba **?** para mostrar la ayuda de la solicitud de confirmación en la línea de comandos.

Si desea reemplazar el comportamiento predeterminado del Shell y suprimir la solicitud de confirmación para los cmdlets a los que se aplica automáticamente, puede incluir el modificador *Confirm* con el valor `$False`, como se observa en el siguiente ejemplo:

    Get-JournalRule | Disable-JournalRule -Confirm:$False

En este caso no se muestra ninguna solicitud de confirmación.


> [!WARNING]
> El valor predeterminado del modificador <EM>Confirm</EM> es <CODE>$True</CODE>. El comportamiento predeterminado del Shell es mostrar automáticamente una solicitud de confirmación. Si suprime este comportamiento predeterminado, instruye al comando que suprima todas las solicitudes de confirmación que aparezcan durante la ejecución del comando. El comando procesará todos los objetos que cumplan los criterios sin confirmación.



## Modificador ValidateOnly

El modificador *ValidateOnly* instruye al comando al que se aplica que valore todas las condiciones y los requisitos necesarios para realizar la operación antes de aplicar cualquier cambio. El modificador *ValidateOnly* está disponible para cmdlets que pueden tardar tiempo en ejecutarse, dependen de varios sistemas o afectan a datos críticos, como los buzones.

Cuando aplica el modificador *ValidateOnly* a un comando, el comando se ejecuta en todo el proceso. El comando realiza todas las acciones como lo haría sin el modificador *ValidateOnly*. Pero no cambia ningún objeto. Cuando termina su proceso, muestra un resumen con los resultados de la validación. Si la validación indica que el comando no ha presentado errores, puede volver a ejecutarlo pero esta vez sin el modificador *ValidateOnly*.

Cuando ejecuta un comando junto al modificador *ValidateOnly*, el modificador *ValidateOnly* se coloca al final del comando.

