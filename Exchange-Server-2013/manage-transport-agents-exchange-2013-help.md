---
title: 'Administrar agentes de transporte: Exchange 2013 Help'
TOCTitle: Administrar agentes de transporte
ms:assetid: f15ab7e4-015d-45b1-9c10-f733d7cd2a36
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb125175(v=EXCHG.150)
ms:contentKeyID: 49896007
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Administrar agentes de transporte

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-04-08_

Los agentes de transporte usan los eventos SMTP para procesar los mensajes a medida que pasan por la canalización de transporte. La mayoría de los agentes de transporte integrados incluidos en Microsoft Exchange Server 2013 son invisibles y no administrables. No obstante, puede instalar y configurar agentes de transporte de terceros en servidores de Exchange en su organización. Para obtener más información acerca de los agentes de transporte, consulte [Agentes de transporte](transport-agents-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 10 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Agentes de transporte" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Solo puede usar el Shell para realizar este procedimiento.

  - La compatibilidad con agentes de transporte no está habilitada de manera predeterminada, pero puede hacerlo. Para obtener instrucciones, vea [Habilitar la compatibilidad para agentes de transporte heredados](enable-support-for-legacy-transport-agents-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Acerca de los procedimientos del agente de transporte en el servicio de transporte front-end en los servidores de acceso de cliente

No puede usar el Shell de administración de Exchange para administrar el agente de transporte en el servicio de transporte front-end o en un servidor de acceso de cliente. En cambio, debe abrir Windows PowerShell en el servidor de acceso de cliente y, a continuación, importar los cmdlets de Exchange en la sesión de Windows PowerShell.


> [!WARNING]
> No se admite la ejecución de cmdlets de Exchange en Windows PowerShell para tareas que no sean la administración de agentes de transporte en el servicio de transporte front-end. Pueden ocurrir consecuencias graves si omite el Shell de administración de Exchange y el control de acceso basado en roles (RBAC), y ejecuta los cmdlets de Exchange en Windows PowerShell. Siempre debe ejecutar los cmdlets de Exchange en el Shell de administración de Exchange. Para obtener más información, consulte <A href="release-notes-for-exchange-2013-exchange-2013-help.md">Notas de la versión de Exchange&nbsp;2013</A>.



Para realizar cualquiera de los procedimientos del agente de transporte descritos en este tema, en el servicio de transporte front-end, debe seguir estos pasos adicionales:

1.  En el servidor de acceso de cliente, abra Windows PowerShell y ejecute el siguiente comando:
    
    ```powershell
    Add-PSSnapin Microsoft.Exchange.Management.PowerShell.SnapIn
    ```
2.  Ejecute el comando descrito, pero agregue el siguiente valor: `-TransportService FrontEnd`.
    
    Por ejemplo, para ver los agentes de transporte en el servicio de transporte front-end en un servidor de acceso de cliente, ejecute el siguiente comando:
    
    ```powershell
    Get-TransportAgent -TransportService FrontEnd
    ```
## Uso del Shell para instalar un agente de transporte

Cuando instala un agente de transporte, Exchange solamente registra las DLL asociadas con el agente de transporte. Debe asegurarse de que todos los archivos, claves de registro y otros objetos en los que depende el agente de transporte estén instalados y configurados correctamente. Después de que Exchange carga las DLL, sigue haciendo referencia a las DLL una vez finalizado el comando.

Los agentes de transporte tienen acceso completo a todos los mensajes de correo electrónico que encuentran. Exchange no restringe en modo alguno el comportamiento de los agentes de transporte. Los agentes de transporte que sean inestables o tengan problemas de seguridad pueden afectar a la estabilidad y seguridad de Exchange. Por lo tanto, solamente debe instalar agentes de transporte en los que confía totalmente y que han sido probados completamente en un entorno de prueba.

Los agentes de transporte están instalados en estado deshabilitado para garantizar que el flujo de correo no se vea afectado por los agentes de transporte que aún no se hayan configurado. Por lo tanto, después de configurar correctamente un agente de transporte, debe habilitarlo.

Utilice la sintaxis siguiente para instalar un agente de transporte.

```powershell
Install-TransportAgent -Name <TransportAgentIdentity> -TransportAgentFactory <"TransportAgentFactory"> -AssemblyPath <"FilePath">
```

En este ejemplo, se instala un agente de transporte ficticio denominado Contoso Transport Agent en el servicio de transporte de un servidor de buzones de correo.

```powershell
Install-TransportAgent -Name "Contoso Transport Agent" -TransportAgentFactory "vendor.exchange.ContosoTransportAgentfactory" -AssemblyPath "C:\Program Files\Vendor\TransportAgent\ContosoTransportAgentFactory.dll"
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que el agente de transporte se instaló correctamente, ejecute el comando `Get-TransportAgent` y compruebe que el agente de transporte esté enumerado.

## Usar el Shell para habilitar un agente de transporte

Use la sintaxis siguiente para habilitar un agente de transporte.

```powershell
Enable-TransportAgent <TransportAgentIdentity>
```

En este ejemplo, se habilita el agente de transporte denominado Contoso Transport Agent en el servicio de transporte de un servidor de buzones de correo.

```powershell
Enable-TransportAgent "Contoso Transport Agent"
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que el agente de transporte se habilitó correctamente, ejecute el comando `Get-TransportAgent | Format-List Name,Enabled` y compruebe que el agente de transporte esté habilitado.

## Usar el Shell para deshabilitar un agente de transporte

Use la sintaxis siguiente para deshabilitar un agente de transporte:

```powershell
Disable-TransportAgent <TransportAgentIdentity>
```

En este ejemplo, se deshabilita el agente de transporte denominado Fabirkam Transport Agent en el servicio de transporte de un servidor de buzones de correo.

```powershell
Disable-TransportAgent "Fabrikam Transport Agent"
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que el agente de transporte se deshabilitó correctamente, ejecute el comando `Get-TransportAgent | Format-List Name,Enabled` y compruebe que el agente de transporte esté deshabilitado.

## Usar el Shell para ver los agentes de transporte

Para ver una lista de resumen de todos los agentes de transporte, ejecute el siguiente comando:

```powershell
Get-TransportAgent
```

Para ver la configuración detallada de un agente de transporte específico, ejecute el siguiente comando:

```powershell
Get-TransportAgent <TransportAgentIdentity> | Format-List
```
En este ejemplo, se proporciona una configuración detallada del agente de transporte denominado Transport Rule Agent.

```powershell
Get-TransportAgent "Transport Rule Agent" | Format-List
```

## Usar el Shell para configurar la prioridad de un agente de transporte

Cuanto más cercana a 0 sea la prioridad de un agente de transporte, antes procesará los mensajes de correo electrónico. No obstante, el evento SMTP en la canalización de transporte donde está registrado el agente de transporte puede hacer que un agente de menor prioridad procese el mensaje antes que un agente de mayor prioridad.

Para modificar la prioridad de un agente de transporte existente, ejecute el siguiente comando:

```powershell
Set-TransportAgent <TransportAgentIdentity> -Priority <Integer>
```

En este ejemplo, se establece en 3 el valor de prioridad para el agente de transporte existente denominado Contoso Transport Agent en el servicio de transporte de un servidor de buzones de correo.

```powershell
Set-TransportAgent "Contoso Transport Agent" -Priority 3
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la prioridad del agente de transporte se configuró correctamente, ejecute el comando `Get-TransportAgent | Format-List Name,Priority` y compruebe el valor de prioridad del agente de transporte.

## Uso del Shell para desinstalar un agente de transporte

Cuando se desinstala el agente de transporte, Exchange elimina el registro de los archivos de DLL usados con el agente. Exchange no quita ningún archivo, clave de registro u otros objetos agregados mediante la instalación del agente de transporte.

Para desinstalar un agente de transporte, ejecute el siguiente comando:

```powershell
Uninstall-TransportAgent <TransportAgentIdentity>
```

En este ejemplo, se desinstala el agente de transporte denominado Fabirkam Transport Agent del servicio de transporte de un servidor de buzones de correo.

```powershell
Uninstall-TransportAgent "Fabrikam Transport Agent"
```
## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que el agente de transporte se desinstaló correctamente, ejecute el comando `Get-TransportAgent` y compruebe que el agente de trasporte no esté enumerado.

