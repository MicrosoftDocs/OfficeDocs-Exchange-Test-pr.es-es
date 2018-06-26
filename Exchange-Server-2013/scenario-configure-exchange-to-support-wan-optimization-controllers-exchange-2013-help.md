---
title: 'Caso: Configurar Exchange para que sea compatible con los controladores de optimización de la WAN: Exchange 2013 Help'
TOCTitle: 'Caso: Configurar Exchange para que sea compatible con los controladores de optimización de la WAN'
ms:assetid: 1f407698-0b71-45a3-867a-640ccf7351da
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee633456(v=EXCHG.150)
ms:contentKeyID: 52062010
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Caso: Configurar Exchange para que sea compatible con los controladores de optimización de la WAN

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2012-09-28_

En Microsoft Exchange Server 2013, el cifrado Seguridad de la capa de transporte (TLS) es obligatorio para todas las comunicaciones SMTP del servicio de transporte entre servidores de buzones. Esto aumenta la seguridad general de la comunicación del servicio de transporte entre los servidores de buzones. No obstante, en ciertas topologías en las que se usan controladores de optimización de WAN (WOC), el cifrado TLS del tráfico SMTP puede ser indeseable. Puede deshabilitar TLS para la comunicación del servicio de transporte entre los servidores de buzones para estos escenarios concretos.

Tenga en cuenta la topología en la siguiente ilustración. El supuesto para esta topología de cuatro sitios es que los sitios de las dos oficinas centrales y la sucursal 2 están bien conectadas, mientras que la conexión entre el sitio de la oficina central 1 y la sucursal 1 es a través de un vínculo WAN. La compañía ha instalado dispositivos WOC en este vínculo para comprimir y optimizar el tráfico a través de WAN.

**Topología de red de muestra con dispositivos WOC**

![Topología de muestras con optimizadores WAN](images/Ee633456.52876869-52f1-4c0f-85b2-7a850643e8a1(EXCHG.150).gif "Topología de muestras con optimizadores WAN")

En esta topología, como Exchange 2013 usa el cifrado TLS para la comunicación entre servidores de buzones, el tráfico SMTP que analiza el vínculo WAN no puede comprimirse. Lo ideal es que todo el tráfico SMTP que analizan el vínculo WAN sean SMTP no cifrado y que se mantenga la seguridad TLS dentro de sitios bien conectados. Exchange 2013 le da opción de deshabilitar el cifrado TLS para el tráfico transmitido entre sitios configurando los conectores de recepción. Al usar esta función en Exchange 2013, puede configurar una excepción para el tráfico SMTP entre el sitio de la oficina central 1 y la sucursal 1, tal como aparece en la imagen siguiente.

**Flujo de mensaje lógico preferido**

![Flujo lógico de mensajes preferido](images/Ee633456.e0fe62fa-1bad-4d43-9eaf-205a9b8d07e1(EXCHG.150).gif "Flujo lógico de mensajes preferido")

La configuración recomendada es limitar el tráfico SMTP no cifrado solamente a los mensajes que pasan a través del vínculo WAN. Por tanto, la comunicación del servicio de transporte entre sitios entre los servidores de buzones de todos los sitios, así como toda la comunicación del servicio de transporte de sitio cruzado entre los servidores de buzones que no incluyan la sucursal 1 debe estar cifradas por TSL.

Para conseguir este resultado, debe hacer las acciones siguientes, en el orden especificado, en cada servidor de buzones de los sitios que contienen los dispositivos WOC (el sitio de la oficina central 1 y la sucursal 1 en la topología de muestra):

1.  Habilite la autenticación degradada de Exchange Server.

2.  Cree un conector de recepción dedicado para administrar el tráfico a través de la conexión que contiene dispositivos WOC.
    
    1.  Configure la propiedad del intervalo de direcciones IP remotas del conector de recepción dedicado a los intervalos de direcciones IP de los servidores de buzones del sitio de Active Directory remoto.
    
    2.  Deshabilite TLS en el conector de recepción dedicado.

Además, deberá realizar las siguientes acciones para garantizar que todo el tráfico SMTP transmitido a través de WAN lo administren los conectores de recepción dedicados que ha creado:

  - Configure los sitios de Active Directory que participarán en la comunicación que no es TLS como sitios de concentradores para forzar que todos los mensajes fluyan a través de los conectores de recepción dedicados (el sitio de la oficina central 1 y la sucursal 1 de la topología de muestra).

  - Compruebe que los costes de vínculo de sitio IP de Active Directory estén configurados de tal forma que garanticen que la ruta de enrutamiento de menor coste para su sitio remoto (la sucursal 1 en la topología de muestra) vaya a través del vínculo de red que tiene los dispositivos WOC. Asigne un coste específico de Exchange a los vínculos de sitio de Active Directory como convenga.

En la siguiente sección se da información general sobre estos pasos. Para leer instrucciones paso a paso sobre cómo configurar la organización para este escenario, vea [Deshabilitar TLS entre sitios de Active Directory](disable-tls-between-active-directory-sites-exchange-2013-help.md).

**Contenido**

Degradar la autenticación a través de conexiones con TLS deshabilitada

Crear y configurar conectores de recepción dedicados

Configurar sitios de concentradores

Configurar los costes de vínculo de sitio de Active Directory específico de Exchange

## Degradar la autenticación a través de conexiones con TLS deshabilitada

