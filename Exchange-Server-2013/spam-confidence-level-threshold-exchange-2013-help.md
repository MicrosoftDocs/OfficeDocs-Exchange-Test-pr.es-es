---
title: 'Umbral de nivel de confianza de correo no deseado: Exchange 2013 Help'
TOCTitle: Umbral de nivel de confianza de correo no deseado
ms:assetid: 0009b4af-be6d-41d2-98bc-b5487272c74a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa995744(v=EXCHG.150)
ms:contentKeyID: 49895428
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Umbral de nivel de confianza de correo no deseado

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-11-17_


> [!NOTE]
> El 1 de noviembre de 2016 Microsoft detuvo las actualizaciones de definiciones de correo no deseado para los filtros de SmartScreen en Exchange y Outlook. Las definiciones existentes de correo no deseado de SmartScreen permanecerán en su lugar, pero es probable que su eficacia se degrade con el tiempo. Para obtener más información, consulte <A href="https://go.microsoft.com/fwlink/p/?linkid=835894">Deprecating support for SmartScreen in Outlook and Exchange</A> (Fin del soporte de SmartScreen en Outlook y Exchange).



En Microsoft Exchange Server 2013, puede definir acciones específicas de acuerdo con los umbrales de nivel de confianza de correo no deseado (SCL). Por ejemplo, puede definir umbrales diferentes para rechazar, eliminar o poner en cuarentena mensajes en un servidor Exchange que ejecute el agente de filtrado de contenido.

La combinación de esta configuración de umbral de SCL en el agente de filtrado de contenido y la configuración de la carpeta correo electrónico no deseado de SCL en el buzón de usuario le ayuda a implementar una estrategia contra correo electrónico no deseado más general y precisa. Esta funcionalidad de ajuste del umbral SCL más precisa y detallada de Exchange 2013 puede ayudarle a reducir el costo general de implementar y mantener una solución contra correo electrónico no deseado en toda su organización de Exchange.

El agente de filtrado de contenido asigna una clasificación de SCL a los mensajes posteriormente en el ciclo contra correo electrónico no deseado, después de que otros agentes contra correo electrónico no deseado hayan procesado los mensajes entrantes. Muchos de los otros agentes contra correo electrónico no deseado que procesan los mensajes entrantes antes de que sean procesados por el agente de filtro de contenido determinan su forma de actuar sobre un mensaje. Por ejemplo, en un servidor de transporte perimetral el agente de filtrado de conexión rechaza cualquier mensaje enviado desde una dirección IP que se encuentre en una lista de bloqueo en tiempo real. El agente de filtrado de remitentes y el agente de filtrado de destinatarios procesan los mensajes de una forma igualmente determinista.

En Exchange 2013, estos agentes deterministas contra correo electrónico no deseado procesan primero los mensajes y, por tanto, reducen considerablemente el número de mensajes que debe procesar el agente de filtrado de contenido. Para obtener más información acerca del orden en el que los agentes contra correo electrónico no deseado procesan los mensajes, vea [Protección contra correo no deseado](anti-spam-protection-exchange-2013-help.md).

Como el filtrado de contenido no es un proceso exacto y determinista, es importante la posibilidad de ajustar la acción que realiza el agente de filtrado de contenido en los diferentes valores del nivel de confianza de correo no deseado. Al ajustar cuidadosamente la configuración del umbral de nivel de confianza de correo no deseado, puede minimizar lo siguiente:

  - El tamaño del almacenamiento de cuarentena de correo electrónico no deseado

  - El número de mensajes de correo electrónico legítimo erróneamente puesto en cuarentena

  - El número de mensajes de correo electrónico legítimo que llega a la carpeta Correo electrónico no deseado del usuario de Microsoft Outlook

  - El número de mensajes de correo electrónico no deseado ofensivos que llega a la carpeta Correo electrónico no deseado o a la Bandeja de entrada del usuario de Outlook

  - El número de mensajes de correo electrónico no deseado que llegan a la Bandeja de entrada del usuario de Outlook

## Acciones de umbral SCL

