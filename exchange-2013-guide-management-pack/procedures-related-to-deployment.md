---
title: Procedimientos relacionados con la implementación
TOCTitle: Procedimientos relacionados con la implementación
ms:assetid: 6b7682bd-fe3d-43b9-a7db-66c0ac17656f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn195909(v=EXCHG.150)
ms:contentKeyID: 53181933
ms.date: 04/03/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Procedimientos relacionados con la implementación

 

_**Última modificación del tema:**   2013-04-17_

Esta sección contiene los procedimientos que puede usar como referencia con el módulo de administración de Exchange Server 2013. Para los procedimientos relacionados con la operación posterior a la implementación, consulte [Procedures related to post-deployment operation](procedures-related-to-post-deployment-operation.md).

## Comprobar el estado de implementación de los agentes

Antes de importar el módulo de administración de Exchange Server 2013, compruebe que los agentes SCOM en sus servidores Exchange estén en funcionamiento y que el estado del sistema operativo se esté informando correctamente en SCOM.

Su cuenta de usuario debe ser miembro del rol Administradores de Operations Manager para realizar este procedimiento.

1.  Inicie sesión en el servidor de SCOM y abra la consola de SCOM.

2.  Haga clic en **Supervisión** y, a continuación, en **Equipos Windows**.

3.  Asegúrese de que todos los servidores Exchange muestren **Correcto**.

![Agentes correctos en la consola SCOM](images/Dn195909.7d1ff0bb-419e-40dc-babf-5fa2fb7229a8(EXCHG.150).png "Agentes correctos en la consola SCOM")

## Compruebe la configuración de proxy del agente

Antes de importar el módulo de administración de Exchange Server 2013, compruebe que el proxy del agente esté habilitado para detección en SCOM. De lo contrario, los agentes de los servidores de Exchange no informarán el estado de Exchange. Debe comprobar esta configuración para todos los servidores Exchange.

Su cuenta de usuario debe ser miembro del rol Administradores de Operations Manager para realizar este procedimiento.

1.  Inicie sesión en el servidor de SCOM y abra la consola de SCOM.

2.  En la consola de Operations, haga clic en **Administración**.

3.  Haga clic en **Administrado por agente**. Haga clic con el botón secundario en el servidor de Exchange y, a continuación, seleccione **Propiedades**.

4.  En la pestaña **Seguridad**, verifique que la casilla **Permitir que este agente actúe como proxy y descubrir objetos administrados en otros ordenadores** esté activada.

5.  Haga clic en **Aceptar**.

## Comprobar la configuración de seguridad del agente

Debido al modelo de seguridad sobre el que se ha probado Exchange 2013, no es posible ejecutar el agente de SCOM en los servidores Exchange bajo una cuenta distinta de la de **LocalSystem**. Si ejecuta el agente bajo una cuenta distinta de la de LocalSystem, las transacciones sintéticas no podrán ejecutarse. Asimismo, es posible que experimente otros problemas.

Su cuenta de usuario debe ser miembro del grupo de roles de administración de servidores para realizar este procedimiento.

1.  Inicie sesión en el servidor Exchange.

2.  Haga clic en **Inicio** \> **Herramientas administrativas** \> **Servicios**.

3.  Desplácese hacia abajo en la lista de servicios hasta encontrar el servicio **Administración de System Center**.

4.  Compruebe que la columna **Iniciar sesión como** muestre **Sistema local**.

5.  Si la columna **Iniciar sesión como** muestra algo diferente, cambie el inicio de sesión del servicio a Sistema local.
    
    1.  Haga clic con el botón secundario en el servicio **Administración de System Center** y seleccione **Propiedades**.
    
    2.  Seleccione la pestaña **Iniciar sesión**.
    
    3.  Haga clic en la opción **Cuenta de sistema local**.
    
    4.  Haga clic en **Aceptar**.

