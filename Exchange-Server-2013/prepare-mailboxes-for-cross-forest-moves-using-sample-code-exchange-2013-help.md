---
title: 'Preparar buzón para pasar entre bosque con código ejemplo: Exchange 2013 Help'
TOCTitle: Preparar buzones para movimientos entre bosques mediante código de ejemplo
ms:assetid: f35ac7a5-bb84-4653-b6d0-65906e93627b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee861124(v=EXCHG.150)
ms:contentKeyID: 49896012
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Preparar buzones para movimientos entre bosques mediante código de ejemplo

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Microsoft Exchange 2013 admite migraciones y movimientos de buzones de correo mediante los cmdlets **New-MoveRequest** y **New-MigrationBatch**. También puede mover el buzón a través del Centro de administración de Exchange (EAC). Puede mover un buzón de correo de un bosque Exchange de origen a un bosque Exchange 2010 de destino.

Para ejecutar **New-MoveRequest**, debe existir un usuario de correo en el bosque de Exchange de destino y el usuario de correo debe contar con un conjunto mínimo de atributos de Active Directory obligatorios.  Puede crear el usuario de correo requerido en el bosque de destino de Exchange personalizando la implementación de Microsoft Identity Lifecycle Manager (ILM) 2007. El código de ejemplo de extensión de reglas basado en ILM descrito en este tema demuestra cómo personalizar la implementación de ILM actual para crear los usuarios habilitados para correo requeridos en el bosque de Exchange 2013 de destino.

