---
title: 'Descargar actualizaciones del motor y definición: Exchange 2013 Help'
TOCTitle: Descargar actualizaciones del motor y definición
ms:assetid: 8f2ca383-e463-4df0-aa5d-29afe2f81aaf
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ657471(v=EXCHG.150)
ms:contentKeyID: 49895773
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Descargar actualizaciones del motor y definición

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-04-08_

Los administradores de Microsoft Exchange Server 2013 pueden descargar manualmente las actualizaciones del motor antimalware y de (la firma) de definiciones. Se recomienda encarecidamente que descargue dichas actualizaciones en su servidor de Exchange antes de empezar a utilizarlo.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 5 minutos

  - Para descargar las actualizaciones, su equipo debe tener acceso a Internet y debe poder establecer una conexión en el puerto TCP 80 (HTTP).

  - UNRESOLVED\_TOKEN\_VAL(PD\_Shell\_Only\_Procedure)

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Antimalware" en el tema [Permisos de protección contra correo electrónico no deseado y antimalware](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Uso del Shell para descargar manualmente las actualizaciones de definiciones y del motor

Para descargar las actualizaciones del motor y de definiciones, ejecute el siguiente comando:

```powershell
& $env:ExchangeInstallPath\Scripts\Update-MalwareFilteringServer.ps1 -Identity <FQDN of server>
```

Este ejemplo descarga manualmente las actualizaciones del motor y de definiciones en un servidor denominado mailbox01.contoso.com:

```powershell
& $env:ExchangeInstallPath\Scripts\Update-MalwareFilteringServer.ps1 -Identity mailbox01.contoso.com
```

Si quiere, puede especificar el parámetro –EngineUpdatePath, que le permite descargar actualizaciones desde un lugar que no sea el predeterminado, http://forefrontdl.microsoft.com/server/scanengineupdate. Puede ser una dirección HTTP o una ruta de acceso UNC. Si es una ruta de acceso UNC, el servicio de red debe tener acceso a la ruta. En este ejemplo, se descargan manualmente las actualizaciones de definición y de motor desde un directorio local a un servidor llamado mailbox01.contoso.com:

```powershell
  & $env:ExchangeInstallPath\Scripts\Update-MalwareFilteringServer.ps1 -Identity mailbox01.contoso.com -EngineUpdatePath \\Server\sharename
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para poder verificar que se han descargado las actualizaciones correctamente, debe acceder al Visor de eventos y visualizar el registro de eventos. Le recomendamos que filtre únicamente los eventos FIPFS, tal como se describe en el siguiente procedimiento.

1.  En el menú **Inicio**, haga clic en **Todos los programas** \> **Herramientas de administración** \> **Visor de eventos**.

2.  En el Visor de eventos, expanda la carpeta **Registros de Windows** y, a continuación, haga clic en **Aplicación**.

3.  En el menú **Acciones**, haga clic en **Filtrar registro actual**.

4.  En el cuadro de diálogo **Filtrar registro actual**, en la lista desplegable **Fuentes de eventos**, seleccione la casilla **FIPFS** y, a continuación, haga clic en **Aceptar**.

Si las actualizaciones del motor se han descargado correctamente, verá la Id. de Evento 6033, que se parecerá a lo siguiente:

`MS Filtering Engine Update process performed a successful scan engine update.`

`Scan Engine: Microsoft`

`Update Path: http://forefrontdl.microsoft.com/server/scanengineupdate`

`Last Update time: ‎2012‎-‎08‎-‎16T13:22:17.000Z`

`Engine Version: 1.1.8601.0`

`Signature Version: 1.131.2169.0`

## Más información

[Configurar directivas antimalware](configure-anti-malware-policies-exchange-2013-help.md)

