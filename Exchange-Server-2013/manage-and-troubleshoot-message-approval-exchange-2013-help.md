---
title: 'Administrar y solucionar problemas de aprobación de mensajes: Exchange 2013 Help'
TOCTitle: Administrar y solucionar problemas de aprobación de mensajes
ms:assetid: 860df43f-a05b-4da3-83f1-68d3123a923d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd298110(v=EXCHG.150)
ms:contentKeyID: 52062037
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Administrar y solucionar problemas de aprobación de mensajes

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Es posible que vea el siguiente mensaje de error al intentar quitar un buzón de arbitraje:


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>No se puede eliminar el buzón de arbitraje &lt;<em>mailbox</em>&gt; porque se está usando para el flujo de trabajo de aprobación para los destinatarios existentes que tienen la función de restricción de participación o de moderación habilitada. Debe deshabilitar las funciones de aprobación en esos destinatarios o especificar un buzón de correo de arbitraje diferente para esos destinatarios antes de quitar este buzón de arbitraje.</p></td>
</tr>
</tbody>
</table>


Un buzón de arbitraje se puede utilizar para manejar el flujo de trabajo de aprobación para destinatarios moderados y las aprobaciones de pertenencia a grupos de distribución. Debe usar PowerShell para encontrar todos los destinatarios que están configurados para usar el buzón de correo de arbitraje. Después de identificar los destinatarios, puede configurarlos para que usen un buzón de correo de arbitraje distinto o puede deshabilitar la moderación para ellos.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 15 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Arbitraje" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Paso 1: Usar el Shell para encontrar todos los destinatarios que usan un buzón de correo de arbitraje que quiere eliminar

Ejecute los comandos siguientes:

    $AM = Get-Mailbox "<arbitration mailbox>" -Arbitration
    $AMDN = $AM.DistinguishedName
    Get-Recipient -RecipientPreviewFilter {ArbitrationMailbox -eq $AMDN}

Por ejemplo, para encontrar todos los destinatarios que usan el buzón de correo de arbitraje denominado Arbitration Mailbox01, ejecute los siguientes comandos:

    $AM = Get-Mailbox "Arbitration Mailbox01" -Arbitration
    $AMDN = $AM.DistinguishedName
    Get-Recipient -RecipientPreviewFilter {ArbitrationMailbox -eq $AMDN}


> [!NOTE]
> El buzón de correo de arbitraje se especifica mediante el nombre distintivo (DN). Si conoce el DN del buzón de correo de arbitraje, puede ejecutar un único comando: <CODE>Get-Recipient -RecipientPreviewFilter {ArbitrationMailbox -eq &lt;DN&gt;}</CODE>.



## Paso 2: Usar el Shell para especificar un buzón de correo de arbitraje distinto o deshabilitar la moderación para los destinatarios

Para impedir que los destinatarios moderados utilicen el buzón de correo de arbitraje que quiere eliminar, puede especificar un buzón de correo de arbitraje distinto o puede deshabilitar la moderación para los destinatarios.

Si decide especificar un buzón de correo de arbitraje distinto para los destinatarios, ejecute el comando siguiente:

    Set-<RecipientType> <Identity> -ArbitrationMailbox <different arbitration mailbox>

Por ejemplo, para volver a configurar el grupo de distribución denominado Todos los empleados de manera que se use el buzón de correo de arbitraje denominado Arbitration Mailbox02 para aprobar la pertenencia a este, ejecute el comando siguiente:

    Set-DistributionGroup "All Employees" -ArbitrationMailbox "Arbitration Mailbox02"

Si decide deshabilitar la moderación para los destinatarios, ejecute el comando siguiente:

    Set-<RecipientType> <Identity> -ModerationEanbled $false

Por ejemplo, para deshabilitar la moderación del buzón denominado Recursos humanos, ejecute el comando siguiente:

    Set-Mailbox "Human Resources" -ModerationEanbled $false

## ¿Cómo saber si el proceso se ha completado correctamente?

El procedimiento se habrá realizado correctamente si puede eliminar el buzón de correo de arbitraje sin recibir el error mencionado.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

