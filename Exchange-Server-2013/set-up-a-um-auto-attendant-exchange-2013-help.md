---
title: 'Configurar un operador automático de mensajería unificada: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Configuración de un operador automático de mensajería unificada
ms:assetid: 0a3492f8-8aba-4904-96fd-6e023175012a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ673508(v=EXCHG.150)
ms:contentKeyID: 49895461
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuración de un operador automático de mensajería unificada

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2015-03-09_

Además de permitir a los usuarios aacceder al correo de voz, la mensajería unificada (MU) le permite crear uno o más Operadores automáticos de mensajería unificada según las necesidades de su organización. Los operadores automáticos de mensajería unificada se pueden utilizar para crear los sistemas de menú de voz de una organización que permiten a los autores de llamadas, tanto internas como externas, localizar, colocar o transferir llamadas a los usuarios o departamentos de la empresa en una organización.

Para conocer tareas de administración adicionales relacionadas con los operadores automáticos de mensajería unificada, consulte [Procedimientos operador automático de mensajería unificada](um-auto-attendant-procedures-exchange-2013-help.md).

## Operadores automáticos

En los entornos de telefonía o mensajería unificada, un operador automático o sistema de menús de operadores automáticos transfiere las llamadas entrantes a la extensión de un usuario o departamento, sin la intervención de un recepcionista ni operador. En muchos sistemas de operadores automáticos, se puede poner en contacto con un recepcionista u operador presionando o diciendo cero. En algunos sistemas de operadores automáticos, hay menús informativos de sólo mensajes y menús de voz para que la organización pueda proporcionar información sobre los horarios de apertura, cómo llegar a las instalaciones, las oportunidades laborales y respuestas a otras preguntas frecuentes. Una vez reproducido el mensaje, la persona que llama es dirigida al recepcionista u operador, o puede volver al menú principal.

Aunque los operadores automáticos pueden ser muy útiles, si no están diseñados y configurados correctamente, pueden confundir y frustrar a los que realizan llamadas. Por ejemplo, especialmente en organizaciones de gran tamaño, si los operadores automáticos no están diseñados correctamente, la persona que llama puede tener que pasar a lo largo de una serie inacabable de preguntas e instrucciones del menú, antes de que se le transfiera finalmente a una persona para que responda a sus preguntas.

## ¿Cómo configuro un operador automático?

En el Centro de administración de Exchange (EAC), los operadores automáticos de mensajería unificada se configuran y administran para atender automáticamente las llamadas recibidas en su organización y permitir a los autores de llamadas seleccionar distintas opciones mediante las teclas de su teléfono. Puede tener un solo operador automático de mensajería unificada que proporcione la navegación básica de menús para los autores de llamadas a su organización, o puede tener varios operadores automáticos anidados y con bifurcaciones que les proporcionen una experiencia más completa. Sin embargo, en ambos casos, debe planificar y configurar los operadores automáticos detenidamente.

Para planificar y crear una nueva estructura de operadores automáticos de mensajería unificada, debe realizar lo siguiente:

1.  Decidir si desea permitir a los usuarios interactuar con el operador automático con entradas de voz.

2.  Decidir el idioma que desea usar para el operador automático principal y si debe crear otros operadores automáticos para aceptar más idiomas.

3.  Decidir el horario comercial y el horario no comercial del operador automático y establecer el horario laboral usando **Horario comercial**. Aunque no es necesario, también puede decidir la programación de vacaciones de este operador automático.
    

    > [!NOTE]
    > También debería establecer la zona horaria del operador.



4.  Decidir si desea los saludos estándar generados por el sistema en horario comercial y en no horario comercial o si desea crear grabaciones personalizadas para los mismos.
    
    Si desea usar saludos personalizados, planifique y grabe sus saludos en horario comercial y en horario no comercial para reproducirlos a los autores de llamadas durante el horario comercial y el horario no comercial. Si lo necesita, también puede crear un saludo de aviso informativo personalizado. Por ejemplo, para su saludo en horario comercial podría usar “Bienvenido a Contoso. Para inglés, pulse o diga 1, para español, pulse o diga 2.” Para el saludo del horario no comercial, podría grabar el texto siguiente: "Bienvenido a Contoso. En este momento, nuestra oficina está cerrada. Estaremos abiertos el lunes a las 8:00."

