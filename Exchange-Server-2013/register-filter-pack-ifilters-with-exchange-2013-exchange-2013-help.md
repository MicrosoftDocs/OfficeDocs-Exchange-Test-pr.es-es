---
title: 'Registrar IFilters de Filter Pack con Exchange 2013: Exchange 2013 Help'
TOCTitle: Registrar IFilters de Filter Pack con Exchange 2013
ms:assetid: 0338980f-3a64-49d3-bc3c-bf6f10f88cb4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ837174(v=EXCHG.150)
ms:contentKeyID: 50556732
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Registrar IFilters de Filter Pack con Exchange 2013

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Las reglas de transporte con condiciones de análisis de datos adjuntos realizan la extracción de textos cuando analizan el contenido de los datos adjuntos. Exchange 2013 puede analizar los tipos de datos adjuntos más usados nativamente. Es posible incluir tipos de datos adjuntos adicionales registrando IFilters en Exchange 2013. En este tema, se muestra cómo registrar IFilters de Microsoft y de otros fabricantes.

Después de registrar un IFilter para un tipo de archivo específico, las reglas de transporte con condiciones de procesamiento de datos adjuntos podrán analizar dichos datos adjuntos. Como resultado, estos tipos de archivo ya no activarán la condición *AttachmentIsUnsupported*.


> [!WARNING]
> Los procedimientos enumerados en este tema implican la modificación del registro en sus servidores Exchange. La edición incorrecta del Registro puede dar lugar a graves problemas que pueden suponer la reinstalación del sistema operativo. Es posible que los problemas derivados de la edición incorrecta del Registro no puedan resolverse. Antes de editar el Registro, realice una copia de seguridad de los datos más importantes.<BR>Estos procedimientos también requieren que detenga y reinicie el servicio de transporte de Microsoft Exchange en sus servidores de buzones.



