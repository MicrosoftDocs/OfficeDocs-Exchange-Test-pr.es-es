---
title: 'Configura servidor transporte perimetral configurar clonada Exchange 2013 Help | Microsoft Docs'
TOCTitle: Configurar el servidor de transporte perimetral mediante una configuración clonada
ms:assetid: 0bbc83e3-e5e8-4480-a8a6-15f035360856
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa996008(v=EXCHG.150)
ms:contentKeyID: 61183321
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar el servidor de transporte perimetral mediante una configuración clonada

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-04-13_

Puede usar los scripts del Shell de administración de Exchange (que se encuentran en %ExchangeInstallPath%Scripts) para duplicar la configuración de un servidor Transporte perimetral. Este proceso se conoce como *configuración clonada*. La *configuración clonada* es la práctica de implementar nuevos servidores de transporte perimetral en función de la información de configuración de un servidor de origen configurado previamente. La información de configuración de un servidor de origen configurado previamente se copia y exporta a un archivo XML, que a continuación se importa en el servidor de destino. Para obtener una descripción general de este proceso, consulte [Configuración clonada del servidor de transporte perimetral](edge-transport-server-cloned-configuration-exchange-2013-help.md).

La información de configuración del servidor Transporte perimetral se almacena en Active Directory Lightweight Directory Services (AD LDS) y no se replica entre varios servidores de transporte perimetral. Mediante una configuración clonada, puede garantizar que cada servidor Transporte perimetral que se implementa en la red perimetral use la misma configuración.

Se usan dos scripts de Shell para realizar tareas de configuración clonada:

  - **ExportEdgeConfig.ps1**   Exporta todas las opciones y datos configurados por el usuario desde un servidor Transporte perimetral y los almacena en un archivo XML.

  - **ImportEdgeConfig.ps1**   Durante el paso de validación de la configuración, el script ImportEdgeConfig.ps1 comprueba todo el archivo XML exportado para ver si la configuración de exportación específica del servidor es válida para el servidor de destino. Si es necesario modificar la configuración, el script escribe la configuración no válida en un archivo de respuesta que se puede modificar para especificar la información del servidor de destino, que después se utiliza durante el paso de importación de la configuración. Durante el paso de importación de la configuración, el script importa todos los valores y datos configurados por el usuario almacenados en el archivo XML intermedio que creó el script ExportEdgeConfig.ps1.

Ambos scripts se encuentran en la carpeta %ExchangeInstallPath%Scripts.

## Antes de empezar

  - Tiempo estimado para finalizar esta tarea: 30 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el entrada «Servidores de transporte perimetral» en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Una configuración clonada no hace que se duplique la configuración de suscripción perimetral de un servidor. Los certificados EdgeSync no están clonados. Es necesario ejecutar el proceso de EdgeSync por separado en cada servidor Transporte perimetral. EdgeSync sobrescribe la configuración que se incluye tanto en la información de la configuración clonada como en la información de replicación de EdgeSync.

  - Si se configuran conectores de envío para que utilicen credenciales, la contraseña se escribe en el archivo XML intermedio en forma de cadena cifrada. Puede utilizar el parámetro *-key* con los scripts ImportEdgeConfig.ps1 y ExportEdgeConfig.ps1 para especificar la cadena de 32 bytes que se utilizará para el cifrado y descifrado de la contraseña. Si no utiliza el parámetro *-key*, se usa una clave de cifrado predeterminada.

  - Solo puede usar el Shell para realizar este procedimiento.Para obtener información sobre cómo abrir el Shell de administración de Exchange en su organización local Exchange, vea [Abrir el Shell](https://technet.microsoft.com/es-es/library/dd638134\(v=exchg.150\)).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Cómo realiza esto?

## Paso 1: exportar los datos de configuración del servidor de origen a un archivo en el servidor de origen

1.  Copie el script ExportEdgeConfig.ps1 a la carpeta raíz del perfil de usuario del servidor de origen.

2.  Para exportar los datos de configuración del servidor de origen a un archivo en el servidor de origen, use la siguiente sintaxis.
    
        ./ExportEdgeConfig.ps1 -CloneConfigData:"<configuration file>"
    
    Por ejemplo, para exportar los datos de configuración del servidor de origen al archivo C:\\CloneConfigData.xml, ejecute el siguiente comando.
    
        ./ExportEdgeConfig.ps1 -CloneConfigData:"C:\CloneConfigData.xml"

## ¿Cómo saber si el paso ha funcionado?

Sabrá que ha exportado correctamente los datos de configuración de origen a un archivo cuando aparezca el mensaje de confirmación: «los datos de configuración del servidor perimetral se exportaron correctamente a: \<ruta de acceso del archivo de salida\>».

## Paso 2: validar el archivo de configuración y crear un archivo de respuesta en el servidor de destino

1.  Copie el archivo de configuración del servidor de origen que exportó en el paso anterior al servidor Transporte perimetral.

2.  Copie el script ImportEdgeConfig.ps1 a la carpeta raíz del perfil de usuario del servidor de destino.

3.  Para validar el archivo de configuración y usar los resultados para crear un archivo de respuesta en el servidor de destino, use la siguiente sintaxis.
    
        ./ImportEdgeConfig.ps1 -CloneConfigData:"<configuration file>" -IsImport $false -CloneConfigAnswer:"<answer file>"
    
    Por ejemplo, para validar el archivo de configuración C:\\CloneConfigData.xml y crear el archivo de respuesta C:\\CloneConfigAnswer.xml, ejecute el siguiente comando.
    
        ./ImportEdgeConfig.ps1 -CloneConfigData:"C:\CloneConfigData.xml" -IsImport $false -CloneConfigAnswer:"C:\CloneConfigAnswer.xml"

4.  Abra el archivo de respuesta y modifique los valores que no sean válidos para el servidor de destino. Si no se requieren modificaciones, el archivo de respuesta no tendrá entradas. Guarde los cambios.

## ¿Cómo saber si el paso ha funcionado?

Sabrá que ha validado correctamente el archivo de configuración y creado un archivo de respuesta cuando aparezca el mensaje de confirmación: «el archivo de respuesta se creó correctamente».

## Paso 3: importar el archivo de configuración en el servidor de destino

Para importar el archivo de configuración en el servidor de destino, use la siguiente sintaxis.

    ./ImportEdgeConfig.ps1 -CloneConfigData:"<Configuration file>" -IsImport $true -CloneConfigAnswer:"<answer file>"

Por ejemplo, para importar el archivo de configuración C:\\CloneConfigData.xml mediante el archivo de respuesta C:\\CloneConfigAnswer.xml, ejecute el siguiente comando.

    ./ImportEdgeConfig.ps1 -CloneConfigData:"C:\CloneConfigData.xml" -IsImport $true -CloneConfigAnswer:"C:\CloneConfigAnswer.xml"

## ¿Cómo saber si el paso ha funcionado?

Sabrá que ha importado correctamente el archivo de configuración en el servidor de destino cuando aparezca el mensaje de confirmación: «se importó correctamente la información de configuración del servidor perimetral».

