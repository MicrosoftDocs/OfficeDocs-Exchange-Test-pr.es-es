---
title: 'No se puede contactar con el servidor DNS principal'
TOCTitle: No se puede contactar con el servidor DNS principal_PrimaryDNSTestFailed
ms:assetid: 5b39cb64-c8f1-4fd3-843b-ecd23f99fe3a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.primarydnstestfailed(v=EXCHG.150)
ms:contentKeyID: 48268172
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# No se puede contactar con el servidor DNS principal\_PrimaryDNSTestFailed

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2016-12-09_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La instalación de Microsoft® Exchange Server 2007 no puede continuar porque no se puede establecer la comunicación con el servidor principal del Sistema de nombres de dominio (DNS).

La instalación de Exchange 2007 requiere que el equipo local se comunique con la base de datos DNS de autoridad para el dominio.

Microsoft Exchange depende de DNS para resolver la dirección IP de su siguiente servidor de destino externo o interno.

La comunicación con el servidor DNS principal puede producir un error por los siguientes motivos:

  - La configuración local TCP/IP no apunta al servidor DNS correcto.

  - El servidor DNS está inactivo o no es accesible debido a un fallo en la red o a otros motivos.

Para resolver este problema:

  - Compruebe que la configuración local TCP/IP apunta al servidor DNS correcto.

Para comprobar la configuración local TCP/IP

1.  Revise la configuración local TCP/IP
    
    Para obtener más información, consulte "Configurar TCP/IP para utilizar DNS" ([https://go.microsoft.com/fwlink/?LinkId=68094](https://go.microsoft.com/fwlink/?linkid=68094)).

<!-- end list -->

  - Compruebe que el servidor DNS se está ejecutando y que se puede establecer contacto con él.

Para comprobar que el servidor DNS se está ejecutando y que se puede establecer contacto con él

1.  Compruebe que el servidor DNS está en ejecución realizando una o varias de las siguientes comprobaciones:
    
      - Observe el estado del servidor DNS desde el programa de administración DNS en el servidor DNS.
    
      - Reinicie el servidor DNS.
        
        Para obtener más información, vea "Iniciar, detener, pausar o reiniciar un servidor DNS" ([https://go.microsoft.com/fwlink/?LinkId=62999](https://go.microsoft.com/fwlink/?linkid=62999)).
    
      - Compruebe la respuesta del servidor DNS con el comando **nslookup**.
        
        Para obtener más información, consulte las instrucciones en "Comprobar la capacidad de respuesta de un servidor DNS mediante el comando nslookup" ([https://go.microsoft.com/fwlink/?LinkId=63000](https://go.microsoft.com/fwlink/?linkid=63000)).

