---
title: 'Filtrado de conexiones en servidores de transporte perimetral: Exchange 2013 Help'
TOCTitle: Filtrado de conexiones en servidores de transporte perimetral
ms:assetid: b513755c-5d3e-44fa-a6cb-771d48b544ac
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124320(v=EXCHG.150)
ms:contentKeyID: 60830018
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Filtrado de conexiones en servidores de transporte perimetral

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

El filtrado de conexiones es una característica contra correo no deseado en Microsoft Exchange Server 2013 que admite o bloquea correo electrónico según el origen del mensaje. El agente de filtrado de conexiones lleva a cabo el filtrado de conexiones, que está disponible solo en los servidores de transporte perimetral. El agente de filtrado de conexiones se basa en la dirección IP del servidor que realiza la conexión para determinar la acción, si la hay, que se realiza en un mensaje entrante.

De manera predeterminada, el agente de filtrado de conexiones es el primer agente contra correo no deseado en evaluar un mensaje entrante en un servidor de transporte perimetral. La dirección IP de origen de la conexión SMTP se comprueba según las direcciones IP permitidas y bloqueadas. Si la dirección IP de origen se ha permitido de forma específica, el mensaje se envía a los destinatarios de la organización sin que otros agentes contra correo no deseado lleven a cabo ningún procesamiento adicional. Si la dirección IP de origen se ha bloqueado de forma específica, la conexión SMTP se cancelará. Si la dirección IP de origen no se ha permitido o bloqueado de forma específica, el mensaje fluye a través de los demás agentes contra correo no deseado en el servidor de transporte perimetral.

El filtrado de conexiones compara las dirección IP del servidor de correo de origen con los valores en la lista de direcciones IP permitidas, la lista de direcciones IP bloqueadas, los proveedores de la lista de IP permitidas y los proveedores de la lista de IP bloqueadas. Es necesario configurar al menos uno de estos cuatro almacenes de datos de direcciones IP para que el filtrado de conexiones funcione. Si no especifica ningún dato de dirección IP, debe deshabilitar el agente de filtrado de conexiones. Para más información, vea [Administrar el filtrado de conexiones en servidores de transporte perimetral](manage-connection-filtering-on-edge-transport-servers-exchange-2013-help.md).

**Contenido**

IP Block list

IP Allow list

IP Block List providers

IP Allow List providers

Test IP Block List providers and IP Allow List providers

Configure connection filtering on Edge Transport servers that aren't directly connected to the Internet

## Lista de direcciones IP bloqueadas

La lista de direcciones IP bloqueadas contiene las direcciones IP de los servidores de correo electrónico que quiere bloquear. Puede mantener de forma manual las direcciones IP de la lista de IP bloqueadas. Puede agregar direcciones IP individuales o intervalos de direcciones IP. Puede especificar una fecha de expiración que especifique durante cuánto tiempo se bloqueará la entrada de dirección IP. Cuando se agote la fecha de expiración, se deshabilitará la entrada de dirección IP en la lista de IP bloqueadas.

Si el agente de filtrado de conexión encuentra la dirección IP de origen en la lista de IP bloqueadas, la conexión SMTP se cancelará después de que se procesen todos los encabezados **RCPT TO** (destinatarios del sobre) en el mensaje.

Las direcciones IP se pueden agregar automáticamente a la lista de IP bloqueadas mediante la característica Reputación del remitente del agente de análisis de protocolo. Para más información, vea [Reputación del remitente y agente de análisis de protocolo](sender-reputation-and-the-protocol-analysis-agent-exchange-2013-help.md).

## Lista de direcciones IP permitidas

La lista de direcciones IP permitidas contiene las direcciones IP de los servidores de correo electrónico que quiere designar como fuentes confiables de correo electrónico. El correo electrónico proveniente de los servidores de correo especificados en la lista de direcciones IP permitidas queda exento del procesamiento por parte de otros agentes contra correo no deseado de Exchange.

Puede mantener de forma manual las direcciones IP de la lista de IP permitidas. Puede agregar direcciones IP individuales o intervalos de direcciones IP. Puede especificar una fecha de expiración que especifique durante cuánto tiempo se admitirá la entrada de dirección IP. Cuando se agote la fecha de expiración, se deshabilitará la entrada en la lista de IP permitidas.

Volver al principio

## Proveedores de listas de IP no admitidas

