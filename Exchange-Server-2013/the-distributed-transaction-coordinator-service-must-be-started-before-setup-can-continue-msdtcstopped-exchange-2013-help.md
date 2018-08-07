---
title: 'Coordinador transacción distribuida iniciar antes programa instalar continuar'
TOCTitle: El servicio Coordinador de transacciones distribuidas debe iniciarse antes de que el programa de instalación pueda continue_MSDTCStopped
ms:assetid: 96e33c94-348e-4a0b-9585-9bee81be4355
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.msdtcstopped(v=EXCHG.150)
ms:contentKeyID: 48268447
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# El servicio Coordinador de transacciones distribuidas debe iniciarse antes de que el programa de instalación pueda continue\_MSDTCStopped

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2012-06-05_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

El programa de instalación de Microsoft Exchange Server 2007 no puede continuar porque se produjo un error al intentar instalar las funciones del servidor Acceso de cliente o Mensajería unificada porque el servicio Coordinador de transacciones distribuidas no está iniciado en el equipo de destino.

El programa de instalación de Exchange 2007 requiere que el estado del servicio Coordinador de transacciones distribuidas del equipo donde esté instalando Microsoft Exchange esté establecido en **Iniciado**.

El servicio Coordinador de transacciones distribuidas proporciona servicios diseñados para garantizar transacciones completas y correctas, incluso en caso de errores de comunicación, de proceso o del sistema.

Cada equipo que participa en una transacción distribuida administra sus propios recursos y datos, además de actuar de acuerdo con otros equipos en la transacción. Ante todo, una transacción distribuida debe confirmar o anular su trabajo por completo en todos los equipos participantes. El Coordinador de transacciones distribuidas desempeña la función de coordinación de transacciones para los componentes participantes y actúa como administrador de transacciones para todos los equipos que administren transacciones.

Las funciones del servidor Acceso de cliente y Mensajería unificada tienen dependencias del servicio Coordinador de transacciones distribuidas.

Para resolver este problema, compruebe que el estado del servicio Coordinador de transacciones distribuidas esté establecido en **Iniciado** en el equipo local y, a continuación, vuelva a ejecutar el programa de instalación de Microsoft Exchange.

Para establecer el estado del servicio Coordinador de transacciones distribuidas en 'Iniciado'

1.  Haga clic con el botón secundario en **Mi PC** y, a continuación, haga clic en **Administrar**.

2.  Expanda el nodo **Servicios y aplicaciones** y, a continuación, haga clic en el nodo **Servicios**.

3.  En el panel derecho, ubique el **Coordinador de transacciones distribuidas**.

4.  Haga clic con el botón secundario en **Coordinador de transacciones distribuidas** y después haga clic en **Propiedades**.

5.  Establezca el **Tipo de inicio** en **Automático** y el **Estado del servicio** en **Iniciado**.

6.  Haga clic en **Aplicar** y, después, en **Aceptar**.

