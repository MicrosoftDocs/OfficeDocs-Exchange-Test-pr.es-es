---
title: 'Descifrado de informe de diarios: Exchange 2013 Help'
TOCTitle: Descifrado de informe de diarios
ms:assetid: c063e2bd-2444-480d-8b35-73f31064a31b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd876936(v=EXCHG.150)
ms:contentKeyID: 49895885
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Descifrado de informe de diarios

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-16_

En Microsoft Exchange Server 2013, Information Rights Management (IRM) permite a los usuarios de Microsoft Outlook 2010 y posteriores y de Microsoft Office Outlook Web App proteger sus mensajes. Es posible crear reglas de protección de Outlook para aplicar automáticamente la protección de IRM a los mensajes antes de que se envíen desde un cliente de Outlook 2010. También es posible crear reglas de protección de transporte para aplicar la protección de IRM a los mensajes en tránsito que coincidan con las condiciones de la regla.

Para obtener información acerca de las reglas de protección de Outlook, consulte [Reglas de protección de Outlook](outlook-protection-rules-exchange-2013-help.md).

## Limitaciones de las soluciones de cifrado estándar

Si su organización cifra los mensajes con soluciones tradicionales como S/MIME, los administradores de registros no podrán examinar ni buscar el contenido cifrado. Puede que el archivado de mensajes cifrados que contienen contenido inaccesible e ilocalizable no cumpla los requisitos empresariales, legales o de cumplimiento. Ante una solicitud de exhibición de documentos electrónicos (eDiscovery) puede resultar extremadamente difícil descifrar, buscar y mostrar contenido de mensajes cifrados; y, de no conseguirlo, puede que la organización quede expuesta a riesgos legales y financieros.

Asimismo, puede que las directivas de mensajería de la organización requieran el cifrado de los mensajes con tareas de diario para que su contenido quede accesible para las herramientas de exhibición de documentos electrónicos, los procesos automatizados y los responsables de registros que tienen acceso a un buzón de correo de diario. El descifrado de informes de diario en Exchange 2010 puede facilitar el cumplimiento de estos requisitos.

Para obtener más información acerca del registro en diario, consulte [Registro en diario](journaling-exchange-2013-help.md).

## Descifrado de informe de diarios

El descifrado de informes de diarios permite almacenar una copia en texto no cifrado de los mensajes protegidos con IRM en los informes de diarios, junto con el mensaje original protegido con IRM. Si el mensaje protegido con IRM contiene datos adjuntos compatibles que se han protegido con el clúster de Rights Management Services (AD RMS) de Active Directory de la organización, también se descifran los datos adjuntos.


> [!IMPORTANT]
> Para usar el descifrado de informes de diarios, se necesita una licencia de acceso de cliente (CAL) de Exchange Enterprise. El descifrado de informes de diarios sólo es compatible con el registro de diarios premium.



El descifrado lo realiza el agente de descifrado de informes de diarios, un agente de transporte centrado en el cumplimiento. El agente de descifrado de informes de diarios se activa con el evento **OnCategorizedMessage**. Los mensajes protegidos en tránsito mediante reglas de protección de transporte ya quedan cifrados por el agente de cifrado, que se activa con el evento **OnRoutedMessage**, antes de llegar al agente de descifrado de informes de diarios. El agente de descifrado de informes de diarios descifra estos mensajes.


> [!NOTE]
> En Exchange&nbsp;2013, el agente de descifrado de informes de diarios es un agente integrado. Los agentes integrados no se incluyen en la lista de agentes generada por el cmdlet <STRONG>Get-TransportAgent</STRONG>. Para obtener más información, consulte <A href="transport-agents-exchange-2013-help.md">Agentes de transporte</A>.



El agente descifra los siguientes tipos de mensajes protegidos con IRM:

  - Mensajes que el usuario protegió con IRM en Outlook Web App.

  - Mensajes que el usuario protegió con IRM en Outlook 2010.

  - Mensajes que se protegieron automáticamente con IRM en Outlook 2010 mediante las reglas de protección de Outlook.

  - Mensajes en tránsito que se protegieron automáticamente con IRM mediante las reglas de protección de transporte.


> [!IMPORTANT]
> Sólo los mensajes protegidos con IRM por el servidor de AD&nbsp;RMS en la organización se descifran con el agente de descifrado de informes de diarios. El agente no descifra los datos adjuntos, si éstos no se han protegido al mismo tiempo que el mensaje (y, por lo tanto, no tienen la misma licencia de uso) o si se ha adjuntado un archivo protegido con IRM a un mensaje sin protección.



## Configuración del descifrado de informes de diarios

El descifrado de informes de diarios se configura con el cmdlet [Set-IRMConfiguration](https://technet.microsoft.com/es-es/library/dd979792\(v=exchg.150\)) en el Shell de administración de Exchange. Sin embargo, antes de configurar el descifrado de informes de diarios, es necesario asignar a los servidores de Exchange 2013 los permisos para descifrar contenido que ha sido protegido con IRM por el servidor de AD RMS. Para ello, se debe agregar el buzón de correo de federación al grupo de superusuarios configurado en el clúster de AD RMS de la organización. Para obtener información más detallada, consulte [Agregar el buzón de la federación para el grupo de usuarios de AD RMS Super](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md).


> [!IMPORTANT]
> En implementaciones de AD&nbsp;RMS entre bosques, en las cuales se ha implementado un clúster de AD&nbsp;RMS en cada bosque, es necesario agregar el buzón de federación al grupo de superusuarios del clúster de AD&nbsp;RMS de cada bosque para permitir que los servidores de transporte de Exchange&nbsp;2013 descifren los mensajes protegidos con cada clúster de AD&nbsp;RMS.



Para obtener información acerca de cómo configurar el descifrado de informes de diarios, consulte [Habilitar o deshabilitar el descifrado de informes de diario](enable-or-disable-journal-report-decryption-exchange-2013-help.md).

Una vez habilitado el descifrado de informes de diarios, puede que el buzón de correo de diario contenga informes de diarios con información confidencial sin cifrar. Es recomendable que el acceso al buzón de correo de diario sea supervisado de cerca y se restrinja únicamente a las personas autorizadas. Esto es recomendable aunque no utilice la protección con IRM para el correo electrónico.

