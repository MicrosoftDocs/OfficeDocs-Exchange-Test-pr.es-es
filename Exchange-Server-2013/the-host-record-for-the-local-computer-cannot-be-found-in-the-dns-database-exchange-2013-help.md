---
title: 'No se encuentra el registro host del PC local en la base de datos DNS: Exchange 2013 Help'
TOCTitle: No se encuentra el registro host del PC local en la base de datos DNS
ms:assetid: 2f18cb65-29fe-4b72-8d68-52fd503d5673
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.hostrecordmissing(v=EXCHG.150)
ms:contentKeyID: 48267958
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# No se encuentra el registro host del PC local en la base de datos DNS

 

_**Se aplica a:**Exchange Server_

_**Última modificación del tema:**2016-12-09_

No se puede continuar con la instalación de Microsoft Exchange Server 2013 porque no se encuentra el registro host (A) de este PC en la base de datos Sistema de nombres de dominio (DNS).

La instalación de Exchange 2013 requiere que el PC local tenga un HOST (A) válido registrado con la base de datos DNS autoritativa para el dominio.

Exchange depende de los registros host (A) del DNS para la dirección IP del siguiente servidor de destino externo o interno.

Para resolver este problema:

  - Compruebe que la configuración local TCP/IP apunta al servidor DNS correcto. Para más información, vea [Configuración de las opciones TCP/IP](https://go.microsoft.com/fwlink/p/?linkid=108281).

  - Use nslookup para comprobar que el registro Host (A) existe en el servidor DNS. Para más información, vea [Para comprobar que hay registros de recursos A en DNS](https://go.microsoft.com/fwlink/?linkid=63001).

Para obtener información sobre la resolución de nombres DNS, la resolución de problemas, y los registros Host (A), consulte los siguientes artículos:

  - [Solucionar problemas de DNS](https://go.microsoft.com/fwlink/p/?linkid=294828)

  - [Administración de registros de recursos](https://go.microsoft.com/fwlink/p/?linkid=294829)

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

¿Encontró lo que buscaba? Tómese un minuto para [enviarnos comentarios](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac) sobre la información que deseaba encontrar.