5.  Planee la estructura de operadores automáticos según sus necesidades empresariales. Por ejemplo, una organización puede que sea una empresa multinacional con oficinas en Alemania y en el Reino Unido, por lo cual necesitará una estructura de operadores automáticos basada en varios idiomas. Otra organización puede que tenga su oficina corporativa en una sede, el departamento de ventas en otra sede y el servicio de soporte técnico en una tercera sede, lo que implica tener un operador automático directamente relacionado con la estructura de la organización.

6.  Decida si necesitará operadores automáticos de reserva DTMF u otros operadores para usarlos si los comandos de voz de los operadores automáticos no funcionan.

7.  Planifique la navegación de menús para el horario comercial y el horario no comercial. Para cada operador automático, incluyendo los operadores automáticos DTMF, deberá planificar y configurar instrucciones del menú y entradas del menú de navegación. Deberá hacerlo para el horario comercial y el horario no comercial.

8.  La hoja de cálculo siguiente contiene un ejemplo que puede utilizar para planear la navegación de menús fuera del horario comercial.
    
    
    <table>
    <colgroup>
    <col style="width: 33%" />
    <col style="width: 33%" />
    <col style="width: 33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><strong>Tecla</strong></th>
    <th><strong>Nombre de la entrada del menú de navegación/instrucciones</strong></th>
    <th><strong>Respuesta que se debe grabar</strong></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>1</p></td>
    <td><p>Selección de idioma a usar inglés.</p></td>
    <td><p>“Pulse o diga 1 para usar inglés.”</p></td>
    </tr>
    <tr class="even">
    <td><p>2</p></td>
    <td><p>Saldo de cuenta</p></td>
    <td><p>“Pulse o diga 2 para obtener su saldo de cuenta.”</p></td>
    </tr>
    <tr class="odd">
    <td><p>3</p></td>
    <td><p>Transferir a ventas</p></td>
    <td><p>&quot;Pulse o diga 3 para pasar a nuestro departamento de ventas.&quot;</p></td>
    </tr>
    <tr class="even">
    <td><p>4</p></td>
    <td><p>Transferencia al servicio de soporte técnico</p></td>
    <td><p>“Pulse o diga 4 para ser transferido a un representante del servicio de soporte técnico.”</p></td>
    </tr>
    <tr class="odd">
    <td><p>5</p></td>
    <td><p>Horario comercial</p></td>
    <td><p>No es necesaria ninguna respuesta.</p></td>
    </tr>
    <tr class="even">
    <td><p>6</p></td>
    <td><p>Ubicación de la empresa</p></td>
    <td><p>No es necesaria ninguna respuesta.</p></td>
    </tr>
    </tbody>
    </table>


9.  Utilizando su plan de navegación de menús, grabe mensajes de asistencia de voz que informen a los autores de llamadas de lo que pueden hacer. Por ejemplo, para la navegación de menús para horario no comercial mostrada en la tabla, podría grabar el script siguiente: Por ejemplo, para la navegación de menús para horario no comercial mostrada en la tabla, podría grabar el texto siguiente: "Para dejar un mensaje para Ventas, presione uno. Para conocer nuestro horario comercial, presione dos. Para conocer nuestra dirección, presione tres."

10. Determine cómo los autores de llamadas accederán a la organización. Considere cómo buscarán y contactarán con los usuarios de su organización. Plantéese también cómo transferir a los autores de llamadas, cómo accederán a una persona o a un representante de la organización y si accederán al operador durante el horario comercial o el horario no comercial.

11. Determine qué llamadas permitirá que realicen los autores de llamadas cuando usen un operador automático concreto. Por ejemplo, si desea permitir a los llamantes que realicen llamadas en un único plan de marcado, a una extensión, o si les permitirá realizar llamadas fuera de la organización.

12. Después de haber planeado su configuración de operadores automáticos, saludos y navegación de menús y haber creado los archivos de audio que contienen grabaciones con sus saludos, mensajes de asistencia de voz de navegación, instrucciones del menú de navegación y respuestas para la navegación por los menús, estará listo para crear y configurar su operador automático. Aquí se muestra cómo:
    
      - [Crear un operador automático de mensajería unificada](create-a-um-auto-attendant-exchange-2013-help.md)
    
      - [Administrar a un operador automático de mensajería unificada](manage-a-um-auto-attendant-exchange-2013-help.md)

13. Si ha creado la estructura y la configuración de operadores automáticos, habilite el operador automático de mensajería unificada para que empiece a aceptar llamadas.

