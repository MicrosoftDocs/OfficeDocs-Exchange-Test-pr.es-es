---
title: 'Exportar e importar etiquetas de retención: Exchange 2013 Help'
TOCTitle: Exportar e importar etiquetas de retención
ms:assetid: 18405ea2-7ccc-475e-bd84-8b040e17bf44
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ907307(v=EXCHG.150)
ms:contentKeyID: 51406480
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exportar e importar etiquetas de retención

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2017-11-15_

Existen varios escenarios en los cuales tal vez desee exportar o importar etiquetas de retención, incluidos:

  - Aplicar las mismas políticas de retención en todos los servidores en una organización con varios bosques Exchange

  - Aplicar las mismas directivas de retención en una implementación híbrida en la que algunos buzones residen en la organización local de Exchange y otros en Exchange Online.

  - Aplicar políticas de retención en un escenario de Archiving Exchange, donde los usuarios con buzones posterior o local Exchange 2010 tienen un archiving basado en la nube.

En estos escenarios, el Asistente para carpeta administrada puede procesar correctamente un elemento que tiene una etiqueta de retención aplicada después de que el elemento o el buzón se mueva a otra organización.


> [!WARNING]
> Para mantener las etiquetas y directivas de retención sincronizadas entre las dos organizaciones, cada vez que realice cambios en una etiqueta y una directiva de retención en la organización de origen, debe realizar este procedimiento para exportar etiquetas y directivas de retención de la organización de origen e importarlas a la organización de destino.<BR>No puede seleccionar etiquetas y directivas de retención específicas para exportar. El script Export-RetentionTags.ps1 exporta todas las directivas y etiquetas de retención de la organización.



Para otras tareas de administración relacionadas con la administración de registros de mensajes, consulte [Procedimientos de administración de registros de mensajería](messaging-records-management-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 10 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Administración de los registros de mensajes" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Los procedimientos de este tema dependen de estos tres archivos en la carpeta `%ExchangeInstallPath%Scripts` en el servidor deExchange:
    
      - Export-RetentionTags.ps1
    
      - Import-RetentionTags.ps1
    
      - MigrateRetentionTags.strings.psd1

  - No puede seleccionar directivas o etiquetas de retención específicas para exportar o importar. El script Export-RetentionTags.ps1 exporta todas las directivas y etiquetas de retención de la organización. El script Import-RetentionTags.ps1 importa todas las directivas y etiquetas de retención del archivo XML que se está importando y sustituye todas las existentes en una organización de Exchange.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Paso 1: Exportar etiquetas de retención de una organización de Exchange local

1.  Ejecute este comando Shell de administración de Exchange para cambiar el directorio en el subdirectorio de **secuencias de comandos** en la ruta de instalación Exchange.
    
    ```powershell
    Cd $Env:ExchangeInstallPath\Scripts
    ```

2.  Ejecute el script Export-RetentionTags.ps1 para exportar las etiquetas de retención a un archivo XML.
    

    > [!IMPORTANT]
    > Si está importando o exportando etiquetas de retención y las políticas de retención para Exchange Online, debe conectar la sesión de Windows PowerShell para Exchange Online. Para obtener más información, consulte <A href="https://technet.microsoft.com/es-es/library/jj984289(v=exchg.150)">Conectarse a Exchange Online mediante PowerShell remoto</A>.

    
    ```powershell
    .\Export-RetentionTags.ps1 "c:\docs\ExportedRetentionTags.xml"
    ```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que ha exportado correctamente las etiquetas y directivas de retención, siga estos pasos:

1.  Vaya a la ruta que especificó en el comando para exportar y compruebe que se ha creado el archivo XML con el nombre especificado.

2.  También puede abrir el archivo XML en un editor de texto para consultar el contenido.

## Paso 2: Importar etiquetas de retención a una organización de Exchange

1.  Ejecute este comando Shell de administración de Exchange para cambiar el directorio en el subdirectorio de **secuencias de comandos** en la ruta de instalación Exchange.
    
    ```powershell
    Cd $Env:ExchangeInstallPath\Scripts
    ```

2.  Ejecute el script Import-RetentionTags.ps1 para importar las etiquetas de retención desde un archivo XML exportado previamente.
    

    > [!IMPORTANT]
    > Si está importando o exportando etiquetas de retención y las políticas de retención para Exchange Online, debe conectar la sesión de Windows PowerShell para Exchange Online. Para obtener más información, consulte <A href="https://technet.microsoft.com/es-es/library/jj984289(v=exchg.150)">Conectarse a Exchange Online mediante PowerShell remoto</A>.

    

    > [!NOTE]
    > Cuando se ejecuta esta secuencia de comandos contra Exchange Online, se puede pedirá que confirme que desea ejecutar el software desde un publicador de confianza. Compruebe que el nombre del editor aparece como <CODE>CN=Microsoft Corporation, OU=MOPR, O=Microsoft Corporation, L=Redmond, S=Washington, C=US</CODE>y, a continuación, haga clic en <STRONG>R</STRONG> para permitir que la secuencia de comandos debe ejecutarse una vez o <STRONG>A</STRONG> ejecutar siempre.

    
    ```powershell
    .\Import-RetentionTags.ps1 "c:\docs\ExportedRetentionTags.xml"
    ```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que ha importado correctamente las etiquetas y directivas de retención, siga estos pasos:

1.  En el EAC, vaya a **Administración de cumplimiento** \> **Etiquetas de retención** y compruebe que las etiquetas de retención se han importado correctamente. Vaya a **Administración de cumplimiento** \> **Directivas de retención** y compruebe que las directivas de retención se han importado correctamente.

2.  Usar los cmdlets de **Get-RetentionPolicy** y **Get-RetentionPolicyTag** para comprobar que se han creado las directivas y etiquetas. Para obtener un ejemplo acerca de cómo recuperar las políticas de retención y etiquetas de retención, consulte los ejemplos en [Get-RetentionPolicyTag](https://technet.microsoft.com/es-es/library/dd298009\(v=exchg.150\)) y [Get-RetentionPolicy](https://technet.microsoft.com/es-es/library/dd298086\(v=exchg.150\)).

