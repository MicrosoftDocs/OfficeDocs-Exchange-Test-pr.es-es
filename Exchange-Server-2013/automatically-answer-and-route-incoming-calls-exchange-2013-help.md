---
title: 'Contestar y enrutar automáticamente las llamadas entrantes: Exchange 2013 Help'
TOCTitle: Contestar y enrutar automáticamente las llamadas entrantes
ms:assetid: d3dcd488-bd57-44cc-bdd4-ddee42a69dde
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124724(v=EXCHG.150)
ms:contentKeyID: 49895936
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Contestar y enrutar automáticamente las llamadas entrantes

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-08-26_

La mensajería unificada de Microsoft Exchange permite crear operadores automáticos de mensajería unificada únicos o múltiples, según las necesidades de la organización. A diferencia de otros componentes de mensajería unificada, como los planes de marcado de mensajería unificada y las puertas de enlace IP de MU, no es necesario crear operadores automáticos MU. Sin embargo, los operadores automáticos ayudan a quienes realizan llamadas, tanto internas como externas, a buscar a los usuarios o departamentos que están en una organización y a transferirles llamadas.  En este tema, se explica la característica de operadores automáticos de la mensajería unificada.

**Contenido**

Operadores automáticos

Operadores automáticos de mensajería unificada

Operadores automáticos con varios idiomas

Saludo personalizado durante el horario comercial y el horario no comercial

Entradas de navegación de menús

Ejemplos de operadores automáticos

## Operadores automáticos

En los entornos de telefonía o mensajería unificada, un operador automático o sistema de menús de operadores automáticos transfiere las llamadas entrantes a la extensión de un usuario o departamento, sin la intervención de un recepcionista ni operador. En muchos sistemas de operadores automáticos, se puede poner en contacto con un recepcionista u operador presionando o diciendo cero. El operador automático es una característica presente en la mayoría de soluciones de centrales de conmutación (PBX), IP PBX y mensajería unificada.

En algunos sistemas de operadores automáticos, hay menús informativos de sólo mensajes y menús de voz para que la organización pueda proporcionar información sobre los horarios de apertura, cómo llegar a las instalaciones, las oportunidades laborales y respuestas a otras preguntas frecuentes. Una vez reproducido el mensaje, la persona que llama es dirigida al recepcionista u operador, o puede volver al menú principal.

En sistemas de operadores automáticos más complejos, el sistema de menús se puede usar para buscar otros menús de operadores automáticos, buscar a un usuario en el sistema o transferir a otra línea de teléfono externa. Asimismo, se puede usar para permitir a la persona que llama interactuar con el sistema en ciertas situaciones, por ejemplo, cuando un estudiante se matricula en una clase de la universidad o consulta sus notas o cuando usted activa una tarjeta de crédito por teléfono.

Aunque los operadores automáticos pueden ser muy útiles, si no están diseñados y configurados correctamente, pueden confundir y frustrar a los que realizan llamadas. Por ejemplo, especialmente en organizaciones de gran tamaño, si los operadores automáticos no están diseñados correctamente, la persona que llama puede tener que pasar a lo largo de una serie inacabable de preguntas e instrucciones del menú, antes de que se le transfiera finalmente a una persona para que responda a sus preguntas.

## Operadores automáticos de mensajería unificada

La mensajería unificada le permite crear uno o más operadores automáticos de mensajería unificada, según las necesidades de la organización. Los operadores automáticos de UM se pueden usar para crear los sistemas de menús de voz de una organización que permiten a quienes realizan llamadas, tanto internas como externas, moverse por el sistema de menús de operadores automáticos de UM para buscar, realizar o transferir llamadas a los usuarios o departamentos de la empresa en una organización.

Si usuarios anónimos o no autenticados llaman a un número de teléfono externo del trabajo, o si los usuarios realizan una llamada interna a un número de extensión definido, serán recibidos por una serie de mensajes de voz que les ayudarán a realizar una llamada a un usuario o a buscar a un usuario en la organización y, a continuación, a realizar una llamada a ese usuario. El operador automático de la mensajería unificada consta de una serie de mensajes de asistencia por voz o archivos .wav que las personas oyen (en lugar de oír a un operador humano) al llamar a una organización que tiene mensajería unificada. El operador automático de mensajería unificada permite a las personas que llaman moverse por el sistema del menú, realizar llamadas o buscar a usuarios mediante Multifrecuencia de tono dual (DTMF) o entradas de voz. Sin embargo, para poder usar el reconocimiento automático de voz o las entradas de voz, debe habilitar el reconocimiento automático de voz en el operador automático de mensajería unificada.

Un operador automático de UM consta de las siguientes funciones:

  - Proporciona saludos informativos o corporativos.

  - Proporciona menús corporativos personalizados. Puede personalizar estos menús para que tengan más de un nivel.

  - Proporciona una función de búsqueda de directorio que permite a la persona que llama buscar un nombre en el directorio de la organización.

  - Permite que el autor de la llamada se conecte al teléfono de los miembros de la organización o les deje mensajes.

