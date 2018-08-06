---
title: 'Configurar Outlook para mostrar remitente original en el buzón de cuarentena | Microsoft Docs'
TOCTitle: Configurar Outlook para mostrar el remitente original en el buzón de cuarentena
ms:assetid: 9249425d-1b06-48a0-ad95-c4eefb641ff4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee861109(v=EXCHG.150)
ms:contentKeyID: 49895781
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar Outlook para mostrar el remitente original en el buzón de cuarentena

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Cuarentena de correo no deseado es una característica del agente de filtrado de contenido que reduce el riesgo de perder mensajes legítimos. La cuarentena de correo no deseado proporciona una ubicación de almacenamiento temporal para mensajes identificados como correo no deseado y que no deben ser entregados a un buzón de usuario dentro de la organización.

Cuando un mensaje coincide con el umbral de cuarentena de correo no deseado, se lo ubica en un informe de no entrega (NDR) y se lo envía al buzón de cuarentena de correo no deseado. Debido a que los mensajes en cuarentena se almacenan como NDR en el buzón de cuarentena, la dirección del administrador de correo de su organización se enumerará como De: dirección para todos los mensajes. No obstante, tener la dirección de remitente original, la dirección de destinatario original y el nivel de confianza de correo no deseado (SCL) original en la lista de campos debería hacer que encontrara con más facilidad el mensaje que desea recuperar.

