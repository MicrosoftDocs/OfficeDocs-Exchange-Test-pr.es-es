---
title: 'Identidad: Exchange 2013 Help'
TOCTitle: Identidad
ms:assetid: e90fae91-37e7-4fdc-9170-44f0dc965c66
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb125042(v=EXCHG.150)
ms:contentKeyID: 49116605
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Identidad

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2012-10-04_

El parámetro *Identity* es un parámetro especial que se puede utilizar con la mayoría de los cmdlets. El parámetro *Identity* ofrece acceso a los identificadores únicos que se refieren a un objeto específico en Microsoft Exchange Server 2013. Esto permite llevar a cabo acciones en un objeto específico de Exchange 2013.

En las secciones siguientes se describe el parámetro Identity y se incluyen ejemplos de cómo usarlo de forma eficaz:

Characteristics of the Identity parameter

Wildcard characters in Identity

Examples of the Identity parameter

## Características del parámetro Identity

El identificador único principal de un objeto de Exchange 2013 es siempre un GUID. Un GUID es un identificador de 128 bits, como `63d64005-42c5-4f8f-b310-14f6cb125bf3`. Este GUID nunca se repite y, por tanto, es siempre único. Sin embargo, no es útil tener que teclear estos GUID regularmente. Por tanto, el parámetro *Identity* también suele estar compuesto de valores de otros parámetros o de un conjunto combinado de valores de varios parámetros de un solo objeto. Estos valores también son únicos en el conjunto de objetos. Puede especificar los valores de estos otros parámetros, como *Name* y *DistriguishedName*, o bien puede generarlos el sistema. El resto de los parámetros que se usan, en caso de haberlos, y cómo se rellenan, depende de cada objeto en sí.

