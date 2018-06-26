---
title: 'Probar una regla de flujo de correo: Exchange 2013 Help'
TOCTitle: Probar una regla de flujo de correo
ms:assetid: 3d949e2a-8ba4-4261-8cfb-736fd2446ea1
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn831862(v=EXCHG.150)
ms:contentKeyID: 63145407
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Probar una regla de flujo de correo

 

_**Se aplica a:**Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

Cada vez que se crea una regla de flujo de correo de Exchange, se recomienda probarla antes de activarla. De este modo, si crea accidentalmente una condición que no es exactamente lo que quiere o interactúa con otras reglas de forma inesperada, no tendrá consecuencias no deseadas.


> [!IMPORTANT]
> Espere 30 minutos después de crear una regla antes de probarla. Si prueba la regla inmediatamente después de crearla, puede producirse un comportamiento incoherente. Si está usando Exchange Server y dispone de varios servidores de Exchange, se puede necesitar incluso más tiempo para que todos los servidores reciban la regla.



## Paso 1: crear una regla en modo de prueba

Para evaluar las condiciones de una regla sin realizar acciones que afecten al flujo de correo, seleccione un modo de prueba. Puede configurar una regla para recibir una notificación por correo electrónico cada vez que se cumple la regla, o bien puede consultar Examinar el seguimiento de mensajes para los mensajes que pueden cumplir con la regla. Existen dos modos de prueba:

  - **Probar sin sugerencias de directivas**   Use este modo junto con una acción de informe de incidentes y podrá recibir un mensaje de correo electrónico cada vez que un correo electrónico cumpla con la regla.

  - **Probar con sugerencias de directivas**   Este modo solo está disponible si usa [Prevención de pérdida de datos](technical-overview-of-dlp-data-loss-prevention-in-exchange.md) (DLP), que viene con algunos planes de suscripción a Exchange Online y Exchange Online Protection (EOP). Con este modo, un mensaje se establece en el remitente cuando el mensaje que envía coincide con una directiva, pero no se realiza ninguna acción de flujo de correo.

Esto es lo que verá cuando se cumpla una regla si incluye la acción de informe de incidentes:

![Mensaje enviado cuando se detecta la regla](images/Dn831862.c1a2db60-3fb9-4ddc-86d5-1757e2250f59(EXCHG.150).png "Mensaje enviado cuando se detecta la regla")

**Usar el modo de prueba con una acción de informe de incidentes**

1.  En el Centro de administración de Exchange (EAC), vaya a **Flujo de correo** \> **Reglas**.

2.  Cree una regla nueva o seleccione una regla existente y, a continuación, seleccione **Editar**.

3.  Desplácese hacia abajo hasta la sección **Elegir un modo para esta regla** y, a continuación, seleccione **Probar sin sugerencias de directivas** o **Probar con sugerencias de directivas**.

4.  Agregar una acción de informe de incidentes:
    
    1.  Seleccione **Agregar acción** o, si no está visible, seleccione **Más opciones** y, a continuación, seleccione **Agregar acción**.
    
    2.  Seleccione **Generar informe de incidentes y enviarlo a**.
    
    3.  Haga clic en **Seleccionar uno** y selecciónese a usted mismo o a otra persona.
    
    4.  Seleccione **Incluye las propiedades del mensaje** y, a continuación, seleccione las propiedades del mensaje que desea incluir en el correo electrónico que reciba. Si no selecciona ninguna, seguirá recibiendo un mensaje de correo cuando se cumpla la regla.

5.  Seleccione **Guardar**.

## Paso 2: evaluar si la regla hace lo que desea

Para probar una regla, puede enviar suficientes mensajes de prueba para confirmar que sucede lo que espera, o bien puede buscar en el seguimiento de mensajes los mensajes enviados por los usuarios de la organización. Asegúrese de evaluar los siguientes tipos de mensajes:

  - Mensajes que espera que cumplan la regla

  - Mensajes que no espera que cumplan la regla

  - Mensajes enviados a personas y por personas de su organización

  - Mensajes enviados a personas y por personas fuera de su organización

  - Respuestas a los mensajes que cumplen la regla

  - Mensajes que pueden provocar interacciones entre varias reglas

## Sugerencias para enviar mensajes de prueba

