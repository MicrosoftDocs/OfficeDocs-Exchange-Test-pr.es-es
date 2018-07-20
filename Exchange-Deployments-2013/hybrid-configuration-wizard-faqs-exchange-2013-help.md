---
title: 'Preguntas más frecuentes del asistente de configuración híbrida: Exchange 2013 Help'
TOCTitle: Preguntas más frecuentes del asistente de configuración híbrida
ms:assetid: e911e6e0-e36e-4430-ac36-c745a10d6c26
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Mt488940(v=EXCHG.150)
ms:contentKeyID: 72045784
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Preguntas más frecuentes del asistente de configuración híbrida

 

_<strong>Se aplica a:</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>Última modificación del tema:</strong>2016-12-09_

Microsoft ha lanzado un nuevo asistente para la configuración híbrida que simplifica la configuración de una implementación híbrida, dotándola de una mayor flexibilidad y garantizando que siempre se ejecuten las versiones más recientes. Esta versión del asistente híbrido está integrada en Exchange 2016 y versiones de Exchange 2013 a partir de la actualización acumulativa 10, pero incluso si ejecuta una actualización acumulativa anterior de Exchange 2013 o Exchange 2010 Service Pack 3 (SP3), puede descargar el nuevo asistente.

Para obtener más información sobre el asistente para la configuración híbrida de Office 365, consulte [Introducing the Microsoft Office 365 Hybrid Configuration Wizard (Introducción al Asistente para la configuración híbrida de Microsoft Office 365)](http://go.microsoft.com/fwlink/?linkid=717122) y [Office 365 Hybrid Configuration Wizard for Exchange 2010](http://go.microsoft.com/fwlink/?linkid=730687) en el blog del equipo de Exchange.

Para descargar el asistente para la configuración híbrida de Office 365, vaya a [http://aka.ms/HybridWizard](http://aka.ms/hybridwizard).

## Preguntas más frecuentes de los clientes

  - P: ¿Qué versiones de Exchange son compatibles con el nuevo asistente de configuración híbrida?  
    R: Debe tener al menos un servidor que cumpla los siguientes requisitos:
    
      - **Exchange 2010**Exchange 2010 SP3 debe instalarse en al menos un servidor que ejecute los roles de servidor Acceso de clientes, Transporte de concentradores y Buzón de correo. También recomendamos que instale el paquete acumulativo de actualizaciones más reciente disponible para Exchange 2010 SP3.
    
      - **Exchange 2013** La última actualización acumulativa de Exchange 2013 debe instalarse en al menos un servidor que ejecute los roles de servidor Acceso de clientes y Buzón de correo. Si no puede instalar la actualización acumulativa más reciente, la versión inmediatamente anterior también es compatible. Las actualizaciones acumulativas más antiguas no son compatibles.
    
      - **Exchange 2016** La última versión de Exchange 2016 debe instalarse en al menos un servidor que ejecute los roles de servidor Buzón de correo.
    
    Por ejemplo, suponga que ha instalado Exchange 2013 CU8 en la organización local y que la última versión disponible de Exchange 2013 es CU10. Para continuar en una configuración híbrida compatible, debe actualizar los servidores de Exchange 2013 como mínimo a CU9. Sin embargo, le recomendamos que actualice a CU10.
    
    Las actualizaciones acumulativas se publican con una frecuencia trimestral, por lo que el hecho de mantener los servidores con las actualizaciones acumulativas más recientes aporta cierta flexibilidad adicional si periódicamente necesita más tiempo para completar las actualizaciones.

<!-- end list -->

  - P: ¿Este asistente de configuración híbrida funciona con Exchange 2007?  
    R: Puede configurar una implementación híbrida con Exchange 2007 en su organización. Sin embargo, para ello debe implementar al menos un servidor que ejecute Exchange 2013 y cumpla los requisitos anteriores.

<!-- end list -->

  - P: ¿Puedo optar por no emplear el nuevo asistente de configuración híbrida?  
    R: No. El nuevo asistente de configuración híbrida es el único asistente compatible con Exchange 2010, Exchange 2013 y Exchange 2016 en la actualidad.

<!-- end list -->

  - P: ¿Puedo actualizar mi configuración híbrida de Exchange 2010 actual a Exchange 2013 o Exchange 2016 con el nuevo asistente de configuración híbrida?  
    R: Sí. Asegúrese de que tiene al menos un servidor que cumpla los requisitos actuales del asistente de configuración híbrida y después ejecútelo. El asistente conocerá el estado actual de la configuración híbrida y le guiará sin problemas por el proceso de actualización.

