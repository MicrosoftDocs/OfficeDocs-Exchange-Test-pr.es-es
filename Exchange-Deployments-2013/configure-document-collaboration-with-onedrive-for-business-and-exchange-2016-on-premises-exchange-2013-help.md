---
title: 'Configurar datos adjuntos modernos con OneDrive para la Empresa y Exchange 2016 local: Exchange 2013 Help'
TOCTitle: Configurar datos adjuntos modernos con OneDrive para la Empresa y Exchange 2016 local
ms:assetid: 799518aa-7cfe-4708-92ee-98057ff168f5
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Mt589761(v=EXCHG.150)
ms:contentKeyID: 70319585
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar datos adjuntos modernos con OneDrive para la Empresa y Exchange 2016 local

 

_<strong>Se aplica a:</strong>Exchange Server 2016_

_<strong>Última modificación del tema:</strong>2016-12-09_

**Resumen:**   Cómo permitir que los usuarios de Exchange Server 2016 local aprovechen las ventajas del uso de la colaboración en documentos mediante OneDrive para la Empresa y SharePoint Online en una configuración híbrida.

Recientemente se ha añadido una nueva opción de datos adjuntos en Office 365. En 2016 de Exchange, esta opción, conocida como *colaboración en documentos*, permite a los usuarios locales integrar datos adjuntos almacenados en OneDrive para la Empresa directamente en sus clientes de Outlook en la web.


> [!NOTE]
> Desde el lanzamiento de Exchange Server 2016, Outlook Web App se conoce como Outlook en la web.



Anteriormente, un usuario enviaba un archivo a otras personas adjuntándolo a un mensaje. Uno o más destinatarios realizaban cambios en sus copias respectivas del archivo, lo cual requería que se combinasen en algún punto. Además, estos archivos adjuntos ocupan espacio de almacenamiento en el buzón de correo de cada usuario. Con la colaboración en documentos, los usuarios insertan un vínculo a un archivo que se almacena en una cuenta de OneDrive para la Empresa, permitiendo la edición del archivo por varias personas en la misma ubicación de origen, sin la necesidad de almacenamiento adicional.

Antes de que el entorno de Exchange 2016 se configure correctamente para la colaboración en documentos, los cuadros de diálogo de datos adjuntos predeterminados del usuario de Outlook en la web tendrán un aspecto similar a este:

![Cuadro de diálogo tradicional de datos adjuntos](images/Mt589761.f8c74d70-42f9-48c6-b263-ce6cef8591a8(EXCHG.150).png "Cuadro de diálogo tradicional de datos adjuntos")

Después de configurar el entorno con las siguientes instrucciones, los cuadros de diálogo de datos adjuntos de Outlook en la web tendrán un aspecto similar a este:

![Cuadro de diálogo de datos adjuntos con los datos adjuntos modernos habilitados](images/Mt589761.89eeae65-ce3a-4c47-b57e-db734a1de95b(EXCHG.150).png "Cuadro de diálogo de datos adjuntos con los datos adjuntos modernos habilitados")

Los usuarios de su organización con buzones locales que tengan una cuenta de OneDrive para la Empresa en Office 365 pueden utilizar el método moderno de datos adjuntos, que les permitirá compartir un documento almacenado en OneDrive para la Empresa con varios destinatarios. La ubicación de los destinatarios (en línea o local) no importa.

