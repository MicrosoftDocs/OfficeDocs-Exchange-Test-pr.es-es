---
title: 'Administrar directivas de DLP: Exchange 2013 Help'
TOCTitle: Administrar directivas de DLP
ms:assetid: ba81fabd-7f7f-4ef7-968f-ce851ada9d70
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ673559(v=EXCHG.150)
ms:contentKeyID: 49895869
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Administrar directivas de DLP

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2015-01-14_

Se pueden ver, cambiar o quitar las directivas de prevención contra la pérdida de datos (DLP) existentes en Microsoft Exchange, mediante el uso del Centro de Administración de Exchange (EAC) o el Shell de Administración de Exchange.

Para otras tareas de administración relacionadas con DLP, consulte [Procedimientos de DLP](dlp-procedures-exchange-2013-help.md) (Exchange Server 2013) o [Procedimientos de DLP](https://technet.microsoft.com/es-es/library/jj938003\(v=exchg.150\)) (Exchange Online).

Para obtener más información acerca del comando de Shell de administración de Exchange, consulte [Usar Powershell con Exchange 2013 (Shell de administración de Exchange)](https://technet.microsoft.com/es-es/library/bb123778\(v=exchg.150\)).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 15-60 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Prevención de pérdida de datos (DLP)" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Para cualquier directiva de DLP, se puede seleccionar uno de tres modos:
    
      -    **Exigir**   Se evalúan las reglas dentro de la directiva para todos los mensajes y tipos de archivos compatibles. Se puede alterar el flujo de correo si se detecta que los datos cumplen con las condiciones de la directiva. Se toman todas las acciones descritas en la directiva.
    
      -    **Probar la directiva de DLP con sugerencias de directiva**   Se evalúan las reglas dentro de la directiva para todos los mensajes y tipos de archivos compatibles. No se podrá alterar el flujo de correo si se detecta que los datos cumplen con las condiciones de la directiva. Es decir, los mensajes no están bloqueados. Si se configuran los consejos de política, se muestran a los usuarios.
    
      -    **Probar la directiva de DLP sin sugerencias de directiva**   Se evalúan las reglas dentro de la directiva para todos los mensajes y tipos de archivos compatibles. No se podrá alterar el flujo de correo si se detecta que los datos cumplen con las condiciones de la directiva. Es decir, los mensajes no están bloqueados. Si se configuran los consejos de política, no se muestran a los usuarios.

  - Una regla individual dentro de una directiva de DPL puede tener su propia configuración del modo. Cuando el modo de una directiva es diferente del modo de una regla dentro de dicha directiva, la configuración de la regla tiene prioridad y se evaluará de acuerdo con su modo.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Ver los detalles de una directiva de DLP existente

Debe consultar las reglas y acciones de la directiva de DLP existente que ya ha establecido para su organización. Esto puede ser útil si experimenta problemas de flujo inesperado de correo electrónico o si su organización cambia la manera en que debe supervisarse la información confidencial.

## Use EAC para ver los detalles dentro de una directiva existente de DLP

1.  En el EAC, desplácese hasta **Administración del cumplimiento** \> **Prevención contra la pérdida de datos**.

2.  Haga doble clic en una de las directivas que aparecen en su lista de directivas o resalte un elemento y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Editar directiva de DLP**, haga clic en **Reglas**.


> [!TIP]
> Puede crear una directiva de DLP y dejarla en modo no activado o deshabilitado. De este modo, no se aplica una directiva y usted puede cambiar los predicados, las acciones o los valores asociados con las reglas antes de iniciar la prueba o comenzar a aplicarla.



## Uso del Shell para ver los detalles dentro de una directiva de DLP existente

En este ejemplo se muestra información sobre la directiva de DLP ficticia denominada Números de empleado. El comando se canaliza en el cmdlet **Format-List** para mostrar la configuración detallada de la directiva DLP especificada.

    Get-DlpPolicy "Employee Numbers" | Format-List

Para obtener información acerca de la sintaxis y los parámetros, consulte [Get-DlpPolicy](https://technet.microsoft.com/es-es/library/jj215752\(v=exchg.150\)).

## Cambiar una directiva de DLP

Puede cambiar una directiva de DLP existente al modificar el nombre de la directiva o las reglas que controlan los efectos de la directiva. Un ejemplo de cambio de regla podría incluir agregar texto de aviso legal personalizado al cuerpo de un mensaje y protección de RMS para mensajes enviados dentro de un dominio específico y que se detecta que incluyen información confidencial. Si está usando plantillas de directivas de DLP, tenga en cuenta que éstas son solo una de las características en Exchange 2013 que pueden ayudar a diseñar y aplicar una directiva sólida y un sistema de cumplimiento para su entorno de mensajería.

## Uso del EAC para cambiar una directiva de DLP existente

1.  En el EAC, desplácese hasta **Administración del cumplimiento** \> **Prevención contra la pérdida de datos**.

2.  Haga doble clic en una de las directivas basadas en plantillas que aparecen en su lista de directivas o resalte un elemento y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Editar directiva de DLP**, haga clic en **Reglas**.

4.  Para cambiar una regla existente, resalte la regla y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

5.  Para agregar una nueva regla en blanco que puede personalizar totalmente, haga clic en **Nuevo**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

6.  Para agregar una regla acerca de la notificación del remitente, bloqueo de mensajes o concesión de sobrescritura, haga clic en la flecha junto al icono **Nuevo**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

7.  Para eliminar una regla, resáltela y haga clic en **Eliminar**![Eliminar icono](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Eliminar icono").

8.  Haga clic en **Guardar** para terminar de modificar la directiva y guardar los cambios.

## Uso del Shell para cambiar una directiva de DLP existente

Se puede especificar la acción y el nivel de notificación de una directiva mediante el uso del Shell de Administración de Exchange. En este ejemplo se configura el modo de una directiva de DPL ficticia denominada Números de empleado para que no se apliquen las acciones y no se muestren los mensajes de notificación.

    Set-DlpPolicy "Employee Numbers" -Mode Audit

Para obtener información acerca de la sintaxis y los parámetros, consulte [Set-DlpPolicy](https://technet.microsoft.com/es-es/library/jj215778\(v=exchg.150\)).

## Eliminar una directiva de DLP

Se puede eliminar permanentemente una política de DLP con el EAC. Una vez que haya eliminado una directiva, esta ya no se aplicará y no se guardará ninguna de las reglas o acciones.

Como opción, puede configurar el estado o modo operativo de una directiva en **Probar la directiva de DLP sin sugerencias de directivas**. De esta manera detiene su aplicación en el entorno de su mensaje pero preserva los valores de configuración detallados de la directiva misma. Esto puede ser útil si existe la posibilidad de que deba aplicar la directiva nuevamente en el futuro.

## Uso del EAC para eliminar una directiva de DLP existente

1.  En el EAC, desplácese hasta **Administración del cumplimiento** \> **Prevención contra la pérdida de datos**.

2.  Seleccione la directiva que quiere quitar de su lista de directivas y luego haga clic en **Eliminar**![Eliminar icono](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Eliminar icono").

## Uso del Shell para eliminar una directiva de DLP existente

En este ejemplo se elimina la directiva de DLP ficticia denominada Números de empleado.

    Remove-DlpPolicy "Employee Numbers"

Para obtener información acerca de la sintaxis y los parámetros, consulte [Remove-DlpPolicy](https://technet.microsoft.com/es-es/library/jj215677\(v=exchg.150\)).

## Más información

[Prevención de pérdida de datos](https://docs.microsoft.com/es-es/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention)

[Sugerencias de directiva](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/set-up-outlook-voice-access)

