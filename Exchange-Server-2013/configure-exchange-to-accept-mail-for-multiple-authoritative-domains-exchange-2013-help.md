---
title: 'Configurar Exchange para aceptar correo de varios dominios autoritativos'
TOCTitle: Configurar Exchange para aceptar correo de varios dominios autoritativos
ms:assetid: 11801f73-4934-4025-a1c1-3935dada7e9b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa996314(v=EXCHG.150)
ms:contentKeyID: 51406475
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar Exchange para aceptar correo de varios dominios autoritativos

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-06-15_

En Microsoft Exchange Server 2013, es fácil agregar varios dominios autoritativos en la organización. Tras agregar un dominio autoritativo, tendrá que decidir cómo usarlo en la organización. Por ejemplo:

  - Si quiere agregar una dirección de correo en el dominio autoritativo para los destinatarios de la organización, ¿prefiere sustituir la dirección principal existente (responder a) de los destinatarios o agregar la nueva dirección de correo como dirección proxy (secundaria)?

  - ¿Quiere que la dirección de correo del nuevo dominio autoritativo se aplique a todos los destinatarios y a todos los tipos de destinatarios? ¿O quiere que la dirección de correo nueva se aplique a determinados tipos de destinatarios o a destinatarios concretos en función de sus propiedades de usuario, por ejemplo, solo a los usuarios del Departamento de finanzas?