No existe límite en el número de operadores automáticos de mensajería unificada que se pueden crear. Cada operador automático de mensajería unificada puede admitir un número ilimitado de extensiones. Un operador automático de mensajería unificada puede hacer referencia a un solo plan de marcado de mensajería unificada. Los operadores automáticos de mensajería unificada también pueden hacer referencia o establecer vínculos a otros operadores automáticos de mensajería unificada.

Una llamada entrante recibida desde un número de teléfono externo o una extensión de teléfono interna se pasa entre servidores de Exchange y luego se envía a un operador automático de mensajería unificada. El administrador configura el operador automático de mensajería unificada para que use archivos de voz (.wav) previamente grabados, que se reproducen por teléfono al autor de la llamada para que pueda moverse por el sistema de menús de mensajería unificada. Puede personalizar todos los archivos .wav que se usan al configurar un operador automático de mensajería unificada para satisfacer las necesidades de la organización.

Volver al principio

## Operadores automáticos con varios idiomas

En ciertas situaciones, es necesario proporcionar a las personas que llaman operadores automáticos con varios idiomas. La opción de idioma que está disponible en un operador automático de MU permite configurar el idioma de los mensajes predeterminados del operador automático. Cuando use los mensajes de sistema predeterminados para el operador automático, éste es el idioma que la persona que llama escuchará cuando el operador automático responda a la llamada entrante. Esta configuración de idioma solo afecta a los avisos del sistema predeterminados. Esta configuración de idioma no afecta a los mensajes personalizados configurados de un operador automático.

En el caso de las implementaciones locales e híbridas, al instalar la versión de inglés de los EE. UU., el idioma inglés será el único disponible para configurar operadores automáticos de mensajería unificada. Sin embargo, si instala una versión localizada (por ejemplo, la japonesa), podrá configurar el operador automático que cree de manera que el idioma predeterminado sea el japonés o el inglés de EE. UU. Pueden instalarse paquetes de idioma de mensajería unificada en un servidor de mensajería unificada para que puedan usarse otros idiomas predeterminados en un operador automático.

Por ejemplo, si tiene una empresa en Estados Unidos que necesita un sistema de menús que ofrezca a las personas que llaman opciones en inglés de Estados Unidos, español y francés, primero debe instalar los paquetes de idioma de mensajería unificada que necesite. En este caso, si tiene instalada la versión de inglés de los EE. UU., solo será necesario instalar los paquetes de idioma de mensajería unificada para español y francés. Sin embargo, puesto que un operador automático de UM sólo puede tener configurado un idioma al mismo tiempo, deberá crear cuatro operadores automáticos: un operador automático principal configurado para que use el inglés de EE.UU. y un operador automático para cada idioma adicional: inglés de Estados Unidos, español y francés. A continuación, deberá configurar el operador automático principal para que tenga la navegación de menús o las asignaciones de teclas adecuadas con el fin de tener acceso al resto de operadores automáticos que ha creado para cada idioma. En este ejemplo, el operador automático principal contestará la llamada entrante y la persona que llama escuchará: "Welcome to Contoso, Ltd. For English, press or say 1. For Spanish, press or say 2. For French, press or say 3."


> [!TIP]
> En Exchange UM, los usuarios de Outlook Voice Access autenticados y sin autenticar no pueden buscar usuarios en el directorio con entradas de voz en ningún idioma. No obstante, las personas que realizan llamadas a un operador automático pueden usar entradas de voz en varios idiomas para desplazarse por los menús de operadores automáticos en el directorio.



Volver al principio

## Saludo personalizado durante el horario comercial y el horario no comercial

Después de crear un operador automático de MU, se usará un aviso predeterminado del sistema para el saludo del menú principal en horario no comercial, que escucharán aquellas personas que llamen después del saludo de bienvenida en horario no comercial. Aunque no se deben sustituir ni cambiar los avisos del sistema, es probable que desee personalizar los saludos y avisos del menú utilizados con los operadores automáticos de MU. A menudo, además de configurar un saludo de bienvenida en horario no comercial personalizado, también deseará crear y configurar un mensaje de saludo del menú principal en horario no comercial personalizado. Después de configurar un mensaje de saludo del menú principal en horario no comercial personalizado, debe habilitar las asignaciones de teclas en el operador automático de mensajería unificada para el horario no comercial.

Un mensaje de saludo personalizado del menú principal en horario no comercial es una lista de opciones que oyen las personas que llaman durante el horario no comercial. Para permitir que las personas que llaman puedan oír un mensaje de saludo del menú principal en horario no comercial, primero, debe configurar el horario comercial y no comercial mediante el EAC o el cmdlet **Set-UMAutoAttendant** en el Shell. Por ejemplo, "Ha llamado a Trey Research en horario no comercial. Si tiene una emergencia médica, cuelgue y llame al 911. Si desea dejar un mensaje para alguno de nuestros médicos, presione 1. Si desea dejar un mensaje para alguno de nuestros fisioterapeutas, presione 2. Si desea dejar un mensaje general para alguno de nuestros coordinadores administrativos, presione 3. Si desea hablar con un operador en horario no comercial, presione 0."

