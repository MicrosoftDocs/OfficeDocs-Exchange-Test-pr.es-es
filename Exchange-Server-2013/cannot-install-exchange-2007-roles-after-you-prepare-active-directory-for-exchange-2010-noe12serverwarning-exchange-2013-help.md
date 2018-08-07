---
title: 'Incapaz instalar rol Exchange 2007 tras prepar. Active Directory Exchange 2010'
TOCTitle: No se pueden instalar roles de Exchange 2007 después de preparar Active Directory para Exchange 2010_NoE12ServerWarning
ms:assetid: 4e579f69-0de9-421c-ba31-4e63a25e6a45
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.noe12serverwarning(v=EXCHG.150)
ms:contentKeyID: 48268112
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# No se pueden instalar roles de Exchange 2007 después de preparar Active Directory para Exchange 2010\_NoE12ServerWarning

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2016-12-09_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Al ejecutar Microsoft Exchange Server 2010**Setup /PrepareAD**, la herramienta Microsoft Exchange Server Analyzer consulta la topología existente de Active Directory para determinar si existen roles de servidor de Microsoft Exchange Server 2007. Si no se detectan los roles de servidor de Exchange 2007, recibirá el siguiente mensaje de advertencia:


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>La instalación va a preparar la organización para Exchange Server 2010 a través de 'Setup /PrepareAD' y no se han detectado roles de Exchange Server 2007 en esta topología. Después de esta operación, no se podrán instalar roles de Exchange Server 2007.</p></td>
</tr>
</tbody>
</table>


Antes de implementar Exchange Server 2010, tenga en cuenta los factores siguientes que pueda que necesiten la implementación de un servidor de Exchange 2007 con todos los roles de servidor instalados antes de la implementación de Exchange 2007:

  - **Aplicaciones implementadas de manera interna o de terceros**   Es posible que las aplicaciones desarrolladas para Exchange 2003 no sean compatibles con Exchange 2010 y se deban actualizar o sustituir. Puede mantener estas aplicaciones y la población del usuario asociado en Exchange 2003 moverlas a Exchange 2007 o sustituir el software con una versión compatible de Exchange 2010.

  - **Coexistencia o requisitos de migración**   Si planifica migrar buzones a su organización, puede implementar Exchange 2007 y usar el Microsoft Transporter Suite o puede usar una solución de migración o coexistencia de terceros. Para descargar Microsoft Transporter Suite, visite [Microsoft Transporter Suite](http://go.microsoft.com/fwlink/?linkid=82688) en el Centro de descarga de Microsoft.

Además, al evaluar las opciones para su organización, asegúrese de haber tenido en cuenta las siguientes cuestiones:

  - ¿Tiene una estrategia para mover las aplicaciones dependientes a Exchange 2010 antes de que finalice la compatibilidad de Exchange 2003? Para obtener más información, visite la página web "Compartir Ciclo de vida del soporte técnico de Microsoft" ([https://go.microsoft.com/fwlink/?LinkID=55839](https://go.microsoft.com/fwlink/?linkid=55839)).

  - ¿Su estrategia requiere la coexistencia de WebDAV y de los servicios web (Exchange 2007)?

  - ¿Se ha planteado el uso de productos de terceros compatibles con Exchange u otras tecnologías de Microsoft que le permitirán cumplir con los requisitos de coexistencia o migración?

  - ¿Cuál es su aproximación al ciclo de vida del hardware (continuar usando tantos servidores existentes de 32 bits como sea posible o adquirir servidores de 64 bits nuevos)?

  - ¿Cuál es su plan para la migración (migrar todos los servidores tan pronto como pueda frente a migrar en una estrategia con fases)? De forma similar, ¿cuál es su escala de tiempo para la coexistencia de varias versiones de Exchange?

Si decide que necesita implementar un servidor de Exchange 2007 antes de implementar Exchange 2010, la implementación de un solo Exchange 2007 con todos los roles de servidor es suficiente para permitir la implementación de futuros servidores de Exchange 2007 en la organización. Para implementar el servidor de Exchange 2007 en su organización de Exchange 2003, siga estos pasos:

1.  Ejecute Exchange 2007**Setup /PrepareSchema**.

2.  Ejecute Exchange 2007**Setup /PrepareAD**.

3.  Ejecute Exchange 2007**Setup /PrepareDomain** en todos los dominios que contengan destinatarios, servidores de Exchange 2003 o catálogos globales que pueda usar un servidor de Exchange.

4.  Instale un servidor de Exchange 2007 con los cuatro roles de servidor (Transporte de concentrador, Acceso de cliente, Buzón de correo y Mensajería unificada).

