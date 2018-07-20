---
title: 'Crear directivas de retención: Exchange 2013 Help'
TOCTitle: Crear directivas de retención
ms:assetid: d8806c98-fea5-492f-906d-f514e25361b2
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150573(v=EXCHG.150)
ms:contentKeyID: 48268740
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Crear directivas de retención

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

En Exchange Online y Exchange Server 2013, puede usar directivas de retención para administrar el ciclo de vida de correo electrónico. Para aplicar directivas de retención, se crean etiquetas de retención, se agregan a una directiva de retención y se aplica la directiva a los usuarios del buzón de correo.

Aquí encontrará un [vídeo](https://go.microsoft.com/fwlink/?linkid=825854) que muestra cómo crear una directiva de retención y aplicarla a un buzón en Exchange Online.

Para otras tareas de administración relacionadas con las directivas de retención, consulte [Procedimientos de administración de registros de mensajería](messaging-records-management-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar esta tarea:  30 minutos.

  - Los procedimientos descritos en este tema requieren permisos específicos. Vea cada procedimiento para ver la información de permisos.

  - Los buzones de correo a los que aplica las directivas de retención deben encontrarse en Exchange Server 2010 o servidores posteriores.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## ¿Cómo realiza esto?

## Paso 1: Crear una etiqueta de retención

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Administración de los registros de mensajes" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

**Uso de EAC para crear etiquetas de retención**

1.  Vaya a **Administración de cumplimiento** \> **Etiquetas de retención** y, luego, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono")

2.  Seleccione una de las opciones para:
    
      - **Aplicado automáticamente a todo el buzón (predeterminado)**   Seleccione esta opción para crear una etiqueta de directiva predeterminada (DPT). Puede usar etiquetas DTP para crear una directiva de eliminación predeterminada o una directiva de archivo predeterminada que se aplique a todos los elementos del buzón de correo.
        

        > [!NOTE]
        > No puede usar la EAC para crear una DTP a fin de eliminar elementos de correo de voz. Para obtener más detalles acerca de cómo crear una DTP para eliminar los elementos de correo de voz, vea el siguiente ejemplo del Shell.

    
      - **Aplicado automáticamente a una carpeta específica**   Seleccione esta opción para crear una etiqueta de directiva de retención (RPT) para una carpeta predeterminada, como **Bandeja de entrada** o **Elementos eliminados**.
        

        > [!NOTE]
        > Solo puede crear RPT con las acciones <STRONG>Eliminar y permitir recuperación</STRONG> o <STRONG>Eliminar permanentemente</STRONG>.

    
      - **Aplicado por los usuarios a elementos y carpetas (personal)**   Seleccione esta opción para crear etiquetas personales. Estas etiquetas permiten a los usuarios de Outlook y Outlook Web App aplicar una configuración de archivo o de eliminación diferente a mensajes o carpetas respecto a la configuración aplicada a la carpeta principal o a todo el buzón.

3.  Las opciones y el título de la página de **nueva etiqueta de retención** depende del tipo de etiqueta seleccionada. Complete los siguientes campos:
    
      - **Nombre** Escriba el nombre de la etiqueta de retención. El nombre de etiqueta se usa solo para mostrar y no afecta la carpeta ni al elemento al que se aplica una etiqueta. Tenga en cuenta que las etiquetas personales que proporcione a los usuarios están disponibles en Outlook y Outlook Web App.
    
      - **Aplicar esta etiqueta a la siguiente carpeta predeterminada**   Esta opción solo está disponible si seleccionó **Aplicado automáticamente a una carpeta específica**.
    
      - **Acción de retención**   Seleccione una de las siguientes acciones para que se lleve a cabo después de que un elemento alcance el período de retención:
        
          - **Eliminar y permitir la recuperación**   Seleccione esta acción para eliminar los elementos, pero permitir a los usuarios que los recuperen con la opción **Recuperar elementos eliminados** en Outlook o Outlook Web App. Los elementos se retienen hasta que se alcance el período de retención de elementos eliminados configurado para la base de datos de buzones o el usuario de buzón.
        
          - **Eliminar permanentemente** Seleccione esta opción para eliminar permanentemente el elemento de la base de datos de buzones de correo.
            

            > [!IMPORTANT]
            > Los buzones o los elementos sujetos a retención local o retención por juicio se retendrán y se mostrarán en las búsquedas de exhibición de documentos electrónicos. Para obtener más información, consulte <A href="in-place-hold-and-litigation-hold-exchange-2013-help.md">Conservación local y retención por juicio</A>.

        
          - **Mover a archivo**   Esta acción solo está disponible si crea una DPT o una etiqueta personal. Elija esta acción para mover elementos al archivo local del usuario.
    
      - **Período de retención** Seleccione una de las siguientes opciones:
        
          - **Nunca**   Seleccione esta opción para especificar que los elementos no se deben eliminar ni mover nunca al archivo.
        
          - **Cuando el elemento alcanza la siguiente antigüedad (en días)**   Seleccione esta opción y especifique el número de días para guardar los elementos antes de que se muevan o eliminen. La antigüedad de retención para todos los elementos admitidos, excepto los del calendario y las tareas, se calcula a partir de la fecha de recepción o creación de un elemento. La antigüedad de retención para los elementos del calendario y las tareas se calcula a partir de la fecha de finalización.
    
      - **Comentario**   Utilice este campo opcional para especificar cualquier comentario o nota administrativa. El campo no se muestra a los usuarios.

**Uso del Shell para crear una etiqueta de retención**

Use el cmdlet **New-RetentionPolicyTag** para crear una etiqueta de retención. Diferentes opciones disponibles en el cmdlet le permiten crear diferentes tipos de etiquetas de retención. Use el parámetro *Type* para crear una DPT (`All`), una RPT (especifique un tipo de carpeta predeterminado, como `Inbox`) o una etiqueta personal (`Personal`).

En este ejemplo se crea una DTP para eliminar todos los mensajes del buzón de correo después de 7 años (2.556 días).

    New-RetentionPolicyTag -Name "DPT-Corp-Delete" -Type All -AgeLimitForRetention 2556 -RetentionAction DeleteAndAllowRecovery

En este ejemplos se crea una DTP para mover todos los mensajes al archivo local en 2 años (730 días).

    New-RetentionPolicyTag -Name "DPT-Corp-Move" -Type All -AgeLimitForRetention 730 -RetentionAction MoveToArchive

En este ejemplo se crea una DPT para eliminar mensajes de correo de voz después de 20 días.

    New-RetentionPolicyTag -Name "DPT-Corp-Voicemail" -Type All -MessageClass Voicemail -AgeLimitForRetention 20 -RetentionAction DeleteAndAllowRecovery

En este ejemplo se crea una RTP para eliminar de forma permanente los mensajes en la carpeta de correo no deseado después de 30 días.

    New-RetentionPolicyTag -Name "RPT-Corp-JunkMail" -Type JunkEmail -AgeLimitForRetention 30 -RetentionAction PermanentlyDelete

En este ejemplo se crea una etiqueta personal para no eliminar nunca un mensaje.

    New-RetentionPolicyTag -Name "Never Delete" -Type Personal -RetentionAction DeleteAndAllowRecovery -RetentionEnabled $false

## Paso 2: Crear una directiva de retención

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Administración de los registros de mensajes" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

**Uso de EAC para crear una directiva de retención**

1.  Vaya a **Administración de cumplimiento** \> **Directivas de retención** y, luego, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono")

2.  En **Nueva directiva de retención**, complete los campos siguientes:
    
      - **Nombre** Escriba el nombre de la directiva de retención.
    
      - **Etiquetas de retención**   Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para seleccionar las etiquetas que desea agregar a esta directiva de retención.
        
        Una directiva de retención puede contener las siguientes etiquetas:
        
          - Una DPT con la acción **Mover a archivo**
        
          - Una DPT con la acción **Eliminar y permitir recuperación** o **Eliminar permanentemente**
        
          - Una DPT para mensajes de correo de voz con las acciones **Eliminar y permitir la recuperación** o **Eliminar permanentemente**
        
          - Una RPT por carpeta predeterminada, como **Bandeja de entrada** para eliminar elementos
        
          - Las etiquetas personales que se desee
            

            > [!NOTE]
            > Si bien es posible agregar cualquier número de etiquetas personales a una directiva de retención, puede resultar confuso para los usuarios el hecho de tener muchas etiquetas personales con diferentes configuraciones de retención. Se recomienda vincular un máximo de diez etiquetas personales a una directiva de retención.

        
        Puede crear una directiva de retención sin agregarle ninguna etiqueta de retención, pero los elementos del buzón a los que se aplica la directiva no se moverán ni se eliminarán. También puede agregar y eliminar etiquetas de retención desde una directiva de retención después de crearla.

**Uso del Shell para crear una directiva de retención**

En este ejemplo se crea la directiva de retención RetentionPolicy-Corp y se usa el parámetro *RetentionPolicyTagLinks* para asociar cinco etiquetas a la directiva.

    New-RetentionPolicy "RetentionPolicy-Corp"  -RetentionPolicyTagLinks "DPT-Corp-Delete","DPT-Corp-Move","DPT-Corp-Voicemail","RPT-Corp-JunkMail","Never Delete"

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-RetentionPolicy](https://technet.microsoft.com/es-es/library/dd297970\(v=exchg.150\)).

## Paso 3: Aplicar una directiva de retención para usuarios de buzones de correo

Después de crear una directiva de retención, debe aplicarla a los usuarios de buzones de correo. Puede aplicar diferentes directivas de retención a diferentes conjuntos de usuarios. Para obtener instrucciones detalladas, consulte [Aplicar una directiva de retención a los buzones](apply-a-retention-policy-to-mailboxes-exchange-2013-help.md).

## ¿Cómo sabe si esta tarea se ha completado correctamente?

Después de crear etiquetas de retención, agréguelas a la directiva de retención y aplique la directiva a un usuario de buzón de correo, la próxima vez que el asistente del buzón de correo de MRM procese el buzón de correo, los mensajes se mueven o eliminan en base a los parámetros que configuró en las etiquetas de retención.

Para comprobar si aplicó la directiva de retención, realice lo siguiente:

1.  Ejecute el siguiente comando de Shell para ejecutar el asistente de MRM manualmente frente a un buzón de correo único.
    
        Start-ManagedFolderAssistant -Identity <mailbox identity>

2.  Inicie sesión en el buzón de correo con Outlook o Outlook Web App y compruebe que los mensajes se eliminan o se mueven a un archivo según la configuración de la directiva.


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