A continuación, se muestran ejemplos de escenarios en los que es posible que la organización de Exchange tenga que recibir y procesar correo de más de un dominio SMTP autoritativo:

  - Está cambiando el nombre del dominio SMTP, pero tiene que seguir aceptando correos del nombre de dominio antiguo durante un tiempo por si acaso los clientes envían mensajes de correo a las direcciones anteriores. Puede establecer la nueva dirección de correo como dirección principal (responder a). De este modo, la dirección nueva será la dirección de correo predeterminada que se mostrará en todos los mensajes de correo que envíe el destinatario. Puede establecer la antigua dirección de correo como dirección secundaria. Esto permitirá al destinatario seguir recibiendo correos enviados a la antigua dirección.

  - Quiere aprovisionar diferentes direcciones de correo para las unidades empresariales de su organización. Por ejemplo, si el bosque de Active Directory «contoso.com» incluye subdominios para las subsidiarias Tailspin Toys y Fourth Coffee, es posible que quiera asignar los nombres de dominio SMTP contoso.com, tailspintoys.com y fourthcoffee.com a los destinatarios de las respectivas unidades empresariales.

  - Proporciona servicios de hospedaje de correo y tiene que aceptar correo de más de un nombre de dominio SMTP.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar esta tarea: 30 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada «Dominios aceptados» en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md) y la entrada «Directivas de direcciones de correo electrónico» en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Si tiene un servidor Transporte perimetral con suscripción en la red perimetral, puede configurar dominios aceptados en un servidor de buzones de la organización de Exchange. La configuración de los dominios aceptados se replica al servidor Transporte perimetral durante la sincronización de EdgeSync. Para obtener más información, consulte [Suscripciones perimetrales](edge-subscriptions-exchange-2013-help.md).

  - Al crear un dominio aceptado, puede usar un carácter comodín (\*) en el espacio de direcciones para indicar que todos los subdominios del espacio de direcciones SMTP también son aceptados por la organización de Exchange. Por ejemplo, para configurar contoso.com y todos sus subdominios como dominios aceptados, escriba **\*.contoso.com** como espacio de direcciones SMTP. No obstante, si los nombres de los subdominios se van a usar en una directiva de direcciones de correo, cada subdominio debe tener una entrada de dominio aceptada explícita.

  - Se necesita un registro MX de DNS público para cada dominio SMTP del que quiera aceptar correo de Internet. Deberá resolver los registros MX para el servidor con conexión a Internet que reciba correo electrónico para la organización.

  - Debe configurar los conectores de envío y de recepción para que la organización de Exchange pueda enviar y recibir correo de Internet.La configuración de los conectores de envío y los conectores de recepción de Internet está determinada por la topología de Exchange. Para más información sobre la configuración de los conectores, consulte [Conectores](connectors-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Cómo realiza esto?

## Paso 1: Crear un dominio autoritativo

## Usar el Centro de administración de Exchange para crear un dominio autoritativo

1.  En el EAC, vaya a **Flujo de correo** \> **Dominios aceptados** y haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

2.  En el campo **Nombre**, escriba el nombre para mostrar del dominio aceptado. Cada dominio aceptado para su organización debe tener un nombre único. Puede ser diferente del nombre del dominio aceptado. Por ejemplo, el dominio contoso.com puede tener el nombre para mostrar Contoso Local Accepted Domain.

3.  En el campo **Dominio aceptado**, especifique un nombre de espacio SMTP para el que la organización acepta mensajes de correo. Por ejemplo, contoso.com.

4.  Seleccione **Dominio autoritativo**.

5.  Haga clic en **Guardar**.

## Usar el Shell para crear un dominio autoritativo

Para crear un nuevo dominio autoritativo, use la siguiente sintaxis.

    New-AcceptedDomain -Name "<Unique Name>" -DomainName <SMTP domain> -DomainType Authoritative

Por ejemplo, para crear un nuevo dominio autoritativo llamado «Fourth Coffee subsidiary» para el dominio fourthcoffee.com, ejecute el siguiente comando:

    New-AcceptedDomain -Name "Fourth Coffee subsidiary" -DomainName fourthcoffee.com -DomainType Authoritative

## ¿Cómo sabe si este paso se ha completado correctamente?

Para comprobar que el dominio autoritativo se creó correctamente, siga uno de estos pasos:

  - En el EAC, vaya a **Flujo de correo** \> **Dominios aceptados**. Compruebe que el dominio aceptado que ha creado aparece y que el valor de **Tipo de dominio** es **Autoritativo**.

  - En el Shell, ejecute el comando **Get-AcceptedDomain**. Compruebe que el dominio que ha creado aparece y que el valor de **DomainType** es `Authoritative`.

## Paso 2: Configurar una directiva de direcciones de correo para el dominio autoritativo

Para usar el dominio autoritativo aceptado que ha creado, debe configurar una directiva de direcciones de correo para el dominio que cumpla con los objetivos que requiere su escenario. Por ejemplo, puede necesitar crear una nueva directiva de direcciones de correo o modificar una existente. Puede sustituir la dirección de correo principal para algunos o todos los destinatarios, y puede conservar o quitar la antigua. En esta sección se presentan dos escenarios de ejemplo.

## Cambiar la dirección de correo principal existente

Para cambiar la dirección de correo principal (responder a) asignada a los destinatarios y mantener la dirección de correo antigua como dirección proxy (secundaria), siga estos pasos:

## Usar el EAC para cambiar la dirección de correo principal existente

1.  En el EAC, vaya a **Flujo de correo** \> **Directivas de direcciones de correo**. Seleccione la directiva de direcciones de correo que quiere modificar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Directiva de direcciones de correo**, haga clic en la pestaña **Formato de dirección de correo**. En la sección **Formato de dirección de correo**, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

3.  En la página **Formato de dirección de correo** que aparece, haga las selecciones siguientes:
    
      - **Seleccionar un dominio aceptado**   Haga clic en la lista desplegable y seleccione el nuevo dominio autoritativo.
    
      - Seleccione **Hacer que este sea el formato de dirección de correo de respuesta**.
    
    When you are finished, click **Save**.

4.  En la página **Directiva de dirección de correo**, haga clic en **Guardar** para guardar los cambios en la directiva.

5.  Se mostrará una advertencia que indicará que la directiva de direcciones de correo electrónico no se aplicará hasta que la actualice. Una vez creada, selecciónela y, a continuación, haga clic en **Aplicar** en el panel de detalles.

## Usar el Shell para cambiar la dirección de correo principal existente

En el Shell, se usan dos comandos diferentes: un comando para modificar la directiva de direcciones de correo existente y otro para aplicar la directiva de direcciones de correo actualizada a los destinatarios de su organización.

Para cambiar la dirección de correo principal existente y conservar la antigua como dirección proxy, ejecute el comando siguiente:

    Set-EmailAddressPolicy <EmailAddressPolicyIdentity> -EnabledEmailAddressTemplates SMTP:<NewPrimaryEmailAddress>,smtp:<OldPrimaryEmailAddress>

Por ejemplo, supongamos que la directiva de direcciones de correo de la organización usa el formato de direcciones de correo *useralias*`@contoso.com`. En este ejemplo se modifica el dominio de la dirección principal (responder a) de la directiva de direcciones de correo denominada «Default Policy» a `@fourthcoffee.com` y se mantiene la antigua dirección principal de respuesta en el dominio `@contoso.com` como dirección proxy (secundaria).

    Set-EmailAddressPolicy "Default Policy" -EnabledEmailAddressTemplates SMTP:@fourthcoffee.com,smtp:@contoso.com


> [!NOTE]
> El calificador <CODE>SMTP</CODE> en mayúsculas especifica la dirección principal (responder a). El calificador <CODE>smtp</CODE> en minúsculas especifica una dirección proxy (secundaria).



Para aplicar la directiva de direcciones de correo actualizada a los destinatarios, use la sintaxis siguiente.

    Update-EmailAddressPolicy <EamilAddressPolicyIdentity>

Por ejemplo, para aplicar la directiva de direcciones de correo actualizada denominada «Default Policy», hay que ejecutar el siguiente comando:

    Update-EmailAddressPolicy "Default Policy"

## Sustituir la dirección de correo principal existente por un conjunto filtrado de destinatarios

No se puede modificar la directiva de direcciones de correo predeterminada para aplicarla a un conjunto filtrado de destinatarios. Debe crear una nueva directiva de direcciones de correo o modificar una existente. En los ejemplos de esta sección se crea una nueva directiva de direcciones de correo. En estos ejemplos, la dirección principal (responder a) del nuevo dominio aceptado sustituye a la antigua dirección principal para los destinatarios especificados sin conservar la antigua dirección principal como dirección de correo proxy (secundaria). Por tanto, los destinatarios afectados ya no podrán recibir correo en su antigua dirección de correo principal.

Además, las directivas de direcciones de correo que se aplican a determinados usuarios deben tener una prioridad más alta (indicada por un valor entero inferior) que la de otras directivas de direcciones de correo, incluida la directiva predeterminada, para que se aplique primero la directiva en cuestión. Dado que dos directivas no pueden tener el mismo valor de prioridad, primero debe disminuir la prioridad de la directiva de direcciones de correo predeterminada de la organización.

## Usar el EAC para cambiar la dirección de correo principal existente por un conjunto filtrado de destinatarios

Para crear direcciones de correo adicionales que se usarán como dirección de correo primaria para un conjunto filtrado de destinatarios, siga estos pasos.

1.  En el EAC, vaya a **Flujo de correo** \> **Directivas de direcciones de correo** y, luego, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

2.  En la página **Directiva de direcciones de correo**, complete los campos siguientes:
    
    1.  **Nombre de la Directiva**   Introduzca un nombre único y descriptivo.
    
    2.  **Formato de dirección de correo**   Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). En la página **Formato de dirección de correo** que aparece, haga las selecciones siguientes:
        
          - **Seleccionar un dominio aceptado**  Haga clic en la lista desplegable y seleccione el nuevo dominio autoritativo.
        
          - **Formato de dirección de correo**   Seleccione el formato de dirección de correo adecuado para la organización.
        
          - Seleccione **Hacer que este sea el formato de dirección de correo de respuesta**.
        
        When you are finished, click **Save**.

