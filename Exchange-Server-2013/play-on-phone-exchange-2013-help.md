---
title: 'Reproducir en teléfono: Exchange 2013 Help'
TOCTitle: Reproducir en teléfono
ms:assetid: 511e4950-340a-48cc-a020-35d11e76b993
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn205136(v=EXCHG.150)
ms:contentKeyID: 54652412
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Reproducir en teléfono

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2013-04-25_

Cuando llega un mensaje de correo de voz, los usuarios pueden elegir escucharlo a través de los altavoces o auriculares de su equipo o usar la característica Reproducir en teléfono. La característica Reproducir en teléfono se incluye con Microsoft Outlook y Outlook Web App, y la configuración para Reproducir en teléfono está disponible en la sección **Reproducir en teléfono** dentro de las opciones de **Correo de voz**. Este tema trata sobre cómo un usuario habilitado para mensajería unificada puede usar la característica Reproducir en teléfono.

## ¿Qué es Reproducir en teléfono?

La característica Reproducir en teléfono permite a los usuarios habilitados para mensajería unificada reproducir mensajes de voz a través de un teléfono. Si un usuario habilitado para mensajería unificada está sentado en el cubículo de su oficina, está usando un equipo público o un equipo que no tiene funciones multimedia habilitadas, o está escuchando un mensaje de voz confidencial, posiblemente no desee que nadie escuche el mensaje de voz a través de los altavoces del equipo, o quizás no pueda hacerlo. Como alternativa, puede reproducirlo con cualquier teléfono, ya sea el de casa, el de la oficina o un teléfono móvil. Para revisar la configuración de Reproducir en teléfono, en Outlook vaya a **Archivo** \> **Información** \> **Administrar correo de voz**. Al hacer clic en **Administrar correo de voz**, se inicia sesión automáticamente en Outlook Web App. También puede iniciar sesión en Outlook Web App mediante un explorador web. En Outlook Web App, vaya a la sección **Opciones** \> **Teléfono** \> **Correo de voz** \> **Reproducir en teléfono** de la página **Correo de voz**.

Cuando el usuario hace clic en la opción de la barra de herramientas Reproducir en teléfono del formulario de correo de voz, se abre el cuadro de diálogo **Reproducir en teléfono**. El cuadro **Reproducir en teléfono** incluye los controles para seleccionar o especificar el número de teléfono que se va a usar para reproducir un mensaje de voz, para iniciar y terminar la llamada, y un mensaje de estado para supervisar la llamada. Si el usuario está vinculado con un plan de marcado de URI de SIP, la dirección SIP aparecerá en el cuadro **Marcar**. Si está vinculado con un plan de marcado E.164, el número E.164 completo aparecerá en el cuadro **Marcar**.


> [!NOTE]
> Solo se puede reproducir un mensaje de voz por vez. Si el usuario intenta iniciar una segunda llamada de Reproducir en teléfono cuando aún se está realizando la llamada anterior, aparecerá un mensaje de error.



## Lista de últimos números de teléfono utilizados

Los usuarios pueden ver una lista de los últimos números de teléfono utilizados en el cuadro **Marcar**. El número de teléfono especificado en la sección **Reproducir en teléfono** siempre aparece como primera entrada y se selecciona automáticamente como número principal para el usuario. Los usuarios pueden usar el menú desplegable para seleccionar otros números de teléfono a los que llamar en lugar del número de teléfono configurado como número principal.


> [!NOTE]
> Para que los usuarios que usan la función Reproducir en teléfono puedan llamar a un número de teléfono externo sin un código de acceso de línea externo (por ejemplo, 425-555-1234 en lugar de 9-425-555-1234), configure reglas de marcado para el país o región en un plan de marcado de mensajería unificada que incluya la línea siguiente: grupo1, 9xxxxxxxxxx, 91xxxxxxxxxx. Una vez que haya configurado las reglas de marcado para el país o región, agregue esta lista a la directiva de buzones de mensajería unificada.



## Botones de Reproducir en teléfono

El cuadro de diálogo **Reproducir en teléfono** ofrece a los usuarios la opción de **Marcar** y **Colgar**. La primera vez que se abre el cuadro de diálogo **Reproducir en teléfono**, el botón **Marcar** está habilitado y el botón **Colgar** está deshabilitado. Después de realizar una llamada, el botón **Marcar** se deshabilita hasta que la llamada finaliza. Para terminar la llamada, haga clic en el botón **Colgar** o cuelgue físicamente el teléfono. Al cerrar el cuadro de diálogo **Reproducir en teléfono** con el botón **Cerrar**, finaliza la llamada en curso. La opción **Reproducir en teléfono** y otras opciones también se encuentran disponibles en la vista previa **Panel de lectura** en Outlook. Si abre el mensaje de correo de voz en una ventana separada, el botón **Reproducir en teléfono** aparece en la barra de herramientas.

## Sección de asunto, envío y estado

La sección inferior del cuadro de diálogo **Reproducir en teléfono** muestra el asunto del mensaje de voz, la fecha y la hora en que se envió y un mensaje que muestra el estado actual de la llamada. Cualquier error específico de la operación Reproducir en teléfono se indica al usuario en esta sección del cuadro de diálogo **Reproducir en teléfono**.

## Validación del número de teléfono

La función Reproducir en teléfono solo realiza una validación simple de los datos que se escriben en el cuadro de diálogo **Reproducir en teléfono**. No se validan los números de teléfono. Si un número de teléfono no es válido, la mensajería unificada devuelve un código de error explicativo al usuario.

