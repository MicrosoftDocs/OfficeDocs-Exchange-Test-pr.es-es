---
title: 'Outlook en cualquier lugar: Exchange 2013 Help'
TOCTitle: Outlook en cualquier lugar
ms:assetid: 9026d461-ec6a-4ef5-ba9d-de33030858f3
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb123741(v=EXCHG.150)
ms:contentKeyID: 48268414
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook en cualquier lugar

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

En Microsoft Exchange Server 2013, la característica Outlook Anywhere, anteriormente conocida como RPC mediante HTTP, permite a los clientes que usan MicrosoftOutlook 2013, Outlook 2010 o Outlook 2007 conectarse a sus servidores de Exchange desde fuera de la red corporativa o por Internet por medio del componente de red RPC mediante HTTP de Windows. Este tema describe la función Outlook Anywhere y enumera las ventajas de utilizar Outlook Anywhere.

**Contenido**

Outlook Anywhere y Exchange 2013

Ventajas del uso de Outlook Anywhere

Implementar Outlook Anywhere

Administrar Outlook Anywhere

Coexistencia de Outlook en cualquier lugar

Prueba de conectividad de Outlook Anywhere

## Outlook Anywhere y Exchange 2013

El componente RPC mediante el HTTP Proxy de Windows, que los cliente de Outlook Anywhere usan para conectarse, engloba llamadas a procedimiento remoto (RPC) con un nivel HTTP. Esto permite que el tráfico atraviese los firewalls de red sin necesidad de abrir puertos RPC. En Exchange 2013, esta característica está habilitada de forma predeterminada, porque Exchange 2013 no permite la conectividad RPC directa.

## Ventajas del uso de Outlook Anywhere

Outlook Anywhere ofrece los siguientes beneficios a los clientes que usan Outlook 2013, Outlook 2010 o Outlook 2007 para obtener acceso a la infraestructura de mensajería de Exchange:

  - Los usuarios tienen acceso remoto a los servidores de Exchange desde Internet.

  - Puede usar la misma dirección URL y el mismo espacio de nombres que usa para Outlook Web App y Microsoft Exchange ActiveSync.

  - Puede usar el mismo certificado de servidor de Capa de sockets seguros (SSL) que usa tanto para Outlook Web App como para Exchange ActiveSync.

  - Las solicitudes no autenticadas de Outlook no pueden tener acceso a los servidores de Exchange.

  - No es necesario usar una red privada virtual (VPN) para tener acceso a los servidores de Exchange a través de Internet.

  - Si ya usa Outlook Web App con SSL o Exchange ActiveSync con SSL, no es necesario abrir ningún puerto adicional desde Internet.

  - Puede comprobar la conectividad de cliente de un extremo a otro para Outlook Anywhere y las conexiones basadas en TCP mediante el cmdlet **Test-OutlookConnectivity**.

## Implementar Outlook Anywhere

En Exchange 2013, Outlook Anywhere está habilitado de forma predeterminada dado que toda la conectividad de Outlook tiene lugar mediante Outlook Anywhere. La única tarea que debe realizar luego de la implementación para usar de forma correcta Outlook Anywhere es instalar un certificado válido de SSL en su servidor de acceso de cliente. Los servidores de buzón de correo de su organización solo requieren el certificado de SSL autofirmado predeterminado.

## Administrar Outlook Anywhere

Puede administrar Outlook en cualquier lugar mediante el uso del Centro de administración de Exchange o el Shell de administración de Exchange.

## Coexistencia de Outlook en cualquier lugar

Si planea instalar Exchange 2013 en un escenario donde coexistan versiones anteriores de Exchange Server, puede seguir teniendo clientes de Outlook 2003 en su organización. Outlook 2003 no es un cliente compatible con Exchange 2013.

Antes de mover el espacio de nombres a Exchange 2013, debe asegurarse de que todos los clientes de Outlook se han actualizado a la versión mínima compatible. Para realizar una conexión de Outlook en cualquier lugar con Exchange 2013 es necesario Outlook 2007 o superior, incluso si el buzón de destino sigue estando en Exchange 2007 o Exchange 2010.

Si actualmente está usando Outlook en cualquier lugar en sus entornos de Exchange 2007 o 2010, para permitir a su servidor de acceso de cliente de Exchange 2013 actuar como proxy para las conexiones a sus servidores de Exchange 2007 o 2010, debe habilitar y configurar Outlook en cualquier lugar en todos los servidores CAS de Exchange 2007 o 2010 de su organización. En cambio, si no está usando en estos momentos Outlook en cualquier lugar en su entorno de Exchange 2007 o 2010, y no quiere empezar a usarlo, no necesita habilitar Outlook en cualquier lugar en el entorno heredado. Para obtener instrucciones sobre cómo habilitar Outlook en cualquier lugar en los servidores de acceso de cliente donde se ejecuta Exchange Server 2007, consulte [Cómo habilitar Outlook en cualquier lugar](https://go.microsoft.com/fwlink/p/?linkid=510497). Para obtener instrucciones sobre cómo habilitar Outlook en cualquier lugar en los servidores de acceso de cliente donde se ejecuta Exchange Server 2010, consulte [Habilitar Outlook en cualquier lugar](https://go.microsoft.com/fwlink/p/?linkid=510502).

Asegúrese de elegir NTLM para la autenticación de IIS cuando habilita Outlook en cualquier lugar en el servidor de acceso de cliente.

Por último, configure el nombre de host externo de Outlook en cualquier lugar para que apunte al nombre de host de Outlook en cualquier lugar de Exchange 2013. Para obtener instrucciones para Exchange Server 2007, consulte [Cómo configurar un nombre de host externo para Outlook en cualquier lugar](https://go.microsoft.com/fwlink/p/?linkid=510530). Para obtener instrucciones para Exchange Server 2010, consulte [Configurar un nombre de host externo para Outlook en cualquier lugar](https://go.microsoft.com/fwlink/p/?linkid=510531).

## Prueba de conectividad de Outlook Anywhere

Puede probar la conectividad de Outlook de cliente de un extremo al otro mediante una de las acciones siguientes:

  - Ejecutar el cmdlet **Test-OutlookConnectivity**. El cmdlet prueba las conexiones de Outlook Anywhere (RPC a través de HTTP). Si se produce un error en la prueba del cmdlet, el resultado muestra el paso en el que se produjo el error. Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Test-OutlookConnectivity](https://technet.microsoft.com/es-es/library/dd638082\(v=exchg.150\)).

  - Ejecutar la prueba de conectividad de Outlook Anywhere mediante el Analizador de conectividad remota de Exchange (ExRCA). Cuando ejecuta esta prueba, obtiene un resumen detallado que muestra dónde se produjo el error en la prueba y qué pasos puede tomar para corregir los problemas. Para obtener más información, consulte [Analizador de conectividad remota de Exchange](exchange-remote-connectivity-analyzer-exchange-2013-help.md).

Las dos pruebas intentan iniciar sesión a través de Outlook Anywhere después de obtener la configuración de servidor del servicio Detección automática. La comprobación de un extremo al otro incluye lo siguiente:

  - Prueba de conectividad de detección automática

  - Validación de DNS

  - Validación de certificados (si el nombre del certificado coincide con el sitio web, si el certificado expiró y si es de confianza)

  - Comprobación de que el firewall esté configurado correctamente (ExRCA comprueba toda la configuración del firewall. El cmdlet prueba la configuración del firewall de Windows.)

  - Confirmación de la conectividad de cliente mediante el inicio de sesión en el buzón de correo del usuario