Puede obtener más información acerca de las implementaciones híbridas en [Implementaciones híbridas de Exchange Server](exchange-server-hybrid-deployments-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 15 minutos

  - Revise el tema [Implementaciones híbridas de Exchange Server](exchange-server-hybrid-deployments-exchange-2013-help.md) y asegúrese de que comprende las áreas que se verán afectadas por la configuración de la implementación híbrida.

  - Revise y complete todos los requisitos de implementación híbrida descritos en [Requisitos previos de implementación híbrida](hybrid-deployment-prerequisites-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](https://technet.microsoft.com/es-es/library/jj150484\(v=exchg.150\)).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Configurar Exchange 2016 para permitir la colaboración en documentos en un entorno híbrido

Compruebe que se hayan completado los siguientes pasos previos y después utilice el siguiente procedimiento para habilitar la colaboración en documentos.

**Requisitos previos**

  - Configurar el entorno de Exchange híbrido utilizando el [Asistente de configuración híbrida](hybrid-configuration-wizard-exchange-2013-help.md) (HCW).

  - Exchange 2016 debe instalarse en la organización local. Exchange 2016 puede coexistir con versiones anteriores de Exchange, pero la colaboración en documentos solo funcionará en los buzones en un servidor de Exchange 2016.

  - El servidor de autenticación debe instalarse con todos los usuarios sincronizados. Puede utilizar el cmdlet [Get-AuthServer](https://technet.microsoft.com/es-es/library/jj218613\(v=exchg.150\)) para buscar el servidor de autenticación. Se recomienda utilizar el HCW desde un servidor de Exchange 2016 para realizar las configuraciones necesarias de OAuth.
    

    > [!IMPORTANT]
    > OAuth entre Exchange 2016 y Office 365 debe configurarse correctamente. Para obtener más información, consulte <A href="https://technet.microsoft.com/es-es/library/dn594521(v=exchg.150)">Configurar la autenticación OAuth entre organizaciones de Exchange y Exchange Online</A>.



  - Los usuarios deben tener licencias adecuadas. Los usuarios con una cuenta de OneDrive para la Empresa deben contar con una licencia de SharePoint Online o OneDrive para la Empresa. Puede comprobar la licencia de un usuario seleccionándolo en el portal de Office 365 y seleccionando el botón **Editar**.
    

    > [!NOTE]
    > Para obtener más información, consulte <A href="http://go.microsoft.com/fwlink/p/?linkid=627455">Configurar OneDrive para la Empresa en Office 365</A>.



Realice los siguientes pasos:

1.  Configure el valor predeterminado de la directiva de buzones de correo de Outlook en la web para establecer la dirección URL del host de OneDrive para la Empresa.
    

    > [!NOTE]
    > Puede ir al Administrador arrendatario de SharePoint Online de Office 365 para recuperar la dirección URL del host de OneDrive para la Empresa. Por ejemplo, https://contoso-mi.sharepoint.com es una dirección URL del host de Mi sitio en los inquilinos de O365 de Contoso.<BR>Aunque la directiva de buzones de correo de Outlook en la web que se incluye con Exchange 2016 se llama "Predeterminada", no se aplica automáticamente a los buzones de correo a menos que la establezca como la directiva predeterminada o la asigne directamente a un buzón de correo.

    
    Empleando el siguiente ejemplo como referencia, utilice el Shell de administración de Exchange para configurar la dirección URL interna y externa de Mi sitio en la directiva de buzones de correo de Outlook en la web Predeterminada:
    
        Set-OwaMailboxPolicy Default -InternalSPMySiteHostURL https://Contoso-my.sharepoint.com -ExternalSPMySiteHostURL https://Contoso-my.sharepoint.com

2.  A continuación, establezca la directiva que acaba de configurar como predeterminada para que se aplique a todos los buzones, o asígnela a usuarios individuales.
    
    Para establecer la directiva como la directiva de buzones de correo de Outlook en la web predeterminada, escriba el siguiente comando en el Shell de administración de Exchange:
    
        Set-OwaMailboxPolicy Default -IsDefault 
    
    Para asignar la directiva a un buzón de correo determinado, escriba el siguiente comando en el Shell de administración de Exchange:
    
        Set-CASMailbox <user mailbox> -OwaMailboxPolicy Default

3.  (Opcional) En cada servidor de Exchange 2016, reinicie **OWAApplicationPool** y la configuración se aplicará inmediatamente. Si no ejecuta este comando, serán necesarios unos minutos para que los servidores de Exchange 2016 apliquen la directiva de buzones de correo actualizada. En el Shell de administración de Exchange ejecute:
    
        Restart-WebAppPool MSExchangeOWAAppPool

Una vez configurado, se le ofrecerá a los usuarios de Outlook en la web la posibilidad de elegir el tipo de datos adjuntos que desean usar en sus mensajes: tradicional o moderno.

![Cuadro de diálogo de las opciones de datos adjuntos, Compartir con OneDrive o Enviar como datos adjuntos](images/Mt589761.7d2f27c2-3638-479a-a577-029ac61e7d95(EXCHG.150).png "Cuadro de diálogo de las opciones de datos adjuntos, Compartir con OneDrive o Enviar como datos adjuntos")