Para otras tareas de administración relacionadas con reglas de transporte, consulte [Administrar reglas de flujo de correo](https://docs.microsoft.com/es-es/exchange/security-and-compliance/mail-flow-rules/manage-mail-flow-rules).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 5 minutos por servidor.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Valores de configuración de Exchange Server" en el tema [Permisos de infraestructura de la Shell y de Exchange](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Debe realizar los siguientes procedimientos en los servidores que ya tengan el rol del servidor de buzones de Exchange 2013 instalado. Si agrega servidores de buzones adicionales después de realizar estos procedimientos, debe volver a realizarlos en los nuevos servidores aprovisionados.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Registro de Microsoft Office 2010 Filter Pack

De manera predeterminada, los siguientes tipos de archivos de Office no son compatibles con las reglas de transporte de Exchange:

  - Office OneNote

  - Office Publisher

Si desea compatibilidad para estos archivos, debe implementar Microsoft Office 2010 Filter Pack. Este Filter Pack no se implementa durante la instalación de Exchange 2013 y no es un requisito previo para la implementación.

## Implementación de Microsoft Office 2010 Filter Pack

La implementación de Office 2010 Filter Pack consta de dos pasos principales:

  - Descargar e instalar Filter Pack, que registra IFilters en Windows (Buscar).

  - Modificar el registro para que IFilters también se registre en Exchange 2013. Esto permite a Exchange proporcionar el análisis de los datos adjuntos para los formatos de archivos.


> [!IMPORTANT]
> Debe ejecutar este procedimiento en todos los servidores de buzones de la organización.



1.  Descargue y guarde Microsoft Office 2010 Filter Pack (`FilterPack64bit.exe`) del [Centro de descarga de Microsoft](https://go.microsoft.com/fwlink/?linkid=191548).

2.  Ejecute el archivo `FilterPack64bit.exe` en su servidor de buzones y siga las instrucciones para completar la instalación.

3.  Inicie el Editor del Registro y busque la siguiente subclave de registro:
    
        HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\HubTransportRole\CLSID

4.  En **CLSID**, agregue una subclave para archivos de OneNote de la siguiente manera:
    
    1.  Haga clic con el botón secundario en **CLSID**, seleccione **Nuevo** y, a continuación, haga clic en **Clave**.
    
    2.  Cambie el nombre de la nueva clave a `{B8D12492-CE0F-40AD-83EA-099A03D493F1}`.
    
    3.  Haga clic en la clave que acaba de crear y establezca el valor **(Default)** en donde instaló Office 2010 Filter Pack. De manera predeterminada, el paquete de filtro se instala en `C:\Program Files\Common Files\Microsoft Shared\Filters\ONIFilter.dll`.
    
    4.  Haga clic con el botón secundario en **{B8D12492-CE0F-40AD-83EA-099A03D493F1}**, seleccione **Nuevo** y, luego, haga clic en **Valor de cadena**.
    
    5.  Nombre el nuevo valor de cadena `ThreadingModel` y establézcalo en `Both`.

5.  En **CLSID**, agregue una subclave para archivos de Publisher de la siguiente manera:
    
    1.  Haga clic con el botón secundario en **CLSID**, seleccione **Nuevo** y, a continuación, haga clic en **Clave**.
    
    2.  Cambie el nombre de la nueva clave a `{A7FD8AC9-7ABF-46FC-B70B-6A5E5EC9859A}`.
    
    3.  Haga clic en la clave que acaba de crear y establezca el valor **(Default)** en donde instaló Office 2010 Filter Pack. De manera predeterminada, el paquete de filtro se instala en `C:\Program Files\Common Files\Microsoft Shared\Filters\PUBFILT.dll`.
    
    4.  Haga clic con el botón secundario en **{A7FD8AC9-7ABF-46FC-B70B-6A5E5EC9859A}**, seleccione **Nuevo** y, luego, haga clic en **Valor de cadena**.
    
    5.  Nombre el nuevo valor de cadena `ThreadingModel` y establézcalo en `Both`.

6.  Busque la clave del registro siguiente:
    
        HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\HubTransportRole\filters

7.  En **filtros**, agregue una subclave para las extensiones .one de la siguiente manera.
    
    1.  Haga clic con el botón secundario en **filtros**, seleccione **Nuevo** y, a continuación, haga clic en **Clave**.
    
    2.  Cambie el nombre de la nueva clave a `.one`.
    
    3.  Haga clic en la clave que acaba de crear y establezca el valor **(Default)** en `{B8D12492-CE0F-40AD-83EA-099A03D493F1}`.

8.  En **filtros**, agregue una subclave para las extensiones .pub de la siguiente manera:
    
    1.  Haga clic con el botón secundario en **filtros**, seleccione **Nuevo** y, a continuación, haga clic en **Clave**.
    
    2.  Cambie el nombre de la nueva clave a `.pub`.
    
    3.  Haga clic en la clave que acaba de crear y establezca el valor **(Default)** en `{A7FD8AC9-7ABF-46FC-B70B-6A5E5EC9859A}`.

9.  Cierre el Editor del Registro.

10. En su servidor de buzones, detenga y luego reinicie los siguientes servicios en el orden especificado:
    
    1.  Detenga el servicio Transporte de Microsoft Exchange.
    
    2.  Detenga el servicio de administración de filtros de Microsoft.
    
    3.  Inicie el servicio de administración de filtros de Microsoft.
    
    4.  Inicie el servicio Transporte de Microsoft Exchange.

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que haya registrado correctamente IFilters de Microsoft Office 2010 Filter Pack, siga estos pasos:

1.  Cree una regla de transporte con las siguientes propiedades. Para ver instrucciones detalladas acerca de cómo crear reglas de transporte, consulte [Administrar reglas de flujo de correo](https://docs.microsoft.com/es-es/exchange/security-and-compliance/mail-flow-rules/manage-mail-flow-rules).
    
      - El remitente es el buzón de correo.
    
      - El contenido de cualquier documento adjunto incluye "Testing IFilters".
    
      - Genere un informe del incidente y envíelo a su buzón de correo.

2.  Cree un archivo de OneNote que contenga la frase "Testing IFilters", adjúntelo a un nuevo mensaje de correo electrónico y envíeselo a usted mismo.

3.  Compruebe que haya recibido un informe del incidente de la regla de transporte para la regla que acaba de crear. Esto confirma que el motor de la regla pudo analizar el contenido del archivo de OneNote.

4.  Repita los pasos 2 y 3 con un archivo de Publisher.

## Registro de IFilters de otros fabricantes para ofrecer compatibilidad para formatos de archivo adicionales

Es posible ampliar la capacidad de análisis de datos adjuntos para tipos de archivos adicionales. Para hacerlo, debe registrar IFilters adicionales de otros fabricantes. Es posible agregar compatibilidad para archivos adicionales mediante la instalación y el registro del IFilter del tipo de archivo en cada uno de sus servidores de buzones.


> [!IMPORTANT]
> Microsoft no ha probado IFilters de terceros con reglas de transporte. Por lo tanto, le recomendamos implementar y probar los IFilters de terceros en un entorno de prueba antes de implementarlos en su entorno de producción.



## Implementación del IFilter de Adobe PDF

En este procedimiento se muestra cómo implementar el [IFilter de Adobe PDF](https://www.adobe.com/support/downloads/detail.jsp?ftpid=4025) para admitir el procesamiento de datos adjuntos en PDF en reglas de transporte.


> [!NOTE]
> De manera predeterminada, Exchange 2013 admite el análisis de archivos PDF en reglas de transporte. El ejemplo de PDF se usa simplemente para demostrar cómo puede ampliar la compatibilidad para tipos de archivos adicionales con IFilters de otros fabricantes.



1.  Descargue el [IFilter de Adobe PDF](https://www.adobe.com/support/downloads/detail.jsp?ftpid=4025) y, a continuación, siga las instrucciones de instalación.

2.  Inicie el Editor del Registro y busque la siguiente subclave:
    
        HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\HubTransportRole\CLSID

3.  En **CLSID**, agregue una subclave para archivos PDF de la siguiente manera:
    
    1.  Haga clic con el botón secundario en **CLSID**, seleccione **Nuevo** y, a continuación, haga clic en **Clave**.
    
    2.  Cambie el nombre de la nueva clave a `{E8978DA6-047F-4E3D-9C78-CDBE46041603}`.
        

        > [!NOTE]
        > Cada IFilter tiene un Id. de clase única (CLSID). Encontrará el CLSID en la documentación de instalación del IFilter que está registrando o si busca la extensión de archivo en la clave <CODE>HKEY_CLASSES_ROOT\CLSID</CODE> en el registro.

    
    3.  Haga clic en la clave que acaba de crear y establezca el valor **(Default)** en donde instaló el IFilter de PDF. De manera predeterminada, el IFilter de PDF se instala en `C:\Program Files\Adobe\Adobe PDF IFilter 9 for 64-bit platforms\bin\PDFFilter.dll`.

4.  Busque la clave del registro siguiente:
    
        HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ExchangeServer\v15\HubTransportRole\filters

5.  En **filtros**, agregue una subclave para las extensiones .pdf de la siguiente manera:
    
    1.  Haga clic con el botón secundario en **filtros**, seleccione **Nuevo** y, a continuación, haga clic en **Clave**.
    
    2.  Cambie el nombre de la nueva clave a `.pdf`.
    
    3.  Haga clic en la clave que acaba de crear y establezca el valor **(Default)** en `{E8978DA6-047F-4E3D-9C78-CDBE46041603}`.

6.  Cierre el Editor del Registro.

7.  En su servidor de buzones, detenga y reinicie los siguientes servicios en el orden especificado:
    
    1.  Detenga el servicio Transporte de Microsoft Exchange.
    
    2.  Detenga el servicio de administración de filtros de Microsoft.
    
    3.  Inicie el servicio de administración de filtros de Microsoft.
    
    4.  Inicie el servicio Transporte de Microsoft Exchange.

## ¿Cómo saber si el proceso se ha completado correctamente?

Use el mismo procedimiento de la sección ¿Cómo saber si el proceso se ha completado correctamente? en este tema, pero remplace los archivos de Publisher con archivos de Adobe PDF.

## Más información

[Usar reglas de transporte para inspeccionar datos adjuntos de mensajes](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md)

[Reglas de transporte o de flujo de correo](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[Condiciones de las reglas de transporte (predicados)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[Acciones de regla de transporte](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)

