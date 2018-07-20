---
title: 'Funcionalidad TLS y terminología relacionada: Exchange 2013 Help'
TOCTitle: Funcionalidad TLS y terminología relacionada
ms:assetid: 294ba2a9-892d-4a90-beec-9d298426b5f4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb430753(v=EXCHG.150)
ms:contentKeyID: 52062011
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Funcionalidad TLS y terminología relacionada

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2014-06-18_

Microsoft Exchange Server 2013 ofrece funciones administrativas y otros cambios que mejoran la administración general de la Seguridad de la capa de transporte (TLS). Debe conocer algunas de las características y funciones relacionadas con la TLS para poder usarlas. Algunos términos y conceptos se aplican a más de una característica relacionada con la TLS. En este tema, se ofrece una breve explicación de cada característica para ayudarlo a entender algunas diferencias y la terminología general relacionada con la TLS y el conjunto de características de seguridad de dominio:

  - **Seguridad de la capa de transporte.**La TLS es un protocolo estándar que se usa para proporcionar comunicaciones Web seguras en Internet o en intranets. Permite a los clientes autenticar servidores y, opcionalmente, a los servidores autenticar clientes. También proporciona un canal seguro ya que cifra las comunicaciones. TLS es la versión más reciente del protocolo Nivel de sockets seguros (SSL).

  - **Mutual TLS.**La autenticación Mutual TLS difiere de la TLS, dado que la TLS se implementa habitualmente. Por lo general, cuando se implementa la TLS, sólo se utiliza para proporcionar confidencialidad en forma de cifrado. No se produce autenticación entre en remitente y el destinatario. Además, cuando TLS se implementa, a veces solo se autentica el servidor de recepción. Esta implementación de TLS es típica de la implementación HTTP de la TLS. Esta implementación, donde sólo se autentica el servidor destinatario, es la SSL.
    
    Con la autenticación Mutual TLS, cada servidor comprueba la identidad del otro servidor mediante la validación de un certificado proporcionado por ese otro servidor. En este escenario, donde los mensajes se reciben de dominios externos a través de conexiones comprobadas en un entorno de Exchange 2013, Microsoft Outlook muestra un icono de **Dominio seguro**.

  - **Seguridad de dominio**  Seguridad de dominio es el conjunto de características (como la administración de certificados, la funcionalidad de conectores y el comportamiento del cliente de Outlook) que habilita la TLS mutua como una tecnología administrable y útil. La función Seguridad de dominio no se admite cuando el correo saliente se enruta a través de un servidor de acceso de cliente de Exchange 2013.

  - En la **TLS oportunista**Exchange 2013, la instalación crea un certificado autofirmado. De manera predeterminada, TLS está habilitado. Esto permite a cualquier sistema de envío cifrar la sesión SMTP entrante para Exchange. De forma predeterminada, Exchange 2013 intenta también la TLS para todas las conexiones remotas.

  - **Confianza directa**  De manera predeterminada, todo el tráfico entre servidores de transporte perimetral y servidores de buzones de correo se autentica y cifra. Una vez más, el mecanismo subyacente de autenticación y cifrado es TLS mutua. En lugar de usar la validación X.509, Exchange 2013 usa la confianza directa para autenticar los certificados. La confianza directa implica que la presencia del certificado en Active Directory o Active Directory Lightweight Directory Services (AD LDS) valide dicho certificado. Active Directory se considera un mecanismo de almacenamiento de confianza. Si se usa la confianza directa, da igual que el certificado tenga una firma personal o esté firmado por una entidad de certificación. Al suscribir un servidor de transporte perimetral a la organización Exchange, la suscripción perimetral publica el certificado del servidor de transporte perimetral en Active Directory para que lo validen los servidores de buzones de correo. El servicio Microsoft Exchange EdgeSync actualiza AD LDS con el conjunto de certificados de servidor de buzones de correo para que los valide el servidor de transporte perimetral.