Para obtener más información acerca de los preparativos para movimientos entre bosques, incluidas las descripciones de los atributos requeridos de Active Directory, consulte [Preparar los buzones para las solicitudes de movimiento entre bosques](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Descargue el código de ejemplo de la página [Prepararse para mover buzones de correo en línea](https://go.microsoft.com/fwlink/p/?linkid=177882) del Centro de descarga de Microsoft.

  - Para ejecutar el código de ejemplo, necesitará ILM 2007 Feature Pack 1 Service Pack 1 (SP1). Para descargar el paquete de características, consulte el artículo 977791 de Microsoft Knowledge Base, [Service Pack 1 (compilación 3.3.1139.2) está disponible para Identity Lifecycle Manager 2007 Feature Pack 1](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=977791).

  - También necesitará lo siguiente:
    
      - Un bosque de origen que ejecuta Exchange 2013, donde reside actualmente el buzón de correo.
    
      - El bosque de destino con Exchange 2013 instalado, donde se trasladará el buzón de correo.

  - Para conectarse al bosque de destino de Exchange 2013, debe tener el permiso adecuado para llamar al cmdlet **UpdateRecipient**. Para ver qué permisos necesita, consulte la sección "Permisos de destinatarios" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Cómo realiza esto?

## Paso 1: Instalar el código de ejemplo ILM

1.  En Microsoft Visual Studio2008, abra Microsoft.Exchange.Sample.OneWayGALSync.sln para ver el código de ejemplo. El código de ejemplo incluye lo siguiente:
    
      - Microsoft.MetadirectoryServicesEx.dll es el archivo binario que se envía con ILM 2007 FP1 SP1, en “\\Archivos de programa\\Microsoft Identity Integration Server\\Bin\\Assemblies”. Se hace referencia en el código de ejemplo.
    
      - OneWaySync.xml se hace referencia en el código de ejemplo.
    
      - La carpeta ILMServerConfig contiene los archivos de configuración de ILM para el agente de administración (MA) de origen, el MA de destino e ILM Metaverse (MV).
    
      - Microsoft.Exchange.Sample.OneWayGALSync.MARules.dll y Microsoft.Exchange.Sample.OneWayGALSync.MVRules.dll (generado a partir del código de ejemplo) que se encuentran bajo “ \\obj\\Debug ”.

2.  En el servidor ILM, copie lo siguiente en \\Archivos de programa\\Microsoft Identity Integration Server\\Extensiones:
    
      - OneWaySync.xml
    
      - Microsoft.Exchange.Sample.OneWayGALSync.MARules.dll
    
      - Microsoft.Exchange.Sample.OneWayGALSync.MVRules.dll

3.  Edite el archivo OneWaySync.xml que copió en la carpeta Extensiones de ILM en el paso 1 para especificar el nombre distintivo (DN) del contenedor de la OU de destino en el bosque de destino de Exchange en el que desea crear los usuarios de correo. Puede usar LDP.exe o ADSIEdit.exe para buscar el contenedor de la OU de destino si no sabe cómo se llama.
    

    > [!NOTE]
    > Si usa este ejemplo junto con ILM GalSync 2007, excluya este contenedor de la lista de contenedores administrados por GalSync2007.



4.  En la Consola de ILM Identity Manager, vaya a **Archivo** \> **Importar configuración de servidor** para importar la configuración del servidor de ILM desde la carpeta ILMServerConfig. Con esta acción se importan dos agentes de administración de Active Directory junto con el esquema Metaverse y la regla de aprovisionamiento.
    

    > [!NOTE]
    > Durante la importación se deben indicar el nombre del bosque y las credenciales, y asociar las particiones del agente de administración de Active Directory (ADMA) que se debe importar con el nombre de partición en su configuración, tanto para el ADMA de origen como para el de destino.



5.  Para que el ADMA admita el bosque de destino de Exchange 2013, en la página **Crear agente de administración**, en el panel **Configurar extensiones**, seleccione **Exchange 2013** en la lista desplegable **Aprovisionar para** y, a continuación, escriba el URI remoto de Windows PowerShell de un servidor de acceso de cliente de Exchange 2010 en **URI de Exchange 2013 RPS**.
    
    **Crear la página del agente de administración**
    
    ![Aprovisionamiento de Exchange 2010 del agente de administración](images/Aa998597.8f403cda-e5e4-4edf-887f-c1ed46cee3f5(EXCHG.150).gif "Aprovisionamiento de Exchange 2010 del agente de administración")  

6.  En la Consola de ILM Identity Manager, en el panel **Crear agente de administración**, abra **Propiedades** para el agente de administración del bosque de origen. Seleccione el asistente **Configurar particiones de directorio** y, a continuación, haga clic en **Contenedores** para seleccionar el contenedor que contendrá los buzones que se van a mover al bosque de destino. Anule la selección de los demás contenedores, es decir, delimite el ámbito del agente de administración de modo que administre únicamente este contenedor. Del mismo modo, en el caso del MA del bosque de destino, seleccione el contenedor para el que se van a aprovisionar usuarios habilitados para correo, es decir, la OU de destino especificada en el paso 2.
    

    > [!NOTE]
    > Si usa este ejemplo junto con ILM GalSync 2007, excluya los dos contenedores de la lista de contenedores administrados por GalSync2007.



7.  Realice una importación completa inicial (solamente de ensayo) en los MA de destino para que ILM pueda encontrar la OU de destino especificada en el paso 2.

## Paso 2: Crear el usuario de correo en el bosque de destino de Exchange

Ahora que ha instalado el código de ejemplo, siga el procedimiento siguiente para crear el usuario de correo necesario en el bosque de destino de Exchange, de modo que se pueda ejecutar **New-MoveRequest** para mover buzones en línea.

1.  En el bosque de origen, use el Centro de administración de Exchange para crear usuarios de buzones en el contenedor seleccionado en el paso 4 "Instalar el código de ejemplo ILM". También puede usar Usuarios y equipos de Active Directory para mover los usuarios de buzones de correo existentes al contenedor.

2.  Realice la importación delta y la sincronización delta en el MA de origen para encontrar los buzones agregados al contenedor de origen y aprovisionar usuarios de correo para dicho MA de destino.

3.  Realice la exportación en el MA de destino para exportar los usuarios de correo aprovisionados en el paso 1 para Active Directory de destino.

4.  Realice la importación delta del MA de destino para confirmar los cambios exportados en el paso 2.

5.  En el bosque de destino, abra el Shell de administración de Exchange y use el cmdlet **New-MoveRequest** para mover buzones desde el bosque de origen.

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la migración se completó correctamente, realice lo siguiente:

  - En el bosque de destino, compruebe que los usuarios que movió del bosque de origen estén presentes en el bosque de destino.

