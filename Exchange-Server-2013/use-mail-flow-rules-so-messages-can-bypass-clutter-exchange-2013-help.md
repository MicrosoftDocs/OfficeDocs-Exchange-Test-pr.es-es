---
title: 'Usar reglas de flujo de correo para que los mensajes puedan evitar Otros correos: Exchange 2013 Help'
TOCTitle: Usar reglas de flujo de correo para que los mensajes puedan evitar Otros correos
ms:assetid: 58e413f0-aa27-4307-bffd-4df03090a15e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn896639(v=EXCHG.150)
ms:contentKeyID: 64141273
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Usar reglas de flujo de correo para que los mensajes puedan evitar Otros correos

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

Si desea asegurarse de que recibe mensajes concretos, puede crear una regla de transporte de Exchange para garantizar que estos mensajes omiten la carpeta de desorden. Vea [Usar Desorden para ordenar los mensajes de prioridad baja en Outlook Web App](https://go.microsoft.com/fwlink/p/?linkid=528411) para obtener más información sobre el desorden.

Para ver otras tareas de administración relacionadas con las reglas de transporte, consulte [Reglas de flujo de correo (reglas de transporte) en Exchange Online](https://technet.microsoft.com/es-es/library/jj919238\(v=exchg.150\)) y el tema de PowerShell [New-TransportRule](https://technet.microsoft.com/es-es/library/bb125138\(v=exchg.150\)). Si acaba de empezar con PowerShell, vea estos temas para obtener ayuda sobre su uso:

  - [Conectarse a Exchange Online mediante PowerShell remoto](https://technet.microsoft.com/es-es/library/jj984289\(v=exchg.150\))

  - [Conexión a Exchange usando Shell remoto](https://technet.microsoft.com/es-es/library/dd335083\(v=exchg.150\))

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 5 minutos

  - Entrada Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el "Reglas de transporte" del tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Usar la IU para crear una regla de transporte para omitir la carpeta de otros correos

Este ejemplo permite que todos los mensajes que tienen el título "Reunión" omitan Otros correos.

1.  En el Centro de administración de Exchange, vaya a **flujo de correo** \> **Reglas**. Haga clic en ![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") y elija **Crear una nueva regla**.

2.  Después de crear la nueva regla, haga clic en **guardar** para iniciar la regla.

![Ejemplo de imagen: Si el asunto contiene «reunión», omitir Otros correos](images/Dn896639.75957aa4-4b2a-4142-92ff-07f8ccc64d82(EXCHG.150).png "Ejemplo de imagen: Si el asunto contiene «reunión», omitir Otros correos")

## Usar el Shell para crear una regla de transporte para omitir la carpeta de desorden

Este ejemplo permite que todos los mensajes que tienen el título "Reunión" omitan el desorden.

    New-TransportRule -Name <name_of_the_rule> -SubjectContainsWords "Meeting" -SetHeaderName "X-MS-Exchange-Organization-BypassClutter" -SetHeaderValue "true"


> [!IMPORTANT]
> En este ejemplo, tanto "X-MS-Exchange-organización-BypassClutter" como "true" distinguen mayúsculas de minúsculas.



Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-TransportRule](https://technet.microsoft.com/es-es/library/bb125138\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Puede comprobar los encabezados de los mensajes de correo electrónico para ver si los mensajes están llegando a la Bandeja de entrada debido a la regla de transporte de omisión del desorden. Seleccione un mensaje de correo electrónico en un buzón de la organización que tenga aplicada la regla de transporte de omisión del desorden. Al mirar los encabezados del mensaje, debería ver el encabezado **X-MS-Exchange-Organization-BypassClutter: true**. Esto significa que la omisión está funcionando. Consulte el tema [Ver la información de encabezado de Internet en un mensaje de correo](https://go.microsoft.com/fwlink/p/?linkid=822530) para obtener más información sobre cómo ver los datos de los encabezados.


> [!NOTE]
> Estos encabezados no aparecen en elementos de calendario, como reuniones aceptadas, enviadas o rechazadas. Estamos trabajando para ampliar las capacidades de desorden a estos elementos del calendario cuanto antes.