Al ajustar las acciones del umbral SCL, puede escalar la acción de filtrado de contenido que se realiza en los mensajes que tengan un mayor riesgo de ser correo electrónico no deseado. Para comprender esta nueva funcionalidad, resulta útil comprender las diferentes acciones del umbral SCL y cómo se implementan:

  - **Umbral de eliminación SCL**   Si el valor de SCL de un mensaje determinado es igual o superior al umbral de eliminación SCL, el agente de filtro de contenido elimina el mensaje. No hay ninguna comunicación en el nivel de protocolo que indique al sistema de envío o al remitente que el mensaje se ha eliminado. Si el valor SCL de un mensaje es inferior al valor del umbral de eliminación de SCL, el agente de filtrado de contenido no elimina el mensaje. En su lugar, compara el valor de nivel de confianza de correo no deseado con el umbral de rechazo de nivel de confianza de correo no deseado.

  - **Umbral de rechazo SCL**   Si el valor de SCL de un mensaje determinado es igual o superior al umbral de rechazo SCL, el agente de filtro de contenido elimina el mensaje y envía una respuesta de rechazo al sistema de envío. Puede personalizar la respuesta de rechazo. En algunos casos, se envía un informe de no entrega (NDR) al remitente original del mensaje. Si el valor SCL de un mensaje es inferior a los valores de umbral de eliminación y rechazo SCL, el agente de filtrado de contenido no elimina ni rechaza el mensaje. En su lugar, compara el valor del nivel de confianza de correo no deseado con el umbral de cuarentena del nivel de confianza de correo no deseado.

  - **Umbral de cuarentena SCL**   Cuando el valor de SCL de un mensaje determinado es igual o superior al umbral de cuarentena SCL, el agente de filtro de contenido envía el mensaje al buzón de cuarentena. Los administradores de correo electrónico deben revisar periódicamente el buzón de cuarentena. Si el valor SCL de un mensaje es inferior a los valores del umbral de eliminación, rechazo y cuarentena de SCL, el agente de filtrado de contenido no elimina, rechaza ni pone en cuarentena el mensaje. En su lugar, el agente de filtrado de contenido envía el mensaje al servidor Buzón de correo apropiado, donde se evalúa el valor de umbral de la carpeta Correo electrónico no deseado del nivel de confianza contra correo no deseado de cada destinatario del mensaje.

  - **Umbral de la carpeta Correo electrónico no deseado del nivel de confianza contra correo no deseado**   Si el valor SCL de un mensaje concreto supera el umbral de la carpeta Correo electrónico no deseado del nivel de confianza contra correo no deseado, el mensaje se entrega a la carpeta Correo electrónico no deseado del usuario. Si el valor SCL de un mensaje es inferior a los valores de umbral de eliminación, rechazo, cuarentena y carpeta Correo electrónico no deseado del nivel de confianza contra correo no deseado, el mensaje se entrega a la Bandeja de entrada del usuario.

El agente de filtro de contenido y la carpeta de correo electrónico no deseado procesan el valor de umbral de SCL de manera diferente. El agente de filtro de contenido lleva a cabo una acción según el valor de umbral de SCL que configure. La carpeta Correo electrónico no deseado lleva a cabo una acción según el valor de umbral de SCL que configure más 1. Por ejemplo, si configura la acción Eliminar con una SCL de 8 en el agente de filtro de contenido, se eliminarán todos los mensajes con una SCL de 8 o superior. No obstante, si configura la carpeta de correo electrónico no deseado con un valor de umbral de 4, todos los mensajes con una SCL de 5 o superior se pasan a la carpeta de correo electrónico no deseado.

Por ejemplo, si establece el umbral de eliminación de SCL en 8, el de rechazo en 7, el de cuarentena en 6 y el de la carpeta Correo electrónico no deseado del nivel de confianza contra correo no deseado en 4, todos los mensajes con un SCL de 5 o un valor inferior se entregarán en la Bandeja de entrada del usuario. Los mensajes con un valor SCL de 5 se colocan en una la carpeta Correo electrónico no deseado del usuario. Los mensajes con un valor SCL de 4 o inferior se colocan en la Bandeja de entrada del usuario.

