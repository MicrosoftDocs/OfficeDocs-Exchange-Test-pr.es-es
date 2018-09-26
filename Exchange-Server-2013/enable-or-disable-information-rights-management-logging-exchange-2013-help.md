---
title: 'Habilita deshabilita registro Information Rights Management Exchange 2013 Help'
TOCTitle: Habilitar o deshabilitar el registro de Information Rights Management
ms:assetid: 6933bc65-4d98-4878-9167-0e9eaac68b6b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ff686962(v=EXCHG.150)
ms:contentKeyID: 49895681
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar o deshabilitar el registro de Information Rights Management

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-12_

En Exchange Server 2013, puede usar los registros de Information Rights Management (IRM) para supervisar las operaciones de IRM y solucionar problemas en ellas. El registro de IRM está habilitado de forma predeterminada.

Los registros de IRM usan el conjunto siguiente de parámetros comunes:

  - *IrmLogEnabled*   Habilita o deshabilita el registro de IRM. Predeterminado: `$true`.

  - *IrmLogMaxAge*   Especifica la antigüedad máxima de los archivos de registro de IRM. Los archivos anteriores a la antigüedad especificada se eliminan. Predeterminado: 30 días.

  - *IrmLogMaxDirectorySize*   Especifica el tamaño máximo del directorio que contiene registros de IRM. Cuando un directorio alcanza su tamaño de archivo máximo, el servidor elimina primero los archivos de registro más antiguos. Predeterminado: 250 MB.

  - *IrmLogMaxFileSize*   Especifica el tamaño máximo de cada archivo de registro de IRM. Cuando un archivo de registro llega al tamaño especificado, se crea uno nuevo. Predeterminado: 10 MB.

  - *IrmLogPath*   Especifica la ubicación del directorio de registros de IRM. Predeterminado: `%ExchangeInstallPath%Logging\IRMLogs`.

Para consultar otras tareas de administración relacionadas con IRM, vea [Procedimientos de Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 2-5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Configurar registro de IRM" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - No puede usar el Centro de administración de Exchange (EAC) para habilitar o deshabilitar el registro de IRM en un servidor. Debe usar el Shell

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Uso del shell para habilitar el registro de IRM en un servidor

En este ejemplo se habilita el registro de IRM en un servidor de buzones.

```powershell
Set-TransportService -Identity EXCH01 -IRMLogEnabled $true
```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-TransportService](https://technet.microsoft.com/es-es/library/jj215682\(v=exchg.150\)).

## Uso del shell para deshabilitar el registro de IRM en un servidor

En este ejemplo se deshabilita el registro de IRM en un servidor de buzones.

```powershell
Set-TransportService -Identity EXCH01 -IRMLogEnabled $false
```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-TransportService](https://technet.microsoft.com/es-es/library/jj215682\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que el registro de IRM se habilitó o deshabilitó correctamente en un servidor, ejecute el cmdlet [Get-TransportService](https://technet.microsoft.com/es-es/library/jj215746\(v=exchg.150\)) para recuperar la configuración de IRM.

En este ejemplo se recuperan todas las propiedades de registro de IRM en el servidor EXCH01.

```powershell
Get-TransportService -Identity EXCH01 | Format-List IRMLog*
```
