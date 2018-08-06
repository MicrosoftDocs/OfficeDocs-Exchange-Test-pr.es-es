---
title: 'Interfaz usuario administración certificados Exchange 2013: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Interfaz de usuario de administración de certificados de Exchange 2013
ms:assetid: 8975848d-07f0-4643-9eac-20aece69945f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ984582(v=EXCHG.150)
ms:contentKeyID: 52062044
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Interfaz de usuario de administración de certificados de Exchange 2013

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-04-21_

La administración de certificados en una implementación de Exchange Server es una de las tareas administrativas más importantes. Asegurar que los certificados estén correctamente definidos y configurados es fundamental para suministrar una infraestructura de mensajería segura para la empresa. En Exchange 2010, la Consola de administración de Exchange (EMC) era el método principal de administración de certificados. En Exchange 2013, la función de administración de certificados está suministrada por la Consola de administración de Exchange (EAC), la nueva interfaz de usuario administrativa de Exchange 2013. En Exchange 2013, se hace énfasis en minimizar el número de certificados que un administrador debe administrar, minimizar la interacción que debe tener el administrador con los certificados y permitir la administración de certificados desde una ubicación central.

## Certificados de servidores de acceso de cliente

El servidor de acceso de cliente en Exchange 2013 es un servidor ligero y sin estado que está diseñado para aceptar conexiones entrantes de cliente y servir como proxy de estas con el servidor de buzones correcto. La interfaz de usuario de administración de certificados de Exchange en el servidor de acceso de cliente puede ayudarle con una variedad de tareas, incluida la solicitud de nuevos certificados y la renovación de certificados expirados o a punto de expirar.

## Descripción de la interfaz de usuario de administración de certificados

Puede acceder a la interfaz de usuario de administración de Exchange a través del EAC seleccionando **Servidores** y después **Certificados**. Mediante la interfaz de usuario de administración, puede realizar las siguientes acciones:

  - **Crear un nuevo certificado** Al seleccionar **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") se inicia el Asistente de Nuevo certificado de Exchange.

  - **Editar un certificado existente** Al seleccionar **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar") en un certificado válido, es posible ver la página de propiedades del certificado.

  - **Eliminar un certificado** Al seleccionar **Eliminar**![Eliminar icono](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Eliminar icono"), cuando un certificado se selecciona, se inicia el cuadro de diálogo de confirmación de eliminación.

  - **Realizar acciones adicionales** Al seleccionar **Más opciones**![Icono Más opciones](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icono Más opciones"), es posible exportar o importar un certificado. Si quiere exportar un certificado, el certificado debe ser válido.

## Expiración del certificado

En versiones anteriores de Microsoft Exchange, no se podía ver fácilmente cuando un certificado digital estaba a punto de expirar. En Exchange 2013, el centro de notificaciones muestra advertencias cuando un certificado almacenado en cualquier servidor Acceso de cliente de Exchange 2013 está a punto de expirar.

## Certificados de servidor de buzones

Una diferencia clave entre Exchange 2010 y Exchange 2013 es que los certificados que se usan en el servidor de buzones de Exchange 2013 son certificados autofirmados. Como todos los clientes se conectan a un servidor de buzones de Exchange 2013 mediante un servidor de acceso de cliente de Exchange 2013, los únicos certificados que necesita administrar son los del servidor de acceso de cliente. El servidor de acceso de clientes automáticamente confía el certificado autofirmado en el servidor buzón de correo de modo que los clientes no reciban advertencias acerca de un certificado autofirmado que no es de confianza siempre que el servidor acceso de clientes tenga un certificado no autofirmado de una entidad de certificación (AC) de Windows o un tercero de confianza. No hay herramientas o cmdlets disponibles para administrar certificados autofirmados en el servidor de buzones. Después de que el servidor se ha instalado correctamente, nunca debería tener que preocuparse por los certificados del servidor de buzones.

## Expiración de certificados autofirmados

De manera predeterminada, el certificado autofirmado que está instalado en el servidor de buzones de Exchange 2013 expirará cinco años contados a partir de la fecha de instalación.

## Cmdlets de certificados

Puede usar los siguientes cmdlets para administrar certificados digitales en un servidor de acceso de cliente de Exchange:

  - Import-ExchangeCertificate Este cmdlet se usa para importar certificados a un servidor. Puede importar un certificado firmado de CA (para completar una solicitud de firma de certificado pendiente (CSR)) o un certificado con una clave privada (archivos PKCS \#12, generalmente con una extensión .pfx, anteriormente exportados desde un servidor junto con la clave privada).

  - Remove-ExchangeCertificate Este cmdlet se usa para quitar certificados de un servidor.

  - Enable-ExchangeCertificate Este cmdlet se usa para asignar servicios a un certificado.

  - Get-ExchangeCertificate Este cmdlet se usa para recuperar un certificado de Exchange según diversos criterios.

  - New-ExchangeCertificate Este cmdlet se usa para crear un nuevo certificado autofirmado o una CSR.

