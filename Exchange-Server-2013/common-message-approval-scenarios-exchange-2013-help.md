---
title: 'Escenarios comunes de aprobación de mensajes: Exchange 2013 Help'
TOCTitle: Escenarios comunes de aprobación de mensajes
ms:assetid: 5c13a07e-c21d-4502-a9f9-fb801197e1dd
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd298007(v=EXCHG.150)
ms:contentKeyID: 49895655
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Escenarios comunes de aprobación de mensajes

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2014-09-29_

Su organización puede necesitar aprobar determinados tipos de mensajes para cumplir requisitos legales o de cumplimiento de normas, o para implementar un flujo de trabajo específico. Estos son algunos ejemplos de escenarios comunes que puede configurar mediante Exchange:

  - Ejemplo 1: Evitar aluviones de correo a grupos de distribución grandes

  - Ejemplo 2: Reenviar mensajes al administrador de un remitente para su aprobación

  - Ejemplo 3: Configurar una cadena de aprobación de mensajes

  - Ejemplo 4: Reenviar los mensajes que coinciden con uno de varios criterios

  - Ejemplo 5: Reenviar un mensaje que contenga información confidencial

## Ejemplo 1: Evitar aluviones de correo a grupos de distribución grandes

Para controlar los mensajes a un grupo de distribución grande, puede requerir que un moderador apruebe los mensajes que se envían a ese grupo. Si no hay criterios para la aprobación de los mensajes, la forma más sencilla de hacerlo es configurar el grupo para que requiera la aprobación de mensajes.

En este ejemplo, todos los mensajes en el grupo Todos los empleados deben ser aprobados, salvo si los remitentes son miembros del grupo de distribución llamado Equipo Legal.

![Configuración de aprobación de mensajes para un grupo de distribución](images/Dd298007.77721509-93f9-4a90-8d77-986db2b0acf4(EXCHG.150).png "Configuración de aprobación de mensajes para un grupo de distribución")

Para requerir que se aprueben los mensajes a un grupo de distribución específico, en el Centro de administración de Exchange (EAC), vaya a **Destinatarios** \> **Grupos**, edite el grupo de distribución y, después, seleccione **Aprobación de mensajes**.

## Ejemplo 2: Reenviar mensajes al administrador de un remitente para su aprobación

Estos son algunos de los tipos comunes de mensajes para los que quizás quiera requerir la aprobación del administrador:

  - Mensajes enviados desde un usuario a determinados grupos de distribución o destinatarios

  - Mensajes enviados a usuarios externos o asociados

  - Mensaje enviado entre dos grupos

  - Mensajes enviados con contenido específico, como el nombre de un cliente específico

  - Mensajes enviados por un asistente

Para requerir que un mensaje se envíe a aprobación, cree primero una regla usando la plantilla **Enviar mensajes a un moderador** y seleccione que los mensajes deben enviarse al administrador del remitente, como se muestra en las capturas de pantalla siguientes.

![Usar una plantilla para crear la nueva regla](images/Dd298007.051a5653-1a09-4db4-908f-48b56cc8d13f(EXCHG.150).png "Usar una plantilla para crear la nueva regla")

Después, defina qué mensajes necesitan aprobación.

Este es un ejemplo donde todos los mensajes enviados por un asistente, Íker Arteaga, a destinatarios externos a la organización requieren la aprobación de un administrador.

![Regla que reenvía mensajes al administrador del usuario](images/Dd298007.7f94c22e-b5ba-45a3-9ccd-31996b6c863a(EXCHG.150).png "Regla que reenvía mensajes al administrador del usuario")

Para empezar, vaya a EAC \> **Flujo de correo** \> **Reglas** y cree una nueva regla usando la plantilla **Enviar mensajes a un moderador**.


> [!IMPORTANT]
> Algunas condiciones y acciones, incluido el reenvío al administrador del remitente, están ocultas de forma predeterminada en la página <STRONG>Nueva regla</STRONG>. Para ver todas las condiciones y acciones, seleccione <STRONG>Más opciones</STRONG>.



## Ejemplo 3: Configurar una cadena de aprobación de mensajes

Puede requerir varios niveles de aprobación para los mensajes. Por ejemplo, puede requerir que los mensajes a un cliente específico sean aprobados primero por un administrador de relaciones con los clientes y, después, por un responsable de cumplimiento de las normas, o puede requerir que los informes de gastos sean aprobados por dos niveles de administradores.

