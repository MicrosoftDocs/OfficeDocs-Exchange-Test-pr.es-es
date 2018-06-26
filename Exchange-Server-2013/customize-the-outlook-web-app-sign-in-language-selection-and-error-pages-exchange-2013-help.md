---
title: 'Personalizar las páginas de inicio de sesión, selección de idioma y error de Outlook Web App: Exchange 2013 Help'
TOCTitle: Personalizar las páginas de inicio de sesión, selección de idioma y error de Outlook Web App
ms:assetid: d8d9f735-7181-428f-9049-b9886dce5159
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee633483(v=EXCHG.150)
ms:contentKeyID: 54652456
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Personalizar las páginas de inicio de sesión, selección de idioma y error de Outlook Web App

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

En este tema se explica cómo personalizar el color y las imágenes de las páginas de inicio de sesión,‏‏ de selección de idioma y de error para Outlook Web App.

El signo Outlook Web App, selección de idioma y las páginas de error se crean basándose en los archivos de gráficos y .css en la carpeta de recursos de temas. Outlook Web App sólo utiliza un conjunto de inicio de sesión, selección de idioma y las páginas de error para todos los temas. Las modificaciones a esas páginas se verán todos los usuarios. Puede encontrar la carpeta de recursos de temas en el directorio de instalación de Exchange en V15\\FrontEnd\\HttpProxy\\owa\\auth\\version\\themes\\resources. Necesitará un editor de texto para cambiar los colores predeterminados y un editor de gráficos para cambiar las imágenes. Si debe coincidir con un color específico y no se puede encontrar a una coincidencia para él en la [Tabla de colores](https://go.microsoft.com/fwlink/p/?linkid=280679), puede utilizar una herramienta de edición de imágenes para muestrear un color y determinar su valor RGB de HTML.

Si tiene muchos servidores compatibles con Outlook Web App y quiere que todos ellos usen las mismas páginas de inicio de sesión, idioma y error, debe copiar los archivos modificados en cada servidor. También debe crear una copia de seguridad de los archivos personalizados. Si reinstala o actualiza Exchange, todos los archivos de las carpetas de temas se sobrescribirán. Deberá volver a copiar los archivos personalizados en la carpeta correspondiente una vez finalizada la reinstalación o actualización.


> [!IMPORTANT]
> Realice copias de seguridad de todos los archivos que va a cambiar antes de empezar a crear las páginas personalizadas de inicio y cierre de sesión.



Para más información sobre cómo crear un tema personalizado, vea [Crear un tema para Outlook Web App](create-a-theme-for-outlook-web-app-exchange-2013-help.md).

## ¿Qué necesita saber antes de empezar?

  - Tiempo estimado para completar esta tarea: 45 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Editor de gráficos" en \&quot;Permisos de Outlook Web App\&quot; en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué quiere hacer?

## Personalizar el color de la página de inicio de sesión

1.  Inicie sesión en el servidor de Exchange y use el Explorador de Windows para ir al directorio de instalación del servidor de Exchange y busque \\V15\\FrontEnd\\HttpProxy\\owa\\auth\\\<versión\>\\themes\\resources.

2.  Use un editor de texto, como el Bloc de notas, para abrir el archivo logon.css.

3.  Busque el valor \#0072 de colores predeterminado c 6 y reemplácelo por el valor HTML RGB del color que desea utilizar. Puede encontrar aquí los valores RGB de HTML: [Tabla de colores](https://go.microsoft.com/fwlink/p/?linkid=280679).

4.  Guarde y cierre el archivo.

## Personalizar el color de la página de error

1.  Inicie sesión en el servidor de Exchange y use el Explorador de Windows para ir al directorio de instalación del servidor de Exchange y busque \\V15\\FrontEnd\\HttpProxy\\owa\\auth\\\<versión\>\\themes\\resources.

2.  Use un editor de texto, como el Bloc de notas, para abrir el archivo errorFE.css.

3.  Busque el valor \#0072 de colores predeterminado c 6 y reemplácelo por el valor HTML RGB del color que desea utilizar. Puede encontrar aquí los valores RGB de HTML: [Tabla de colores](https://go.microsoft.com/fwlink/p/?linkid=280679).

4.  Guarde y cierre el archivo.

## Personalizar el color de la página de selección de idioma

1.  Inicie sesión en el servidor de Exchange y use el Explorador de Windows para ir al directorio de instalación del servidor de Exchange y busque \\V15\\Client Access\\OWA\\version\\Owa2\\resources\\styles.

2.  Use un editor de texto, como el Bloc de notas, para abrir el archivo LanguageSelection.css.

3.  Busque el valor \#0072 de colores predeterminado c 6 y reemplácelo por el valor HTML RGB del color que desea utilizar. Puede encontrar aquí los valores RGB de HTML: [Tabla de colores](https://go.microsoft.com/fwlink/p/?linkid=280679).

4.  Guarde y cierre el archivo.

## Personalizar las imágenes en las páginas de inicio de sesión y de error

Use una herramienta de edición de imágenes para abrir y modificar las imágenes que se usan para crear las páginas de inicio de sesión y de error.

1.  Inicie sesión en el servidor de Exchange y use el Explorador de Windows para ir al directorio de instalación del servidor de Exchange y busque \\V15\\FrontEnd\\HttpProxy\\owa\\auth\\\<versión\>\\themes\\resources.

2.  Use un editor de gráficos para abrir y modificar los siguientes archivos:
    
      - owa\_text\_blue.png, para cambiar el logotipo de texto de "Outlook Web App".
    
      - olk\_logo\_white.png, para cambiar el logotipo de la aplicación en la barra izquierda.
    
      - olk\_logo\_white\_cropped.png, para cambiar la imagen del panel del lado izquierdo de la página de error.
    
      - sign\_in\_arrow.png, para cambiar el icono izquierdo del botón de inicio de sesión.
    
      - olk\_exchange\_text\_blue.png, para cambiar el logotipo de "Outlook Mobile" en un diseño con el parámetro tnarrow.
    
      - olk\_logo\_white\_small.png se usa en el parámetro tnarrow.
    
      - olk\_exchange\_text\_stacked\_white\_small.png se usa en el parámetro tnarrow.

3.  Busque el valor \#0072 de colores predeterminado c 6 y reemplácelo por el valor HTML RGB del color que desea utilizar. Puede encontrar aquí los valores RGB de HTML: [Tabla de colores](https://go.microsoft.com/fwlink/p/?linkid=280679).

4.  Guarde y cierre el archivo.

## ¿Cómo saber si el proceso se ha completado correctamente?

Abra la página de inicio de sesión de Outlook Web App en Internet Explorer. Si va a probar los cambios del sitio web predeterminado en el servidor que hospeda el directorio virtual de Outlook Web App, abra Internet Explorer y escriba la dirección URL https://localhost/owa.

Si no ve los cambios, haga lo siguiente:

1.  En la barra de herramientas, seleccione **Configuración** \> **Opciones de Internet** \> **General**.

2.  En **Historial de exploración**, seleccione **Eliminar**.

3.  Seleccione **Archivos temporales de Internet y archivos de sitios web** y luego seleccione **Eliminar**.

4.  Cuando Internet Explorer termine con la eliminación, seleccione **Aceptar** para cerrar **Opciones de Internet**.

5.  Actualice la ventana del explorador.


> [!TIP]
> Para ver los efectos de los cambios, puede dejar abierto el archivo .css que está modificando y actualizar la ventana del explorador después de guardar cada cambio.


