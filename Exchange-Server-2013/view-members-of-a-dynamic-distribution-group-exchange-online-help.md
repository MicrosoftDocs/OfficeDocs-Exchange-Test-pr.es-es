---
title: 'Ver los miembros de un grupo de distribución dinámico: Exchange 2013 Help'
TOCTitle: Ver los miembros de un grupo de distribución dinámico
ms:assetid: 40b100c6-864e-4c82-9f98-08dd5c83e378
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb232019(v=EXCHG.150)
ms:contentKeyID: 48268038
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ver los miembros de un grupo de distribución dinámico

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2018-03-02_

Los grupos de distribución dinámica son grupos de distribución cuya pertenencia está basada en filtros de destinatarios específicos más que en un conjunto de destinatarios definidos. MicrosoftExchange brinda filtros personalizados para facilitar la creación de filtros de destinatarios para grupos de distribución dinámica. Un *filtro predefinido* es un filtro de uso común que puede usar para satisfacer diversos criterios de filtrado de destinatarios. Puede especificar los tipos de destinatario que desea incluir en el grupo de distribución dinámica. Además, también puede especificar una lista de condiciones que los destinatarios deben cumplir. Puede usar el Shell para obtener una vista previa de los destinatarios de un grupo de distribución dinámico que usa filtros predefinidos.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  2 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Grupos de distribución dinámica" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el Shell para obtener una vista previa de los miembros de un grupo de distribución dinámico

En este ejemplo se devuelve la lista de miembros para el grupo de distribución dinámica denominada a empleados de tiempo completo. El primer comando guarda el objeto de grupo de distribución dinámica en la variable `$FTE`. El segundo comando utiliza el cmdlet **Get-Recipient** para enumerar a los destinatarios que coinciden con los criterios definidos para el grupo de distribución dinámica.
  ```
    $FTE = Get-DynamicDistributionGroup "Full Time Employees"
  ```
  ```
    Get-Recipient -RecipientPreviewFilter $FTE.RecipientFilter -OrganizationalUnit $FTE.RecipientContainer
  ```
  
Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-DynamicDistributionGroup](https://technet.microsoft.com/es-es/library/bb124762\(v=exchg.150\)) y [Get-Recipient](https://technet.microsoft.com/es-es/library/aa996921\(v=exchg.150\)).


> [!NOTE]
> No puede ver a los miembros de un grupo de distribución dinámica mediante el CEF.



## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que ha visitado con éxito los miembros de un grupo de distribución dinámica, realice lo siguiente:

  - En el Shell, se devuelve una lista de los miembros después de que ejecute el comando anterior para ver una vista previa de la lista de miembros del grupo de distribución dinámico. Por ejemplo, si creó un buzón de correo nuevo con propiedades que coincidan con el filtro del destinatario para el grupo de distribución dinámico, este nuevo usuario se debería mostrar en la lista de miembros del grupo.

