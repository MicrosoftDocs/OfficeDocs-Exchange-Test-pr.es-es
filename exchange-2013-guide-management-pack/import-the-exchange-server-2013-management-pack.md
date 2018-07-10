---
title: Importación del módulo de administración de Exchange Server 2013
TOCTitle: Importación del módulo de administración de Exchange Server 2013
ms:assetid: dc929928-61b8-448b-9ae5-d3fa73a18ee9
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn195914(v=EXCHG.150)
ms:contentKeyID: 53181937
ms.date: 04/03/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Importación del módulo de administración de Exchange Server 2013

 

_**Última modificación del tema:**   2013-03-30_

Comencemos con la importación del módulo de administración para su implementación de SCOM.

## Requisitos previos

Antes de importar el módulo de administración, compruebe que se cumplan las siguientes condiciones:

  - Tiene una de las siguientes versiones de System Center Operations Manager implementadas en su organización.
    
      - System Center Operations Manager 2012 RTM o posterior
    
      - System Center Operations Manager 2007 R2 o posterior

  - Ya ha implementado agentes de SCOM en sus servidores de Exchange. [Comprobar el estado de implementación de los agentes](procedures-related-to-deployment.md).

  - Los agentes de SCOM de sus servidores de Exchange se ejecutan en la cuenta del sistema local. [Comprobar la configuración de seguridad del agente](procedures-related-to-deployment.md).

  - Los agentes de SCOM de los servidores de Exchange están configurados para que actúen como proxy y puedan detectar objetos administrados en otros equipos. [Compruebe la configuración de proxy del agente](procedures-related-to-deployment.md).

  - Su cuenta de usuario es miembro del rol de administradores de Operations Manager.

## Importación del módulo de administración de Exchange Server 2013

Siga los pasos siguientes para importar el módulo de administración de Exchange Server 2013. Este procedimiento implica que haya extraído el contenido del módulo de administración a un disco local en su servidor de System Center Operations Manager (SCOM). Para descargar el módulo de administración de Exchange Server 2013:

1.  Inicie sesión en el servidor de SCOM y descargue el módulo de administración de Exchange Server 2013 desde el [Centro de descargas de Microsoft](http://go.microsoft.com/fwlink/p/?linkid=268587).

2.  Extraiga el contenido del módulo de administración en una carpeta del sistema mediante la ejecución del archivo `ExchangeServerManagementPack.msi`.

3.  Inicie la Consola de SCOM. En la consola de SCOM, haga clic en **Administración**.

4.  Haga clic con el botón secundario en **Módulos de administración** y luego haga clic en **Importar módulos de administración**.

5.  Se abre el Asistente para importar módulos de administración. Seleccione **Agregar** y, a continuación, haga clic en **Agregar desde disco**.

6.  Se abrirá el cuadro de diálogo **Seleccionar módulos de administración que se van a importar**. Vaya al directorio en el que extrajo el módulo de administración. Haga clic en el archivo `Microsoft.Exchange.15.mp` y luego haga clic en **Abrir**.

7.  En la página **Seleccionar módulos de administración** aparecerá el módulo de administración de Exchange Server 2013. Haga clic en **Instalar**.

8.  Aparecerá la página **Importar módulos de administración** y mostrará el progreso. Si se produce algún problema en alguna de las fases del proceso de importación, seleccione el paquete de administración de la lista para ver los detalles sobre el estado.

9.  Cuando la importación esté completa, haga clic en **Cerrar**.

10. Haga clic en **Ver** y luego en **Actualizar**, o presione F5 para ver el módulo de administración de Microsoft Exchange Server 2013 en la lista de módulos de administración.

Ahora que ya ha importado el módulo de administración, vea [Introducción al módulo de administración de Exchange Server 2013](getting-started-with-exchange-server-2013-management-pack.md) para obtener más información sobre el nuevo panel.

