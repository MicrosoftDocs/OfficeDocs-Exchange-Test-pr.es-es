---
title: 'Instalar un paquete de idioma de mensajería unificada: Exchange 2013 Help'
TOCTitle: Instalar un paquete de idioma de mensajería unificada
ms:assetid: ed14ffa5-c9b0-4367-b5da-564024b360ff
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd876951(v=EXCHG.150)
ms:contentKeyID: 49895996
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Instalar un paquete de idioma de mensajería unificada

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2016-12-09_

Para que un idioma esté disponible en la lista de idiomas de mensajería unificada de un plan de marcado de mensajería unificada o un operador automático de mensajería unificada, primero debe instalar el paquete de idioma de mensajería unificada apropiado. Para instalar el paquete de idioma en un servidor de buzones de correo, debe ejecutar el servicio de mensajería unificada de Microsoft Exchange mediante el archivo ejecutable autoextraíble específico del idioma o el comando **setup.exe /AddUmLanguagePack**. Antes de instalar un paquete de idioma de mensajería unificada, debe descargarlo a una carpeta local del servidor de buzones de correo. Puede descargar los paquetes de idioma de mensajería unificada de [Paquetes de idioma de mensajería unificada para Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=266542). Hay un archivo ejecutable independiente para cada idioma.

Después de instalar el paquete de idioma de mensajería unificada adecuado, puede ver los paquetes de idioma de UM instalados en la lista desplegable de la página **Configuración** de un plan de marcado de mensajería unificada o la lista desplegable **Idioma de la interfaz de voz automatizada** de la página **General** de un operador automático de mensajería unificada. Además, puede configurar el idioma predeterminado para que no sea el inglés de Estados Unidos (en-US) en los planes de marcado de mensajería unificada y en los operadores automáticos.


> [!WARNING]
> Los paquetes de idioma de mensajería unificada para Microsoft Exchange Server 2007 o Exchange 2007 Service Pack&nbsp;1&nbsp;(SP1), SP2, o SP3 o Exchange 2010 Service Pack&nbsp;1&nbsp;SP1, SP2 o SP3 no se pueden usar en un servidor de buzones de correo de Exchange&nbsp;2013.



Para consultar otras tareas relacionadas con los idiomas de mensajería unificada, vea [Procedimientos de lenguajes, mensajes y saludos de mensajería unificada](um-languages-prompts-and-greetings-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Servidor de buzones de correo (servicio de mensajería unificada)" en [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Compruebe que el servidor de buzones de correo esté instalado en un equipo diferente que el servidor de acceso de cliente o que el servidor de acceso de cliente y los servidores de buzones de correo estén en el mismo hardware.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso del archivo de instalación de paquetes de idiomas de UM (.exe) para instalar un paquete de idioma de UM

1.  En el [Centro de descarga de Microsoft](https://go.microsoft.com/fwlink/p/?linkid=266542), descargue el archivo del paquete de idioma de mensajería unificada (.exe) en una carpeta local del servidor de buzones de correo.

2.  Haga doble clic en el archivo UMLanguagePack.*\<CultureCode\>.exe*. Por ejemplo, para obtener el paquete de idioma de mensajería unificada de alemán, debe descargar el archivo denominado UMLanguagePack.de-DE.exe.

3.  
    
    En el Asistente para la instalación de Exchange 2013, en la página **Contrato de licencia**, lea detenidamente las condiciones del contrato, seleccione la opción **Acepto los términos del contrato de licencia** y, después, haga clic en **Siguiente**.

4.  
    
    En la página **Paquete de idioma de mensajería unificada**, compruebe que aparezca el idioma correcto en la ventana **Se instalarán los siguientes paquetes de idioma de mensajería unificada** y, a continuación, haga clic en **Instalar**.

5.  Haga clic en **Finalizar** para completar la instalación del paquete de idioma de UM.

## Uso de setup.exe para instalar un paquete de idioma de UM

En este ejemplo, se instala el paquete de idioma de mensajería unificada del japonés (ja-JP), el cual se ha descargado a la carpeta D:\\Exchange\\UMLanguagePacks de un servidor de buzones de correo.

```powershell
setup.exe /AddUmLanguagePack:ja-JP /s:d:\Exchange\UMLanguagePacks /IAcceptExchangeServerLicenseTerms
```

En este ejemplo, se instalan los paquetes de idiomas de UM del español de México (es-MX) y del alemán (de-DE), los cuales se han descargado a la carpeta D:\\Exchange\\UMLanguagePacks de un servidor de buzones de correo.

    setup.exe /AddUmLanguagePack:es-MX,de-DE /s:d:\Exchange\UMLanguagePacks /IAcceptExchangeServerLicenseTerms


> [!WARNING]
> Si no usa el parámetro /IAcceptExchangeServerLicenseTerms, aparecerá el siguiente error: Instalación desatendida de Microsoft Exchange Server 2013. Necesita aceptar los términos de licencia para instalar Microsoft Exchange Server 2013. Para leer el contrato de licencia, visite http://go.microsoft.com/fwlink/p/?LinkId=150127. Para aceptar el contrato de licencia, agregue el parámetro /IAcceptExchangeServerLicenseTerms al comando que está ejecutando. Para obtener más información, ejecute setup /?.



Para obtener más información sobre los idiomas de mensajería unificada disponibles y los códigos de idioma, consulte [Idiomas, mensajes y saludos de mensajería unificada](um-languages-prompts-and-greetings-exchange-2013-help.md).

