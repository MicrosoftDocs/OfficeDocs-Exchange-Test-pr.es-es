---
title: 'Uso del script RollAlternateserviceAccountCredential.ps1 en el Shell'
TOCTitle: Uso del script RollAlternateserviceAccountCredential.ps1 en el Shell
ms:assetid: 6ac55aae-472a-4ed6-83df-2d0e7b48e05c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ff808311(v=EXCHG.150)
ms:contentKeyID: 63918704
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Uso del script RollAlternateserviceAccountCredential.ps1 en el Shell

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Se puede usar el script RollAlternateServiceAccountPassword.ps1 en Exchange Server 2013 para actualizar una credencial de la cuenta de servicio alternativa (credencial ASA) y distribuir la actualización a servidores de acceso de cliente específicos.


> [!NOTE]
> El shell de administración de Exchange no carga las secuencias de comandos automáticamente. Todos los scripts deben estar precedidos por "<STRONG>.\\</STRONG>". Por ejemplo, para ejecutar el scripts RollAlternateServiceAccountPassword.ps1, escriba <CODE>.\RollAlternateServiceAccountPassword.ps1</CODE>.




> [!NOTE]
> Esta secuencia se proporciona en inglés solamente.



Para obtener más información acerca del uso y la escritura de secuencias de comandos, vea [Scripting con el Shell de administración de Exchange](https://technet.microsoft.com/es-es/library/bb123798\(v=exchg.150\)).

## Sintaxis
```powershell
    RollAlternateServiceAccountPassword.ps1 -Scope <Object> -Identity <Object> -Source <Object> -
```

## Descripción detallada

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Seguridad de acceso de cliente" en el tema sobre permisos de acceso de cliente.

## Detalles técnicos de la secuencia de comandos de credenciales de cuenta de servicio alternativa

Esta secuencia de comandos facilita la instalación y el mantenimiento de la credencial ASA. Una vez creada la credencial ASA y establecidos los nombres principales de servicio adecuados, la secuencia de comandos se puede usar para distribuir la credencial a todos los servidores de acceso de cliente de destino.

Para usar el script, debe identificar a qué servidores quiere dirigirse y qué credencial quiere usar como credencial ASA.

## Ámbito de servidor

Se puede optar por que la secuencia de comandos alcance a todos los servidores de acceso de cliente en el bosque, todos los miembros de una matriz del servidor de acceso de cliente en particular, o bien servidores específicos. Los parámetros disponibles son *ToEntireForest*, *ToArraryMembers* y *ToSpecificServers*. Si dirige el script a servidores específicos o a miembros de una matriz de servidores específica, el parámetro *Identity* debe especificarse con los nombres de servidores o matrices de servidores a los que quiere dirigirse.

## Origen de la credencial

La secuencia de comandos puede copiar la contraseña de la cuenta de servicio alternativa de un servidor existente. O bien, se puede especificar la cuenta que desea usar y permitir que la secuencia de comandos genere una nueva contraseña para la cuenta. Los parámetros disponibles son *GenerateNewPasswordFor* y *CopyFrom*. El parámetro *GenerateNewPasswordFor* exige que especifique una cadena de cuenta en el formato siguiente: DOMINIO\\Nombre de cuenta Si se usa una cuenta de equipo, hay que agregar “$” al final del nombre de la cuenta, por ejemplo CONTOSO\\CtaServidorCliente$. El parámetro *CopyFrom* toma el nombre de un servidor de acceso de cliente como origen de la credencial.

## Generar una nueva contraseña para una credencial

La contraseña se crea a partir de la secuencia de comandos. No requiere la entrada del usuario. La secuencia de comandos intentará distribuir la contraseña a todos los equipos de destino y, a continuación, intentará actualizar la credencial de la cuenta Active Directory con la contraseña que se acaba de generar.

La contraseña que se acaba de generar tiene 73 caracteres y cumplirá con los requisitos estándar de contraseña segura. Si los requisitos de contraseña son diferentes, es posible que se deba establecer la contraseña de forma manual y después copiarla en los servidores de destino.

Para evitar la interrupción del servicio, la secuencia de comandos examina cada servidor de acceso de cliente y mantiene la contraseña actual además de agregar la nueva contraseña. Una vez ejecutada la secuencia de comandos, la credencial ASA compartida podrá usar cualquiera de las 2 contraseñas: la contraseña actual, tal como está guardada en Active Directory o la nueva contraseña que aún no se ha establecido en Active Directory.

Todas las contraseñas que ya no son válidas, como una contraseña expirada, se quitarán de los servidores de destino. Si no se puede cambiar la contraseña en Active Directory, posiblemente porque la contraseña expiró, el script intentará restablecer la contraseña. Esta tarea requerirá que la cuenta ejecute la secuencia de comandos para tener permisos para restablecer las contraseñas de cuenta del equipo Active Directory o las contraseñas de cuenta de usuario, en función de que su cuenta de servicio alternativa sea una cuenta de equipo o una cuenta de usuario.

Si las contraseñas no se cambian correctamente para todos los servidores de acceso de cliente de destino, si se actualiza la contraseña de Active Directory se puede producir un error de autenticación. Si la secuencia de comandos se ejecuta en modo desatendido, no actualizará la contraseña de Active Directory con la nueva contraseña, a menos que todos los servidores de acceso de cliente de destino se hayan actualizado correctamente. Si la secuencia de comandos se ejecuta en modo asistido, se le preguntará si desea actualizar la contraseña en Active Directory.

## Crear una tarea programada para automatizar el mantenimiento de contraseñas

Si desea que la secuencia de comandos cree una tarea programada para mantener la contraseña de forma continua, use el parámetro *CreateScheduledTask*. Este parámetro exige una cadena para el nombre de la tarea que desea crear.


> [!NOTE]
> Ejecute la secuencia de comandos y compruebe que funcione correctamente en modo asistido antes de crear la tarea programada desatendida.



La secuencia de comandos crea un archivo .cmd en la carpeta en la que se ubica la secuencia de comandos. A continuación, crea una tarea para ejecutar ese archivo .cmd cada tres semanas. Se puede usar el Programador de tareas de Windows para modificar la tarea programada, por ejemplo, para establecer que se ejecute con mayor o menor frecuencia. De forma predeterminada, la tarea se ejecutará como el usuario que esté conectado actualmente. Además, el script solo se ejecutará cuando el usuario haya iniciado sesión en el equipo. Recomendamos que modifique la tarea programada para ejecutarse con el usuario conectado o sin conexión. También puede optar por ejecutarla con una cuenta diferente, si es que esa cuenta tiene permisos de Active Directory para restablecer la contraseña, así como el rol de administrador de empresa de Exchange. Al crear una tarea programada, la secuencia se ejecutará automáticamente en el modo desatendido.

## Tareas fuera de ámbito de la secuencia de comandos

La secuencia de comandos no administra los SPN de la credencial ASA ni permite quitar una cuenta de servicio alternativa desde un servidor. Para quitar una cuenta de servicio alternativa de un servidor, vea la sección [Turn Kerberos authentication off](configuring-kerberos-authentication-for-load-balanced-client-access-servers-exchange-2013-help.md) en [Configurar la autenticación de Kerberos para servidores de acceso de cliente con equilibrio de carga](configuring-kerberos-authentication-for-load-balanced-client-access-servers-exchange-2013-help.md).

## Solución de problemas de la secuencia

Le recomendamos que ejecute la secuencia y compruebe que funcione correctamente en modo asistido antes de crear la tarea programada desatendida. Para obtener información sobre la solución de problemas, vea [Solución de problemas del script RollAlternateServiceAccountCredential.ps1](troubleshooting-the-rollalternateserviceaccountcredential-ps1-script-exchange-2013-help.md).

## Validación de la secuencia de comandos

Los resultados de la secuencia de comandos al ejecutarla de forma interactiva con la marca detallada deben indicar qué operaciones de la secuencia de comandos se realizaron correctamente. Para confirmar que se actualizaron los servidores de acceso de cliente, puede comprobar la marca de tiempo de la última modificación en la credencial ASA. En el siguiente ejemplo se genera una lista de servidores de acceso de cliente y la última vez que se actualizó la cuenta de servicio alternativa.

```powershell
    Get-ClientAccessServer -IncludeAlternateServiceAccountCredentialstatus |Fl Name, AlternateServiceAccountConfiguration
```

También se puede examinar el registro de eventos en el equipo en el cual se ejecuta la secuencia de comandos. Las entradas del registro de eventos para el script se encuentran en el registro de eventos de aplicación y pertenecen a la *MSExchange Management Application* de origen.En la tabla siguiente se indican los eventos registrados y el significado de cada uno de ellos.

### Identificadores de eventos de la secuencia de comandos y sus explicaciones

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Evento</th>
<th>Explicación</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>14001</p></td>
<td><p>Comenzar</p></td>
</tr>
<tr class="even">
<td><p>14002</p></td>
<td><p>Éxito (información)</p></td>
</tr>
<tr class="odd">
<td><p>14003</p></td>
<td><p>Con éxito pero con advertencias.</p>
<p>La secuencia de comandos encontró algunos problemas, pero pudo resolverlos, o la entrada del usuario confirmó que no fue necesario. Si la secuencia de comandos se está ejecutando en modo interactivo, lea los resultados de la secuencia de comandos para conocer más detalles de advertencia.</p></td>
</tr>
<tr class="even">
<td><p>14004</p></td>
<td><p>Error</p></td>
</tr>
</tbody>
</table>


Si la secuencia de comandos se ejecuta como tarea programada, los resultados se registran en el servidor Exchange, en la carpeta **Registro** en una subcarpeta llamada **RollAlternateServiceAccountPassword**.

Puede usar el registro para confirmar que la tarea se ha ejecutado correctamente.

## Parámetros


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parámetro</th>
<th>Obligatorio</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ToEntireForest</em></p></td>
<td><p>Opcional</p></td>
<td><p>El parámetro <em>ToEntireForest</em> dirige la secuencia de comandos a todos los servidores de acceso de cliente en el bosque.</p></td>
</tr>
<tr class="even">
<td><p><em>ToArrayMembers</em></p></td>
<td><p>Opcional</p></td>
<td><p>El parámetro <em>ToArrayMembers</em> dirige la secuencia de comandos a todos los miembros de una matriz de servidor de acceso de cliente.</p>

> [!NOTE]
> Si usa el parámetro <EM>ToArrayMembers</EM> o el parámetro <EM>ToSpecificServers</EM>, debe especificar los nombres de servidor o los nombres de matriz de servidores mediante el parámetro <EM>Identity</EM>.


</td>
</tr>
<tr class="odd">
<td><p><em>ToSpecificServers</em></p></td>
<td><p>Opcional</p></td>
<td><p>El parámetro <em>ToSpecificServers</em> dirige la secuencia de comandos a servidores específicos.</p>

> [!NOTE]
> Si usa el parámetro <EM>ToArrayMembers</EM> o el parámetro <EM>ToSpecificServers</EM>, debe especificar los nombres de servidor o los nombres de matriz de servidores mediante el parámetro <EM>Identity</EM>.


</td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Necesario</p></td>
<td><p>El parámetro <em>Identity</em> especifica el nombre de la matriz de servidor de acceso de cliente de los servidores específicos que tiene como destino.</p></td>
</tr>
<tr class="odd">
<td><p><em>GenerateNewPasswordFor&lt;String&gt;</em></p></td>
<td><p>Opcional</p></td>
<td><p>El parámetro <em>GenerateNewPasswordFor</em> especifica que la secuencia de comandos debe generar una nueva contraseña para ASA. El valor de la cadena debe ser la cuenta ASA con el siguiente formato: DOMINIO\Nombre de cuenta Si usa una cuenta de equipo, debe agregar el carácter $ al final del nombre de cuenta.</p></td>
</tr>
<tr class="even">
<td><p><em>CopyFrom&lt;String&gt;</em></p></td>
<td><p>Opcional</p></td>
<td><p>El parámetro <em>CopyFrom</em> especifica qué credencial se copia desde otro servidor de acceso de cliente. El valor de cadena especificado es el nombre del servidor de acceso de cliente.</p></td>
</tr>
<tr class="odd">
<td><p><em>Mode</em></p></td>
<td><p>Opcional</p></td>
<td><p>El modificador <em>Mode</em> especifica si la secuencia de comandos se ejecuta en modo asistido o desatendido. El modo desatendido no solicita la entrada del cliente y selecciona automáticamente opciones más conservadoras cuando es necesario.</p></td>
</tr>
<tr class="even">
<td><p><em>CreateScheduledTask&lt;String&gt;</em></p></td>
<td><p>Opcional</p></td>
<td><p>El parámetro <em>CreateScheduledTask</em> le indica a la secuencia de comandos que cree una tarea programada para realizar la actualización de la credencial ASA. El valor de cadena es el nombre de la tarea programada que se va a crear.</p>

> [!NOTE]
> Esta secuencia de comandos crea un archivo .cmd en la carpeta en la que se ubica la secuencia de comandos. La tarea programada ejecutará el archivo .cmd una vez cada tres semanas. La tarea se puede editar directamente en el Programador de tareas de Windows&nbsp;para cambiar la frecuencia de la tarea.


</td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Opcional</p></td>
<td><p>El modificador <em>WhatIf</em> indica al comando que simule las acciones que llevaría a cabo en el objeto. Mediante el uso del modificador <em>WhatIf</em>, puede ver los cambios que se producirían sin tener que aplicarlos. No es necesario especificar un valor con el modificador <em>WhatIf</em>.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>El modificador <em>Confirm</em> hace que el comando pause el procesamiento y requiere que usted reconozca qué hará el comando antes de seguir con el procesamiento. No es necesario especificar un valor con el modificador <em>Confirm</em>.</p></td>
</tr>
<tr class="odd">
<td><p><em>Verbose</em></p></td>
<td><p>Opcional</p></td>
<td><p>El parámetro <em>Verbose</em> indica a la secuencia de comandos que realice el registro detallado, de modo que la información adicional acerca de las acciones de la secuencia de comandos se escriba en el archivo de registro.</p></td>
</tr>
<tr class="even">
<td><p><em>Debug</em></p></td>
<td><p>Opcional</p></td>
<td><p>El parámetro <em>Debug</em> indica a la secuencia de comandos que ese ejecute en modo de depuración. Este parámetro se debe usar para determinar por qué se produce un error en la secuencia de comandos.</p></td>
</tr>
</tbody>
</table>


## Ejemplos

## Ejemplo 1

En este ejemplo, la secuencia de comandos se usa para insertar la credencial en todos los servidores de acceso de cliente en el bosque en la primera configuración.

```powershell
    .\RollAlternateserviceAccountPassword.ps1 -ToEntireForest -GenerateNewPasswordFor "Contoso\ComputerAccount$" -Verbose
```

## Ejemplo 2

En este ejemplo se genera una nueva contraseña para la credencial ASA de cuenta de usuario y se distribuye la contraseña a todos los miembros de las matrices de servidor de acceso de cliente donde coincide \*buzón\* en el nombre.

```powershell
    .\RollAlternateserviceAccountPassword.ps1 -ToArrayMembers *mailbox* -GenerateNewPasswordFor "Contoso\UserAccount" -Verbose
```

## Ejemplo 3

En este ejemplo se programa una tarea programada de implementación automatizada de contraseña una vez al mes, denominada “Exchange-RollAsa”. Se actualizará la credencial ASA de todos los servidores de acceso de cliente en todo el bosque con una nueva contraseña generada por la secuencia de comandos. Se crea la tarea programada, pero no se ejecuta la secuencia de comandos. Cuando se ejecuta la tarea programada, la secuencia de comandos se ejecuta en modo desatendido.

```powershell
    .\RollAlternateServiceAccountPassword.ps1 -CreateScheduledTask "Exchange-RollAsa" -ToEntireForest -GenerateNewPasswordFor 'contoso\computerAccount$'
```

## Ejemplo 4

En este ejemplo se actualiza la credencial ASA para todos los servidores de acceso de cliente en la matriz de servidores de acceso de cliente con el nombre CAS01. Se obtiene la credencial desde la cuenta ServiceAc1 del equipo Active Directory en el dominio Contoso.

```powershell
    .\RollAlternateserviceAccountPassword.ps1 -ToArrayMembers "CAS01" -GenerateNewPasswordFor "CONTOSO\ServiceAc1$" 
```

## Ejemplo 5

En este ejemplo, se muestra cómo se puede usar la secuencia de comandos para distribuir ASA a un equipo nuevo o un equipo que está volviendo a estar en servicio, ya sea por el aumento del tamaño de la matriz de servidores o porque está introduciendo los miembros de la matriz después del mantenimiento.

Debe actualizar la credencial ASA antes de que el servidor de acceso de cliente reciba tráfico. Copie la credencial ASA compartida desde cualquier servidor de acceso de cliente que ya esté configurado correctamente. Por ejemplo, si el Servidor A actualmente tiene una credencial ASA en funcionamiento y se acaba de agregar el Servidor B a la matriz, la secuencia de comandos se puede usar para copiar la credencial (incluso la contraseña) desde el Servidor A al Servidor B. Esto resulta útil si el Servidor B se encontraba fuera de servicio o aún no era miembro de la matriz la última vez que se implementó la contraseña.

```powershell
.\RollAlternateServiceAccountPassword.ps1 -CopyFrom ServerA -ToSpecificServers ServerB -Verbose
```

