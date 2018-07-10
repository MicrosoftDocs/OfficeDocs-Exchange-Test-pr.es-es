---
title: 'Descifrado de transporte: Exchange 2013 Help'
TOCTitle: Descifrado de transporte
ms:assetid: 4267c46d-f488-404d-a5cb-51f9127461c0
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd638122(v=EXCHG.150)
ms:contentKeyID: 49895595
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Descifrado de transporte

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-04-07_

En Microsoft Exchange Server 2013, Microsoft Outlook 2010 y posteriores, y Microsoft OfficeOutlook Web App, los usuarios pueden usar Information Rights Management (IRM) para proteger sus mensajes. Puede crear reglas de protección de Outlook para aplicar la protección IRM de manera automática en los mensajes antes de que se envíen de un cliente Outlook 2010. También es posible crear reglas de protección de transporte para aplicar la protección de IRM a los mensajes en tránsito que coincidan con las condiciones de la regla. El descifrado de transporte permite el acceso a los contenidos de mensajería protegidos para aplicar políticas de mensajería.

Para otras tareas de administración relacionadas con la administración de IRM, consulte [Procedimientos de Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

## Limitaciones de otras soluciones de cifrado

Si es esencial que su organización proteja información confidencial, incluida la información de alto impacto comercial (HBI) y la información de identificación personal (PII), piense en cifrar los mensajes de correo electrónico y los archivos adjuntos. Las soluciones de cifrado de correo electrónico, tales como S/MIME, han estado disponibles desde hace tiempo. Estas soluciones de cifrado han observado varios niveles de adopción en los diferentes tipos de organizaciones. Sin embargo, estas soluciones presentan los siguientes desafíos:

  - **Incapacidad de aplicar directivas de mensajería**   Las organizaciones, además, enfrentan requisitos de conformidad que solicitan la inspección del contenido de mensajería para garantizar que cumple con las directivas de mensajería. Sin embargo, los mensajes cifrados con la mayoría de las soluciones de cifrado basadas en clientes, incluso, S/MIME, evitan la inspección del contenido en el servidor. Sin la inspección de contenido, una organización no puede validar que todos los mensajes enviados o recibidos por sus usuarios cumplan con las directivas de mensajería. Por ejemplo, para cumplir con una norma legal, ha configurado una regla de transporte que detecte PII, tal como un número de seguro social, y aplica de manera automática un aviso de exención de responsabilidad en el mensaje. Si el mensaje está cifrado, el agente de reglas de transporte en el servidor de transporte no puede tener acceso al contenido del mensaje y, por lo tanto, no aplicará el aviso de exención de responsabilidad. Esto produce una infracción de la directiva.

  - **Seguridad disminuida**   El software antivirus no puede examinar el contenido de los mensajes cifrados, lo que expone más a una organización a riesgos de contenido malicioso, tales como virus y gusanos. La mayoría de los usuarios, generalmente, consideran que los mensajes cifrados son confiables; esto aumenta la probabilidad de que un virus se propague por toda la organización. Por ejemplo, ha configurado una regla de protección de Outlook para que aplique automáticamente la protección IRM en todos los mensajes enviados a la lista de distribución Todos los empleados con la plantilla Servicios de administración de derechos confidenciales (RMS). Una estación de trabajo de un usuario está infectada con un virus que se propaga con Responder a todos para responder los mensajes. Si el mensaje que contiene el virus está cifrado, el detector antivirus no puede examinar el mensaje.

  - **Impacto a los agentes de transporte personalizados**   Muchas organizaciones desarrollas agentes de transporte personalizados por diferentes motivos, tales como reunir requisitos de procesamiento adicionales para el cumplimiento, la seguridad o el enrutamiento personalizado del mensaje. Los agentes de transporte personalizados desarrollados por una organización para inspeccionar o modificar mensajes no pueden procesar mensajes cifrados. Si los agentes de transporte personalizados desarrollados por su organización no pueden tener acceso al contenido del mensaje, el cifrado del mensaje puede hacer que su organización no cumpla los objetivos para los cuales los agentes de transporte personalizados se desarrollaron.

## Uso de descifrado de transporte para contenido cifrado

En Exchange 2013, las funciones de IRM mencionan estos desafíos. Si los mensajes están protegidos con IRM, el descifrado de transporte le permite descifrarlos en tráfico. Los mensajes protegidos mediante IRM son descifrados por el agente de descifrado, un agente de transporte orientado al cumplimiento de normas.


> [!NOTE]
> En Exchange&nbsp;2013, el agente de Descifrado es un agente integrado. Los agentes integrados no están incluidos en la lista de agentes que devuelve el cmdlet <STRONG>Get-TransportAgent</STRONG>. Para obtener más información, consulte <A href="transport-agents-exchange-2013-help.md">Agentes de transporte</A>.



El agente de descifrado descifra los siguientes tipos de mensajes protegidos por IRM:

  - Mensajes protegidos por IRM por el usuario de Outlook Web App.

  - Mensajes protegidos por IRM por el usuario de Outlook 2010.

  - Mensajes protegidos por IRM automáticamente por las reglas de protección de Outlook en Exchange 2013 y en Outlook 2010.


> [!IMPORTANT]
> El agente de descifrado solo descifra los mensajes protegidos por IRM por el servidor AD&nbsp;RMS de su organización.




> [!NOTE]
> Los mensajes protegidos en tránsito mediante las reglas de protección de transporte no requieren que el agente de descifrado los descifre. El agente de descifrado se activa en los eventos de transporte <STRONG>OnEndOfData</STRONG> y <STRONG>OnSubmit</STRONG>. El agente de Reglas de transporte aplica las reglas de protección de transporte. Este agente se activa en el evento <STRONG>OnRoutedMessage</STRONG>, y el agente de cifrado aplica la protección por IRM en el evento <STRONG>OnRoutedMessage</STRONG>. Para obtener más información acerca de los agentes de transporte y una lista de eventos de SMTP en los cuales se pueden registrar, consulte <A href="transport-agents-exchange-2013-help.md">Agentes de transporte</A>.



El descifrado de transporte se realiza en el primer servidor transporte de Exchange 2013 que administra un mensaje en un bosque de Active Directory. Si el mensaje se transfiere a un servidor de transporte en otro bosque de Active Directory, el mensaje se descifra de nuevo. Después del descifrado, el contenido no cifrado está disponible para otros agentes de transporte de ese servidor. Por ejemplo, el agente de reglas de transporte en un servidor de transporte puede inspeccionar el contenido de los mensajes y aplicar las reglas de transporte. En el mensaje no cifrado, se pueden realizar todas las acciones especificadas en la regla, tales como aplicar un aviso de exención de responsabilidad o modificar el mensaje de alguna otra manera. Los agentes de transporte de terceros, tales como los detectores de virus, pueden examinar el mensaje para ver si contienen virus y malware. Después de que otros agentes de transporte hayan inspeccionado el mensaje y, posiblemente, lo hayan modificado, el mensaje se cifra nuevamente con los mismos derechos de usuario que tenía antes de que el agente de descifrado lo descifrara. El mismo mensaje no es descifrado nuevamente por el otro servicio de transporte en otros servidores de buzones de correo de la organización.

Los mensajes descifrados por el agente de descifrado no dejan el servidor de transporte sin que se cifren nuevamente. Si ocurre un error transitorio cuando se descifra o se cifra el mensaje, el servidor de transporte intenta la operación dos veces. Después del tercer error, éste se trata como un error permanente. Si se producen errores permanentes, incluidos los errores transitorios tratados como errores permanentes después de los reintentos, el servidor de transporte realiza lo siguiente:

  - Si se produce un error permanente durante el descifrado, se envía un informe de no entrega (NDR) solamente si el descifrado de transporte se establece en `Mandatory` y el mensaje cifrado se envía con el NDR. Para obtener información más detallada de las opciones de configuración disponibles para el descifrado de transporte, consulte Configuring Transport Decryption más adelante en este tema.

  - Si el error permanente ocurre durante el recifrado, siempre se envía un NDR sin el mensaje descifrado.


> [!IMPORTANT]
> Todos los agentes personalizados o de terceros instalados en el servicio de transporte tienen acceso al mensaje descifrado. Debe tener en cuenta el comportamiento de dichos agentes de transporte. Se recomienda que compruebe todos los agentes de transporte personalizados y de terceros exhaustivamente antes de implementarlos en el entorno de producción.<BR>Después de que el agente de descifrado descifra el mensaje, si un agente de transporte crea un mensaje nuevo e incluye (adjunta) el mensaje original al nuevo, sólo se protege el mensaje nuevo. El mensaje original, que se convierte en un archivo adjunto de un mensaje nuevo, no se vuelve a cifrar. Un destinatario que reciba dicho mensaje puede abrir el mensaje adjunto y realizar acciones, como reenviar o responder, y pasar por alto el cumplimiento de derechos.



## Configuración del descifrado de transporte

El descifrado de transporte se configura con el cmdlet [Set-IRMConfiguration](https://technet.microsoft.com/es-es/library/dd979792\(v=exchg.150\)) del Shell de administración de Exchange. Sin embargo, antes de configurar el descifrado de transporte, debe proporcionar a los servidores de Exchange 2013 el derecho a descifrar contenido protegido por su servidor AD RMS. Esto se logra si se agrega el buzón de correo federado a grupos de superusuarios configurados en el grupo AD RMS de su organización.


> [!IMPORTANT]
> En implementaciones de AD&nbsp;RMS entre bosques en donde tiene un grupo AD&nbsp;RMS implementado en cada bosque, debe agregar el buzón de correo federado al grupo de superusuarios en el grupo AD&nbsp;RMS de cada bosque para permitir que el servicio de transporte en un servidor de buzones de correo Exchange&nbsp;2013 o en un servidor de transporte de concentradores de Exchange 2010 descifre los mensajes protegidos de cada grupo AD&nbsp;RMS.



Para obtener información más detallada, consulte [Agregar el buzón de la federación para el grupo de usuarios de AD RMS Super](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md).

Exchange 2013 permite dos configuraciones diferentes cuando se habilita el descifrado de transporte:

  - **Obligatorio**   Cuando el descifrado de transporte se establece en `Mandatory`, el agente de descifrado rechaza el mensaje y devuelve un NDR al remitente en caso de que un error permanente se devuelva durante el descifrado de un mensaje. Si su organización no desea entregar un mensaje en caso de que éste no se pueda descifrar de manera satisfactoria y que se apliquen acciones como el análisis de antivirus y las reglas de transporte, debe elegir esta configuración.

  - **Opcional**   Cuando el descifrado de transporte se establece en Opcional, el agente de descifrado usa un enfoque de mayor esfuerzo. Los mensajes que se pueden descifrar se descifran, pero los mensajes con un error permanente durante el descifrado también se entregan. Si su organización prioriza la entrega de mensajes por sobre la directiva de mensajería, debe usar esta configuración.

Para obtener más información acerca de la configuración de descifrado de transporte, consulte [Habilitar o deshabilitar el descifrado de transporte](enable-or-disable-transport-decryption-exchange-2013-help.md).