3.  **Ejecutar esta directiva en esta secuencia con otras directivas**   Normalmente, las directivas que se aplican a determinados usuarios deben tener una prioridad superior (indicada por un valor entero inferior) a las de otras directivas de direcciones de correo, incluida la directiva predeterminada.

4.  **Especificar los tipos de destinatarios a los que se aplica esta dirección de correo**   Seleccione los tipos de destinatarios a los que quiere que se aplique esta directiva de direcciones de correo.

5.  **Crear reglas para definir aún más los destinatarios a los que se aplica esta directiva de direcciones de correo**   Haga clic en **Agregar una regla** para restringir los destinatarios a los que se aplicará esta directiva. Esto crea una declaración **And** booleana. Repita este paso tantas veces como sea necesario.
    

    > [!WARNING]
    > Si aplica demasiadas reglas, es posible restringir la directiva de direcciones de correo electrónico hasta que no contenga ningún usuario.



6.  Haga clic en **Vista previa de destinatarios a los que se aplica la directiva** para ver los destinatarios a quienes se aplicará esta directiva.

7.  
    
    Haga clic en **Guardar** para guardar los cambios y crear la directiva.

8.  Se mostrará una advertencia que indicará que la directiva de direcciones de correo electrónico no se aplicará hasta que la actualice. Una vez creada, selecciónela y, a continuación, haga clic en **Aplicar** en el panel de detalles.

