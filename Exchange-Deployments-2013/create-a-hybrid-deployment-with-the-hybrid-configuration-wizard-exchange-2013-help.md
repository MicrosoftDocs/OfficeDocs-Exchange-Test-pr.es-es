---
title: 'Creación de una implementación híbrida con el Asistente de configuración híbrida: Exchange 2013 Help'
TOCTitle: Creación de una implementación híbrida con el Asistente de configuración híbrida
ms:assetid: 997a25d3-7fb3-4d4e-bb28-defcbf542c99
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ200787(v=EXCHG.150)
ms:contentKeyID: 48268934
ms.date: 03/14/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Creación de una implementación híbrida con el Asistente de configuración híbrida

Este tema se está redactando.  

_<strong>Se aplica a:</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>Última modificación del tema:</strong>2016-12-09_

Al establecer una implementación híbrida, puede extender la experiencia de características enriquecidas y el control administrativo de la organización local existente de Exchange Server a la nube. Una implementación híbrida también admite una solución de archivado basado en la nube para sus buzones locales mediante el Archivado de Exchange Online Archiving, y también puede ser un paso intermedio hacia una migración total de sus buzones locales a Exchange Online.

En este tema se trata la configuración de una implementación híbrida de su organización de Exchange local y su organización de Exchange Online en Office 365 para empresas mediante el Asistente para la configuración híbrida. En este tema, se crea una implementación híbrida para la siguiente configuración de organización:

  - La organización local es una organización de Exchange local de un solo bosque.

  - La organización local no usa un servicio de Microsoft Exchange Online Protection (EOP) existente para la protección local.

  - La organización local no tiene servidores Transporte perimetral implementados. El Asistente para la configuración híbrida admite la configuración de servidores Transporte perimetral como parte de una implementación híbrida, pero la configuración de los servidores de transporte perimetral durante el asistente no se cubre en este tema.


> [!IMPORTANT]
> La configuración de una implementación híbrida con el Asistente para la configuración híbrida requiere varios requisitos previos importantes del asistente para que se complete correctamente y para que las características de implementación híbrida funcionen correctamente. Debe completar todos los requisitos previos que se describen en el tema <A href="hybrid-deployment-prerequisites-exchange-2013-help.md">Requisitos previos de implementación híbrida</A> antes de usar el Asistente para la configuración híbrida para crear y configurar su implementación híbrida.<BR>Además, el <A href="http://technet.microsoft.com/exdeploy2013">Asistente de implementación del servidor de Exchange</A> es una herramienta basada en web gratuita que lo ayuda a configurar una implementación híbrida entre su organización local y Office&nbsp;365, o bien, a migrar completamente a Office 365. La herramienta le realiza una pequeña serie de preguntas simples y luego, en función de sus respuestas, crea una lista de comprobación con instrucciones para configurar su entorno híbrido. Se recomienda encarecidamente que use el Asistente de implementación para generar una lista de comprobación de implementación híbrida personalizada para las necesidades específicas de su organización.



Para otras tareas de administración relacionadas con las implementaciones híbridas, consulte [Procedimientos de implementación híbrida](hybrid-deployment-procedures-exchange-2013-help.md).

