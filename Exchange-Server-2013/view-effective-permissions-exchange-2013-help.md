---
title: 'Ver permisos efectivos: Exchange 2013 Help'
TOCTitle: Ver permisos efectivos
ms:assetid: ae6cb7cf-f998-44a6-a69a-02ad736c8260
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd638167(v=EXCHG.150)
ms:contentKeyID: 49895835
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Ver permisos efectivos

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-09_

Los permisos en Microsoft Exchange Server 2013 se otorgan mediante funciones de administración que se asignan a grupos de funciones de administración, directivas de asignación de funciones de administración, grupos de seguridad universal o directamente a usuarios. Se conceden permisos a los usuarios si pertenecen a los grupos de funciones o a los grupos de seguridad universal, o tienen asignadas funciones de asignación de funciones.

La mayoría de los permisos se conceden según la pertenencia a grupos de funciones o a la asignación de directivas de asignación a usuarios finales. Si bien el uso de los grupos de funciones y las directivas de asignación facilitan la concesión de permisos a grandes cantidades de usuarios, quizá no se pueda saber quién es miembro de un grupo de funciones o a quién se ha asignado una directiva de asignación. En este sentido, el modificador *GetEffectiveUsers* del cmdlet **Get-ManagementRoleAssignment** resulta útil. Muestra los usuarios a los que se ha concedido los permisos conforme a una función de administración en los grupos de funciones, las directivas de asignación y los grupos de seguridad universal a los que se han asignado.

El modificador *GetEffectiveUsers* se usa con el cmdlet **Get-ManagementRoleAssignment** cuando se usa el parámetro *Role*. Si este modificador se especifica con una determinada función, el cmdlet **Get-ManagementRoleAssignment** examina todos los elementos asignados a la función, por ejemplo grupos de funciones, directivas de asignación y grupos de seguridad universal, y obtiene los miembros de todos ellos.


> [!NOTE]
> El modificador <EM>GetEffectiveUser</EM> no obtiene los usuarios que son miembros de un grupo de funciones externas vinculados. En vez de generar una lista de usuarios, si se encuentra un grupo de funciones vinculado, se muestra <STRONG>Todos los miembros del grupo vinculados</STRONG>. Para obtener más información acerca de permisos en varios bosques, consulte <A href="understanding-multiple-forest-permissions-exchange-2013-help.md">Descripción de permisos de bosques múltiples</A>.



Para obtener más información acerca de funciones de administración, grupos de funciones y directivas de asignación, consulte [Descripción del control de acceso basado en funciones](understanding-role-based-access-control-exchange-2013-help.md). Para obtener más información acerca de asignaciones de funciones de administración, consulte [Descripción de las asignaciones de funciones de administración](understanding-management-role-assignments-exchange-2013-help.md).

¿Busca otras tareas de administración relacionadas con los permisos de administración? Consulte [Permisos](permissions-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte elLas entradas "Grupos de funciones" o "Directiva de asignación de funciones" en el tema [Permisos de administración de roles](role-management-permissions-exchange-2013-help.md).

  - Los procedimientos de este tema sólo pueden realizarse en el Shell. No puede usar el Centro de Administración de Exchange (EAC) para ver los permisos vigentes.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Uso del Shell para obtener una lista de todos los usuarios reales

Para obtener una lista de todos los usuarios a los que una función de administración ha concedido permisos, use la sintaxis siguiente.

```powershell
Get-ManagementRoleAssignment -Role <role name> -GetEffectiveUsers
```

En este ejemplo, aparecen todos los usuarios a los que la función Destinatarios de correo ha concedido permiso.

```powershell
Get-ManagementRoleAssignment -Role "Mail Recipients" -GetEffectiveUsers
```

Si desea modificar las propiedades que aparecen en la lista o exportar la lista a un archivo con valores separados por comas (CSV), consulte Uso del Shell para personalizar el resultado y mostrarlo más adelante en este tema.

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd351024\(v=exchg.150\)).

## Uso del Shell para buscar un determinado usuario en una función

Para buscar un usuario concreto al que una función de administración haya concedido permiso, use el cmdlet **Get-ManagementRoleAssignment** para obtener una lista de todos los usuarios reales; a continuación, canalice el resultado del cmdlet al cmdlet **Where**. El cmdlet **Where** filtra el resultado y devuelve únicamente el usuario que se ha especificado. Use la siguiente sintaxis.

```powershell
Get-ManagementRoleAssignment -Role <role name> -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "<name of user>" }
```

En este ejemplo, se busca al usuario David Strome en la función Registro en diario.

```powershell
Get-ManagementRoleAssignment -Role Journaling -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "David Strome" }
```

Si desea modificar las propiedades que se devuelven en la lista o exportar la lista a un archivo .csv, consulte Uso del Shell para personalizar el resultado y mostrarlo más adelante en este tema.

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd351024\(v=exchg.150\)).

## Uso del Shell para buscar un determinado usuario en todas las funciones

Para saber todas las funciones de las que recibe permisos un usuario, use el cmdlet **Get-ManagementRoleAssignment** para obtener una lista de todos los usuarios reales; a continuación, canalice el resultado del cmdlet al cmdlet **Where**. El cmdlet **Where** filtra el resultado y devuelve únicamente las asignaciones de función que conceden los permisos de usuario.

```powershell
Get-ManagementRoleAssignment -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "<name of user>" }
```

En este ejemplo, se buscan todas las asignaciones de funciones que conceden permisos al usuario Kim Akers.

```powershell
Get-ManagementRoleAssignment -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "Kim Akers" }
```

Si desea modificar las propiedades que se devuelven en la lista o exportar la lista a un archivo CSV, consulte Uso del Shell para personalizar el resultado y mostrarlo más adelante en este tema.

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd351024\(v=exchg.150\)).