## Usar el Shell para cambiar la dirección de correo principal existente por un conjunto filtrado de destinatarios

Para cambiar la dirección de correo principal por un conjunto filtrado de destinatarios, use el comando siguiente:

    New-EmailAddressPolicy -Name <Policy Name> -Priority <Integer> -IncludedRecipients <RecipientTypes> <Conditional Recipient Properties> -EnabledEmailAddressTemplates SMTP:@<NewPrimaryEmailAddress>

En este ejemplo se crea una directiva de direcciones de correo denominada «Fourth Coffee Recipients», se asigna esa directiva a los usuarios de buzones de correo del departamento Fourth Coffee y se define la prioridad más alta para la directiva de forma que se aplique la primera. Recuerde que la antigua dirección de correo principal no se conserva para estos destinatarios, por lo que no podrán recibir correo en sus antiguas direcciones de correo principales.

    New-EmailAddressPolicy -Name "Fourth Coffee Recipients" -Priority 1 -IncludedRecipients MailboxUsers -ConditionalDepartment "Fourth Coffee" -EnabledEmailAddressTemplates SMTP:@fourthcoffee.com

Para aplicar la nueva directiva de direcciones de correo a los destinatarios afectados, ejecute el siguiente comando:

    Update-EmailAddressPolicy "Fourth Coffee Recipients"

## ¿Cómo sabe si este paso se ha completado correctamente?

Para comprobar que ha configurado correctamente una directiva de direcciones de correo para el dominio autoritativo, siga uno de estos pasos:

  - En el EAC, vaya a **Flujo de correo** \> **Directivas de direcciones de correo**. Compruebe que se han aplicado las directivas en el orden correcto. Seleccione las directivas nuevas o actualizadas que haya y, en el panel de detalles, compruebe el formato de dirección de correo (incluidos los destinatarios) y si la directiva se ha aplicado.

  - En el Shell, ejecute los comandos **Get-EmailAddressPolicy** y `Get-EmailAddressPolicy "<Policy Name>"| Format-List` para comprobar los detalles de las directivas.

## ¿Cómo sabe si esta tarea se ha completado correctamente?

Para comprobar si ha configurado Exchange para que acepte correo de varios dominios autoritativos, haga lo siguiente:

1.  Envíe mensajes de prueba a un destinatario afectado desde un buzón externo a la organización de Exchange. Compruebe que las direcciones de correo aceptan correo correctamente.

2.  Envíe mensajes de prueba desde un buzón de destinatario afectado a un destinatario externo y compruebe la dirección «De» del mensaje.