La autenticación Kerberos se usa con el cifrado TLS en Exchange. Al deshabilitar TLS en la comunicación del servicio de transporte entre los servidores de buzones, deberá usar otra forma de autenticación. Cuando Exchange 2013 se comunica con otros servidores que ejecutan Exchange y que no son compatibles con **X-ANONYMOUSTLS**, se degrada para usar la autenticación Generic Security Services Application Programming Interface (GSSAPI). Todas las comunicaciones del servicio de transporte entre los servidores de buzones de Exchange 2013 usan **X-ANONYMOUSTLS**. Al configurar el servicio de transporte en su servidor de buzones para usar la autenticación degradada de Exchange Server, en realidad está habilitando la autenticación GSSAPI para la comunicación del servicio de transporte con otros servidores de buzones de Exchange 2013.

Volver al principio

## Crear y configurar conectores de recepción dedicados

Debe crear conectores de recepción que solamente sean responsables de manejar el tráfico cifrado que no sea TLS. Al usar conectores de recepción diferentes para este propósito se asegura de que todo el tráfico que no pase a través del vínculo WAN continúe protegido por el cifrado TLS.

Para restringir los conectores de recepción dedicados a únicamente el tráfico a través de la WAN, hay que configurar la propiedad de intervalo de direcciones IP remotas. Exchange siempre usa el conector con el intervalo de direcciones IP remotas más específico. Por lo tanto, son preferibles estos conectores nuevos en lugar del conector de recepción predeterminado configurado para recibir mensajes desde cualquier parte.

Volviendo a la topología de muestra, suponga que la subred de clase C, 10.0.1.0/24, se usa para el sitio de la oficina central 1 y que 10.0.2.0/24 se usa para la sucursal 1. Para preparar la deshabilitación de TLS entre estos dos sitios, debe:

1.  Cree un conector de recepción denominado WAN en cada servidor de buzones en el sitio de la oficina central 1 y la sucursal 1.

2.  Configure el intervalo de direcciones IP remotas de 10.0.2.0/24 en cada conector de recepción dedicado del sitio de la oficina central 1.

3.  Configure el intervalo de direcciones IP remotas de 10.0.2.0/24 en cada conector de recepción dedicado de la sucursal 1.

4.  Deshabilite TLS en todos los conectores de recepción dedicados.

El resultado aparece en la imagen siguiente (con la propiedad de intervalo de direcciones IP remotas de los conectores de recepción denominados WAN en paréntesis). Solo aparece un servidor de buzones en la sucursal 1; la sucursal 2 se omite para que se vea más claramente.

**Configuración del conector de recepción**

![Configuración del conector de recepción](images/Ee633456.1821b3db-1f7a-4ae7-afbc-5c99e117f976(EXCHG.150).gif "Configuración del conector de recepción")

Volver al principio

## Configurar sitios de concentradores

De forma predeterminada, el servidor de buzones de Exchange 2013 intentará una conexión directa con el servidor de buzones más próximo al destino final de un mensaje concreto. En la topología de muestra, si un usuario de la sucursal 2 envía un mensaje a un usuario de la oficina central 1, el servidor de buzones de la sucursal 2 se conectará con el servidor de buzones de la sucursal 1 directamente para entregar ese mensaje. Dicha conexión se cifrará y por lo tanto no será deseada en la topología específica. Para que estos mensajes pasen a través de los servidores de buzones del sitio de la oficina central 1, de modo que garanticen que no están cifrados mientras están en tránsito hacia el vínculo WAN, el sitio de la oficina central 1 y la sucursal 1 deben estar configurados como sitios de concentradores. En resumen, cualquier sitio donde tenga un servidor de buzones con un conector de recepción con TLS deshabilitado debe estar configurado como sitio de concentradores, de modo que pueda forzar que los servidores de otros sitios redirijan el tráfico a través de ese sitio. Para obtener más información, consulte [Configuración de enrutamiento de correo de Exchange en Active Directory](configure-exchange-mail-routing-settings-in-active-directory-exchange-2013-help.md).

Volver al principio

## Configurar los costes de vínculo de sitio de Active Directory específico de Exchange

Configurar los sitios de concentradores solamente no es suficiente para garantizar que el tráfico no sea cifrado en el vínculo WAN. Esto sucede porque Exchange enrutará los mensajes a través de los sitios de concentradores únicamente si los sitios están en la ruta de enrutamiento de menor coste. Por ejemplo, supongamos que los costes de vínculo de sitio IP de nuestra topología de muestra están configurados en Active Directory tal como aparece en la imagen siguiente (el sitio de la oficina central 2 se omite para mayor claridad).

**Costos de los vínculos a sitios IP de la topología de muestra**

![Costos de vínculos del sitio IP para topología de muestras](images/Ee633456.099deb15-795a-417a-b6aa-925b3bedf8b4(EXCHG.150).gif "Costos de vínculos del sitio IP para topología de muestras")

En este caso, la ruta de la sucursal 2 a la sucursal 1 que pasa por el sitio de concentradores tiene un costo total de 12 (6+6), mientras que el costo de la ruta directa es 10. Por lo tanto, ninguno de los mensajes de la sucursal 2 a la sucursal 1 pasará por el sitio de la oficina central 1 y todo el tráfico será cifrado para TLS.

Para evitar este problema, debe designar un coste específico de Exchange superior a 12 para el vínculo de sitio IP entre la sucursal 2 y la sucursal 1, tal como aparece en la imagen siguiente. Esto asegurará que todos los mensajes pasen a través del canal no cifrado entre el sitio de la oficina central 1 y la sucursal 1.

**Topología de muestra configurada con los costos de los vínculos a sitios IP específicos de Exchange**

![Topología de muestras con costos de Exchange](images/Ee633456.cd036fe0-c37d-479e-a4c1-235e17e90ca7(EXCHG.150).gif "Topología de muestras con costos de Exchange")

Para obtener más información, consulte [Configuración de enrutamiento de correo de Exchange en Active Directory](configure-exchange-mail-routing-settings-in-active-directory-exchange-2013-help.md).

Volver al principio

