---
title: 'Outlook for iOS and Android: Exchange 2013 Help'
TOCTitle: Outlook for iOS and Android
ms:assetid: 3a66817c-30da-4965-a6db-2955b5365b0f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Mt465744(v=EXCHG.150)
ms:contentKeyID: 70061296
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook for iOS and Android

 

_**Se aplica a:**Exchange Server 2010, Exchange Server 2013_

_**Última modificación del tema:**2018-04-02_

**Resumen:** este artículo contiene la arquitectura y la información de seguridad para los administradores acerca de Outlook para iOS y Android en un intercambio de 2013 entorno local.

La aplicación de Outlook para iOS y Android está diseñada para reunir a correo electrónico, calendario, contactos y otros archivos, permitiendo a los usuarios de su organización hacer más desde sus dispositivos móviles. Este artículo proporciona una visión general de la arquitectura y el diseño de almacenamiento de información de la aplicación, para que los administradores de Exchange pueden implementar y mantener Outlook para iOS y Android en sus organizaciones de Exchange.


> [!NOTE]
> El <A href="https://support.office.com/es-es/article/outlook-for-ios-and-android-help-center-cd84214e-a5ac-4e95-9ea3-e07f78d0cde6">Centro de ayuda de Outlook para iOS y Android</A> está disponible para los usuarios, incluida la ayuda para usar la aplicación en dispositivos determinados e información de solución de problemas.



## Arquitectura de Outlook para iOS y Android

Outlook para iOS y Android consta de una aplicación front-end que está instalada en los dispositivos móviles y de un servicio en la nube escalable y seguro en el back-end, conocido como el *servicio Outlook*. El procesamiento de información en el servicio Outlook habilita las características avanzadas y las funciones que mejoran la experiencia de Outlook, así como la estabilidad y el rendimiento. Esta arquitectura se basa en el servicio Outlook para el procesamiento intensivo, minimizando los recursos necesarios de los dispositivos de los usuarios.

Entre los ejemplos de lo que el servicio Outlook proporciona a los usuarios se incluye:

  - Categorización de la Bandeja de entrada prioritaria.

  - Característica para cancelar la suscripción en un clic de las listas de distribución de correo.

  - Mejorar la velocidad de búsqueda y la eficacia.

  - La capacidad de reenviar y enviar archivos grandes sin descargarlos primero en un dispositivo móvil.

## Almacenamiento en caché de datos

Para mejorar el rendimiento, se almacena en caché un subconjunto de correo electrónico, calendario y datos de archivo desde el buzón de cada usuario en el servicio de Outlook. Actualmente, este servicio se ejecuta en Microsoft Azure. Se está moviendo el servicio Outlook a Office 365 y va a tener que mover completado pronto.

La información en el servicio de Outlook se almacena actualmente en los Estados Unidos o en Europa, dependiendo de la dirección IP del cliente que se conecta. Cuando se mueve el servicio Outlook a Office 365, se alineará los principios expuestos en el centro de confianza de Office 365 con una estrategia de centros de datos de configuración regional. En Office 365, país o región, que escribe el administrador del cliente durante la instalación inicial de los servicios, de un cliente determina la ubicación de almacenamiento de información primario para los datos de ese cliente. Para obtener más información, consulte [El centro de confianza de Office 365](https://go.microsoft.com/fwlink/p/?linkid=525776).

## Preguntas más frecuentes del almacenamiento en caché de datos

A continuación se muestran las preguntas más frecuentes sobre el almacenamiento de datos en Outlook para iOS y Android.

## ¿Qué cantidad de datos del buzón de un usuario se almacena en caché en el servicio Outlook?

Aproximadamente un mes de datos de contactos, calendario y correo electrónico. El proceso de almacenamiento en caché se determina mediante un algoritmo que tiene en cuenta, entre otros factores, el tamaño de un buzón, la importancia relativa de una carpeta determinada dentro del buzón (por ejemplo, la carpeta Bandeja de entrada predeterminada en comparación con una carpeta que ha creado el usuario) y la frecuencia con la que un usuario accede a una carpeta determinada.

El servicio Outlook almacena los datos adjuntos de la siguiente manera: Cuando un usuario solicita abrir datos adjuntos de correo electrónico en Outlook, el servicio recupera los datos adjuntos del servidor de Exchange y los almacena temporalmente. En ese momento, los datos adjuntos se envían a la aplicación en el dispositivo móvil del usuario. Los datos anteriores a un mes se vacían del servicio de manera rutinaria; en este momento los datos adjuntos solo estarán disponibles en el servidor de Exchange.

## ¿Cómo quito mi información del servicio Outlook?

Tiene tres opciones para quitar su información del servicio Outlook.

  - Opción 1: Inicie un borrado remoto de cada usuario que haya usado la aplicación Outlook para iOS y Android para conectarse a Office 365 o Exchange.

  - Opción 2: Que todos los usuarios eliminen la aplicación Outlook. Los datos se eliminarán aproximadamente de 3 a 7 días.

  - Opción 3: Que cada usuario quite su cuenta de la aplicación Outlook y, después, elimine la aplicación de sus dispositivos móviles. Para quitar una cuenta, los usuarios deben seguir estos pasos:
    
    1.  En la aplicación Outlook, en **Configuración**, pulse **Configuración de cuenta**.
    
    2.  Pulse **Seleccionar una cuenta** y, después, con la cuenta seleccionada, pulse **Quitar cuenta**.
    
    3.  Pulse **Dispositivo y datos remotos**.

## ¿Cómo se protegen los datos del buzón almacenados en caché temporalmente mientras se almacenan en el servicio Outlook?

Puede leer acerca de cómo nuestros datos están protegidos actualmente en el [Centro de confianza de Azure](https://azure.microsoft.com/support/trust-center/). Como se mencionó anteriormente, cambiamos de domicilio de Azure y Office 365. La seguridad de estos servicios está cubierta en [El centro de confianza de Office 365](https://go.microsoft.com/fwlink/p/?linkid=525776).

