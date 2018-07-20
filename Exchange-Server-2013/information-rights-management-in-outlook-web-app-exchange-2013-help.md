---
title: 'Information Rights Management en Outlook Web App: Exchange 2013 Help'
TOCTitle: Information Rights Management en Outlook Web App
ms:assetid: 60a49dab-17ac-4d2c-9b41-7d87250d6c00
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd876891(v=EXCHG.150)
ms:contentKeyID: 49895662
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Information Rights Management en Outlook Web App

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Los trabajadores de información usan cada vez más el correo electrónico para intercambiar información confidencial. Para garantizar la seguridad de esta información, una organización puede usar Information Rights Management (IRM) para aplicar protección persistente al contenido de los mensajes. Antes de Microsoft Exchange Server 2010, el uso eficaz de la protección de IRM se limitaba a los clientes de Outlook. En Exchange Server 2007, los usuarios de Microsoft Outlook Web Access tenían que descargar el complemento de Rights Management para Microsoft Internet Explorer a fin de poder tener acceso al contenido protegido por IRM.

En Exchange 2013, el servicio IRM de Outlook Web App le permite a sus usuarios obtener acceso a la amplia funcionalidad de IRM que ofrece Exchange para aplicar protección de IRM persistente al contenido de los mensajes.

La siguiente funcionalidad IRM está disponible en Outlook Web App:

  - **Envío de mensajes protegidos por IRM**   Tal como lo muestra la siguiente imagen, los usuarios de Outlook Web App pueden usar la lista desplegable de permisos y seleccionar una plantilla de directivas de permisos para aplicar al mensaje. Esto permite a los usuarios enviar mensajes protegidos por IRM desde Outlook Web App. Los encargados de realizar la protección de IRM de los mensajes son los servidores de acceso de cliente.
    
    ![Envío de un mensaje protegido mediante IRM desde OWA](images/Dd876891.fa8cabb5-c049-46dc-8b29-9d9957dbfd3e(EXCHG.150).gif "Envío de un mensaje protegido mediante IRM desde OWA")  

  - **Adjuntos protegidos por IRM**   Cuando el usuario envía un mensaje protegido por IRM desde Outlook Web App, todos los archivos adjuntos a él también reciben la misma protección de IRM, con la misma plantilla de directivas de permisos que el mensaje. En Exchange 2013, la protección de IRM se aplica a los archivos asociados con Microsoft Office Word, Excel y PowerPoint, como así también a los archivos .xps y a los mensajes de correo electrónico. La protección IRM se aplica a un dato adjunto solo si aún no está protegido por IRM. Para obtener más información acerca de las plantilla de directivas de derechos de Active Directory Rights Management Services (AD RMS), vea [Information Rights Management](information-rights-management-exchange-2013-help.md).
    

    > [!NOTE]
    > En Outlook Web App, IRM solo protege los archivos adjuntos compatibles mencionados en esta sección. No se protegen los archivos adjuntos de formato no admitido. Cuando el usuario de Outlook Web App proteja un mensaje y adjunte un archivo de formato no admitido, aparecerá una notificación, informándole que solo se protegerán los tipos de archivo compatibles.

    

    > [!IMPORTANT]
    > La protección IRM no puede aplicarse a un mensaje que ya esté firmado o cifrado con S/MIME. Para aplicar la protección de IRM, se debe quitar del mensaje la firma y el cifrado de S/MIME. Esta misma regla afecta a los mensajes protegidos por IRM; el usuario no puede firmarlos ni cifrarlos mediante el uso de S/MIME.



  - **Lectura de mensajes protegidos por IRM**   Los mensajes protegidos por remitentes que usen el clúster de AD RMS de su organización se presentarán en el panel de vista previa de Outlook Web App. No es necesario instalar ningún complemento y el equipo no necesita involucrarse en la implementación de AD RMS. En el momento en que el usuario abre un mensaje o lo visualiza en el panel de vista previa, se lo descifra mediante la licencia de uso agregada por el agente de licencias previas. Después de ser descifrado, el mensaje se muestra en el panel de vista previa. Si no hay una licencia previa disponible, Outlook Web App solicita una al servidor AD RMS y luego muestra el mensaje. Al leer datos adjuntos protegidos por IRM en Outlook Web App, no está disponible la presentación de documentos Web-Ready.
    

    > [!NOTE]
    > En Outlook Web App, IRM no puede evitar que un usuario realice una captura de pantalla con la funcionalidad Imprimir pantalla del mismo modo en que lo hacen Outlook y otras aplicaciones de Office. Esto afecta al permiso de EXTRACCIÓN, el cual evita que se copie el contenido del mensaje, si así lo indica la plantilla de directiva de permisos de AD&nbsp;RMS.



  - **Compatibilidad de IRM multiplataforma, entre exploradores**   En Outlook Web App IRM ofrece compatibilidad de varias plataformas entre exploradores. En Outlook Web App, IRM es compatible con todos los exploradores que admite Exchange 2013, incluso con sistemas operativos de Apple Macintosh y Linux. Para obtener más información acerca de los exploradores y sistemas operativos compatibles, consulte [Exploradores compatibles con Outlook Web App](https://go.microsoft.com/fwlink/p/?linkid=129362).

  - **Presentación de documentos WebReady**   En Exchange 2013, los usuarios pueden ver documentos adjuntos protegidos con IRM mediante la presentación de documentos WebReady. Esto permite a los usuarios ver los documentos adjuntos compatibles sin tener que descargar, el archivo adjunto usa la aplicación asociada.

¿Está buscando tareas de administración relacionadas con la administración de IRM? Consulte [Procedimientos de Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

## Habilitar IRM en Outlook Web App

Para habilitar IRM en Outlook Web App, debe agregar el buzón de correo de la federación, un buzón del sistema que el programa de instalación de Exchange 2013 crea para el grupo de superusuarios en AD RMS. Para obtener detalles, vea [Agregar el buzón de la federación para el grupo de usuarios de AD RMS Super](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md). Esto permite a los servidores Exchange 2013 obtener acceso a los mensajes protegidos con IRM.

También puede habilitar IRM en Outlook Web App con el cmdlet [Set-IRMConfiguration](https://technet.microsoft.com/es-es/library/dd979792\(v=exchg.150\)) del Shell de administración de Exchange. Esto habilitará IRM en Outlook Web App para su organización de Exchange 2013. Puede deshabilitar o habilitar IRM en Outlook Web App para un directorio virtual de Outlook Web App. También puede controlar IRM en Outlook Web App con los siguientes niveles de granularidad:

  - **Directorio virtual de Per-Outlook Web App**   Para habilitar o deshabilitar IRM en Outlook Web App para un directorio virtual de Outlook Web App, use el cmdlet **Set-OWAVirtualDirectory** y establezca el parámetro *IRMEnabled* en `$false` o `$true` (predeterminado). Este permite deshabilitar IRM en Outlook Web App para un directorio virtual en un servidor de acceso de cliente Exchange 2013, mientras está habilitado en otro directorio virtual en un servidor de acceso de cliente distinto.

  - **Directiva de buzón de Per-Outlook Web App**   Para habilitar o deshabilitar IRM en Outlook Web App para una directiva de buzón de Outlook Web App, use el cmdlet **Set-OWAMailboxPolicy** y establezca el parámetro *IRMEnabled* en `$false` o `$true` (predeterminado). Esto permite habilitar IRM en Outlook Web App para un grupo de usuarios y deshabilitarlo para otro grupo de usuarios mediante la asignación de una directiva de buzón de Outlook Web App diferente.

Para obtener más información, consulte [Habilitar o deshabilitar el servicio Information Rights Management en los servidores de acceso de cliente](enable-or-disable-information-rights-management-on-client-access-servers-exchange-2013-help.md).

