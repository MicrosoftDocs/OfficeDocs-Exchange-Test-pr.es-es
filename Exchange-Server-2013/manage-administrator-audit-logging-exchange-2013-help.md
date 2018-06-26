---
title: 'Administrar el registro de auditoría de administrador: Exchange 2013 Help'
TOCTitle: Administrar el registro de auditoría de administrador
ms:assetid: 15c284c0-b8e6-42ca-9913-7c59fdb6885d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd335109(v=EXCHG.150)
ms:contentKeyID: 50556744
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Administrar el registro de auditoría de administrador

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2013-05-17_

El registro de auditoría de administrador en Microsoft Exchange Server 2013 le permite crear una entrada de registro cada vez que se ejecute un cmdlet especificado. Las entradas de registro le proporcionan información sobre qué cmdlet se ejecutó, qué parámetros se usaron, quién ejecutó el cmdlet y qué objetos estuvieron afectados. Para obtener más información acerca del registro de auditoría del administrador, consulte [Registro de auditoría de administrador](administrator-audit-logging-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: menos de 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Registro de auditoría del administrador" en el tema [Permisos de infraestructura de la Shell y de Exchange](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - El registro de auditoría de administrador usa la replicación de Active Directory para replicar las opciones de configuración que se especifiquen en los controladores de dominio de la organización. En función de la configuración de replicación, los cambios que realice pueden no aplicarse de inmediato a todos los servidores de Exchange 2013 en la organización.

  - Los cambios en la configuración del registro de auditoría se actualizan cada 60 minutos en los equipos que tienen shell abierto al momento de realizar un cambio de configuración. Si desea aplicar los cambios de inmediato, cierre y vuelva a abrir el shell en cada equipo.

  - Un comando puede tardar hasta 15 minutos a partir de su ejecución en aparecer en los resultados de búsqueda del registro de auditoría. Esto se debe a que las entradas del registro de auditoría deben indexarse antes de que puedan hacerse búsquedas en ellas. Si un comando no aparece en el registro de auditoría del administrador, espere unos minutos y vuelva a hacer la búsqueda.

  - Debe usar el Shell para hacer este tipo de procedimientos.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Especificar los cmdlets que se van a auditar

De manera predeterminada, el registro de auditoría crea una entrada de registro para cada cmdlet que se ejecuta. Si está habilitando el registro de auditoría por primera vez y quiere observar el comportamiento, no debe cambiar la lista de auditoría del cmdlet. Si previamente especificó cmdlets para auditar y ahora desea auditar todos los cmdlets, puede auditar todos los cmdlets si especifica el carácter comodín asterisco (\*) con el parámetro *AdminAuditLogCmdlets* del cmdlet **Set-AdminAuditLogConfig**, como se muestra en el siguiente comando.

    Set-AdminAuditLogConfig -AdminAuditLogCmdlets *

Puede especificar qué cmdlets auditar si proporciona una lista de cmdlets mediante el parámetro *AdminAuditLogCmdlets*. Cuando proporciona una lista de cmdlets para auditar, puede proporcionar cmdlets únicos, cmdlets con caracteres comodín asterisco (\*) o una combinación de ambos. Cada entrada de la lista está separada por comas. Todos los siguientes valores son válidos:

  - `New-Mailbox`

  - `*TransportRule`

  - `*Management*`

  - `Set-Transport*`

En este ejemplo, se auditan los cmdlets especificados en la lista anterior.

    Set-AdminAuditLogConfig -AdminAuditLogCmdlets New-Mailbox, *TransportRule, *Management*, Set-Transport*

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-AdminAuditLogConfig](https://technet.microsoft.com/es-es/library/dd298169\(v=exchg.150\)).

## Especificar los parámetros que se van a auditar

De forma predeterminada, el registro de auditoría crea una entrada de registro para todos los cmdlets que se ejecutan, independientemente de los parámetros especificados. Si está habilitando el registro de auditoría por primera vez y quiere observar el comportamiento, no debe cambiar la lista de auditoría de parámetros. Si previamente especificó parámetros para auditar y ahora desea auditar todos los parámetros, puede hacerlo si especifica el carácter comodín asterisco (\*) con el parámetro *AdminAuditLogParameters* del cmdlet **Set-AdminAuditLogConfig**, como se muestra en el siguiente comando.

    Set-AdminAuditLogConfig -AdminAuditLogParameters *

Puede especificar qué parámetros desea auditar mediante el parámetro *AdminAuditLogParameters*. Cuando proporciona una lista de parámetros para auditar, puede proporcionar parámetros únicos, parámetros con caracteres comodín asterisco (\*) o una combinación de ambos. Cada entrada de la lista está separada por comas. Todos los siguientes valores son válidos:

  - `Database`

  - `*Address*`

  - `Custom*`

  - `*Region`


> [!NOTE]
> Para una entrada de registro de auditoría cuando un comando se ejecuta, el comando debe incluir, al menos, uno o más parámetros que existan en, al menos, uno o más cmdlets especificados con el parámetro <EM>AdminAuditLogCmdlets</EM>.



En este ejemplo, se auditan los parámetros especificados en la lista anterior.

    Set-AdminAuditLogConfig -AdminAuditLogParameters Database, *Address*, Custom*, *Region

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-AdminAuditLogConfig](https://technet.microsoft.com/es-es/library/dd298169\(v=exchg.150\)).

## Especificar el límite de antigüedad del registro de auditoría

El límite de antigüedad del registro de auditoría determina durante cuánto tiempo se conservarán las entradas del registro de auditoría. Cuando una entrada del registro supera el límite de antigüedad, se elimina. El valor predeterminado es de 90 días.

Puede especificar el número de días, horas, minutos y segundos que se deben conservar en las entradas del registro de auditoría. Para especificar un valor, use el formato dd.hh.mm:ss, donde se aplica lo siguiente:

  - **dd**   Número de días que se conservará la entrada del registro de auditoría

  - **hh**   Número de horas que se conservará la entrada del registro de auditoría

  - **mm**   Número de minutos que se conservará la entrada del registro de auditoría

  - **ss**   Número de segundos que se conservará la entrada del registro de auditoría


> [!WARNING]
> Puede definir el límite de antigüedad del registro de auditoría en un valor menor que el límite de antigüedad actual. Para ello, se eliminan todas las entradas del registro cuya antigüedad supere el nuevo límite de antigüedad.<BR>Si define el límite de antigüedad en 0, Exchange&nbsp;elimina todas las entradas del registro de auditoría.<BR>Se recomienda otorgar permiso para configurar el límite de antigüedad del registro de auditoría solamente a los usuarios de mayor confianza.



En este ejemplo, se especifica un límite de antigüedad de dos años y seis meses.

    Set-AdminAuditLogConfig -AdminAuditLogAgeLimit 913.00:00:00

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-AdminAuditLogConfig](https://technet.microsoft.com/es-es/library/dd298169\(v=exchg.150\)).

## Habilitar o deshabilitar el registro de los cmdlets Test

Los cmdlets que comienzan con el verbo **Test** no se registran de forma predeterminada. Esto se debe a que los cmdlets **Test** pueden generar una cantidad importante de datos en un período corto. Solamente puede habilitar el registro de los cmdlets **Test** durante períodos cortos de tiempo.

Este comando habilita el registro de los cmdlets **Test**.

    Set-AdminAuditLogConfig -TestCmdletLoggingEnabled $True

Este comando deshabilita el registro de los cmdlets **Test**.

    Set-AdminAuditLogConfig -TestCmdletLoggingEnabled $False

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-AdminAuditLogConfig](https://technet.microsoft.com/es-es/library/dd298169\(v=exchg.150\)).

## Deshabilitación del registro de auditoría de administrador

Para deshabilitar el registro de auditoría de administrador, use el comando siguiente.

    Set-AdminAuditLogConfig -AdminAuditLogEnabled $False

## Habilitación del registro de auditoría de administrador

Para habilitar el registro de auditoría de administrador, use el comando siguiente.

    Set-AdminAuditLogConfig -AdminAuditLogEnabled $True

## Consulta de la configuración del registro de auditoría del administrador

Para consultar los parámetros de registro de auditoría del administrador que ha configurado para la organización, use el siguiente comando.

    Get-AdminAuditLogConfig

