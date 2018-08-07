---
title: 'Pruebas y solución de problemas con el cmdlet Test-UMConnectivity'
TOCTitle: Pruebas y solución de problemas con el cmdlet Test-UMConnectivity
ms:assetid: 08e67a99-e37f-4afd-bd58-455b62580af7
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa995978(v=EXCHG.150)
ms:contentKeyID: 56271495
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Pruebas y solución de problemas con el cmdlet Test-UMConnectivity

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-06-25_

Después de instalar los servidores de acceso de cliente y de buzones de correo y configurar la Mensajería unificada, puede usar varias pruebas de diagnóstico y una aplicación de teléfono basado en software para comprobar la conectividad telefónica y el funcionamiento de los Servicios de mensajería unificada.

## Test-UMConnectivity

El cmdlet **Test-UMConnectivity** se puede usar para comprobar la conectividad con servidores de acceso de cliente y de buzones de correo de varias formas, según los parámetros que se usen con el cmdlet. Para comprobar la funcionalidad de la mensajería unificada, puede usar estas pruebas:

  - **Local**   El cmdlet **Test-UMConnectivity** comprueba la comunicación de voz sobre IP (VoIP) con los servidores de buzones de correo que se ejecutan en el mismo PC local.

  - **Local con TUILogon**   El cmdlet **Test-UMConnectivity** trata de establecer una comunicación de VoIP con el servidor de buzones de correo que se ejecuta en el mismo PC. Si se conecta, intenta iniciar sesión en uno o varios buzones habilitados para MU al enviar el número de extensión y el PIN del buzón. Si se proporciona el parámetro *–TUILogon*, también se deben proporcionar los siguientes valores de parámetros con la información correspondiente del buzón de la prueba:
    
      - *–Phone*   Este parámetro debe contener el número de extensión para el buzón de prueba.
    
      - *–PIN*   Este parámetro debe contener el PIN del buzón habilitado para MU.
    
      - *–UMDialPlan   *Este parámetro debe contener el plan de marcado asociado al buzón de la prueba.

  - **Remoto**   El cmdlet **Test-UMConnectivity** trata de conectarse a un servidor de acceso de cliente remoto realizando una llamada a través de una puerta de enlace VoIP. Después de conectarse, realiza comprobaciones de conectividad en el servidor de acceso de cliente remoto y en las rutas de medios.
    

    > [!NOTE]
    > Si recibe el siguiente mensaje, debe reiniciar el Servicio de mensajería unificada de MicrosoftExchange, porque se detuvo o no está respondiendo: "La tarea Test-UMConnectivity encontró un error al intentar realizar una llamada. Detalles: No se puede establecer una conexión".


