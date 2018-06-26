---
title: 'Permitir usuarios de mail reenviar llamadas de voz: Exchange 2013 Help'
TOCTitle: Permitir usuarios de mail reenviar llamadas de voz
ms:assetid: 1f8e0a53-3d9d-4f8c-9be3-9f1e2a4347a3
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd335138(v=EXCHG.150)
ms:contentKeyID: 50556747
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permitir usuarios de mail reenviar llamadas de voz

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2013-02-22_

La característica Reglas de respuesta a llamada se presentó por primera vez en Exchange 2010. Con esta característica, los usuarios habilitados para el correo de voz pueden controlar cómo se deben manejar sus llamadas entrantes. El modo en que se aplican las reglas de respuesta a llamada a las llamadas entrantes es similar al modo en que se aplican las reglas de bandeja de entrada a los mensajes de correo electrónico entrantes.

Un usuario habilitado para correo de voz crea y configura las reglas de respuesta a llamada con Outlook o Outlook Web App. Las reglas se almacenan junto con otros ajustes de voz en el buzón de correo del usuario. Es posible configurar un total de nueve reglas de respuesta a llamada para cada buzón de correo habilitado para la mensajería unificada. Estas reglas son independientes de las reglas de la Bandeja de entrada configuradas por los usuarios y no ocupan ninguna parte de la cuota de almacenamiento de las reglas de la Bandeja de entrada del usuario.

De manera predeterminada, cuando un usuario está habilitado para la Mensajería unificada (MU) y el correo de voz, no se configuran reglas de respuesta a llamada. Si el sistema de correo de voz contesta una llamada entrante, puede solicitarle al autor de la llamada que deje un mensaje de voz o, si el autor de la llamada no recibe una solicitud, igualmente podrá dejar un mensaje de voz para el usuario.

Si sus usuarios desean dejar que el sistema de correo de voz solamente conteste las llamadas entrantes y grabe un mensaje de voz, no será necesario que cree reglas de respuesta a llamada. No obstante, si desea configurar condiciones o acciones, lo puede hacer en la sección **Reglas de respuesta a llamada** de la página **Correo de voz**, de Outlook Web App. En la sección **Reglas de respuesta a llamada**, es posible crear, editar y eliminar reglas de contestador automático.

## Funcionamiento de las reglas de respuesta a llamada

Una regla de contestador automático consta de dos partes: condiciones y acciones. Se pueden asociar una o más condiciones a una sola regla de contestador automático. La regla de contestador automático solo se procesará si se cumplen las condiciones correspondientes a esa regla. También, se pueden asociar una o más acciones a una sola regla de contestador automático. Estas acciones determinan las opciones que se le ofrecerán a la persona que llama cuando se procese la regla de contestador automático.

Las reglas de respuesta a llamada admiten las siguientes condiciones:

  - Persona que realiza la llamada

  - Hora del día

  - Estado de disponibilidad del calendario

  - Si las respuestas automáticas están activadas para el correo electrónico

Además, admiten las siguientes acciones:

  - Encontrarme

  - Transferir la llamada a otra persona

  - Dejar un mensaje de voz

Si el usuario graba un saludo personalizado para la regla de contestador automático, debe incluir la opción de menú en el saludo personalizado cuando configure la regla de contestador automático. De lo contrario, Mensajería unificada no generará un aviso de menú que informe al llamador de las opciones que tiene. Después de que se reproduce el saludo personalizado, el servidor espera a recibir la entrada de la persona que llama. Si no se incluye una opción de menú en el saludo, la persona que llama no podrá ingresar ninguna entrada y el servidor le preguntará "¿Todavía se encuentra allí?"

## Condiciones

Las condiciones son reglas que se pueden aplicar a las reglas de contestador automático. Mediante la combinación de condiciones, es posible crear numerosas reglas de contestador automático que se activarán cuando se cumplan las condiciones. Para crear una regla predeterminada que se aplique a todas las llamadas, se debe crear una regla que no contenga ninguna condición.

Existen tres condiciones que pueden usarse al configurar reglas de respuesta a llamada, estas incluyen:

  - Identificador de llamada

  - Hora del día

  - Estado de disponibilidad

## Acciones

Las acciones se usan para definir lo que se desea que ocurra cuando se cumple una condición. Los dos tipos de acciones son:

  - Encontrarme

  - Transferir llamadas

**Agregar la acción Encontrarme**

