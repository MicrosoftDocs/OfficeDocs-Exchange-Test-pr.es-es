---
title: 'Reglas de protección de Outlook: Exchange 2013 Help'
TOCTitle: Reglas de protección de Outlook
ms:assetid: bd7d0ad7-1f8e-46da-a74b-58c58f3eff93
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd638178(v=EXCHG.150)
ms:contentKeyID: 49895878
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Reglas de protección de Outlook

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

Todos los días, los trabajadores de la información intercambian información confidencial por correo electrónico, incluso informes y datos financieros, información del cliente y del empleado e información y especificaciones confidenciales del producto. Con Microsoft Exchange Server 2013, Microsoft Outlook y Microsoft OfficeOutlook Web App, los usuarios pueden usar Information Rights Management (IRM) para proteger los mensajes mediante la aplicación de una plantilla de directivas de derechos de Active Directory Rights Management Services (AD RMS). Esto requiere implementar AD RMS en la organización. Para obtener más información acerca de AD RMS, consulte [Rights Management Services de Active Directory](https://go.microsoft.com/fwlink/p/?linkid=129823).

Sin embargo, cuando se deja a criterio de los usuarios, es posible que los mensajes se envíen en texto no cifrado y sin la protección de IRM. En organizaciones que utilizan el correo electrónico como servicio hospedado, existe el riesgo de filtración de información cuando el mensaje sale del cliente y se enruta y almacena fuera de los límites de la organización. Aunque las empresas de hospedaje de correo electrónico pueden disponer de comprobaciones y procedimientos bien definidos para contribuir a mitigar el riesgo de filtración de información, una vez que un mensaje abandona los límites de una organización, ésta pierde el control sobre la información. Las reglas de protección de Outlook pueden ayudar a proteger contra este tipo de filtraciones de información.

Para tareas de administración relacionadas con la administración de IRM, consulte [Procedimientos de Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

## Protección automática de IRM en Outlook

En Exchange 2013, las reglas de protección de Outlook ayudan a su organización a protegerse ante el riesgo de filtraciones de información mediante la aplicación automática de la protección de IRM a los mensajes de Exchange 2013. Los mensajes se protegen con IRM antes de abandonar al cliente de Outlook. Esta protección también se aplica a los datos adjuntos que usan formatos de archivo compatibles.

Al crear reglas de protección de Outlook en un servidor de Exchange 2013, las reglas se distribuyen automáticamente a Outlook 2010 por medio de los servicios Web Exchange. Para que Outlook 2010 aplique la regla, la plantilla de directivas de derechos de AD RMS especificada debe estar disponible en los equipos de los usuarios.


> [!IMPORTANT]
> Si se elimina una plantilla de directivas de derechos del servidor de AD&nbsp;RMS, es necesario modificar cualquier regla de protección de Outlook&nbsp;que utilizara la plantilla eliminada. Si una regla de protección de Outlook&nbsp;sigue utilizando una plantilla de directivas de derechos que se ha eliminado y la organización tiene habilitado el descifrado de transporte, el agente de descifrado no podrá descifrar el mensaje protegido con una plantilla que ya no está disponible. Si el descifrado de transporte está configurado como obligatorio, el servicio de transporte rechazará el mensaje y enviará un informe de no entrega (NDR) al remitente. Para obtener más información acerca del descifrado de transporte, consulte <A href="transport-decryption-exchange-2013-help.md">Descifrado de transporte</A>. Para obtener más información acerca de las plantillas de directivas de derechos de AD&nbsp;RMS, consulte <A href="https://go.microsoft.com/fwlink/p/?linkid=179455">Consideraciones acerca de las plantillas de directivas de AD RMS</A>.<BR>En Windows Server 2008 y superior, las plantillas de directivas de derechos se pueden archivar en lugar de eliminarlas. Las plantillas archivadas todavía se pueden utilizar para emitir licencias de contenido pero, al crear o modificar una regla de protección de Outlook, las plantillas archivadas no se incluyen en la lista de plantillas.



Las reglas de protección de Outlook son similares a las reglas de protección de transporte. Ambos tipos se aplican según las condiciones de los mensajes y ambos protegen los mensajes mediante la aplicación de una plantilla de protección de derechos de AD RMS. Sin embargo, las reglas de protección de transporte se aplican en el servicio de transporte en el servidor Buzón de correo por parte del agente de reglas de transporte. Las reglas de protección de Outlook se aplican en Outlook 2010, antes de que el mensaje salga del equipo del usuario. Los mensajes protegidos por una regla de protección de Outlook entran en la canalización de transporte con la protección de IRM ya aplicada. Asimismo, los mensajes protegidos con una regla de protección de Outlook también quedan almacenados en formato cifrado en la carpeta Elementos enviados del buzón de correo del remitente.


> [!NOTE]
> Si el descifrado de transporte está habilitado en la organización de Exchange, los mensajes protegidos por IRM con una regla de protección de Outlook&nbsp;que usa el servidor de AD&nbsp;RMS de la organización se pueden descifrar con el agente de descifrado en el servicio de transporte. El agente de reglas de transporte u otros agentes de transporte instalados en el servidor de transporte pueden examinar el contenido de los mensajes. Para obtener más información acerca del descifrado de transporte, consulte <A href="transport-decryption-exchange-2013-help.md">Descifrado de transporte</A>.



Cuando se utilizan reglas de protección de transporte, los usuarios ignoran si un mensaje se protegerá automáticamente en el servidor de transporte. Cuando se aplica una regla de protección de Outlook a un mensaje de Outlook 2010, los usuarios saben si el mensaje estará protegido por IRM. Si es necesario, los usuarios también pueden seleccionar otra plantilla de directivas de derechos.

## Creación de reglas de protección de Outlook

Para crear reglas de protección de Outlook, es necesario utilizar el cmdlet [New-OutlookProtectionRule](https://technet.microsoft.com/es-es/library/dd298182\(v=exchg.150\)) en el Shell de administración de Exchange. Para obtener instrucciones detalladas, consulte [Crear una regla de protección de Outlook](create-an-outlook-protection-rule-exchange-2013-help.md).

Al crear una regla se puede especificar si el usuario podrá invalidarla, ya sea eliminando la protección de IRM o aplicando otra plantilla de directivas de derechos de AD RMS a la especificada en la regla. Si un usuario invalida la protección de IRM aplicada por una regla de protección de Outlook, Outlook 2010 inserta el encabezado `X-MS-Outlook-Client-Rule-Overridden` en el mensaje, lo cual permite determinar que el usuario ha invalidado la regla.

## Predicados en las reglas de protección de Outlook

Las reglas de protección de Outlook permiten utilizar tres predicados para aplicar automáticamente la protección de IRM en Outlook 2010:

  - **FromDepartment**   El predicado *FromDepartment* busca el atributo de departamento del remitente en Active Directory y protege automáticamente el mensaje con IRM si el departamento del remitente coincide con el que se ha especificado en la regla. Por ejemplo, se puede crear una regla de protección de Outlook para proteger automáticamente todos los mensajes enviados por el departamento de investigación.

  - **SentTo**   Puede que la organización necesite proteger mensajes enviados a determinados destinatarios confidenciales como, por ejemplo, los grupos de distribución Toda la empresa o Finanzas. Utilizando el predicado *SentTo*, es posible crear una regla de protección de Outlook para proteger automáticamente con IRM los mensajes enviados a los destinatarios especificados.

  - **SentToScope**   El predicado *SentToScope* permite crear una regla de protección de Outlook para proteger automáticamente con IRM los mensajes enviados dentro y fuera de la organización. Por ejemplo, se puede utilizar el predicado *SentToScope* con el predicado *FromDepartment* para proteger con IRM los mensajes enviados por un departamento concreto a usuarios internos.