De forma predeterminada, no puede seleccionar estos campos en Microsoft Outlook. Antes de poder agregar estos campos a la vista de mensajes, primero debe crear un formulario de Outlook que agregue al remitente, al destinatario y el SCL originales como campos opcionales que puede seleccionar. Después de crear este formulario personalizado, podrá configurar Outlook para que muestre estos campos en la vista de mensajes.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar este procedimiento: 15 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Acceso a buzones" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Este procedimiento requiere que haya configurado el buzón de cuarentena de correo no deseado. Para obtener más información, consulte [Configurar un buzón de cuarentena de correo no deseado](configure-a-spam-quarantine-mailbox-exchange-2013-help.md).

  - Para tener acceso al buzón de cuarentena, debe configurar un perfil de Outlook para ese buzón y, a continuación, abrir el buzón mediante Outlook. Para obtener más información acerca de cómo configurar y utilizar varios perfiles de Outlook, vea [Descripción general de correo electrónico perfiles Outlook](https://go.microsoft.com/fwlink/p/?linkid=178975).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Paso 1: Usar el Bloc de notas para crear un formulario de Outlook personalizado

1.  Abra el Bloc de notas y copie el siguiente código en el documento.
    
        [Description]
        MessageClass=IPM.Note
        CLSID={00020D31-0000-0000-C000-000000000046}
        DisplayName=Quarantine Extension Form
        Category=Standard
        Subcategory=Form
        Comment=This form allows the Original Sender (ReceivedRepresentingEmailAddress), Original Recipient (To), and Original SCL (OriginalScl) values to be viewed as columns.
        LargeIcon=IPML.ico
        SmallIcon=IPMS.ico
        Version=3.0
        Locale=enu
        Hidden=1
        Owner=Microsoft Corporation
        Contact=Your Name
        
        [Platforms]
        Platform1=Win16
        Platform2=NTx86
        Platform9=Win95
        
        [Platform.Win16]
        CPU=ix86
        OSVersion=Win3.1
        
        [Platform.NTx86]
        CPU=ix86
        OSVersion=WinNT3.5
        
        [Platform.Win95]
        CPU=ix86
        OSVersion=Win95
        
        [Properties]
        Property01=ReceivedRepresentingEmailAddress
        Property02=DisplayTo
        Property03=OriginalScl
        
        [Property.ReceivedRepresentingEmailAddress]
        Type=31
        NmidInteger=0x0078
        DisplayName=ReceivedRepresentingEmailAddress
        
        [Property.DisplayTo]
        Type=31
        NmidInteger=0x0E04
        DisplayName=DisplayTo
        
        [Property.OriginalScl]
        Type=3
        NmidPropset={41F28F13-83F4-4114-A584-EEDB5A6B0BFF}
        NmidString=OriginalScl
        DisplayName=OriginalScl
        
        [Verbs]
        Verb1=1
        
        [Verb.1]
        DisplayName=&Open
        Code=0
        Flags=0
        Attribs=2
        
        [Extensions]
        Extensions1=1
        
        [Extension.1]
        Type=31
        NmidPropset={00020D0C-0000-0000-C000-000000000046}
        NmidInteger=1
        Value=1000000000000000

2.  Guarde el archivo en su carpeta de formularios de Office con los siguientes valores:
    
      - **Ruta** *\<Ruta de instalación de Office\>*\\\<*Versión de Office\>*\\Formularios\\*\<LCID\>*
        
          - *\<Ruta de instalación de Office\>*   Para las versiones de 32 bits de Office en las versiones de 32 bits de Microsoft Windows, o bien para las versiones de 64 bits de Office en las versiones de 64 bits de Windows, la ruta predeterminada es `C:\Program Files\Microsoft Office`. Para las versiones de 32 bits de Office en las versiones de 64 bits de Windows, la ruta predeterminada es `C:\Program Files (x86)\Microsoft Office`.
        
          - *\<Versión de Office\>* Para Outlook 2007, el valor es `Office12`. Para Outlook 2010, el valor es `Office14`. Para Outlook 2013, el valor es `Office15`.
        
          - *\<LCID\>* Este es el valor de su Id. de configuración regional (LCID). Por ejemplo, el LCID para inglés de los EE.UU. es 1033. Para obtener más información, consulte [KB221435: Lista de identificadores de configuración regional compatibles en Word](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=221435).
    
      - **Nombre**   Para el resto de este procedimiento, por defecto el archivo se denomina `QTNE.cfg`. El nombre del archivo no es importante, pero asegúrese de incluir el valor entre comillas para que se guarde como QTNE.cfg y no como QTNE.cfg.txt.
    
    Por ejemplo, para la versión de 32 bits en inglés de Outlook 2013 instalada en una versión de 64 bits de Windows, guarde el archivo como:
    
        "C:\Program Files (x86)\Microsoft Office\Office15\Forms\1033\QTNE.cfg"
    

    > [!NOTE]
    > Si un control de acceso de usuario (UAC) de Windows impide que guarde el archivo en la ubicación correcta, guárdelo primero en una ubicación temporal y después cópielo.



## Paso 2: Configurar Outlook para utilizar el formulario de Outlook personalizado

Utilice uno de los siguientes procedimientos en función de la versión de Outlook instalada en su equipo.

## Configurar Outlook 2010 o Outlook 2013

1.  En Outlook 2010 o Outlook 2013, haga clic en **Archivo** \> **Opciones** \> **Avanzadas**.

2.  En la sección **Desarrolladores**, haga clic en **Formularios personalizados**.

3.  En el cuadro de diálogo **Opciones**, haga clic en **Administrar formularios**.

4.  En el cuadro de diálogo **Administrador de formularios**, haga clic en **Instalar**. Vaya a la ubicación del archivo `QTNE.cfg`, selecciónelo y haga clic en **Abrir**. En el cuadro de diálogo **Propiedades de formulario**, revise la información y después haga clic en **Aceptar** para instalar el formulario de extensiones en cuarentena en su biblioteca de formularios personales.

5.  En el cuadro de diálogo **Administrador de formularios**, haga clic en **Cerrar**. Haga clic en **Aceptar** dos veces para cerrar los cuadros de diálogo restantes y volver a la interfaz principal de Outlook.

6.  En la ficha **Inicio** de la vista **Correo** del Buzón de entrada, haga clic con el botón secundario en la fila de encabezado de columna (puede que necesite expandir el ancho de la lista de mensajes para ver las columnas) y, a continuación, haga clic en **Configuración de la vista**.

7.  En el cuadro de diálogo **Configuración de la vista avanzada**, haga clic en **Columnas**.

8.  En el cuadro de diálogo **Mostrar columnas**, en la lista desplegable **Seleccionar columnas disponibles de**, baje hasta el final de la lista y seleccione **Formularios**.

9.  En el cuadro de diálogo **Seleccionar formularios comerciales para esta carpeta**, en el campo **Formularios seleccionados**, seleccione **Mensaje** y haga clic en **Quitar**. En el campo **Formularios personales**, seleccione **Formulario de extensiones en cuarentena** y, a continuación, haga clic en **Agregar**. Cuando haya terminado, haga clic en **Cerrar**.

10. En el cuadro de diálogo **Mostrar columnas**, en la sección **Columnas disponibles**, seleccione uno o varios de los campos siguientes y haga clic en **Agregar** después de seleccionar cada campo.
    
      - **ReceivedRepresentingEmailAddress**   Remitente original
    
      - **DisplayTo**   Destinatario original (tenga en cuenta que esto aparece como **Para** después de agregarlo)
    
      - **OriginalScl**   SCL original
    
    Use los botones **Subir** o **Bajar** para colocar las columnas en la vista. Para obtener mejores resultados, coloque los tres nuevos campos después del campo **Datos adjuntos** y antes del campo **De**. Al finalizar, haga clic en **Aceptar** dos veces para volver a la interfaz principal de Outlook.

## Configurar Outlook 2007

1.  En Outlook 2007, haga clic en **Herramientas** \> **Opciones**.

2.  En el cuadro de diálogo **Opciones**, haga clic en la ficha **Otros**; después, en **General**, haga clic en **Opciones avanzadas**.

3.  En el cuadro de diálogo **Opciones avanzadas**, haga clic en **Formularios personalizados**; después, en el cuadro de diálogo **Formularios personalizados**, haga clic en **Administrar formularios**.

4.  En el cuadro de diálogo **Administrador de formularios**, haga clic en **Instalar**. Vaya a la ubicación del archivo `QTNE.cfg`, selecciónelo y haga clic en **Abrir**. En el cuadro de diálogo **Propiedades de formulario**, revise la información y después haga clic en **Aceptar** para instalar el formulario de extensiones en cuarentena en su biblioteca de formularios personales.

5.  Cierre el cuadro de diálogo **Administrador de formularios** y, a continuación, haga clic en **Aceptar** para cerrar los cuadros de diálogo restantes y volver a la interfaz principal de Outlook 2007.

6.  En la vista **Correo** de la Bandeja de entrada, haga clic con el botón secundario en la fila de encabezado de columna (puede que necesite expandir el ancho de la lista de mensajes para ver las columnas) y, a continuación, seleccione **Personalizar la vista actual**.

7.  En el cuadro de diálogo **Personalizar vista: mensajes**, haga clic en **Mostrar campos**.

8.  En el cuadro de diálogo **Mostrar campos**, en la lista desplegable **Seleccionar campos disponibles en**, baje hasta el final de la lista y seleccione **Formularios**.

9.  En el cuadro de diálogo **Seleccionar formularios comerciales para esta carpeta**, en el campo **Formularios seleccionados**, seleccione **Mensaje** y haga clic en **Quitar**. En el campo **Formularios personales**, seleccione **Formulario de extensiones en cuarentena** y, a continuación, haga clic en **Agregar**. Cuando haya terminado, haga clic en **Cerrar**.

10. En el cuadro de diálogo **Mostrar campos**, en la sección **Campos disponibles**, seleccione uno o varios de los campos siguientes y haga clic en **Agregar** después de seleccionar cada campo.
    
      - **ReceivedRepresentingEmailAddress**   Remitente original
    
      - **DisplayTo**  Destinatario original (tenga en cuenta que esto aparece como **Para** después de agregarlo)
    
      - **OriginalScl**   SCL original
    
    Use los botones **Subir** o **Bajar** para colocar las columnas en la vista. Para obtener mejores resultados, coloque los tres nuevos campos después del campo **Datos adjuntos** y antes del campo **De**. Al finalizar, haga clic en **Aceptar** dos veces para volver a la interfaz principal de Outlook 2007.

## ¿Cómo saber si el proceso se ha completado correctamente?

Sabrá si este procedimiento ha funcionado si puede ver los valores de remitente original, destinatario original o SCL original de los mensajes en cuarentena en el buzón de cuarentena de correo no deseado mediante Outlook.