Cuando el autor de la llamada selecciona Buscarme, el sistema de correo de voz intenta localizarle en un máximo de dos números de teléfono diferentes y, si está disponible en uno de ellos, le conecta con el autor de la llamada.

  - Se puede especificar el texto que se leerá a la persona que llame. Por ejemplo, si especifica "Asuntos urgentes" para indicar a los autores de llamadas que solo deben seleccionar esta acción si necesitan hablar con usted sobre temas importantes, el sistema de correo de voz dirá "Para Asuntos urgentes, presione la tecla 1."

  - Se debe asociar la acción Encontrarme con el número del teclado telefónico que deberá presionar la persona que llame para seleccionar esta acción. En el ejemplo anterior, la tecla **1** del teléfono es el número que deben presionar quienes llamen para ubicarlo en uno de los números telefónicos que especifique.

  - A continuación, tiene que especificar el número o los números de teléfono que marcará el sistema de correo de voz. Si especifica dos números, se llamará al segundo cuando no esté disponible en el primero. Cada número de teléfono que especifique tiene una duración asociada. La duración es el período durante el cual el sistema de correo de voz intentará marcar el número antes de pasar al siguiente. En caso de que no sea posible comunicarse con usted, el sistema de correo de voz regresará al menú de opciones.

  - Una vez que haya introducido esta información, haga clic en **Aplicar** para guardar la configuración de Encontrarme.

**Agregar acciones de Transferencia de llamadas**

Al establecer la acción Transferencia de llamada, se le ofrece a quien llama la opción de transferirlo al número telefónico de otra persona. Existen varias opciones disponibles cuando se desea transferir una llamada entrante a otro teléfono o contacto.

  - Se puede especificar el texto que se leerá a la persona que llame. Por ejemplo, puede especificar "Asuntos urgentes" para informar a los autores de llamadas que seleccionen esta opción cuando necesiten hablar con alguien sobre algún tema importante.

  - Se debe asociar la acción **Transferencia de llamada** con el número del teclado telefónico que deberá presionar la persona que llame para seleccionar esta acción.

  - Cuando se elige la acción Transferencia de llamada, se debe especificar una persona o un número telefónico al que se transferirá a quien llame. Se puede elegir un número telefónico o seleccionar un contacto a quien llamar cuando el autor de la llamada presiona la tecla correspondiente del teclado de su teléfono. Si se indica un contacto que se encuentra en el directorio de la empresa, el sistema de correo de voz intentará transferir la llamada al número de extensión de dicho contacto.

  - Además de especificar una persona o un número al cual transferir la llamada, también se debe indicar el número del teclado telefónico que deberá presionar la persona que llame para seleccionar la acción Transferencia de llamada.

  - Una vez que haya introducido esta información, haga clic en **Aplicar** para guardar la configuración de Transferencia de llamada.

## Selección de una regla de contestador automático para cada llamada entrante

Después de crear y configurar las reglas de contestador automático, la mensajería unificada hará lo siguiente:

1.  Determinará si el usuario ha creado alguna regla de contestador automático. De lo contrario, ofrecerá a la persona que llama la posibilidad de dejar un mensaje de voz.

2.  Si hay una o más reglas de contestador automático configuradas, evaluará cada una de esas reglas. Se procesará la primera de las reglas cuyas condiciones se cumplan.

3.  Después de evaluar todas las reglas, si no encuentra una regla cuyas condiciones se cumplan, le solicitará al cliente que deje un mensaje de voz.

## Reglas de marcado

Según la configuración de las reglas de contestador automático, es posible que se transfiera una llamada entrante. Cuando esto ocurre, el número telefónico al que se transfiere la llamada queda sujeto a las reglas y las restricciones de marcado establecidas en la directiva de buzón de correo de MU a la que se encuentra asociado el destinatario de la llamada. Para más información sobre las llamadas externas y las reglas y restricciones de marcado, vea [Permitir que los usuarios realicen llamadas](allow-users-to-make-calls-exchange-2013-help.md).

## Habilitación y deshabilitación de las reglas de respuesta a llamada

De manera predeterminada, las reglas de respuesta a llamada se habilitan automáticamente para los usuarios habilitados para MU. Sin embargo, puede deshabilitar las reglas de respuesta a llamada para los usuarios mediante la deshabilitación de dicha característica en una directiva de buzón de correo de MU o en el buzón de correo del usuario. Para obtener información detallada acerca de la habilitación y la deshabilitación de las reglas de respuesta a llamada, consulte los siguientes temas:

  - [Permitir o impedir que los usuarios de la misma directiva de buzón de mensajería unificada desde la creación de reglas de respuesta de llamada](allow-or-prevent-users-in-the-same-um-mailbox-policy-from-creating-call-answering-rules-exchange-2013-help.md)

  - [Permitir o impedir la creación de reglas de respuesta de llamada de un usuario](allow-or-prevent-a-user-from-creating-call-answering-rules-exchange-2013-help.md)

