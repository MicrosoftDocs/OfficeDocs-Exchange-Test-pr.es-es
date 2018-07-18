---
title: Usar módulo de administración de Exchange Server para solucionar problemas
TOCTitle: Usar el módulo de administración de Exchange Server 2013 para solucionar problemas
ms:assetid: c9672dad-1e67-4f07-bad9-539a67f2ac70
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn195913(v=EXCHG.150)
ms:contentKeyID: 53181936
ms.date: 04/03/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Usar el módulo de administración de Exchange Server 2013 para solucionar problemas

 

_**Última modificación del tema:**   2013-04-09_

En [Introducción al módulo de administración de Exchange Server 2013](getting-started-with-exchange-server-2013-management-pack.md) encontrará una introducción al panel de módulo de administración Este tema sirve de orientación para saber cómo se puede usar dicho panel para solucionar un problema. El proceso queda ilustrado de mejor forma con un ejemplo. Imaginemos el siguiente escenario:

Fernando Acedo es un administrador de Exchange en Contoso. Abre la consola SCOM y hace clic en **Estado del servidor** en el panel de Exchange Server 2013 para ver el estado de sus servidores Exchange. Advierte que uno de sus servidores CAS está en estado crítico en **Componentes del servicio**.

![Error en el servidor CAS](images/Dn195913.32a265d9-68e0-4d8c-9f83-1d10cdda1f84(EXCHG.150).png "Error en el servidor CAS")

Fernando hace doble clic en el servidor y se abre la ventana **Explorador de estado**, donde ve que el componente de servicio en mal estado es el conjunto de mantenimiento OWA.Proxy. Hace clic en este conjunto de mantenimiento para ver información sobre él.

![Detalles del conjunto de mantenimiento del servidor CAS que ha presentado error](images/Dn195913.8e4d05a6-9128-40d8-b262-e60e9affc973(EXCHG.150).png "Detalles del conjunto de mantenimiento del servidor CAS que ha presentado error")

El vínculo incluido en los recursos de conocimiento externos lleva a Fernando al tema [Solución de problemas del conjunto de mantenimiento OWA.Proxy](https://technet.microsoft.com/es-es/library/jj737712\(v=exchg.150\)). En este artículo, Fernando ve que lo primero que hay que hacer es comprobar si el problema persiste. Siguiendo las instrucciones, ejecuta el siguiente comando en el Shell para comprobar el estado actual del conjunto de mantenimiento OWA.Proxy:

```Powershell
    Get-ServerHealth Server1.contoso.com | ?{$_.HealthSetName -eq "OWA.Proxy"}
```

Al ejecutar este comando, obtiene lo siguiente:

```Powershell
    Server          State           Name                 TargetResource       HealthSetName   AlertValue ServerComp
                                                                                                         onent
    ------          -----           ----                 --------------       -------------   ---------- ----------
    Server1         Online          OWAProxyTestMonitor  MSExchangeOWAAppPool OWA.Proxy       Unhealthy  OwaProxy
    Server1         Online          OWAProxyTestMonitor  MSExchangeOWACale... OWA.Proxy       Healthy    OwaProxy
```

Fernando ve que el problema reside en el grupo de aplicaciones de OWA. El siguiente paso consiste en volver a ejecutar la sonda asociada del monitor con el mantenimiento incorrecto. Consultando la tabla del tema sobre cómo solucionar problemas del conjunto de mantenimiento OWA.Proxy, averigua que la sonda que hay que volver a ejecutar es OWAProxyTestProbe. Ejecuta el siguiente comando:

```Powershell
    Invoke-MonitoringProbe OWA.Proxy\OWAProxyTestProbe -Server Server1.contoso.com | Format-List
```

Analiza la salida del valor ResultType y ve que la sonda genera un error:

```Powershell
    ResultType : Failed
```

Ahora pasa a la sección sobre las acciones de recuperación de OWAProxyTestMonitor del artículo. Se conecta a Server1 por medio del Administrador de IIS para ver si MSExchangeOWAAppPool se está ejecutando en el servidor IIS. Tras confirmar que se está ejecutando, el siguiente paso le indica que recicle MSExchangeOWAAppPool:

```Powershell
    C:\Windows\System32\Inetsrv\Appcmd recycle APPPOOL MSExchangeOWAAppPool
```

Tras constatar que MSExchangeOWAAppPool se recicla correctamente, vuelve atrás para ver si el problema persiste, para lo cual vuelve a ejecutar la sonda por medio del cmdlet Invoke-MonitoringProbe y, esta vez, comprueba que el resultado es el adecuado. Luego, ejecuta el siguiente comando para comprobar que el conjunto de mantenimiento vuelve a mostrar un estado **Correcto**:

```Powershell
    Get-ServerHealth Server1.contoso.com | ?{$_.HealthSetName -eq "OWA.Proxy"}
```

Esta vez ve que el problema se ha solucionado.

```Powershell
    Server          State           Name                 TargetResource       HealthSetName   AlertValue ServerComp
                                                                                                         onent
    ------          -----           ----                 --------------       -------------   ---------- ----------
    Server1         Online          OWAProxyTestMonitor  MSExchangeOWAAppPool OWA.Proxy       Healthy    OwaProxy
    Server1         Online          OWAProxyTestMonitor  MSExchangeOWACale... OWA.Proxy       Healthy    OwaProxy
```

Vuelve a la consola SCOM y confirma que está arreglado.

![Estado del servidor](images/Dn195913.c863be83-fc4b-4daf-a18b-27b1aae15b1d(EXCHG.150).png "Estado del servidor")

El escenario aquí abordado es una sencilla demostración del flujo de trabajo de solución de problemas al ver una alerta en la consola SCOM. Si bien los detalles pueden variar, este flujo de trabajo será generalmente bastante parecido en cada problema que se notifique en la consola.