Obtenga más información sobre las implementaciones híbridas en [Implementaciones híbridas de Exchange Server](exchange-server-hybrid-deployments-exchange-2013-help.md). Obtenga más información sobre Office 365 en [¿Qué es Office 365?](http://go.microsoft.com/fwlink/?linkid=266712).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 30 minutos
    

    > [!IMPORTANT]
    > La configuración de los requisitos para una implementación híbrida tardará considerablemente más que el tiempo estimado para completar los procedimientos del Asistente para la configuración híbrida que se detallan en este tema. Por ejemplo, iniciar la sesión en Office 365 para empresas, configurar la sincronización de Active Directory y asignar licencias de Exchange Online necesitan más tiempo y puede que también impliquen cambios en la topología de la red. Debería planificar más tiempo del que se indica para completar este procedimiento para el tiempo general para completar la configuración de la implementación híbrida de un extremo a otro.



  - Entrada "Implementaciones híbridas" Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el en el tema [Permisos de infraestructura de la Shell y de Exchange](https://technet.microsoft.com/es-es/library/dd638114\(v=exchg.150\)).

  - Debe ejecutar el Asistente para la configuración híbrida desde un equipo que ejecute la versión más reciente de una versión compatible de Exchange. Los pasos finales del Asistente para la configuración híbrida para configurar la autenticación de OAuth de Exchange requieren que los pasos se lleven a cabo desde un servidor de Exchange local o desde cualquier estación de trabajo o servidor unido a dominio. Además, el proceso de autenticación de OAuth funciona mejor cuando se usa la versión de escritorio de Internet Explorer 11 o superior.

  - Revise el tema [Implementaciones híbridas de Exchange Server](exchange-server-hybrid-deployments-exchange-2013-help.md) y asegúrese de que comprende las áreas que se verán afectadas por la configuración de la implementación híbrida.

  - Revise y complete todos los requisitos de implementación híbrida descritos en [Requisitos previos de implementación híbrida](hybrid-deployment-prerequisites-exchange-2013-help.md).

  - La herramienta Analizador de conectividad remota de Microsoft comprueba la conectividad externa de su organización local de Exchange y garantiza que esté lista para configurar una implementación híbrida. Le recomendamos encarecidamente que compruebe su organización local con la herramienta Analizador de conectividad remota antes de configurar la implementación híbrida con el asistente para configuraciones híbridas. Obtenga más información en [Herramienta Analizador de conectividad remota](http://go.microsoft.com/fwlink/p/?linkid=167905).

  - Se recomienda encarecidamente configurar el inicio de sesión único mediante la sincronización de contraseña de Azure Active Directory Connect. El inicio de sesión único permite a los usuarios acceder tanto a la organización local como a las organizaciones de Exchange Online con un solo nombre de usuario y contraseña. El inicio de sesión único también garantiza que no se soliciten las credenciales a los usuarios cuando accedan a contenido archivado en la organización de Exchange Online al usar Archivado de Exchange Online. Para obtener más información sobre la sincronización de contraseña, consulte [Sincronización de Azure AD Connect: implementación de la sincronización de contraseñas](http://go.microsoft.com/fwlink/p/?linkid=723513)

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](https://technet.microsoft.com/es-es/library/jj150484\(v=exchg.150\)).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Use el Centro de administración de Exchange y el Asistente para la configuración híbrida para crear una implementación híbrida

Utilice el procedimiento siguiente para crear y configurar una implementación híbrida:

1.  En el EAC de un servidor de Exchange de su organización local, vaya al nodo **Híbrido**.

2.  En el nodo **Híbrido**, haga clic en **Configurar** para escribir las credenciales de Office 365.
    

    > [!IMPORTANT]
    > Si su organización local se encuentra ubicada en China y su inquilino de Office&nbsp;365 está hospedado en 21Vianet, debe activar la casilla <STRONG>Mi organización de Office 365 está hospedada en 21Vianet</STRONG>. Si el inquilino de Office 365 está hospedado en 21Vianet y esta casilla no está activada, el Asistente para la configuración híbrida no se conectará con el servicio de 21Vianet, no se reconocerán las credenciales de la cuenta de Office 365 y el asistente no se completará correctamente.



3.  En el aviso para iniciar sesión en Office 365, seleccione **Iniciar sesión en Office 365** y especifique las credenciales de la cuenta. La cuenta a la que se conecte debe ser un administrador global de Office 365.

4.  Haga clic en **Configurar** para iniciar el Asistente para la configuración híbrida.

5.  En la página **Descarga del Asistente para la configuración híbrida de Microsoft Office 365**, haga clic en **Haga clic aquí** para descargar el asistente. Cuando se le solicite, haga clic en **Instalar** en el cuadro de diálogo **Instalación de aplicación**.

6.  Haga clic en **Siguiente** y después, en la sección **Organización de Exchange Server local**, seleccione **Detectar un servidor que ejecute Exchange 2013 CAS o Exchange 2016**. El asistente intentará detectar un servidor de Exchange local. Si el asistente no detecta un servidor de Exchange o, si desea usar un servidor diferente, seleccione **Especificar un servidor que ejecute Exchange 2013 CAS o Exchange 2016** y luego especifique el FQDN interno de un servidor de buzones de correo de Exchange.

7.  En la sección **Office 365 Exchange Online**, seleccione **Microsoft Office 365** y después haga clic en **Siguiente**.

8.  En la página **Credenciales**, en la sección **Escriba sus credenciales de la cuenta local**, seleccione **Usar las credenciales actuales de Windows** para que el asistente use la cuenta con la que ha iniciado sesión para acceder a la implementación de Active Directory local y a los servidores de Exchange. Si desea especificar un conjunto de credenciales diferente, anule la selección de **Usar las credenciales actuales de Windows** y especifique el nombre de usuario y la contraseña de una cuenta de Active Directory que desee usar. Independientemente de qué cuenta seleccione, la cuenta usada debe ser miembro del grupo de seguridad de administradores de la organización.

9.  En la sección **Escriba sus credenciales de Office 365**, especifique el nombre de usuario y la contraseña de una cuenta de Office 365 que tenga permisos de administrador global. Haga clic en **Siguiente**.

10. En la página **Validando conexiones y credenciales**, el asistente se conectará a la organización local y a la organización de Office 365 para validar las credenciales y examinar la configuración actual de ambas organizaciones. Haga clic en **Siguiente** cuando termine.

11. En **Dominios híbridos**, seleccione los dominios que desea incluir en la implementación híbrida. En la mayoría de las implementaciones puede dejar la columna **Detectar automáticamente** establecida en **Falso** para cada dominio. Seleccione solo **Verdadero** junto a un dominio si necesita forzar al asistente para que use la información de detección automática de un dominio específico. Haga clic en **Siguiente**.
    

    > [!IMPORTANT]
    > Este paso para la selección de un dominio para el asistente de configuración híbrida puede aparecer o no cuando ejecuta el asistente.<BR>Este paso no aparecerá si: 
    > <UL>
    > <LI>
    > <P>Tiene un solo dominio local aceptado y agregado a su inquilino de Office 365. Debido a que este es el único dominio disponible para la configuración de implementaciones híbridas, el dominio se selecciona automáticamente y este paso se saltea durante el asistente.</P>
    > <LI>
    > <P>No hay ningún dominio local aceptado y agregados a su inquilino de Office 365. En este caso, recibirá un mensaje de error y tendrá que agregar por lo menos un dominio a su inquilino de Office&nbsp;365 antes de continuar. Puede hacer esto usando el portal administrativo de Office&nbsp;365, u, opcionalmente, configurando los Servicios de Federación Active Directory (AD&nbsp;FS) en su organización local.</P></LI></UL>Este paso aparecerá si tiene más de un dominio local aceptado y agregado a su inquilino Office&nbsp;365.



12. En la página **Confianza de federación**, haga clic en **Habilitar** y después en **Siguiente**.

13. En la página **Propiedad del dominio**, haga clic en **Hacer clic para copiar al portapapeles** para copiar la información de token de la prueba de dominio de los dominios seleccionados para incluirlos en la implementación híbrida. Abra un editor de textos como el Bloc de notas y pegue la información de token de estos dominios. Antes de continuar en el Asistente para la configuración híbrida, debe usar esta información para crear un registro TXT para cada dominio en su DNS público. Consulte la ayuda del host del DNS para obtener más información sobre cómo agregar un registro TXT a la zona DNS. Haga clic en **Siguiente** después de que se hayan creado los registros TXT y de que se hayan replicado los registros de DNS.

14. En la página **Certificado de transporte**, en el campo **Seleccionar un servidor de referencia**, seleccione el servidor de Exchange que tenga el certificado que configuró anteriormente en la lista de comprobación.

15. En el campo **Seleccionar un certificado**, seleccione el certificado que usará para el transporte de correo seguro. Esta lista muestra los certificados digitales emitidos por una Entidad de certificación (CA) de terceros instalada en los servidores de buzones de correo seleccionados en el paso anterior. Haga clic en **Siguiente**.

16. En la página **FQDN de la organización**, escriba el FQDN accesible desde el exterior del servidor de Exchange accesible desde Internet. Office 365 usa este FQDN para configurar los conectores del servicio para el transporte de correo seguro entre sus organizaciones de Exchange. Por ejemplo, escriba "mail.contoso.com". Haga clic en **Siguiente**.

17. Las selecciones de configuración de implementación híbrida se han actualizado y están preparadas para iniciar los cambios de servicios de Exchange y la configuración de la implementación híbrida. Haga clic en **Actualizar** para iniciar el proceso de configuración. Mientras se ejecuta el proceso de configuración híbrida, el asistente muestra las áreas de servicios y características que se están configurando para la implementación híbrida a medida que se actualizan.

18. El asistente muestra un mensaje de finalización con el botón **Cerrar**. Haga clic en **Cerrar** para completar el proceso de configuración de implementación híbrida y para cerrar el asistente.

## Configurar la autenticación OAuth entre organizaciones de Exchange y Exchange Online

Para las implementaciones híbridas combinadas de Exchange 2013/2010 y Exchange 2013/2007, el Asistente para la configuración híbrida no configura la nueva conexión de autenticación basada en OAuth de la implementación híbrida entre Office 365 y las organizaciones locales de Exchange. Estas implementaciones seguirán usando el proceso de confianza de federación de forma predeterminada. Sin embargo, ciertas características de Exchange 2013 como la Administración de registros de mensaje (MRM), el archivado local de Exchange y la exhibición de documentos electrónicos local solo se encuentran totalmente disponibles en la organización mediante el uso del nuevo protocolo de autenticación de OAuth de Exchange. Recomendamos a las organizaciones con entornos combinados de Exchange 2013/2010 y Exchange 2013/2007 que quieran implementar estas características como parte de una nueva implementación híbrida con Exchange Online que configuren la autenticación de OAuth de Exchange después de configurar la implementación híbrida con el Asistente para la configuración híbrida.

Para conocer los pasos detallados de la configuración, vea [Configurar la autenticación OAuth entre organizaciones de Exchange y Exchange Online](https://technet.microsoft.com/es-es/library/dn594521\(v=exchg.150\)).

Para más información sobre las características de seguridad y cumplimiento de normas de Exchange que usan la autenticación de OAuth, vea:

  - [Uso de la autenticación de OAuth para admitir el archivado en una implementación híbrida de Exchange](https://technet.microsoft.com/es-es/library/dn689104\(v=exchg.150\))

  - [Uso de la autenticación de OAuth para admitir la exhibición de documentos electrónicos en una implementación híbrida de Exchange](https://technet.microsoft.com/es-es/library/dn497703\(v=exchg.150\))

## ¿Cómo saber si el proceso se ha completado correctamente?

La finalización correcta del Asistente para la configuración híbrida será su primera indicación de que los pasos de configuración híbrida han funcionado correctamente.

Para verificar que ha creado y configurado correctamente su implementación híbrida, realice lo siguiente:

  - Ejecute el siguiente comando en el Shell de Administración de Exchange para la organización local. Este comando muestra los valores y la configuración de la implementación híbrida, las características híbridas y los extremos de transporte. Compruebe que estos valores sean correctos.
    
        Get-HybridConfiguration

  - Confirme que el Asistente para la administración de configuración híbrida haya completado todos los pasos examinando el registro de configuración híbrida. De manera predeterminada, el registro de la configuración híbrida se encuentra en el servidor del buzón local C:\\Program Files\\Microsoft\\Exchange Server\\V15\\Logging\\Update-HybridConfiguration.

  - Mueva un buzón local existente a la organización de Exchange Online para probar la característica de mover el buzón o cree un buzón de usuario nuevo en la organización de Exchange Online para probar el uso de disponibilidad compartida entre dos organizaciones. Cualquier acción del buzón también le permitirá probar y confirmar que la entrega de mensajes entre las organizaciones locales y de Exchange Online funciona correctamente con buzones existentes y que la entrega de mensajes es segura y se trata como mensajes internos en la organización de Exchange.
    
      - Use el EAC y vaya a **Empresa** \> **Destinatarios** \> **Buzones** para crear un buzón remoto nuevo en Exchange Online.
    
      - Use el EAC y vaya a **Office 365** \> **Destinatarios** \> **Migración** para mover un buzón existente a Exchange Online.

