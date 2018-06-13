---
title: 'Solucionar problemas de una implementación híbrida: Exchange 2013 Help'
TOCTitle: Solucionar problemas de una implementación híbrida
ms:assetid: bbae72f3-6a1e-4cbf-80da-d8f73d969c6b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ659053(v=EXCHG.150)
ms:contentKeyID: 49895007
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Solucionar problemas de una implementación híbrida

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2016-04-29_

La configuración de una implementación híbrida en Exchange con el asistente para la configuración híbrida minimiza en gran medida los potenciales problemas que podrían surgir durante la implementación híbrida. Sin embargo, existen áreas típicas fuera del alcance del asistente para la configuración híbrida que, si se configuran incorrectamente, pueden presentar problemas en una implementación híbrida. Este tema cubre las siguientes áreas comunes en las que pueden surgir problemas y traza los pasos básicos para verificar o corregir los problemas:

  - Servidores de Exchange locales

  - Certificados

  - Errores específicos del Asistente para configuración híbrida


> [!NOTE]
> En este tema, "servidores Exchange" hace referencia a lo siguiente: 
> <UL>
> <LI>
> <P><STRONG>Servidores de acceso de cliente</STRONG> de Exchange 2013 y anteriores</P>
> <LI>
> <P><STRONG>Servidores de buzones</STRONG> de Exchange 2016 y posteriores</P></LI></UL>



Para obtener más información, consulte [Implementaciones híbridas de Exchange Server](exchange-server-hybrid-deployments-exchange-2013-help.md).

