---
title: 'Simplificar la dirección URL de Outlook Web App: Exchange 2013 Help'
TOCTitle: Simplificar la dirección URL de Outlook Web App
ms:assetid: 5fb6a873-f3cf-4f82-87d1-2ff6e47a0080
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998359(v=EXCHG.150)
ms:contentKeyID: 54652439
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Simplificar la dirección URL de Outlook Web App

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-07-16_

**Resumen:**  Use los procedimientos de este artículo para simplificar la dirección URL que los usuarios de la organización usan para tener acceso a OWA en Exchange 2013.

Puede simplificar la dirección URL de MicrosoftOutlook Web App que usan los usuarios para tener acceso a su buzón de Exchange Server 2013.

Para simplificar el acceso a Outlook Web App para los usuarios, es posible que desee configurar la página web de Outlook Web App, que generalmente es el sitio web predeterminado en IIS, para que redirija los usuarios automáticamente a https. El procedimiento de la sección "Usar el Administrador de IIS para simplificar la dirección URL de Outlook Web App y forzar la redirección a SSL" redirige una solicitud de http://*servidor* a https://*servidor*/owa. Para ayudar a proteger la información enviada entre el cliente y el servidor, el sitio web predeterminado está configurado para que requiera la capa de sockets seguros (SSL) durante la instalación.

Cuando configure la redirección desde un directorio de nivel superior en Windows Server 2008, la configuración se propagará a los directorios inferiores. Por ejemplo, al configurar el redireccionamiento en el sitio web predeterminado al directorio virtual /owa, la configuración establecida también aparece en la página de redireccionamiento HTTP de todos los directorios virtuales, como /Autodiscover, /Exchange y /Public. Por lo tanto, será necesario que quite la redirección de todos los directorios virtuales, excepto del que desee redirigir.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 10 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Administrador de IIS" en la sección Permisos de Outlook Web App del tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Paso 1: Usar el Administrador de IIS para simplificar la dirección URL de Outlook Web App y forzar la redirección a SSL

1.  Inicie el Administrador de IIS

2.  Expanda su equipo local, expanda **Sitios** y, a continuación, haga clic en **Sitio web predeterminado**.

3.  En la parte inferior del panel Página principal del sitio web, haga clic en **Vista Características**, si esa opción no está ya seleccionada.

4.  En la sección **IIS**, haga doble clic en **Redirección HTTP**.

5.  Seleccione la casilla de verificación **Redirigir las solicitudes a este destino**.

6.  Escriba la ruta absoluta del directorio virtual /owa. Por ejemplo, escriba **https://mail.contoso.com/owa**.

7.  En **Comportamiento de redirección**, seleccione la casilla de verificación **Redireccionar solo las solicitudes de contenido en este directorio (no en los subdirectorios)**.

8.  En la lista **Código de estado**, haga clic en **Encontrado (302)**.

9.  En el panel Acciones, haga clic en **Aplicar**.

10. Haga clic en **Sitio web predeterminado**.

11. En el panel de inicio del sitio web predeterminado, haga doble clic en **Configuración de SSL**.

12. En **Configuración de SSL**, desactive **Requerir SSL**.
    

    > [!NOTE]
    > Si no desactiva la casilla <STRONG>Requerir SSL</STRONG>, los usuarios no serán redirigidos cuando entran a una URL no segura. Por el contrario, obtendrán un error de acceso denegado.



## Paso 2: Quitar el redireccionamiento de los directorios virtuales

Para quitar el redireccionamiento de un directorio virtual, siga estos pasos:

1.  Abra una ventana de símbolo del sistema.

2.  Desplácese al \<*directorio de Windows*\>\\system32\\Inetsrv.

3.  Ejecute los comandos siguientes:
    
    1.  `appcmd set config "Default Web Site/autodiscover" /section:httpredirect /enabled:false -commit:apphost`
    
    2.  `appcmd set config "Default Web Site/ecp" /section:httpredirect /enabled:false -commit:apphost`
    
    3.  `appcmd set config "Default Web Site/ews" /section:httpredirect /enabled:false -commit:apphost`
    
    4.  `appcmd set config "Default Web Site/owa" /section:httpredirect /enabled:false -commit:apphost`
    
    5.  `appcmd set config "Default Web Site/oab" /section:httpredirect /enabled:false -commit:apphost`
    
    6.  `appcmd set config "Default Web Site/powershell" /section:httpredirect /enabled:false -commit:apphost`
    
    7.  `appcmd set config "Default Web Site/rpc" /section:httpredirect /enabled:false -commit:apphost`
    
    8.  `appcmd set config "Default Web Site/rpcwithcert" /section:httpredirect /enabled:false -commit:apphost`
    
    9.  `appcmd set config "Default Web Site/Microsoft-Server-ActiveSync" /section:httpredirect /enabled:false -commit:apphost`

4.  Para finalizar, ejecute el comando `iisreset/noforce`.

Cuando configura la redirección desde un directorio de nivel superior, se puede crear un archivo web.config en \<*unidad*\>\\Archivos de programa\\Microsoft\\Exchange Server\\\<*versión*\>\\ClientAccess\\oab. Si esto ha sucedido y luego elimina la redirección, Outlook puede congelarse cuando los usuarios hagan clic en **Enviar y recibir**. Para evitar que esto suceda después de eliminar la redirección, elimine el archivo web.config de \<*unidad*\>\\Archivos de programa\\Microsoft\\Exchange Server\\\<*versión*\>\\ClientAccess\\oab.

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que simplificó correctamente la dirección URL de Outlook Web App y la redirigió a una conexión SSL, haga lo siguiente:

1.  Abra un explorador web y especifique la nueva dirección URL para Outlook Web App, con el formato http://\<*URL*\>.

2.  Debería ser redireccionado a la página de inicio de sesión de Outlook Web App a través de una conexión SSL.