Con frecuencia los proveedores de listas de IP bloqueadas se conocen como *listas de bloqueo en tiempo real* o RBL. Los proveedores de listas de IP bloqueadas compilan listas de direcciones IP de servidores de correo que envían correo no deseado. Muchos proveedores de listas de IP bloqueadas también compilan listas de direcciones IP de servidores de correo que podrían usarse para enviar correo no deseado. Entre los ejemplos se incluyen servidores de correo configurados para retransmisión abierta, proveedores de acceso a Internet (ISP) que asignan direcciones IP dinámicas e ISP que admiten tráfico de servidor de correo SMTP desde cuentas de acceso telefónico.

Cuando se configura el filtrado de conexiones para usar un proveedor de listas de IP bloqueadas, el agente de filtrado de conexiones compara la dirección IP del servidor de correo que realiza la conexión con la lista de direcciones IP en el proveedor de listas de IP bloqueadas. Si hay una coincidencia, el mensaje no se admite en la organización. Puede configurar el filtrado de conexiones para usar varios proveedores de listas de IP bloqueadas y puede asignar distintos valores de prioridad a cada proveedor.

El agente de filtrado de conexiones comprueba la dirección IP de origen en la lista de IP permitidas y la lista de IP bloqueadas. Si la dirección IP no existe en ninguna lista, el agente de filtrado de conexiones consulta al proveedor de listas de IP bloqueadas según el valor de prioridad que se le haya asignado. Si la dirección IP se define en un proveedor de listas de IP bloqueadas, el servidor de transporte perimetral espera y procesa el encabezado **RCPT TO**, responde al servidor que envía correo con un error `SMTP 550` y cierra la conexión. La conexión no se cancela inmediatamente para que se pueda registrar el intento de conexión y porque se pueden especificar destinatarios que están exentos de que los proveedores de listas de IP bloqueen sus mensajes.

La dirección IP no se define en ninguno de los proveedores de listas de IP bloqueadas, el agente de filtrado de contenido entrega el mensaje al siguiente agente de transporte en el servidor de transporte perimetral.

Para cada proveedor de listas de IP bloqueadas, puede personalizar el error `SMTP 550` que se devuelve al remitente cuando se bloquea un mensaje. Debe identificar al proveedor de listas de IP bloqueadas que identificó el origen del mensaje como correo no deseado. Si un servidor de correo de origen legítimo se identifica erróneamente como un origen de correo no deseado, el administrador puede ponerse en contacto con el proveedor de listas de IP bloqueadas y adoptar las medidas necesarias para eliminar el servidor de correo del proveedor de listas de IP bloqueadas.

Los proveedores de listas de IP bloqueadas pueden devolver códigos diferentes para identificar por qué una dirección IP está definida en sus listas. Casi todos los proveedores de listas de IP bloqueadas devuelven máscaras de bits o tipos de datos de valores absolutos. Dentro de estos tipos de datos, el proveedor de listas de IP bloqueadas puede usar varios valores para clasificar la dirección IP por tipo de amenaza.

Hay varios asuntos que se deben considerar al usar proveedores de listas de IP bloqueadas:

  - Las interrupciones o retrasos en el servicio del proveedor de listas de IP bloqueadas pueden provocar retrasos en el procesamiento de mensajes en el servidor de transporte perimetral. Siempre debe seleccionar proveedores de listas de IP bloqueadas confiables.

  - Los servidores de origen que sabe que son legítimos pueden identificarse erróneamente como orígenes de correo no deseado. Por ejemplo, el servidor de correo se puede configurar de forma involuntaria para que funcione como una retransmisión abierta. Siempre debe seleccionar proveedores de listas de IP bloqueadas que ofrezcan procedimientos claros para la evaluación y eliminación de sus servicios.

Volver al principio

## Ejemplos de máscara de bits o valor absoluto.

En esta sección, se muestra un ejemplo de los códigos de estado que devuelven la mayoría de los proveedores de listas de bloqueo. Para obtener más detalles sobre los códigos de estado que devuelve el proveedor, vea la documentación de ese proveedor en concreto.

Para los tipos de datos de máscara de bits, el servicio proveedor de listas de direcciones IP bloqueadas devuelve un código de estado 127.0.0.*x*, donde el entero *x* es cualquiera de los valores que se muestran en la siguiente tabla.

### Valores y códigos de estado de los tipos de datos de máscara de bits

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Valor</th>
<th>Código de estado</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p>La dirección IP está en una lista de direcciones IP bloqueadas.</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p>El servidor SMTP está configurado para actuar como una retransmisión abierta.</p></td>
</tr>
<tr class="odd">
<td><p>4</p></td>
<td><p>La dirección IP admite una dirección IP de marcado.</p></td>
</tr>
</tbody>
</table>


