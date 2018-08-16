---
title: 'Quitar una búsqueda de eDiscovery local: Exchange 2013 Help'
TOCTitle: Quitar una búsqueda de exhibición de documentos electrónicos local
ms:assetid: 78461a78-1255-4a26-9d36-c6b8eb82a4f9
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd298078(v=EXCHG.150)
ms:contentKeyID: 49895727
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Quitar una búsqueda de exhibición de documentos electrónicos local

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-07-14_

En Microsoft Exchange Server 2013, puede usar el servicio de exhibición de documentos electrónicos local para hacer búsquedas del contenido de los buzones de correo. Puede quitar una búsqueda de exhibición de documentos electrónicos local en cualquier momento. Al eliminar la búsqueda, los resultados de búsqueda se eliminan del buzón de exhibición de documentos electrónicos.


> [!WARNING]
> La eliminación de una búsqueda de exhibición de documentos electrónicos local hará que se eliminen todos los resultados de búsqueda copiados en un buzón de exhibición de documentos electrónicos.



## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 2-5 minutos.

  - Para eliminar una búsqueda de exhibición de documentos electrónicos local con retención local habilitada, primero debe eliminar dicha retención de la búsqueda. Para obtener información más detallada, consulte [Crear o quitar una conservación local](create-or-remove-an-in-place-hold-exchange-2013-help.md).

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Exhibición de documentos electrónicos en contexto" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## ¿Qué desea hacer?

## Usar el EAC para quitar una búsqueda de exhibición de documentos electrónicos local

1.  Desplácese a **Administración del cumplimiento** \> **Suspensión y exhibición de documentos electrónicos local**.

2.  En la vista de lista, seleccione la búsqueda de exhibición de documentos electrónicos local que desea quitar y, a continuación, haga clic en **Eliminar**![Eliminar icono](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Eliminar icono").

## Usar el Shell para quitar una búsqueda de exhibición de documentos electrónicos local

Para obtener un ejemplo sobre cómo eliminar una búsqueda de exhibición de documentos electrónicos local, consulte la sección "Ejemplos" en [Remove-MailboxSearch](https://technet.microsoft.com/es-es/library/dd298130\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para verificar que ha quitado correctamente una búsqueda de exhibición de documentos electrónicos local, siga uno de los procedimientos siguientes:

  - Utilice el EAC para verificar que la búsqueda ya no aparece en la vista de lista de la ficha **Exhibición de documentos electrónicos local**.

  - Use el cmdlet **Get-MailboxSearch** para recuperar las búsquedas de exhibición de documentos electrónicos local. Para obtener un ejemplo sobre cómo recuperar búsquedas de exhibición de documentos electrónicos local, consulte la sección "Ejemplos" en [Get-MailboxSearch](https://technet.microsoft.com/es-es/library/dd351021\(v=exchg.150\)).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