## Uso del Shell para personalizar el resultado y mostrarlo

Es posible que el resultado del cmdlet **Get-ManagementRoleAssignment** no proporcione la información que esperaba. El resultado del cmdlet contiene muchas más propiedades a las que puede tener acceso. A continuación se presentan algunas de las propiedades que podrían ser útiles:

  - **EffectiveUserName**   Nombre del usuario.

  - **Función**   Función que concede los permisos.

  - **RoleAssigneeName**   Grupo de funciones, directiva de asignación o grupo de seguridad universal asignado a la función y que contiene al usuario en la propiedad `EffectiveUserName`.

  - **RoleAssigneeType**   Indica si la función se asigna a un grupo de funciones, una directiva de asignación, un grupo de seguridad universal o un usuario.

  - **AssignmentMethod**   Indica si la asignación entre la función y el elemento al que se asigna la función es directa o indirecta.

  - **CustomRecipientWriteScope**   Indica el ámbito de escritura de destinatarios personalizado, si lo hubiera, que se aplicó a la asignación de función en el momento de crearse. El ámbito especificado en esta propiedad anula el ámbito de escritura de destinatarios implícito especificado en la propiedad `RecipientWriteScope`.

  - **CustomConfigWriteScope**   Indica el ámbito de escritura de configuración personalizado, si lo hubiera, que se aplicó a la asignación de función en el momento de crearse. El ámbito especificado en esta propiedad anula el ámbito de configuración de escritura implícito especificado en la propiedad `ConfigWriteScope`.

  - **RecipientReadScope**   Indica el ámbito de lectura de destinatarios implícito que se asigna a la función.

  - **RecipientWriteScope**   Indica el ámbito de escritura de destinatarios implícito que se asigna a la función.

  - **ConfigReadScope**   Indica el ámbito de lectura de configuración implícito que se asigna a la función.

  - **ConfigWriteScope**   Indica el ámbito de escritura de configuración implícito que se asigna a la función.

Para seleccionar las propiedades que desea mostrar en la lista, prácticamente se usan los mismos comandos de las secciones Uso del Shell para obtener una lista de todos los usuarios reales, Uso del Shell para buscar un determinado usuario en una función y Uso del Shell para buscar un determinado usuario en todas las funciones. La diferencia estriba en que los resultados de los comandos se canalizan a los cmdlets **Format-Table** o **Select-Object**. El cmdlet **Format-Table** es útil para visualizar la lista de resultados en la pantalla. El cmdlet **Select-Object** es útil para visualizar la lista de resultados en un archivo .csv.

Los dos cmdlets permiten especificar las propiedades que desea ver y su orden de aparición. El cmdlet **Format-Table** brinda más opciones si se visualizan los resultados en una pantalla; por su parte, el cmdlet **Select-Object** no modifica para nada los resultados, cosa que resulta útil al canalizar la lista a un archivo .csv.

Para obtener más información sobre los cmdlets **Format-Table** y **Select-Object**, consulte [Trabajar con salidas de comandos](working-with-command-output-exchange-2013-help.md).

## Obtención en pantalla de una lista personalizada

1.  Elija la información que desea ver y busque el comando relacionado a través de uno de los siguientes procedimientos:
    
      - Uso del Shell para obtener una lista de todos los usuarios reales
    
      - Uso del Shell para buscar un determinado usuario en una función
    
      - Uso del Shell para buscar un determinado usuario en todas las funciones

2.  Elija las propiedades que desee ver en la lista.

3.  Use la sintaxis siguiente para ver la lista.
    
    ```powershell
    <command to retrieve list > | Format-Table <property 1>, <property 2>, <property ...>
    ```

En este ejemplo, se encuentra al usuario David Strome en todas las funciones y se muestran las propiedades `EffectiveUserName`, `Role`, `CustomRecipientWriteScope` y `CustomConfigWriteScope`.

```powershell
Get-ManagementRoleAssignment -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "David Strome" } | Format-Table EffectiveUserName, Role, CustomRecipientWriteScope, CustomConfigWriteScope
```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd351024\(v=exchg.150\)).

## Obtención de una lista personalizada en un archivo .csv

Para exportar una lista a un archivo .cvs, se necesita canalizar el resultado del comando **Get-ManagementRoleAssignment** del pertinente procedimiento mencionado anteriormente al cmdlet **Select-Object**. A continuación, el resultado del cmdlet **Select-Object** se canaliza al cmdlet **Export-CSV**, que guarda el resultado en formato .csv en un archivo con el nombre que desee asignarle.

1.  Elija la información que desea ver y busque el comando relacionado a través de uno de los siguientes procedimientos:
    
      - Uso del Shell para obtener una lista de todos los usuarios reales
    
      - Uso del Shell para buscar un determinado usuario en una función
    
      - Uso del Shell para buscar un determinado usuario en todas las funciones

2.  Elija las propiedades que desee ver en la lista.

3.  Use la sintaxis siguiente para exportar la lista a un archivo .csv.
    
    ```powershell
    <command to retrieve list > | Select-Object <property 1>, <property 2>, <property ...> | Export-CSV <filename>
    ```

En este ejemplo, se encuentra al usuario David Strome en todas las funciones y se muestran las propiedades `EffectiveUserName`, `Role`, `CustomRecipientWriteScope` y `CustomConfigWriteScope`.

```powershell
Get-ManagementRoleAssignment -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "David Strome" } | Select-Object EffectiveUserName, Role, CustomRecipientWriteScope, CustomConfigWriteScope | Export-CSV c:\output.csv
```

El archivo .csv ya puede verse en el visor que elija.

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd351024\(v=exchg.150\)).

