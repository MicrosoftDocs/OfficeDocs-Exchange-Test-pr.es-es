---
title: 'Crear una directiva de nomenclatura de grupos de distribución: Exchange 2013 Help'
TOCTitle: Crear una directiva de nomenclatura de grupos de distribución
ms:assetid: b2ffb654-345d-4be1-be8e-83d28901373e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ218693(v=EXCHG.150)
ms:contentKeyID: 49115862
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Crear una directiva de nomenclatura de grupos de distribución

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2012-11-01_

Una *directiva de nomenclatura de grupo* permite estandarizar y administrar los nombres de los grupos de distribución creados por los usuarios de la organización. Puede requerir que se añada un prefijo o sufijo concreto al nombre de un grupo de distribución cuando se crea y puede bloquear el uso de determinadas palabras. Esto le ayuda a minimizar el uso de palabras inadecuadas en los nombres de grupo.

Una directiva de nomenclatura de grupos:

  - Aplica una estrategia de nomenclatura coherente para los grupos creados por los usuarios.

  - Identifica los grupos de distribución en la libreta de direcciones compartida.

  - Sugiere la función o la pertenencia del grupo.

  - Identifica el tipo de usuarios que son miembros probables del grupo.

  - Identifica la región geográfica en la que se usa el grupo.

  - Bloquea las palabras inadecuadas en los nombres de grupo.

¿Cómo funciona una directiva de nomenclatura de grupos? Cuando un usuario crea un grupo, especifica un nombre en el campo Nombre para mostrar. Una vez creado el grupo, Microsoft Exchange aplica la directiva de nomenclatura de grupos al añadir un prefijo o sufijo definido en la directiva de nomenclatura de grupo. El nombre completo se muestra en la lista de grupos de distribución en el Centro de Administración de Exchange (EAC), la libreta de direcciones compartida y los campos Para:, CC: y De: en los mensajes de correo electrónico. Si un usuario intenta usar una palabra que ha bloqueado, obtendrá un mensaje de error al intentar guardar el nuevo grupo y se pedirá que quite la palabra bloqueada y vuelva a guardar el grupo.

Aquí hay algunos ejemplos de una directiva de nomenclatura de grupos. En cada, **\<Nombre de grupo\>** se encuentra un nombre descriptivo otorgado por la persona que crea el grupo. Exchange agrega los prefijos y sufijos definidos por la directiva para el nombre para mostrar cuando se crea el grupo.

  - Cadenas de texto, con caracteres de subrayado, usadas para un solo prefijo (**DG**) y sufijo (**Usuarios**):
    
    **DG\_\<Group Name\>\_Users**

  - Varios prefijos (**DG** y **Contoso**) y un sufijo (**Usuarios**), mediante cadenas de texto:
    
    **DG\_Contoso\_\<Group Name\>\_Users**

  - Un atributo (**Department**) usado para el prefijo:
    
    **Department\_\<Group Name\>**
    
    Por ejemplo, suponga que en su centro educativo se rellena el atributo Department para el profesorado. A continuación se ofrece un ejemplo de un nombre de grupo creado por un profesor del departamento de psicología:
    
    **Psicología\_cognitiva201**
    
    En este ejemplo, el carácter de subrayado (\_) se proporciona como la única cadena de texto en un segundo prefijo para separar el nombre del departamento del nombre de grupo.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - La entrada "Grupos de distribución" Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - La longitud máxima del nombre del grupo es de 64 caracteres. Se incluye el número combinado de caracteres del prefijo, el nombre de grupo que proporciona el usuario y el sufijo.

  - La directiva de nomenclatura de grupos solo se aplica a los grupos que crean los usuarios. Si usted u otros administradores utilizan la EAC para crear grupos de distribución, la directiva de nomenclatura de grupos se ignora y no se aplica al nombre del grupo.

  - Los nombres de grupo se crean sin espacios. Se recomienda usar un carácter de subrayado (\_) u otro marcador de posición entre las cadenas de texto, los atributos y el nombre del grupo.

  - Puede utilizar Windows PowerShell para invalidar la directiva de nomenclatura del grupo cuando crea o edita un grupo de distribución. Para obtener más información, consulte [Invalidar la directiva de nomenclatura de grupos de distribución](override-the-distribution-group-naming-policy-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Utilice la EAC para crear una directiva de nomenclatura de grupos

1.  En la EAC, seleccione **Grupos** \> **Más** \> **Configurar la directiva de nomenclatura de grupos**.

2.  En **Directiva de nomenclatura de grupos**, configure el prefijo al seleccionar **Atributo** o **Texto** en el menú desplegable.
    
      - **Atributo**   Seleccione el atributo y, a continuación, haga clic en **Aceptar**.
    
      - **Texto**   Escriba la cadena de texto y haga clic en **Aceptar**.
    
    Observe que la cadena de texto que escribió o el atributo que seleccionó se muestra como un hipervínculo. Haga clic en el hipervínculo para cambiar la cadena de texto o el atributo.

3.  Haga clic en **Agregar** para agregar prefijos adicionales.

4.  Para el sufijo, seleccione **Atributo** o **Texto** en el menú desplegable y configure el sufijo.

5.  Haga clic en **Agregar** para agregar sufijos adicionales.
    
    Después de agregar un prefijo o sufijo, observe que se muestra una vista previa de la directiva de nomenclatura de grupo.

6.  Para eliminar un prefijo o un sufijo de la directiva, haga clic en **Eliminar**![Eliminar](images/JJ218693.37ba42c3-6f0d-42f3-b69b-ff912a99b5b7(EXCHG.150).gif "Eliminar").

7.  Haga clic en **Palabras bloqueadas** para agregar o quitar palabras bloqueadas.
    
      - Para agregar una palabra a la lista, escriba la palabra que se bloqueará y haga clic en **Agregar**![Agregar símbolo para carpetas excluidas en la migración de correo electrónico](images/JJ218693.444d5c83-821f-472c-b733-e84308e2531e(EXCHG.150).gif "Agregar símbolo para carpetas excluidas en la migración de correo electrónico").
    
      - Para quitar una palabra de la lista, selecciónela y haga clic en **Quitar**.
    
      - Para editar una palabra bloqueada existente, selecciónela y haga clic en **Editar**.

8.  Cuando haya terminado, haga clic en **Guardar**.

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si creó una directiva de nomenclatura de grupos correctamente, haga lo siguiente:

  - En la EAC, seleccione **Grupos** \> **Más** \> **Configurar la directiva de nomenclatura de grupo**.
    
    En la página **Directiva de nomenclatura de grupos**, la directiva de nomenclatura de grupo que definió aparece en **Vista previa de la directiva**.

  - En Windows PowerShell, ejecute el siguiente comando para mostrar la directiva de nomenclatura de grupos.
    
        Get-OrganizationConfig | FL DistributionGroupNamingPolicy

