---
title: 'Crear un tema para Outlook Web App: Exchange 2013 Help'
TOCTitle: Crear un tema para Outlook Web App
ms:assetid: 7e1fa13c-3de3-45c2-b1fa-e74fc8487bda
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb201700(v=EXCHG.150)
ms:contentKeyID: 54652444
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Crear un tema para Outlook Web App

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Un *tema* define el color de fondo, las fuentes, los colores de resaltado, los iconos y el encabezado que utiliza MicrosoftOutlook Web App. Cada tema es una colección de archivos multimedia y hojas de estilo en cascadas (archivos .css) almacenados en el directorio de instalación \\Client Access\\OWA\\prem\\*version*\\resources\\themes del servidor de MicrosoftExchange. Cada tema se almacena en su propio subdirectorio de \\themes.

El tema predeterminado se encuentra en \\Client Access\\OWA\\prem\\*version*\\resources\\themes\\base. Cada carpeta de tema contiene todos los archivos que se necesitan para definir un tema. Estos archivos incluyen archivos CSS, gráficos y un archivo .xml que define el nombre del tema. Puede crear temas adicionales copiando todos los archivos de un tema a una carpeta nueva y modificando estos archivos según sea necesario.

De forma predeterminada, se instalan varios temas cuando se instala Exchange Server 2013 de la siguiente manera:

  - Los archivos CSS (.css) definen colores, degradados y fuentes.

  - Los archivos de imagen (.png) proporcionan los iconos y otros elementos gráficos. Si edita cualquiera de los iconos, no cambie su tamaño. Si cambia el tamaño de alguno de los elementos gráficos, pruebe los cambios para comprobar que los elementos se ajustan correctamente.

Estos archivos se almacenan en el directorio de instalación del servidor de acceso de cliente, en \\Client Access\\OWA\\prem\\*\<version\>*\\resources\\themes. Cada tema se almacena en un subdirectorio de temas. Puede crear temas adicionales si copia un tema existente y modifica la copia.

Después de crear un tema, es posible que también desee [Personalizar las páginas de inicio de sesión, selección de idioma y error de Outlook Web App](customize-the-outlook-web-app-sign-in-language-selection-and-error-pages-exchange-2013-help.md).


> [!NOTE]
> La versión ligera de Outlook Web App no admite temas.




> [!WARNING]
> Si tiene varios servidores compatibles con Outlook Web App, debe copiar el tema personalizado en cada servidor. También debe crear una copia de seguridad de los temas personalizados. Si vuelve a instalar Exchange o lo actualiza, todos los archivos de las carpetas de temas se sobrescribirán. Deberá volver a copiar su tema en la carpeta correspondiente una vez haya finalizado la reinstalación o actualización.<BR>Haga copias de seguridad de todos los archivos que vaya a modificar antes de comenzar a crear su tema personalizado.



## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar esta tarea:  60 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Directorios virtuales de Outlook Web App" en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Necesita acceso de administrador al servidor local para realizar estos procedimientos.

  - Necesitará un editor de texto para cambiar los colores predeterminados y un editor de gráficos para cambiar las imágenes. Si debe coincidir con un color específico y no se puede encontrar a una coincidencia para él en la [Tabla de colores](https://go.microsoft.com/fwlink/p/?linkid=280679), puede utilizar una herramienta de edición de imágenes para muestrear un color y determinar su valor RGB de HTML.

  - Se recomienda que utilice las siguientes directrices cada vez que cambie o cree un tema de Outlook Web App:
    
      - Si decide editar un tema existente, haga copias de seguridad de los archivos originales antes de comenzar a editarlos.
    
      - No elimine la carpeta \\Client Access\\OWA\\prem\\*version*\\resources\\themes\\base ni los archivos que contiene.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Cómo realiza esto?

## Paso 1: Crear un nuevo tema de Outlook Web App

Para empezar, debe crear una carpeta para el tema nuevo y, después, copiar los archivos de un tema existente en esta carpeta nueva.

1.  Inicie sesión en el servidor de Exchange que hospede el directorio virtual de Outlook Web App. Para ello, utilice una cuenta que tenga delegada la pertenencia al grupo Administradores local.

2.  Abra el Explorador de Windows y busque el directorio de instalación del servidor de Exchange.

3.  En \\Client Access\\OWA\\prem\\*version*\\resources\\themes, cree una carpeta nueva y nómbrela; por ejemplo, Fourth Coffee.

4.  Copie todos los archivos del otro tema en la carpeta nueva.

## Paso 2: Nombrar el tema nuevo

Para establecer el nombre para mostrar del tema nuevo, haga lo siguiente:

1.  Abra la copia de themeinfo.xml que se encuentra en la carpeta del tema personalizado que acaba de crear.

2.  Busque el valor `displayname` del tema y cámbielo por el nombre que desee utilizar. Por ejemplo, `displayname = "Fourth Coffee Theme"`.

3.  Guarde y cierre themeinfo.xml.

## Paso 3: Cambiar el criterio de ordenación del tema nuevo (opcional)

Si lo desea, puede cambiar el criterio de ordenación del tema nuevo editando el archivo themeinfo.xml. El criterio de ordenación determina la posición del tema en el panel **Cambiar tema** del menú Configuración.

Para cambiar el criterio de ordenación del tema nuevo mediante el archivo themeinfo.xml, haga lo siguiente:

1.  Abra la copia de themeinfo.xml que se encuentra en la carpeta del tema personalizado.

2.  Busque el valor `sortorder` del tema y cámbielo para reflejar el lugar que desea que ocupe el tema nuevo en la lista. Los temas se ordenarán según el valor numérico en orden ascendente. De forma predeterminada, el tema base es el primero y su valor `sortorder` es \&quot;0\&quot;. Por ejemplo, `sortorder="<number>"`.

3.  Guarde y cierre themeinfo.xml.

## Paso 4: Modificar el tema nuevo

Una vez que haya copiado los archivos y le haya asignado un nombre al tema, podrá personalizarlo. Los siguientes elementos se pueden personalizar en un tema de Outlook Web App:

  - Archivos de imagen, que definen el área de encabezado y los iconos.

  - Archivos CSS, que definen las fuentes y los colores.

## Archivos de imagen

Las imágenes del tema se almacenan en dos carpetas en \\themes*\\\<nombre de tema\>*\\images\\. La carpeta \\images\\0 contiene las imágenes que se usarán en los idiomas que se leen de izquierda a derecha (como el inglés) y los idiomas que se leen de derecha a izquierda usarán las imágenes de la carpeta \\images\\rtl.


> [!NOTE]
> Algunas de las imágenes que están en la carpeta \images\rtl son iguales a las de la carpeta \images\0, pero reflejadas.



Para personalizar el tema, puede usar una herramienta de edición de imágenes y modificar las siguientes imágenes:

  - Headerbgmain.png
    
      - Esta es la imagen del encabezado principal. Se recomienda que no supere la altura de encabezado de 30 píxeles. El tema predeterminado no tiene imagen de fondo, por lo que esta imagen es transparente. Para obtener un ejemplo de un tema que tenga una imagen de fondo personalizada, vea la imagen en la carpeta del tema **Blueprint**.

  - Headerbgright.png
    
      - Esta se utiliza como imagen de mosaico detrás del encabezado. El tema predeterminado no tiene imagen de fondo de mosaico, por lo que esta imagen es transparente. Para obtener un ejemplo de un tema que tenga una imagen de fondo de mosaico personalizada, vea la imagen en la carpeta del tema **Blueprint**.

  - sprite1.mouse.png
    
      - Esta contiene la mayoría de las imágenes que se utilizan en un tema. Puede cambiar el color de las imágenes para que coincidan con el tema, así como cambiar el logotipo de texto predeterminado de Outlook Web App
    
      - Para evitar cualquier tipo de problemas, no cambie el tamaño de los iconos individuales del duendecillo y asegúrese de guardarlo como un archivo .png transparente.

  - themepreview.png
    
      - Esta imagen se utilizará para representar el tema en el panel **Cambiar tema** del menú Configuración de Outlook Web App.

## Colores y fuentes

Los archivos de hoja de estilos en cascada (.css) definen los colores y fuentes que se utilizan en un tema y se almacenan en varias carpetas en \\themes\\*\<nombre de tema\>*. La carpeta \\*\<nombre de tema\>*\\0 contiene archivos .css que se usarán en los idiomas que se leen de izquierda a derecha (como el inglés) y los idiomas que se leen de derecha a izquierda utilizarán los archivos .css de la carpeta \\*\<nombre de tema\>*\\rtl. También hay carpetas específicas para cada idioma (por ejemplo, \\ja, \\ko, \\zhs y \\zht) que contienen archivos .css que se utilizarán con esos idiomas.

Comience modificando la carpeta \\*\<theme name\>*\\images\\0. Se utilizan cuatro colores en cada tema que se pueden personalizar.

  - BrandColor: \#0072C6

  - NavBarHoverColor: \#4C9CD7

  - UnreadColor: \#2A8DD4

  - FocusColor: \#DFEDFA

Con un editor de texto como Bloc de notas, puede buscar y reemplazar todas las instancias de estos valores con los colores de su tema en los siguientes dos archivos: owa2styles.mouseCSS y owa2styles2.mouseCSS. Debe hacerlo en todas las carpetas del tema nuevo que contengan estos archivos .css.

## Paso 5: Definir el tema predeterminado de Outlook Web App

La configuración de un nuevo tema predeterminado solo afectará a los usuarios que no hayan cambiado su tema en el menú Configuración de Outlook Web App.

Para que todos los usuarios usen de forma obligatoria el tema predeterminado, debe deshabilitar la selección del tema y definir un tema predeterminado.

## Usar el Shell para definir el tema predeterminado para Outlook Web App

En este ejemplo se define el tema predeterminado para Outlook Web App, donde el nombre del servidor es `fourthcoffee`, el nombre del directorio virtual es `owa`, el nombre del sitio web es `default web site` y el tema está en la carpeta llamada `Custom`.

```powershell
    set-owavirtualdirectory -identity "fourthcoffee\owa (default web site)" -defaulttheme Custom 
```

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Set-OwaVirtualDirectory](https://technet.microsoft.com/es-es/library/bb123515\(v=exchg.150\)).

## Usar el Shell para deshabilitar la selección de tema para Outlook Web App

En este ejemplo se deshabilita la selección de tema en Outlook Web App, donde el nombre del servidor es `fourthcoffee`, el nombre del directorio virtual es `owa` y el nombre del sitio web es `default web site`.

```powershell
    set-owavirtualdirectory -identity "fourthcoffee\owa (default web site)" -themeselectionenabled $false 
```

También puede completar ambos comandos simultáneamente, como se muestra en el siguiente ejemplo:

```powershell
    set-owavirtualdirectory -identity "fourthcoffee\owa (default web site)" -defaulttheme Custom -themeselectionenabled $false
```

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Set-OwaVirtualDirectory](https://technet.microsoft.com/es-es/library/bb123515\(v=exchg.150\)).

## Paso 6: Ejecutar iisreset/noforce para guardar los cambios

Si agrega o cambia un tema o bien si cambia su nombre o su criterio de ordenación, debe detener e iniciar el servicio Internet Information Services (IIS) para que el cambio surta efecto. Para ello, abra una ventana del símbolo del sistema en el servidor donde haya creado el tema nuevo y ejecute el comando **iisresest /nforce**.

## ¿Cómo sabe si esta tarea se ha completado correctamente?

1.  Inicie sesión en Outlook Web App usando el directorio virtual del servidor donde ha creado el tema nuevo. Si va a probar los cambios realizados al sitio web predeterminado del servidor de Exchange que hospeda el directorio virtual de Outlook Web App, puede probar el tema abriendo Internet Explorer e introduciendo la URL https://localhost/owa.

2.  Cambie al tema personalizado seleccionando el menú Configuración \> **Cambiar tema** y, a continuación, el tema personalizado.

## Si no ve los últimos cambios realizados y ha ejecutado iisreset/noforce

1.  En la barra de herramientas de Internet Explorer, seleccione el menú Configuración \> **Opciones de Internet**.

2.  En la pestaña **General**, en **Historial de exploración**, seleccione **Eliminar** y, a continuación, compruebe que la opción **Archivos temporales de Internet y archivos de sitios web** está marcada. Después, seleccione **Eliminar** para quitar esos archivos.

3.  Seleccione **Aceptar** para cerrar **Opciones de Internet**.

4.  Seleccione **Actualizar** para ver los cambios.

Es posible que tenga que repetir estos pasos para ver los cambios cada vez que modifique los archivos de temas. Si va a realizar varios cambios, puede dejar Outlook Web App abierto y repetir la ejecución de **iisreset/noforce** en el servidor y el borrado de archivos temporales de Internet Explorer tantas veces como sea necesario.

