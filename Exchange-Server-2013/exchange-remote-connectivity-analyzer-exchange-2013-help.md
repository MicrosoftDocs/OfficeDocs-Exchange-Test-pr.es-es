---
title: 'Analizador de conectividad remota de Exchange: Exchange 2013 Help'
TOCTitle: Analizador de conectividad remota de Exchange
ms:assetid: dd26698e-d00c-47f5-a7aa-c3894fe86c75
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ff701693(v=EXCHG.150)
ms:contentKeyID: 49895963
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Analizador de conectividad remota de Exchange

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2014-09-22_

El Analizador de conectividad remota (ExRCA) de MicrosoftExchange le ayuda a asegurarse de que la conectividad para los servidores de Exchange está configurada correctamente. Si tiene problemas, también puede ayudarle a encontrarlos y solucionarlos. El sitio web de ExRCA puede ejecutar pruebas para comprobar MicrosoftExchange ActiveSync, servicios Web Exchange, MicrosoftOutlook y la conectividad del correo electrónico en Internet.

## Pruebas del Analizador de conectividad remota

Puede realizar varias pruebas con el ExRCA. Las siguientes pruebas funcionan en Exchange 2007 y versiones posteriores:

  - Exchange ActiveSync

  - Servicios web de Exchange

  - Outlook

  - Correo electrónico de Internet

## Pruebas de Exchange ActiveSync

Puede ejecutar las siguientes pruebas para Exchange ActiveSync:

  - **Exchange ActiveSync:** esta prueba estimula los pasos que utiliza un dispositivo móvil para conectarse a un servidor de Exchange mediante Exchange ActiveSync.

  - **Detección automática de Exchange ActiveSync:** esta prueba lo guía por los pasos que un dispositivo de Exchange ActiveSync usa para obtener la configuración del servicio Detección automática.

## Pruebas de conectividad de los servicios Web Exchange

Las pruebas de los servicios Web Exchange comprueban la configuración de muchos de los servicios Web Exchange. Puede ejecutar las siguientes pruebas para los servicios Web Exchange:

  - **Sincronización, notificación, disponibilidad y respuestas automáticas:** estas pruebas lo guían a través de muchas tareas básicas de los servicios Web Exchange para confirmar que están funcionando. Esto resulta útil para los administradores de TI que desean solucionar problemas de acceso externo mediante Entourage EWS u otros clientes de servicios web.

  - **Acceso de cuenta de servicio (desarrolladores):** esta prueba comprueba la disponibilidad de una cuenta de servicio para acceder a un buzón especificado, crear y eliminar elementos en él, y tener acceso a este a través de la suplantación de Exchange. Esta prueba la utilizan principalmente los desarrolladores de aplicaciones para probar la capacidad de acceso a buzones con credenciales alternativas.

## Pruebas de conectividad de Microsoft Office Outlook

Puede ejecutar las siguientes pruebas para la conectividad de Outlook:

  - **Outlook Anywhere (RPC sobre HTTP):** esta prueba lo guía por los pasos que Outlook usa para conectarse a través de Outlook Anywhere (RPC sobre HTTP).

  - **Detección automática de Outlook:** esta prueba lo guía por los pasos que Outlook usa para obtener la configuración del servicio Detección automática. Esta prueba no se conecta realmente a un buzón.

## Pruebas de correo electrónico de Internet

Puede ejecutar las siguientes pruebas para el correo electrónico de Internet:

  - **Correo** **SMTP entrante:** esta prueba lo guía por los pasos que un servidor de correo de Internet usa para enviar correo SMTP entrante al dominio.

  - **Correo SMTP saliente:** esta prueba comprueba que la dirección IP saliente cumpla determinados requisitos. Esto incluye comprobaciones de DNS inversa, id. de remitente y RBL.

  - **Correo electrónico POP:** esta prueba lo guía por los pasos que un cliente de correo electrónico usa para conectarse a un buzón mediante POP3.

  - **Correo electrónico IMAP:** esta prueba lo guía por los pasos que un cliente de correo electrónico usa para conectarse a un buzón mediante IMAP.