Puede configurar los ajustes de eliminación de SCL, rechazo, cuarentena y carpeta Correo electrónico no deseado en las siguientes ubicaciones:

  - **En la configuración del agente de filtrado de contenido (configuración SCL del servidor para transporte)**   Usa el cmdlet **Set-ContentFilterConfig** para habilitar y deshabilitar y establecer los umbrales de eliminación, rechazo y cuarentena de SCL en Exchange Server donde ejecute el agente de filtrado de contenido. Con el tiempo, cuando analice la funcionalidad de correo electrónico no deseado y las métricas proporcionadas por las características de creación de registros e informes contra correo no deseado, puede realizar ajustes adicionales en esas configuraciones de umbral de nivel de confianza de correo no deseado cuando sea preciso.
    
    Los parámetros SCL disponibles en el cmdlet **Set-ContentFilterConfig** se describen en la tabla siguiente.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Parámetro</th>
    <th>Descripción</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><em>SCLDeleteEnabled</em></p></td>
    <td><p>Este parámetro habilita o deshabilita la eliminación de un mensaje sin un informe de no entrega (NDR) cuando el valor SCL del mensaje es superior o igual al valor especificado por el parámetro <em>SCLDeleteThreshold</em>. La entrada válida para este parámetro es <code>$true</code> o <code>$false</code>.</p></td>
    </tr>
    <tr class="even">
    <td><p><em>SCLDeleteThreshold</em></p></td>
    <td><p>La entrada válida para este parámetro es un número entero de 0 a 9 inclusive. El valor de este parámetro debería ser superior al de los otros parámetros del umbral SCL. Este parámetro sólo es significativo si el valor del parámetro<em>SCLDeleteEnabled</em> es <code>$true</code>.</p></td>
    </tr>
    <tr class="odd">
    <td><p><em>SCLRejectEnabled</em></p></td>
    <td><p>Este parámetro habilita o deshabilita el rechazo de un mensaje con un NDR cuando el valor SCL del mensaje es superior o igual al valor especificado por el parámetro <em>SCLRejectThreshold</em>. La entrada válida para este parámetro es <code>$true</code> o <code>$false</code>.</p></td>
    </tr>
    <tr class="even">
    <td><p><em>SCLRejectThreshold</em></p></td>
    <td><p>La entrada válida para este parámetro es un número entero de 0 a 9 inclusive. El valor de este parámetro debería se inferior al parámetro <em>SCLDeleteThreshold</em>, pero superior a los otros parámetros del umbral SCL. Este parámetro sólo es significativo si el valor del parámetro <em>SCLRejectEnabled</em> es <code>$true</code>.</p></td>
    </tr>
    <tr class="odd">
    <td><p><em>SCLQuarantineEnabled</em></p></td>
    <td><p>Este parámetro habilita o deshabilita el envío de un mensaje al buzón de cuarentena de correo no deseado cuando el valor SCL del mensaje es superior o igual al valor especificado por el parámetro <em>SCLQuarantineThreshold</em>. La entrada válida para este parámetro es <code>$true</code> o <code>$false</code>.</p>
    <p>Para obtener más información acerca del buzón de cuarentena de correo no deseado, vea <a href="spam-quarantine-exchange-2013-help.md">Cuarentena de correo electrónico no deseado</a>.</p></td>
    </tr>
    <tr class="even">
    <td><p><em>SCLQuarantineThreshold</em></p></td>
    <td><p>La entrada válida para este parámetro es un número entero de 0 a 9 inclusive. El valor de este parámetro debería ser inferior al parámetro <em>SCLRejectThreshold</em>, pero superior al parámetro <em>SCLJunkThreshold</em> en los cmdlets <strong>Set-OrganizationConfig</strong> o <strong>Set-Mailbox</strong>. Este parámetro sólo es significativo si el valor del parámetro<em>SCLQuarantineThreshold</em> es <code>$true</code>.</p></td>
    </tr>
    </tbody>
    </table>


  - **En los ajustes de configuración de la organización (configuración SCL de toda la organización)**   Use el cmdlet **Set-OrganizationConfig** para establecer el umbral de la carpeta Correo electrónico no deseado del nivel de confianza contra correo no deseado de todos los buzones de la organización.
    
    Los parámetros SCL disponibles en el cmdlet **Set-OrganizationConfig** se describen en la tabla siguiente. Para ver un ejemplo de uso de SCLJunkThreshold, vea [Establecer las configuraciones de filtro de correo no deseado en los buzones de correo](configure-anti-spam-settings-on-mailboxes-exchange-2013-help.md).
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Parámetro</th>
    <th>Descripción</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><em>SCLJunkThreshold</em></p></td>
    <td><p>Este parámetro especifica el valor SCL que un mensaje debe exceder para que el mensaje se coloque en la carpeta Correo electrónico no deseado del buzón del destinatario. La entrada válida para este parámetro es un número entero de 0 a 9 inclusive. El valor de este parámetro debería ser inferior al de los otros parámetros del umbral SCL. Por ejemplo, si especifica el valor 4, los mensajes con un valor SCL de 5 o superior se trasladan a la carpeta Correo electrónico no deseado del usuario.</p></td>
    </tr>
    </tbody>
    </table>


  - **En buzones de usuario (configuración de SCL por destinatario)**   Puede usar el cmdlet **Set-Mailbox** para habilitar o deshabilitar los umbrales de eliminación, rechazo, cuarentena y carpeta Correo electrónico no deseado de SCL por destinatario en buzones individuales. Sólo puede usar el cmdlet **Set-Mailbox** para habilitar o deshabilitar el umbral de la carpeta Correo electrónico no deseado del nivel de confianza contra correo no deseado de los buzones individuales. Los umbrales de eliminación, rechazo y cuarentena de SCL por destinatario se almacenan en Active Directory y se replican en los servidores de transporte perimetral suscritos mediante el servicio Microsoft Exchange EdgeSync. El agente de filtro de contenido usa las configuraciones de umbrales del nivel de confianza de correo no deseado por destinatario, aunque haya establecido las configuraciones del nivel de confianza de correo no deseado por servidor transporte. Por tanto, si ha establecido los umbrales del nivel de confianza de correo no deseado por destinatario, el agente de filtro de contenido usa los umbrales del nivel de confianza de correo no deseado por destinatario para usuarios específicos en lugar de la configuración del nivel de confianza de correo no deseado en dicho agente. Para ver ejemplos, vea [Establecer las configuraciones de filtro de correo no deseado en los buzones de correo](configure-anti-spam-settings-on-mailboxes-exchange-2013-help.md).
    

    > [!NOTE]
    > Los umbrales SCL por destinatario no se aplican a correos recibidos a través de grupos de distribución.

    
    Los mismos parámetros SCL están disponibles en el cmdlet **Set-Mailbox** que está disponible en los cmdlets **Set-ContentFilterConfig** y **Set-OrganizationConfig**:
    
      - *SCLDeleteEnabled*
    
      - *SCLDeleteThreshold*
    
      - *SCLRejectEnabled*
    
      - *SCLRejectThreshold*
    
      - *SCLQuarantineEnabled*
    
      - *SCLQuarantineThreshold*
    
      - *SCLJunkThreshold*
    
    Sin embargo, todos los parámetros SCL en el cmdlet **Set-Mailbox** también aceptan el valor `$null`. Si una configuración de SCL en un buzón de correo está en blanco (`$null`), la configuración del agente de filtrado de contenido correspondiente o la configuración de la organización se aplica al buzón. Si una configuración de SCL en un buzón tiene el valor de `$true` o de `$false`, la configuración en el buzón invalida la configuración correspondiente de toda la organización en el agente de filtrado de contenido o en la configuración de la organización.
    
    El parámetro SCL que sólo está disponible en el cmdlet **Set-Mailbox** se describe en la tabla siguiente.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Parámetro</th>
    <th>Descripción</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><em>SCLJunkEnabled</em></p></td>
    <td><p>Este parámetro habilita o deshabilita el envío de un mensaje a la carpeta Correo electrónico no deseado del usuario cuando el valor SCL del mensaje es superior o igual al valor especificado por el parámetro <em>SCLQuarantineThreshold</em>. La entrada válida para este parámetro es <code>$true</code>, <code>$false</code> o <code>$null</code>.</p>
    <p>Tenga en cuenta que el filtrado de correo electrónico no deseado está habilitado de forma predeterminada para todos los buzones de correo de usuario de la organización. De forma predeterminada, el parámetro <em>Enabled</em> se establece en el valor <code>$true</code> en el cmdlet <strong>Set-MailboxJunkEmailConfiguration</strong> para todos los buzones de correo de usuario.</p></td>
    </tr>
    </tbody>
    </table>
    
    Para obtener más información acerca de la configuración de los umbrales SCL en un buzón de correo, vea [Establecer las configuraciones de filtro de correo no deseado en los buzones de correo](configure-anti-spam-settings-on-mailboxes-exchange-2013-help.md).

## Supervisión de los umbrales SCL

Puede usar varios scripts integrados ubicados en la carpeta `%ExchangeInstallPath%Scripts`, como **get-AntispamSCLHistogram.ps1**, para recopilar datos de resultados de filtrado. Si los datos indican que debe realizar ajustes inmediatos, vuelva a configurar dichos umbrales. En caso contrario, recopile los datos y analice los informes de correo electrónico no deseado para determinar si son necesarios los ajustes.