De manera predeterminada, al crear un operador automático de mensajería unificada, los saludos o avisos en horario comercial o no comercial no están configurados y no se define ninguna entrada de navegación de menús para los mensajes del menú principal, tanto en horario comercial como en horario no comercial. Para configurar correctamente los saludos y textos personalizados del menú principal en horario no comercial, debe:

1.  Configurar el horario comercial y no comercial en la página **Horario comercial**.

2.  Crear el archivo de saludo que se usará para el saludo de bienvenida en horario no comercial.

3.  Configure el saludo de bienvenida en horario no comercial en la página**Saludos**.

4.  Crear el archivo de saludo que se usará para el saludo de texto del menú principal en horario no comercial.

5.  Configure el saludo de texto del menú principal en horario no comercial en la página **Saludos**.

6.  Habilite la navegación de menús y agregue entradas de navegación de menús en la página **Navegación de menús**.

Volver al principio

## Entradas de navegación de menús

Si usa el saludo de texto predeterminado del menú principal y define una o varias entradas de navegación de menús, el motor de conversión de texto a voz (TTS) de mensajería unificada sintetizará un mensaje de menú principal. Sin embargo, el motor de conversión de texto a voz solo sintetizará un mensaje de menú principal si el saludo predeterminado está configurado y se ha definido al menos una entrada de navegación de menús. El motor de conversión de texto a voz no sintetizará un mensaje de menú principal si usted usa un mensaje predeterminado de menú principal, por ejemplo, "Para el departamento de ventas, presione 1. Para el departamento de soporte, presione 2." Para crear este mensaje de menú principal, tiene que crear dos entradas de navegación de menús: una llamada "Departamento de ventas" y la otra "Departamento de soporte técnico" y, a continuación, configurar la entrada de la asignación de teclas para reproducir un archivo de audio, transferir a un número de extensión o enviar a la persona que llama a otro operador automático.

Cuando configure las entradas de navegación de menús, defina las opciones y operaciones que se realizarán si una persona que llama dice una frase cuando usa un operador automático habilitado para voz o pulsa la tecla en el teclado del teléfono cuando usa un operador automático que no está habilitado para voz. Para configurar las entradas de navegación de menús para un operador automático, debe:

  - Habilitar la navegación de menús en horario comercial.

  - Agregar entradas de navegación de menús.

  - Escribir el nombre de la entrada de navegación de menús.

  - Seleccione una opción de la lista **Cuando se presiona esta tecla** y use el cuadro **Reproducir el siguiente archivo de audio** para descargar el archivo de audio para reproducir.

  - Configurar la acción que desee realizar:
    
      - Transferir a esta extensión
    
      - Transferir a este operador automático de mensajería unificada
    
      - Dejar un mensaje de voz para este usuario
    
      - Anunciar la ubicación de la empresa
    
      - Anunciar el horario comercial

Volver al principio

## Ejemplos de operadores automáticos

Los siguientes ejemplos demuestran cómo puede usar los operadores automáticos de UM con la mensajería unificada:

  - **Ejemplo 1**   En una compañía llamada Contoso, Ltd., los que llamen desde fuera pueden usar tres números de teléfono externos: 425-555-0111 (oficinas corporativas), 425-555-0122 (soporte técnico) y 425-555-0133 (ventas). Los departamentos de Recursos Humanos, Administración y Contabilidad tienen extensiones de teléfono internas y se debe tener acceso a las mismas a través del operador automático de UM de las oficinas corporativas.
    
    Para crear una estructura de operador automático de UM que sea compatible con esta situación, cree y configure tres operadores automáticos de UM que tengan los números de teléfono externos apropiados. Cree otros tres operadores automáticos de UM para cada departamento de las oficinas corporativas. A continuación, configure cada operador automático de mensajería unificada según sus requisitos, tales como el tipo de saludo u otra información de navegación.

  - **Ejemplo 2**   En una compañía llamada Contoso, Ltd., los clientes externos llaman a un número principal de la compañía: 425-555-0100. Cuando una persona llama desde el exterior al número externo, el operador automático de mensajería unificada responde e informa a la persona que llama diciendo: "Bienvenido a Contoso, Ltd. Presione o diga 'uno' para que su llamada se transfiera a la administración corporativa. Presione o diga 'dos' para ser transferido al servicio técnico. Presione o diga 'tres' para que su llamada se transfiera a información corporativa. Presione o diga 'cero' para hablar con el operador." Para crear una estructura de operador automático de UM compatible con esta situación, cree un operador automático de UM que tenga extensiones personalizadas que enruten la llamada al número de extensión apropiado.

Volver al principio