Para crear este tipo de aprobación de varios niveles, cree una regla de transporte para cada nivel de aprobación. Cada regla detecta los mismos patrones en los mensajes, de la siguiente manera:

  - La primera regla reenvía el mensaje al primer aprobador. Cuando el primer aprobador acepta el mensaje, el mensaje se pasa automáticamente al aprobador de la segunda regla.

  - Si todos los aprobadores de la cadena seleccionan **Aprobar** cuando reciben la solicitud de aprobación, cuando se completa la última aprobación de la cadena, el mensaje original se envía a los destinatarios previstos.

  - Si todas las personas de la cadena de aprobación seleccionan **Rechazar** al recibir la solicitud de aprobación, el remitente recibe un mensaje de rechazo.

  - Si alguna de las solicitudes de aprobación no se aprueba en el plazo de expiración (2 días para Exchange Online, 5 días para Exchange Server 2013), el remitente recibe un mensaje de expiración.

En el ejemplo siguiente se da por hecho que tiene un cliente llamado Blue Yonder Airlines y que quiere que tanto el administrador de relaciones con los clientes como el responsable de cumplimiento de las normas aprueben todos los mensajes que vayan a este cliente. Crea dos reglas, una para cada aprobador. La primera regla va al aprobador de primer nivel. La segunda regla va al aprobador de segundo nivel.

![Dos reglas utilizadas para dos niveles de aprobación](images/Dd298007.29686c05-eaa0-42b9-86ad-d577f656392c(EXCHG.150).png "Dos reglas utilizadas para dos niveles de aprobación")

La primera regla identifica todos los mensajes que contienen el nombre de la compañía Blue Yonder Airlines en el asunto o en el mensaje, y envía estos mensajes al administrador interno de relaciones con los clientes para Blue Yonder Airlines, Andrés Delgadillo.

![Regla para aprobación de primer nivel](images/Dd298007.e22d1c04-85c5-4227-88e6-b118d5593350(EXCHG.150).png "Regla para aprobación de primer nivel")

La segunda regla envía estos mensajes al responsable de cumplimiento de las normas, Tomás Navarro.

![Regla de aprobación de segundo nivel con los mismos criterios](images/Dd298007.5d888786-8e48-4459-ab86-8a4b9a016d58(EXCHG.150).png "Regla de aprobación de segundo nivel con los mismos criterios")

## Ejemplo 4: Reenviar los mensajes que coinciden con uno de varios criterios

Dentro de una regla de transporte, deben cumplirse todas las condiciones configuradas en la regla para que la regla coincida. Si quiere aplicar las mismas acciones para cualquiera de las condiciones, debe crear una regla independiente para cada una.

Para ello, en la página **Reglas** de EAC, cree una regla para la primera condición. Seleccione la regla, seleccione **Copiar** y cambie las condiciones de la nueva regla para que coincida con la segunda condición.

Tenga cuidado al crear varias reglas con condiciones "O" para no terminar enviando varias veces un mensaje al aprobador. Para evitar este problema, agregue una excepción a la segunda regla para que ignore los mensajes que coincidan con la primera regla.

Por ejemplo, una única regla no puede comprobar si un mensaje contiene "oferta de venta" en el asunto o en el título del archivo adjunto. Para evitar que el mensaje se envíe varias veces al aprobador, si la primera regla comprueba "oferta de venta" en el asunto o en el cuerpo del mensaje, la segunda regla que comprueba "oferta de venta" en el contenido del archivo adjunto necesita una excepción que contenga los criterios de la primera regla.

![Usar una excepción para la segunda regla](images/Dd298007.c39bbdcf-c619-4f84-8922-114ad1da824d(EXCHG.150).png "Usar una excepción para la segunda regla")


> [!NOTE]
> Las excepciones están ocultas de forma predeterminada en la página <STRONG>Nueva regla</STRONG>. Para ver todas las condiciones y acciones, seleccione <STRONG>Más opciones</STRONG>.



## Ejemplo 5: Reenviar un mensaje que contenga información confidencial

Si tiene la característica [Prevención de pérdida de datos](https://docs.microsoft.com/es-es/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention) (DLP), muchos tipos de información confidencial están predefinidos. Con DLP, ve que el mensaje contiene una condición de información confidencial. Tenga o no DLP, puede crear condiciones que identifiquen determinados patrones de información confidencial que sean únicos para su organización.

Este es un ejemplo en el que los mensajes con información confidencial requieren aprobación. En este ejemplo, los mensajes que contienen un número de tarjeta de crédito requieren aprobación.

![Regla que reenvía correo electrónico con información confidencial](images/Dd298007.7ec1ca74-5d20-42ea-a9ee-3a8b25beb7df(EXCHG.150).png "Regla que reenvía correo electrónico con información confidencial")

## Vea también


[Administrar la aprobación de mensajes](https://docs.microsoft.com/es-es/exchange/security-and-compliance/mail-flow-rules/manage-message-approval)