Una manera de probar es iniciar sesión como el remitente y el destinatario de un mensaje de prueba.

  - Si no tiene acceso a varias cuentas en su organización, puede probar en una [cuenta de prueba de Office 365](https://go.microsoft.com/fwlink/p/?linkid=402791) o crear temporalmente algunos usuarios falsos en la organización.

  - Como por lo general un explorador web no permite tener sesiones abiertas simultáneamente en el mismo equipo que inició sesión en varias cuentas, puede usar la [exploración de InPrivate en Internet Explorer](https://go.microsoft.com/fwlink/p/?linkid=402784), o bien un equipo, un dispositivo o un explorador web diferente para cada usuario.

## Examinar el seguimiento de mensajes

El seguimiento de mensajes incluye una entrada para cada regla que se cumple para el mensaje y una entrada para cada acción de la regla. Esto resulta útil para controlar lo que sucede con los mensajes de prueba y también para controlar lo que sucede con los mensajes reales que pasan a través de la organización.

![Traza de mensaje que muestra las acciones de regla de transporte](images/Dn831862.64179f28-5c8c-421b-b630-cc1f7de9a34f(EXCHG.150).png "Traza de mensaje que muestra las acciones de regla de transporte")

1.  En el EAC, vaya a **Flujo de correo** \> **Seguimiento de mensajes**.

2.  Busque los mensajes que desea rastrear con criterios como el remitente y la fecha de envío. Para obtener ayuda sobre cómo especificar criterios, vea [Ejecutar un seguimiento de mensajes y ver los resultados](https://technet.microsoft.com/es-es/library/jj200712\(v=exchg.150\)).

3.  Después de localizar el mensaje que desea rastrear, haga doble clic en él para ver los detalles sobre el mensaje.

4.  Busque **Regla de transporte** en la columna **Evento**. En la columna **Acción** se muestra la acción concreta realizada.

## Paso 3: cuando las pruebas hayan terminado, establecer la regla para exigir

1.  En el EAC, vaya a **Flujo de correo** \> **Reglas**.

2.  Seleccione una regla y, a continuación, seleccione **Editar**.

3.  Seleccione **Exigir**.

4.  Si usó una acción para generar un informe de incidentes, seleccione la acción y, a continuación, seleccione **Quitar**.

5.  Seleccione **Guardar**.


> [!TIP]
> Para evitar sorpresas, informe a los usuarios sobre las reglas nuevas.



## Sugerencias de solución del problema

Estos son algunos problemas comunes y sus soluciones:

  - **Todo parece correcto, pero la regla no funciona.**
    
    En ocasiones se necesitan más de 15 minutos para que un flujo de correo nuevo esté disponible. Espere unas cuantas horas y, después, vuelva a probar. Compruebe también si otra regla podría estar interfiriendo. Intente cambiar esta regla a prioridad 0 moviéndola a la parte superior de la lista.

  - **Se agrega un aviso de declinación de responsabilidades al mensaje original y todas las respuestas, en lugar de simplemente al mensaje original.**
    
    Para evitar esto, puede agregar una excepción a la regla del aviso de declinación de responsabilidades para buscar una frase única en el aviso.

  - **Mi regla tiene dos condiciones y deseo que la acción se produzca cuando se cumpla alguna de las condiciones, pero se produce cuando se cumplen ambas condiciones.**
    
    Debe crear dos reglas, una para cada condición. Puede copiar la regla fácilmente seleccionando **Copiar** y después puede quitar una condición del original y la otra condición de la copia.

  - **Trabajo con grupos de distribución y** **El remitente es** (**SentTo**) **no parece funcionar.**
    
    **SentTo** coincide con los mensajes en los que uno de los destinatarios es un buzón, un usuario habilitado para correo o un contacto, pero no se puede especificar un grupo de distribución con esta condición. En su lugar, use **El cuadro Para contiene un miembro de este grupo** (**SentToMemberOf**).

## Otras opciones de prueba

Si está usando Exchange Online o Exchange Online Protection, use un informe de regla para comprobar el número de veces que cada regla coincide. Para que se incluyan en los informes, una regla debe tener activada la casilla **Auditar esta regla con el nivel de gravedad**. Estos informes ayudan a detectar tendencias de uso de las reglas y a identificar las reglas que no coinciden.

Para ver un informe de reglas, en el Centro de administración de Office 365, seleccione **Informes**.


> [!NOTE]
> Aunque la mayoría de los datos del informe son de las últimas 24 horas, algunos datos pueden tardar hasta 5 días en aparecer.



![Informe que muestra el uso de la regla](images/Dn831862.df5bf202-741d-432a-b71d-b37143f0ec0a(EXCHG.150).png "Informe que muestra el uso de la regla")

Para obtener más información, vea [Ver informes de protección de correo](https://go.microsoft.com/fwlink/p/?linkid=402958).

## ¿Necesita más ayuda?

[Administrar reglas de flujo de correo](manage-mail-flow-rules-exchange-2013-help.md)

[Reglas de flujo de correo (reglas de transporte) en Exchange Online](https://technet.microsoft.com/es-es/library/jj919238\(v=exchg.150\)) (Exchange Online)

[Reglas de flujo de correo (reglas de transporte) en Exchange Online Protection](https://technet.microsoft.com/es-es/library/dn271424\(v=exchg.150\)) (Exchange Online Protection)

[Reglas de transporte o de flujo de correo](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange Server)