El parámetro *Identity* también se considera un parámetro de posición. Si no se especifica ninguna etiqueta de parámetro, se asume que el primer argumento de un cmdlet es el parámetro *Identity*. Esto reduce el número de pulsaciones necesarias al introducir los comandos. Para obtener más información acerca de los parámetros de posición, consulte [Parámetros](https://technet.microsoft.com/es-es/library/bb124388\(v=exchg.150\)).

El siguiente ejemplo muestra el uso del parámetro *Identity* mediante el valor del parámetro *Name* único del conector de recepción. Este ejemplo también muestra cómo omitir el nombre del parámetro *Identity* porque *Identity* es un parámetro posicional.

    Get-ReceiveConnector -Identity "From the Internet"
    Get-ReceiveConnector "From the Internet"

Como todos los objetos en Exchange 2013, este conector de recepción también se puede referir a su único GUID. Por ejemplo, si el conector de recepción llamado `"From the Internet"` también se asigna al GUID `63d64005-42c5-4f8f-b310-14f6cb125bf3`, también puede recuperar el conector de recepción mediante el siguiente comando:

    Get-ReceiveConnector 63d64005-42c5-4f8f-b310-14f6cb125bf3

Volver al principio

## Caracteres comodín en Identity

Algunos cmdlets **Get** pueden aceptar un carácter comodín (`*`) como parte del valor que envía a *Identity* al ejecutar el cmdlet. Al utilizar un comodín con el parámetro *Identity*, puede especificar un nombre parcial y recuperar una lista de objetos que coincidan con dicho nombre parcial. Puede colocar un carácter comodín al principio o al final del valor de *Identity*, pero no puede colocar el carácter en medio de una cadena. Por ejemplo, los comandos `Get-Mailbox David*` y `Get-Mailbox *anders*` son válidos, pero `Get-Mailbox Reb*ca` no es un comando válido.

Algunos cmdlets **Get** recuperan objetos de Exchange 2013 que se organizan de forma jerárquica o con una relación de principal y secundario. Es posible que exista un grupo de objetos principales que también contengan sus propios objetos secundarios. Los objetos que tienen una relación de principal y secundario pueden tener un parámetro *Identity* con la sintaxis de `<parent>\<child>`.

Cuando un parámetro *Identity* tiene una sintaxis de `<parent>\<child>`, algunos cmdlets permiten usar un carácter comodín (\*) para sustituir todos o algunos de los nombres de elementos principales o secundarios. Por ejemplo, si desea buscar todos los objetos secundarios denominados "Contoso" en todos los objetos principales, puede usar la sintaxis `"*\Contoso"`. Del mismo modo, si desea buscar todos los objetos secundarios con un nombre parcial de "Auth" que existen en el objeto principal de `"ServerA" `, puede usar la sintaxis `"ServerA\Auth*"`.

Algunos cmdlets (aunque no todos) permiten especificar sólo la parte del elemento secundario del parámetro Identity cuando se ejecuta un comando. En este caso, el valor predeterminado de los cmdlets es el objeto principal actual al que se obtiene acceso. Por ejemplo, existen dos conectores de recepción denominados "Contoso Receive Connector" en MBX1 y MBX2. Si ejecuta el comando `Get-ReceiveConnector "Contoso Receive Connector"` en MBX2, sólo se devuelve el conector de recepción en el servidor MBX2.

El comportamiento específico del parámetro Identity y los caracteres comodín depende del cmdlet que se esté ejecutando. Para más información sobre el cmdlet que se está ejecutando, consulte el contenido de las funciones específicas del cmdlet.

Volver al principio

## Ejemplos del parámetro Identity

Los ejemplos descritos en este tema ilustran cómo el parámetro *Identity* puede aceptar diferentes valores únicos para referirse a objetos específicos de la organización de Exchange 2013. Estos ejemplos también ilustran cómo la etiqueta de parámetro *Identity* se puede omitir para reducir el número de pulsaciones cuando se escriben comandos.

## Mensajes DSN

Los ejemplos de esta sección se refieren a los mensajes de notificación de estado de entrega (DSN) que se pueden configurar en una organización de Exchange 2013. El primer ejemplo muestra cómo recuperar el DSN 5.4.1 mediante el cmdlet **Get-SystemMessage**. En el cmdlet **Get-SystemMessage**, el parámetro *Identity* consta de varios datos que se configuran en cada objeto de mensaje de DSN. Estos datos incluyen el idioma en el que está escrito el DSN, si su ámbito es interno o externo y su código de mensaje de DSN, como en el siguiente ejemplo:

    Get-SystemMessage en\internal\5.4.1

También se puede recuperar este mensaje de DSN mediante su GUID como en el siguiente ejemplo, porque todos los objetos en Exchange 2013 tienen un GUID:

    Get-SystemMessage 82ca7bde-1c2d-4aa1-97e1-f298a6f10222

Para obtener más información sobre la composición del parámetro *Identity* cuando se utiliza con los cmdlets **SystemMessage**, consulte [Identidad de mensajes DSN](dsn-message-identity-exchange-2013-help.md).

## Entradas de funciones de administración

Los ejemplos de esta sección hacen referencia a las entradas de función de administración que componen las funciones de administración de Exchange 2013. Las funciones de administración se usan para controlar los permisos que se conceden a los administradores y usuarios finales. Las entradas de funciones de administración se componen de dos partes: la función de administración a la que están asociadas y un cmdlet. Del mismo modo, el parámetro Identity se compone tanto del nombre de la función de administración como del nombre de cmdlet. Por ejemplo, a continuación se incluye la entrada de rol del cmdlet **Set-Mailbox** en el rol `Mail Recipients`:

    Mail Recipients\Set-Mailbox

La entrada del rol `Mail Recipients\Set-Mailbox` es una de las varias entradas en el rol `Mail Recipients`. Para ver todas las entradas de rol en el rol `Mail Recipients`, puede utilizar el siguiente comando:

    Get-ManagementRoleEntry "Mail Recipients\*"

Para ver todas las entradas de rol en el rol `Mail Recipients` que contengan la cadena "`Mailbox`", use el siguiente comando:

    Get-ManagementRoleEntry "Mail Recipients\*Mailbox*"

Para ver todas las funciones de administración en las que **Set-Mailbox** es una de las entradas de la función, use el siguiente comando:

    Get-ManagementRoleEntry *\Set-Mailbox

Con las entradas de función puede usar el carácter comodín de distintos modos para consultar la información que desee en Exchange 2013.

Para obtener más información acerca de los roles de administración, consulte [Descripción de los roles de administración](understanding-management-roles-exchange-2013-help.md).

Volver al principio

