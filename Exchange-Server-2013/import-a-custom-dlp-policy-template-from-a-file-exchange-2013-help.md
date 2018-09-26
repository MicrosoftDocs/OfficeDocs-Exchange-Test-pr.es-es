---
title: 'Importar plantilla directiva DLP personalizada de archivo: Exchange 2013 Help'
TOCTitle: Importar una plantilla de directiva DLP personalizada desde un archivo
ms:assetid: 83f49dbd-f9b1-498e-b548-1529c5e1ccdb
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150531(v=EXCHG.150)
ms:contentKeyID: 48267680
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Importar una plantilla de directiva DLP personalizada desde un archivo

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2016-08-09_

Puede administrar la información confidencial con las directivas de DLP mediante la importación de un archivo que contiene la configuración de información de directivas. Pueden desarrollarse plantillas de directivas DLP independientes de Exchange como archivos XML. Pero deben cumplir con requisitos de formato específicos para funcionar correctamente. Opcionalmente, las directivas que se exportan de una versión anterior de Exchange se pueden importar a Microsoft Exchange Server 2013.


> [!WARNING]  
> Debe habilitar sus directivas de DLP en modo de prueba antes de ejecutarlo en su entorno de producción. Durante dichas pruebas, se recomienda que configure buzones de usuarios de ejemplo y envíe mensajes de prueba que invoquen las directivas de prueba para confirmar los resultados.



## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 15 minutos

  - entrada Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el "Prevención de pérdida de datos (DLP)" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]  
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Use el EAC para importar una plantilla de directiva DLP personalizada desde un archivo

Use el siguiente procedimiento para importar una plantilla de directiva de DLP personalizada desde un archivo. Para evitar confusiones, proporcione un nombre exclusivo a cada parte de su directiva o regla cuando tenga la opción de introducir su propio nombre.

1.  En el EAC, vaya a **Administración de cumplimiento** \> **Prevención de pérdida de datos**.

2.  Haga clic en la flecha que se encuentra junto al icono **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") y, a continuación, haga clic en **Importar directiva**.

3.  En la página **Importar directiva**, complete los campos siguientes:
    
    1.  **Seleccione el archivo para importar** Agregue el nombre del archivo de directiva que desea instalar.
    
    2.  **Nombre** Agregue un nombre que distinga esta directiva de las demás.
    
    3.  **Descripción** Opcionalmente, agregue una descripción que resuma esta directiva.
    
    4.  **Más opciones** Seleccione el modo o estado para esta directiva. La nueva directiva no estará completamente habilitada hasta que especifique que debe estarlo. El modo predeterminado para una directiva es de prueba sin notificaciones.
    
    5.  Haga clic en **Siguiente** para validar e importar la directiva.

## Use el Shell para importar una plantilla de directiva DLP personalizada desde un archivo

En este ejemplo se importa un archivo de plantilla de directiva de DLP personalizada en el archivo C:\\Mis documentos\\DLP Backup.xml. Importar una colección de directivas de DLP desde un archivo XML elimina o sobrescribe todas las directivas de DLP preexistentes que se definieron en la organización. Asegúrese de que tiene una copia de seguridad de la colección de directivas DLP antes de importar y sobrescribir las directivas DLP actuales.

```powershell
Import-DlpPolicyCollection -FileData ([Byte[]]$(Get-Content -Path " C:\My Documents\DLP Backup.xml " -Encoding Byte -ReadCount 0))
```

## Más información

[Prevención de pérdida de datos](https://docs.microsoft.com/es-es/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention)