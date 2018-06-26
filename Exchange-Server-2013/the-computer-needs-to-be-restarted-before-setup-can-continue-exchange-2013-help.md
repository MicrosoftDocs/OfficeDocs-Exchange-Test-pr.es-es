---
title: 'Se debe reiniciar el equipo para continuar con la instalación: Exchange 2013 Help'
TOCTitle: Se debe reiniciar el equipo para continuar con la instalación
ms:assetid: d5c73280-4e54-473a-b328-9673af11e2c0
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.rebootpending(v=EXCHG.150)
ms:contentKeyID: 48268733
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Se debe reiniciar el equipo para continuar con la instalación

 

_**Se aplica a:**Exchange Server_

_**Última modificación del tema:**2016-12-09_

El programa de instalación de Microsoft Exchange Server 2013 no puede continuar porque se ha detectado que debe reiniciarse el equipo local para completar la instalación de otros programas o actualizaciones de Windows.

## ¿Por qué ocurre esto?

Cuando se instalan los programas y actualizaciones de Windows, se hacen cambios en los archivos almacenados en el equipo. Algunas veces, durante la instalación, un programa o actualización de Windows necesita hacer un cambio en un archivo que está en uso. Cuando esto ocurre, es necesario reiniciar el equipo para poder instalar cualquier otro programa, como Exchange 2013. El programa de instalación de Exchange requiere que se hayan terminado todas las demás instalaciones para poder comprobar que se hayan instalado todos los requisitos previos que necesita para funcionar correctamente.

Algunas veces, es posible que la instalación de un programa anterior o actualización de Windows no se complete correctamente. Cuando esto sucede, se pueden dejar atrás los cambios que hacen que Windows y otros programas consideren necesario un reinicio. Lamentablemente, como la instalación errónea nunca limpia estos cambios, se puede bloquear la instalación de las actualizaciones de Windows y otros programas. Seguirá viendo este error cada vez que ejecute el programa de instalación de Exchange si esto sucede.

## ¿Cómo corrijo este error?

En la mayoría de los casos, solo debe reiniciar el equipo para superar este error. Sin embargo, hay ocasiones en las que podría obtener este error de nuevo incluso aunque ya haya reiniciado el equipo. Esto puede suceder cuando la instalación de un programa o actualización de Windows necesita realizar cambios adicionales y dichos cambios también requieren que se reinicie el equipo. Si ve este error después de reiniciar el equipo, intente reiniciarlo de nuevo.

Si ya reinició el equipo más de dos o tres veces y sigue viendo este error, intente volver a instalar los programas o actualizaciones de Windows que haya instalado recientemente. Esto podría permitir que una instalación errónea se complete correctamente.

Si tras reiniciar el equipo y volver a instalar los programas recientes o actualizaciones de Windows, *sigue* recibiendo este error, le recomendamos que se ponga en contacto con el soporte técnico de Microsoft. Ellos le ayudarán a encontrar el motivo por el que Windows y otros programas consideran que es necesario reiniciar el equipo. Para ponerse en contacto con el soporte técnico de Microsoft, vaya a [Soporte para Microsoft Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=525940).


> [!WARNING]
> Aunque pueda resultar tentador hacerlo, le recomendamos encarecidamente que no intente solucionar el problema eliminando manualmente o cambiando claves o valores en el Registro de Windows. Si bien al hacerlo puede corregir el problema en el momento, podría provocar otros problemas más adelante. Esto es especialmente importante si la instalación errónea era una actualización de Windows.


