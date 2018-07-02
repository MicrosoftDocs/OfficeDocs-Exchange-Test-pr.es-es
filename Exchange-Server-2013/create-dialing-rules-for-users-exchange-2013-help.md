---
title: 'Crear reglas de marcado para usuarios: Exchange 2013 Help'
TOCTitle: Crear reglas de marcado para usuarios
ms:assetid: c11e3d62-3eb1-4d7e-8741-9bede593e2df
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ898502(v=EXCHG.150)
ms:contentKeyID: 51406548
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Crear reglas de marcado para usuarios

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2015-03-09_

Los grupos de reglas de marcado consisten en entradas de reglas de marcado. Las reglas de marcado se usan para modificar un número de teléfono antes de enviarlo al sistema telefónico local (PBX) o IP PBX para las llamadas salientes. Las reglas de marcado tienen dos finalidades:

  - Especifican los números que se pueden marcar para las llamadas salientes. Al crear una regla de marcado, se especifican los formatos de número que se pueden marcar. Se rechaza cualquier número que no coincida con uno de los formatos especificado. Si no establece ninguna regla de marcado, los autores de llamadas pueden realizar llamadas dentro de su organización pero no llamadas salientes.

  - Transforman los números marcados antes de mandarlos al sistema telefónico local. Las reglas de marcado pueden quitar o agregar números al número marcado. Por ejemplo, puede usar las reglas de marcado para agregar el código de acceso a línea externa del sistema telefónico, o bien agregar o quitar el código nacional/regional para los números de larga distancia o locales.

Para especificar los tipos de llamadas salientes que desea permitir para un plan de marcado de mensajería unificada, cree un grupo de reglas de marcado con reglas de marcado y úselas para autorizar las llamadas salientes de los usuarios de Outlook Voice Access y los autores de llamada que marquen en un operador automático de mensajería unificada. Cree grupos de reglas de marcado independientes para las llamadas nacionales/regionales y para las internacionales.


> [!NOTE]
> Si integra la mensajería unificada con Microsoft&nbsp;Lync Server, le recomendamos que cree al menos un grupo de reglas de marcado y autorice a dicho grupo en los planes de marcado de URI de SIP, en las directivas de buzones de correo de mensajería unificada y en los operadores automáticos de mensajería unificada para permitir que todas las llamadas salientes se reenvíen a Lync Server.



Para otras tareas de administración relacionadas con las llamadas externas, consulte [Permitir a los usuarios realizar llamadas a procedimientos](allowing-users-to-make-calls-procedures-exchange-2013-help.md).

## Ejemplos de reglas de marcado usadas habitualmente


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Patrón de número</strong></p></td>
<td><p><strong>Número marcado</strong></p></td>
<td><p><strong>¿Cuándo se debe usar esta regla de marcado?</strong></p></td>
</tr>
<tr class="even">
<td><p>*</p></td>
<td><p>*</p></td>
<td><p>Permitir todas las llamadas salientes.</p></td>
</tr>
<tr class="odd">
<td><p>1425xxxxxxx</p></td>
<td><p>91425xxxxxxx</p></td>
<td><p>Impedir que los usuarios obtengan una extensión interna o un error cuando se olviden de marcar el número de línea de acceso externo.</p></td>
</tr>
<tr class="even">
<td><p>1xxxxxxxxxx</p></td>
<td><p>1xxxxxxxxxx</p></td>
<td><p>Permitir todos los números que empiezan por 1.</p></td>
</tr>
<tr class="odd">
<td><p>xxxxxxx</p></td>
<td><p>1425xxxxxxx</p></td>
<td><p>Agregar 1 y el código de área local 425 a los números de siete dígitos.</p></td>
</tr>
</tbody>
</table>


## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 3 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Planes de marcado de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Si va a aplicar grupos de reglas de marcado a las directivas de buzones de correo de mensajería unificada, deberá confirmar que hay creada una directiva de buzones de correo de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Si va a aplicar grupos de reglas de marcado a los operadores automáticos de mensajería unificada, deberá confirmar que hay creado una operador automático de mensajería unificada. Para conocer los pasos detallados, consulte [Crear un operador automático de mensajería unificada](create-a-um-auto-attendant-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Usar el EAC para crear una regla de marcado

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, haga clic en **Configurar**.

3.  En la página **Plan de marcado de mensajería unificada** \> **Reglas de marcado**, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") en **Reglas de marcado nacionales** o **Reglas de marcado internacionales**.

4.  En la página **Nueva regla de marcado**, especifique la siguiente información:
    
      - **Nombre de la regla de marcado**   Escriba el nombre del grupo de reglas de marcado del que desea que forme parte esta regla. Para combinarla con otras reglas, use el mismo nombre de grupo. Para crear un nuevo grupo de reglas de marcado, escriba un nuevo nombre único.
    
      - **Patrón de número para transformar (máscara de número)**   Escriba el patrón de número que se va a transformar antes de marcar, por ejemplo, 91425xxxxxxx. Si el autor de llamada marca un número coincidente, la mensajería unificada lo transforma al número marcado antes de realizar la llamada. Escriba solo números y el carácter comodín (x). El patrón de número también se denomina *máscara de número*.
    
      - **Número marcado   **Escribe el número que se marcará. Use solo números y el carácter comodín (x), como en el patrón de número 9xxxxxxx. Los caracteres comodín (x) se sustituyen por los dígitos del número original marcado por el usuario. Asegúrese de que la cantidad de caracteres comodín del número marcado es la misma que la del patrón de número.
    
      - **Comentario   **Escriba un comentario o una descripción para esta regla de marcado. Puede usar el comentario para describir lo que hace la regla, por ejemplo, "Agregar un 9 a las llamadas salientes".

5.  Haga clic en **Aceptar** para guardar la regla de marcado. Puede continuar introduciendo reglas, con el mismo nombre del grupo de reglas de marcado correspondiente a las reglas que desea autorizar de forma conjunta.

