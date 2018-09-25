---
title: 'Ver o configurar los directorios virtuales de aplicación web de Outlook: Exchange 2013 Help'
TOCTitle: Ver o configurar los directorios virtuales de aplicación web de Outlook
ms:assetid: 90babcf6-4486-4e01-9819-6d3ca4ed756c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd298140(v=EXCHG.150)
ms:contentKeyID: 49895778
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ver o configurar los directorios virtuales de aplicación web de Outlook

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2013-08-12_

Puede usar el EAC o el Shell para ver o configurar las propiedades de un directorio virtual de Outlook Web App.


> [!WARNING]
> En Exchange Online, los administradores no pueden ver ni configurar directorios virtuales de Outlook Web App.



Si utiliza el Shell para ver las propiedades de un directorio virtual de Outlook Web App, la información devuelta es un subconjunto de la información disponible. Por ejemplo, si utiliza el cmdlet **Get-OWAVirtualDirectory** para ver las propiedades, Exchange devuelve la siguiente información:

  - Nombre de directorio virtual

  - Nombre de servidor

  - Versión del servidor de Exchange

También puede recuperar la información de un directorio virtual específico en un servidor determinado mediante los parámetros disponibles. Para obtener más información acerca de los parámetros para el cmdlet **Get-OWAVirtualDirectory**, consulte [Get-OwaVirtualDirectory](https://technet.microsoft.com/es-es/library/aa998588\(v=exchg.150\)).

Si utiliza el EAC para ver las propiedades de un directorio virtual de Outlook Web App, podrá ver la mayoría de propiedades del mismo.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  10 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Directorios virtuales de Outlook Web App" en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para ver o configurar las propiedades del directorio virtual de Outlook Web App

1.  En el EAC, haga clic en **Servidores** \> **Directorios virtuales**.
    
    Puede usar las listas desplegables para seleccionar el tipo de servidor y de directorio virtual. De forma predeterminada, aparecen todos los servidores y directorios virtuales.

2.  En el panel de resultados, haga clic para seleccionar el directorio virtual que desea ver o editar y, a continuación, haga clic en **Editar**.

3.  En la ficha **General**, puede ver las propiedades del sitio web predeterminado de Outlook Web App y especificar una URL externa y una URL interna. Vea o seleccione las opciones siguientes:
    
      - **Servidor**   (Sólo lectura.) **Servidor** muestra el nombre del servidor host del directorio virtual de Outlook Web App.
    
      - **Versión**   (Sólo lectura.) **Versión** muestra la versión del servidor de Exchange en la que está el directorio virtual.
    
      - **Sitio web**   (Sólo lectura.) **Sitio web** muestra el nombre del sitio web.
    
      - **Versión de Outlook Web App** (de solo lectura) **Versión de Outlook Web App** muestra la versión del servidor de Exchange.
    
      - **Modificado**   (Sólo lectura.) **Modificado** muestra la fecha y la hora en que se modificó por última vez el directorio virtual.
    
      - **URL interna**   En este cuadro de texto, especifique la dirección URL utilizada para obtener acceso a este sitio web desde una red interna. Durante la instalación de Exchange 2013, se configura automáticamente una URL interna. La configuración de la dirección URL interna predeterminada para un servidor abierto y no abierto a Internet es https://\<Nombre del equipo\>/owa.
    
      - **URL externa**   En este cuadro de texto, especifique la dirección URL utilizada para obtener acceso al sitio web desde Internet. De manera predeterminada, la **URL externa** está en blanco. Para servidores de acceso de cliente abierto a Internet, la **URL externa** se debe establecer con el valor publicado en DNS para ese sitio de Active Directory. Para los servidores de Exchange 2013 que no tengan presencia en Internet, la configuración **URL externa** debe dejarse en blanco.

4.  En la ficha **Autenticación**, especifique métodos de autenticación, el formato de inicio de sesión y el dominio de inicio de sesión.
    
      - **Usar uno o varios métodos de autenticación estándar**   Seleccione esta opción para usar uno o varios de los siguientes métodos de autenticación estándar:
        
        **Autenticación de Windows integrada**   Este método requiere que los usuarios tengan un nombre de cuenta de usuario y una contraseña de Windows Server 2008 o Windows Server 2012 válidos para obtener acceso a la información. Los usuarios no deberán introducir sus nombres de cuenta ni sus contraseñas. En su lugar, el servidor negocia con los paquetes de seguridad de Windows instalados en el equipo cliente. La autenticación integrada de Windows permite al servidor autenticar usuarios sin pedirles información ni transmitir información sin cifrar mediante la red. Para que este método funcione, el equipo cliente debe ser miembro del mismo dominio que los servidores que ejecutan Exchange o de un dominio en el que confíe el dominio en que se encuentra el servidor de Exchange.
        
        **Autenticación de texto implícita para servidores del dominio Windows**   Este método transmite contraseñas por medio de la red como valor de hash para mayor seguridad. La autenticación implícita se puede usar únicamente en los dominios de Windows Server 2008 y Windows Server 2012 para los usuarios que tengan una cuenta almacenada en Active Directory. Para obtener más información acerca de la autenticación implícita, consulte la documentación de Windows Server.
        
        **Autenticación básica (la contraseña se envía como texto no cifrado)**   Este método es un mecanismo simple de autenticación definido por la especificación HTTP que codifica el nombre de inicio de sesión y la contraseña de un usuario antes de enviar las credenciales del usuario al servidor. Para garantizar la máxima seguridad de la contraseña, debe usar el cifrado de Capa de sockets seguros (SSL) entre los equipos cliente y el servidor que tiene la función del servidor Acceso de cliente instalada.
    
      - **Usar autenticación basada en formularios**   La autenticación basada en formularios proporciona una seguridad mejorada para los directorios virtuales de Outlook Web App. La autenticación basada en formularios crea una página de inicio de sesión para Outlook Web App. Puede configurar el tipo de solicitud de inicio de sesión que utiliza la autenticación basada en formularios. Por ejemplo, puede configurar la autenticación basada en formularios para que solicite a los usuarios información sobre su dominio y nombre de usuario, con el formato dominio\\nombre de usuario en la página de inicio de sesión de Outlook Web App.
        

        > [!IMPORTANT]
        > La autenticación basada en formularios no proporcionará un canal seguro a menos que SSL esté habilitado.

        
        Seleccione una de las siguientes opciones:
        
        **Dominio\\nombre de usuario**   Este campo requiere que el usuario escriba su dominio y nombre de usuario con el formato dominio\\nombre de usuario. Por ejemplo, si hay un usuario llamado Kweku en el dominio Contoso, el inicio de sesión sería contoso\\kweku.
        
        **Nombre principal de usuario (UPN)** Si se especifica el formato de inicio de sesión del nombre principal del usuario (UPN), el cuadro **Nombre de usuario** en la página de inicio de sesión de Outlook Web App guía a los usuarios para que escriban su dirección de correo electrónico, por ejemplo, kweku@contoso.com. Si el UPN de un usuario no es idéntico a la dirección de correo electrónico, el usuario no podrá acceder a Outlook Web App mediante la solicitud de inicio de sesión de **PrincipalName**. La práctica recomendada es usar la solicitud de inicio de sesión de **PrincipalName** solo si los UPN de los usuarios coinciden con sus direcciones de correo electrónico.
        
        **Solo nombre de usuario** El usuario únicamente especifica el nombre de usuario, sin el nombre de dominio; por ejemplo, Kweku. Si usa la solicitud de inicio de sesión **Solo nombre de usuario** para la autenticación basada en formularios, también debe especificar la propiedad **Dominio de inicio de sesión**. La propiedad **Dominio de inicio de sesión** determina el dominio predeterminado que se usará cuando un usuario intente iniciar sesión en Outlook Web App. Por ejemplo, si el dominio predeterminado es Contoso y un usuario del dominio llamado Kweku inicia sesión en Outlook Web App, solo es necesario escribir Kweku como nombre de usuario. El servidor utilizará el dominio predeterminado Contoso. Si el usuario no es miembro del dominio Contoso, será necesario escribir el nombre de usuario y el dominio.

5.  En la ficha **Características**, especifique las características que desea habilitar o deshabilitar para los usuarios de Outlook Web App en un directorio virtual.
    

    > [!NOTE]
    > La configuración de las características para usuarios individuales sobrescribe la del directorio virtual. Es posible cambiar la configuración de la segmentación para usuarios individuales mediante el cmdlet <STRONG>Set-CASMailbox</STRONG> o mediante las directivas de buzón de Outlook Web App. Para obtener más información, consulte <A href="outlook-web-app-mailbox-policies-exchange-2013-help.md">Directivas de buzones de Outlook Web App</A>.

    
    Utilice las casillas para habilitar o deshabilitar funciones. Las funciones más comunes se muestran de forma predeterminada. Para ver todas las características que se pueden habilitar o deshabilitar, haga clic en **Más opciones**.
    

    > [!NOTE]
    > La opción para habilitar o deshabilitar la versión estándar de Outlook Web App usando la casilla <STRONG>Cliente premium</STRONG> está en desuso y se quitará de la configuración. La versión estándar de Outlook Web App está siempre habilitada.



6.  En la ficha **Acceso a los archivos**, utilice las casillas para configurar el acceso a archivos y ver las opciones de los usuarios. El acceso a archivos permite que un usuario abra o vea el contenido de los archivos adjuntos a un correo electrónico.
    
    El acceso a archivos se puede controlar en función de si el usuario inició sesión en un equipo público o privado. La opción para que los usuarios seleccionen el acceso al equipo privado o público están disponibles únicamente al utilizar la autenticación basada en formularios. El resto de formas de autenticación están establecidas de forma predeterminada en el acceso mediante equipo privado.
    
      - **Acceso directo a archivos**   Seleccione esta casilla si desea habilitar el acceso directo a archivos. El acceso directo a archivos permite a los usuarios abrir los archivos adjuntos a los mensajes de correo electrónico.
    
      - **Visualización de documento preparada para Web**   Active esta casilla si desea habilitar documentos compatibles para convertirlos en HTML y mostrarlos en un explorador web.
    
      - **Forzar la visualización de documento preparada para web cuando haya un convertidor disponible**   Active esta casilla si desea forzar la conversión de los documentos a HTML y su visualización en un explorador web antes de que los usuarios puedan abrirlos en la aplicación de visualización. Los documentos solo podrán abrirse en la aplicación de visualización si está habilitado el acceso directo a archivos.

7.  Haga clic en **Guardar** para actualizar la directiva.

## Usar el Shell para configurar las propiedades del directorio virtual de Outlook Web App

En este ejemplo, se habilita la autenticación basada en formularios en el directorio virtual predeterminado de Outlook Web App, en el servidor Contoso.

```powershell
set-OwaVirtualDirectory -Identity "Contoso\owa (default web site)" -FormsAuthentication $true
```

Para obtener más información sobre sintaxis y parámetros, consulte [Set-OwaVirtualDirectory](https://technet.microsoft.com/es-es/library/bb123515\(v=exchg.150\)).

## Usar el Shell para ver las propiedades del directorio virtual de Outlook Web App

Este ejemplo permite ver las propiedades de todos los directorios virtuales de Outlook Web App en todos los sitios web de Internet Information Services (IIS), en todos los equipos que tengan el rol de servidor de acceso de cliente instalado en una organización de Exchange.

```powershell
Get-OWAVirtualDirectory
```

Este ejemplo permite ver las propiedades de un directorio virtual de Outlook Web App en el sitio web de IIS predeterminado, en el servidor local de Exchange.

```powershell
Get-OWAVirtualDirectory -identity "<Exchange Server Name>\owa (default web site)"
```

Este ejemplo permite ver las propiedades de todos los directorios virtuales de Outlook Web App en un sitio web de IIS, en un servidor específico de Exchange.

```powershell
Get-OWAVirtualDirectory -server <Exchange Server Name>
```

Este ejemplo permite ver los valores de las propiedades de todos los directorios virtuales de Outlook Web App en todos los sitios web de IIS, en todos los servidores de acceso de cliente de una organización de Exchange.

```powershell
Get-OWAVirtualDirectory | format-list
```

Para obtener más información sobre sintaxis y parámetros, consulte [Get-OwaVirtualDirectory](https://technet.microsoft.com/es-es/library/aa998588\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que ha editado correctamente un directorio virtual de Outlook Web App:

1.  En el EAC, haga clic en **Servidores** \> **Directorios virtuales** y, a continuación, seleccione un directorio virtual específico de Outlook Web App.

2.  Haga clic en el botón **Editar** para ver las propiedades del directorio virtual.

3.  Haga clic en **Guardar** o **Cancelar** para cerrar la página de propiedades.