Para otras tareas de administración relacionadas con las implementaciones híbridas, consulte [Procedimientos de implementación híbrida](hybrid-deployment-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar esta tarea: Varía dependiendo del tipo de problemas en la implementación híbrida

  - Entrada "Implementaciones híbridas" Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el en el tema [Permisos de infraestructura de la Shell y de Exchange](https://technet.microsoft.com/es-es/library/dd638114\(v=exchg.150\)).

  - La guía en este tema se aplica a las implementaciones híbridas configuradas con el asistente para la configuración híbrida. Las implementaciones híbridas configuradas manualmente quedan fuera de este tema.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](https://technet.microsoft.com/es-es/library/jj150484\(v=exchg.150\)).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué quiere hacer?

## Solucionar problemas con servidores de Exchange

La configuración de los servidores de Exchange locales es, por lo general, el área donde ocurre la mayoría de los problemas que pueden surgir durante una implementación híbrida. Por lo general, las áreas que necesitan examinarse son las siguientes:

  - **Disponibilidad**   La publicación correcta de los servidores de Exchange en Internet es vital para el correcto funcionamiento de las características en su implementación híbrida. Para que las características híbridas funcionen correctamente, debe configurar su firewall local u otros dispositivos de seguridad para permitir el acceso entrante de Internet a los extremos de Detección automática y Exchange Web Services (EWS) de los servidores de Exchange locales. Asimismo, los servidores de Exchange también deben estar configurados para aceptar el correo SMTP entrante. Si el servicio de protección en línea de Microsoft Exchange (EOP) incluido en su organización de Office 365 no llega a los servidores locales de Exchange, el transporte de correo seguro desde la organización de Exchange Online a la organización local no funcionará correctamente.

  - **Certificados**   El certificado digital que se usa para el transporte de correo seguro entre la organización local y la organización de Exchange Online debe estar instalado en todos los servidores locales de Exchange con conexión a Internet que se comunicarán con Exchange Online, debe ser emitido por una entidad de certificación (CA) de terceros, no debe estar caducado, y debe tener asignados los servicios IIS y SMTP. Si el certificado no cumple estos requisitos, el transporte de correo seguro de la organización de Exchange Online a la organización local no funcionará correctamente. Encontrará más información sobre los requisitos de los certificados en "Solucionar problemas con los certificados", más adelante en este tema.

## ¿Cómo saber si los servidores de Exchange están configurados correctamente?

Para comprobar que publicó correctamente sus servidores locales de Exchange, use el Analizador de conectividad remota de Microsoft para verificar la conectividad entrante de Internet a los servidores locales de Exchange. Haga lo siguiente:

1.  Vaya a la herramienta [Analizador de conectividad remota](https://www.testexchangeconnectivity.com/).

2.  Este paso es para realizar una prueba general de las tareas EWS para confirmar que funcionan y que el extremo EWS está configurado.
    
    Ejecute la prueba de **sincronización, notificación, disponibilidad y respuestas automáticas (OOF)** en la sección **Pruebas de conectividad de Servicios web de Microsoft Exchange**, y verifique que no haya ningún error. Si se producen errores, corrija los elementos que identifica la prueba.

3.  Este paso es para realizar una prueba general del servicio Autodiscover para confirmar que funciona y que el extremo Autodiscover está configurado.
    
    Ejecute la prueba **Outlook Autodiscover** en la sección **Pruebas de conectividad de Microsoft Office Outlook**, y compruebe que no haya errores. Si se producen errores, corrija los elementos que identifica la prueba.

4.  Este paso es para realizar una prueba general de la conectividad de SMTP y confirmar que los servidores de Exchange pueden recibir correo entrante de Internet.
    
    Ejecute la prueba **Correo electrónico SMTP entrante** en la sección **Pruebas de correo electrónico de Internet**, y compruebe que no haya errores. Si se producen errores, corrija los elementos que identifica la prueba.

## Solucionar problemas con los certificados

La configuración de los certificados instalados en los servidores locales de Exchange podría ser una fuente de problemas durante una implementación híbrida. En la mayoría de los casos, los siguientes problemas relacionadas con los certificados afectan a la funcionalidad híbrida:

  - **Tipo de certificado**   El certificado digital usado para el transporte híbrido seguro, que se define en el asistente para la configuración híbrida debe ser emitido por una CA de terceros. No se pueden usar certificados autofirmados para la autenticación de transporte híbrido. Si involuntariamente se asigna o selecciona un certificado autofirmado, el transporte de correo seguro entre la organización Exchange Online y la organización local no funcionará correctamente.

  - **Servicios asignados**   El servicio Internet Information Service (IIS) así como el servicio Simple Mail Transport Protocol (SMTP) deben estar asignados al certificado digital usado para el transporte híbrido. Si no se asignan estos servicios, el transporte de corre seguro entre la organización de Exchange Online y la organización local no funcionará correctamente.

  - **Instalación**   El certificado digital usado para el transporte de correo seguro entre la organización local y la organización de Exchange Online debe estar instalado en todos los servidores locales de Exchange. Si está realizando la implementación híbrida con servidores de transporte perimetral locales, el certificado digital también debe estar instalado en sus servidores de transporte perimetral. Si el certificado no está instalado en los servidores locales, el transporte de correo seguro entre la organización de Exchange Online y la organización local no funcionará correctamente.

  - **Vencimiento**   El certificado digital usado para el transporte de correo seguro entre la organización local y la organización de Exchange Online no debe estar vencido. Si el certificado está vencido, el transporte de correo seguro entre la organización de Exchange Online y la organización local no funcionará correctamente.

## ¿Cómo saber si los certificados están configurados correctamente?

Para comprobar que el certificado para el transporte de correo híbrido está configurado correctamente en sus servidores locales de Exchange, siga estos pasos:

1.  En un servidor Exchangex local, abra el Shell de administración de Exchange.

2.  En el Shell de administración de Exchange, ejecute el siguiente comando:
    
        Get-ExchangeCertificate| format-list

3.  Localice la información del certificado que definió en el asistente para la configuración híbrida para usar para el transporte de correo seguro.

4.  Verifique que se asignan los siguientes valores de parámetro al certificado:
    
      - **Parámetro IsSelfSigned**   El valor de este parámetro debe ser *False*.
    
      - **Parámetro RootCAType**   El valor de este parámetro debe ser *Third Party*.
    
      - **Parámetro de servicios**   El valor de este parámetro debe ser *IIS, SMTP*.
    
      - \-**Parámetro NotAfter**   El valor de este parámetro es la fecha de vencimiento del certificado. La fecha indicada aquí no debe estar vencida.

## Solucionar errores específicos del Asistente para configuración híbrida

Si recibe un error mientras ejecuta el Asistente para configuración híbrida, a menudo se puede resolver con solo unas pocas comprobaciones o acciones. Consulte las siguientes sugerencias para resolver los mensajes o problemas específicos que pueden surgir al ejecutar el Asistente para configuración híbrida.

  - **Mensaje: "No se puede encontrar el conector de recepción predeterminado en el servidor \<nombre del servidor\>"**   Este mensaje aparece si el conector de recepción en cualquiera de los servidores de Exchange que aparecen en el siguiente atributo no escucha el puerto TCP 25 para los protocolos IPv4 e IPv6: `(Get-HybridConfiguration).ReceivingTransportServers.`
    
      -  
        Ejecute el siguiente comando en el Shell de administración de Exchange para comprobar si los conectores de recepción en los servidores de Exchange que aparecen al ejecutar `(Get-HybridConfiguration).ReceivingTransportServers.` tienen los enlaces adecuados.
        
            Get-ReceiveConnector -Server <Server Name> | FT Identity, Bindings
        
        Aparecerá la siguiente entrada relativa a los servidores de Exchange: `{[::]:25, 0.0.0.0:25}`
        
        Si este enlace no figura, deberá agregarlo al conector de recepción usando el parámetro *Bindings* del cmdlet **Set-ReceiveConnector**. Para obtener información detallada, consulte [Set-ReceiveConnector](https://technet.microsoft.com/es-es/library/bb125140\(v=exchg.150\)).