Para los tipos de valor absoluto, el proveedor de listas de IP bloqueadas devuelve respuestas explícitas que definen por qué la dirección IP está definida en sus listas de bloqueo. La siguiente tabla muestra ejemplos de valores absolutos y las respuestas explícitas.

### Valores y códigos de estado de los tipos de datos de valores absolutos

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Valor</th>
<th>Respuesta explícita</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>127.0.0.2</p></td>
<td><p>La dirección IP es un origen directo de correo no deseado.</p></td>
</tr>
<tr class="even">
<td><p>127.0.0.4</p></td>
<td><p>La dirección IP envía correos masivos.</p></td>
</tr>
<tr class="odd">
<td><p>127.0.0.5</p></td>
<td><p>Se sabe que el servidor remoto que envía el mensaje admite retransmisiones abiertas multifase.</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Proveedores de listas de IP admitidas

Los proveedores de listas de IP permitidas también se conocen como *listas seguras* o *listas blancas*. Los proveedores de listas de IP permitidas se configuran de la misma forma que los proveedores de listas de IP bloqueadas, pero los resultados son opuestos: definen direcciones IP de servidores de correo que definitivamente no están asociados con actividad de correo no deseado. Si la dirección IP del servidor de correo que realiza la conexión está definida en un proveedor de listas de IP permitidas, el mensaje queda exento del procesamiento por parte de otros agentes contra correo no deseado de Exchange. Por esta razón, los proveedores de listas de IP bloqueadas se usan con mucha más frecuencia que los proveedores de listas de IP permitidas. Elija los proveedores de listas de IP permitidas con cuidado.

Volver al principio

## Probar los proveedores de listas de IP bloqueadas y permitidas

Una vez que haya configurado el filtrado de conexiones para usar un proveedor de listas de IP bloqueadas o un proveedor de listas de IP permitidas, puede ejecutar pruebas para comprobar que los proveedores estén funcionando correctamente. Casi todos los proveedores ofrecen direcciones IP de prueba que se pueden usar para probar sus servicios. Al probar un proveedor, el agente de filtrado de conexiones emite una consulta DNS que debe dar como resultado una respuesta específica del proveedor. Para obtener más información acerca de cómo probar direcciones IP en un servicio proveedor de listas de direcciones IP bloqueadas o IP permitidas, vea[Administrar el filtrado de conexiones en servidores de transporte perimetral](manage-connection-filtering-on-edge-transport-servers-exchange-2013-help.md).

Volver al principio

## Configurar el filtrado de conexiones en servidores de transporte perimetral que no están directamente conectados a Internet

Puede usar el filtrado de conexiones en servidores de transporte perimetral que no reciben correo electrónico directamente desde Internet. En este caso, el servidor de transporte perimetral está detrás de otro servidor de correo que recibe y procesa mensajes directamente desde Internet. Por ejemplo, la organización puede enviar tráfico de correo electrónico a través de un dispositivo, servicio o servidor contra correo no deseado antes de que los mensajes lleguen al servidor de transporte perimetral. En tal caso, el agente de filtrado de conexiones debe extraer la correcta dirección IP de origen del mensaje. Para ello, el agente de filtrado de conexiones necesita analizar los valores del campo del encabezado **Received** en el encabezado de mensaje y comparar esos valores con las direcciones IP conocidas del servidor de correo que se sitúa entre el servidor de transporte perimetral e Internet.

Cada servidor de correo que acepta y retransmite un mensaje SMTP en la ruta de entrega agrega su propio campo del encabezado **Received** en el encabezado del mensaje. El encabezado **Received** normalmente contiene el nombre de dominio y la dirección IP del servidor de correo que procesó el mensaje.

Si el servidor de transporte perimetral no acepta mensajes directamente desde Internet, se debe usar el parámetro *InternalSMTPServers* en el cmdlet **Set-TransportConfig** de un servidor de buzones de correo de Exchange 2013 para identificar la dirección IP del servidor de correo que se sitúa entre el servidor de transporte perimetral e Internet. EdgeSync se encarga de replicar los datos de las direcciones IP en los servidores Transporte perimetral. Cuando el servidor de transporte perimetral recibe mensajes, el agente de filtrado de conexiones asume que una dirección IP en un campo del encabezado **Received** que no coincide con un valor especificado por el parámetro *InternalSMTPServers* es la dirección IP de origen que necesita comprobarse. Por lo tanto, es necesario especificar todos los servidores SMTP internos para que el filtrado de conexiones funcione correctamente.

Volver al principio

