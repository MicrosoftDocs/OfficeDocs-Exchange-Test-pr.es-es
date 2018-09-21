---
title: 'Usar Telnet para probar la comunicación SMTP: Exchange 2013 Help'
TOCTitle: Usar Telnet para probar la comunicación SMTP
ms:assetid: 8a5f6715-baa4-48dd-8600-02c6b3d1aa9d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb123686(v=EXCHG.150)
ms:contentKeyID: 52062041
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Usar Telnet para probar la comunicación SMTP

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

En este tema se explica cómo utilizar Telnet para probar la comunicación SMTP (protocolo simple de transferencia de correo) entre servidores de mensajería. De forma predeterminada, SMTP escucha en el puerto 25. Si usa Telnet en el puerto 25, puede introducir los comandos SMTP que se usan para conectarse a un servidor SMTP y enviar un mensaje exactamente del mismo modo que si la sesión de Telnet fuera un servidor de mensajería SMTP. Puede ver el éxito o error de cada paso del proceso de conexión y envío de mensajes.

A continuación se describen los escenarios donde se recomienda utilizar Telnet para probar la comunicación SMTP a o desde los servidores de transporte que existen en la organización de Microsoft Exchange:

  - Conéctese al servidor Exchange accesible desde Internet de su organización desde un host ubicado fuera de la red perimetral y envíe un mensaje de prueba.

  - Conéctese a un servidor de mensajería remoto desde el servidor Exchange accesible desde Internet de su organización y envíe un mensaje de prueba.

El procedimiento incluido en este tema muestra cómo usar el cliente Telnet, que es un componente incluido con Microsoft Windows. Algunos clientes Telnet de terceros pueden requerir una sintaxis distinta a la del componente Telnet de Windows.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 30 minutos

  - Los permisos de Exchange no se aplican a los procedimientos de este tema. Estos procedimientos se realizan en el sistema operativo de Exchange Server o de un ordenador cliente.

  - Es preferible realizar los procedimientos de este tema conectándose a y desde servidores con acceso a Internet que permitan conexiones anónimas. La transmisión de mensajes entre servidores Exchange internos está cifrada y autenticada. Para poder conectarse por Telnet al servicio de Transporte de concentradores en un servidor de buzones de correo, deberá crear un conector de recepción que esté configurado para admitir accesos anónimos o autenticación básica para recibir mensajes. Si el conector admite autenticación básica, necesitará una utilidad para convertir las cadenas de texto que se utilizan para el nombre de usuario y la contraseña a formato Base64. Como el nombre de usuario y la contraseña se distinguen fácilmente cuando se utiliza la autenticación básica, no se recomienda este tipo de autenticación sin cifrado.

  - Si se conecta a un servidor de mensajería remoto, es recomendable que siga los procedimientos de este tema en el servidor Exchange con acceso a Internet. De este modo evitará que el mensaje de prueba sea rechazado por los servidores de mensajería remotos configurados para validar la dirección IP de origen, el nombre de dominio del sistema de nombres de dominio (DNS) correspondiente y la dirección IP de búsqueda inversa de cualquier host de Internet que intenta enviar un mensaje al servidor.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Cómo realiza esto?

## Paso 1: Instalar el cliente de Telnet en Windows

De forma predeterminada, el cliente de Telnet no está instalado en la mayoría de las versiones de cliente o servidor de los sistemas operativos Microsoft Windows. Para instalarlo, vea [Instalación del cliente Telnet](https://go.microsoft.com/fwlink/p/?linkid=179054).

## Paso 2: Usar Nslookup para encontrar el FQDN o la dirección IP en el registro MX del servidor SMTP remoto

Para conectarse a un servidor SMTP de destino mediante Telnet en el puerto 25, debe usar el nombre de dominio completo (FQDN) o la dirección IP del servidor SMTP. Si no conoce el FQDN o la dirección IP, el modo más sencillo de buscar esta información es mediante la herramienta de línea de comandos Nslookup, que permite buscar el registro MX del dominio de destino.

1.  En un símbolo del sistema, escriba **nslookup** y presione ENTRAR. Este comando abre la sesión de Nslookup.

2.  Escriba **set type=mx** y, a continuación, presione ENTRAR.

3.  Escriba **set timeout=20** y, a continuación, presione ENTRAR. De forma predeterminada, los servidores DNS de Windows tienen un límite de tiempo de espera de DNS recurrente de 15 segundos.

4.  Escriba el nombre del dominio cuyo registro MX desea buscar. Por ejemplo, para buscar el registro MX del dominio fabrikam.com, escriba **fabrikam.com.** y, a continuación, presione ENTRAR.
    

    > [!NOTE]
    > El punto final (&nbsp;<STRONG>.</STRONG>&nbsp;) indica un FQDN. El uso del punto impide la adición accidental de cualquier sufijo de DNS predeterminado configurado para la red al nombre de dominio.

    
    El resultado del comando será similar al siguiente:
    
        fabrikam.com mx preference=10, mail exchanger = mail1.fabrikam.com
        fabrikam.com mx preference=20, mail exchanger = mail2.fabrikam.com
        mail1.fabrikam.com internet address = 192.168.1.10
        mail2 fabrikam.com internet address = 192.168.1.20
    
    Puede utilizar cualquier nombre de host o dirección IP asociados a los registros MX como el servidor SMTP de destino. Un valor de preferencia inferior indica un servidor SMTP preferido. Puede utilizar varios registros MX y diferentes valores de preferencia para el equilibrio de carga y la tolerancia a errores.

5.  Cuando esté preparado para finalizar la sesión de Nslookup, escriba **exit** y, a continuación, presione ENTRAR.


> [!NOTE]
> Las restricciones de proxy de Internet o firewall impuestas en la red interna de su organización pueden impedir el uso de la herramienta Nslookup para realizar consultas en servidores DNS públicos de Internet.



## Paso 3: Usar Telnet en el puerto 25 para probar la comunicación de SMTP

En este ejemplo, se utilizan los siguientes valores:

  - **Servidor SMTP de destino**   mail1.fabrikam.com

  - **Dominio de origen**   contoso.com

  - **Dirección de correo electrónico del remitente**   chris@contoso.com

  - **Dirección de correo electrónico del destinatario**   kate@fabrikam.com

  - **Asunto del mensaje**   Prueba de Contoso

  - **Cuerpo del mensaje**   Éste es un mensaje de prueba


> [!NOTE]
> <UL>
> <LI>
> <P>Los comandos del cliente Telnet no distinguen entre mayúsculas y minúsculas. Para mayor claridad, se ponen en mayúsculas los verbos del comando SMTP.</P>
> <LI>
> <P>No es posible utilizar la tecla de retroceso una vez se haya conectado al servidor SMTP de destino en la sesión de Telnet. Si comete un error al escribir un comando SMTP, debe presionar la tecla ENTRAR y volver a escribir el comando. Los comandos SMTP no reconocidos o errores de sintaxis tienen como resultado un mensaje de error similar al siguiente:</P><PRE><CODE>500 5.3.3 Unrecognized command</CODE></PRE></LI></UL>



1.  En un símbolo del sistema, escriba **telnet** y presione ENTRAR. Este comando abre la sesión de Telnet.

2.  Escriba **set localecho** y, a continuación, presione ENTRAR. Este comando opcional le permite ver los caracteres conforme los escribe. Es posible que sea necesaria esta configuración en algunos servidores SMTP.

3.  Tipo **set logfile***\<filename\>*. Este comando opcional permite registrar la sesión de Telnet en el archivo de registro especificado. Si sólo especifica un nombre de archivo, la ubicación del archivo de registro es el directorio de trabajo actual. Si especifica una ruta de acceso y un nombre de archivo, la ruta debe encontrarse en el equipo local. Tanto la ruta como el nombre de archivo que especifique deben indicarse en formato Microsoft DOS 8.3. La ruta de acceso que especifique debe existir. Si especifica un archivo de registro que no existe, éste se creará.

4.  Escriba **open mail1.fabrikam.com 25** y, a continuación, presione ENTRAR.

5.  Escriba **EHLO contoso.com** y, a continuación, presione ENTRAR.

6.  Escriba **MAIL FROM:chris@contoso.com** y, a continuación, presione ENTRAR.

7.  Escriba **RCPT TO:kate@fabrikam.com NOTIFY=success,failure** y, a continuación, presione ENTRAR. El comando NOTIFY opcional define los mensajes particulares de notificación de estado de entrega (DSN) que el servidor SMTP de destino debe proporcionar al remitente. Los mensajes de DSN se definen en RFC 1891. En este caso, usted está solicitando un mensaje de DSN para la entrega de mensajes correcta o errónea.

8.  Escriba **DATA** y, a continuación, presione ENTRAR. Recibirá una respuesta similar a la siguiente:
    
    ```powershell
354 Start mail input; end with <CLRF>.<CLRF>
```

9.  Escriba**Asunto: Prueba de Contoso** y, a continuación, presione ENTRAR.

10. Presione ENTRAR. RFC 2822 requiere una línea en blanco entre el campo de encabezado de `Subject:` y el cuerpo del mensaje.

11. Escriba **Éste es un mensaje de prueba** y, a continuación, presione ENTRAR.

12. Presione ENTRAR, escriba un punto ( **.**) y, a continuación, presione ENTRAR. Recibirá una respuesta similar a la siguiente:
    
    ```powershell
250 2.6.0 <GUID> Queued mail for delivery
```

13. Para desconectarse del servidor SMTP de destino, escriba **QUIT** y, a continuación, presione ENTRAR. Recibirá una respuesta similar a la siguiente:
    
    ```powershell
221 2.0.0 Service closing transmission channel
```

14. Para cerrar la sesión de Telnet, escriba **quit** y, a continuación, presione ENTRAR.

## Paso 4: Evaluar los resultados de la sesión de Telnet

En esta sección, se proporciona información sobre las respuestas que pueden proporcionarse a los comandos siguientes, que se usaron en el ejemplo anterior.

  - Abrir correo1.fabrikam.com 25

  - EHLO contoso.com

  - MAIL FROM:chris@contoso.com

  - RCPT TO:kate@fabrikam.com NOTIFY=success,failure
    

    > [!NOTE]
    > Los códigos de repuesta SMTP de 3 dígitos definidos en RFC&nbsp;2821 son los mismos para todos los servidores de mensajería SMTP. Las descripciones de texto pueden diferir ligeramente en algunos servidores de mensajería SMTP.



## Open mail1.fabrikam.com 25

**Respuesta correcta**   `220 mail1.fabrikam.com Microsoft ESMTP MAIL Service ready at <day-date-time>`

**Respuesta de error**   `Connecting to mail1.fabrikam.com...Could not open connection to the host, on port 25: Connect failed`

**Posibles motivos del error**

  - El servicio SMTP de destino no está disponible.

  - Existen restricciones en el firewall de destino.

  - Existen restricciones en el firewall de origen.

  - Se especificó una dirección IP o un FQDN incorrecto para el servidor SMTP de destino.

  - Se especificó un número de puerto incorrecto.

## EHLO contoso.com

**Respuesta correcta**   `250 mail1.fabrikam.com Hello [<sourceIPaddress>]`

**Respuesta de error**   `501 5.5.4 Invalid domain name`

**Posibles motivos del error**   Existen caracteres no válidos en el nombre de dominio. Asimismo, también pueden existir restricciones de conexión en el servidor SMTP de destino.


> [!NOTE]
> EHLO es el verbo de Protocolo simple extendido de transferencia de mensajes (ESMTP) definido en RFC&nbsp;2821. Los servidores ESMTP pueden anunciar sus capacidades durante la conexión inicial. Estas capacidades incluyen el tamaño de mensaje máximo aceptado y los métodos de autenticación admitidos. HELO es el verbo SMTP más antiguo definido en RFC&nbsp;821. La mayoría de los servidores de mensajería SMTP admiten ESMTP y EHLO.



## MAIL FROM:chris@contoso.com

**Respuesta correcta**   `250 2.1.0 Sender OK`

**Respuesta de error**   `550 5.1.7 Invalid address`

**Posibles motivos del error**   Hay un error de sintaxis en la dirección de correo electrónico del remitente.

**Respuesta de error**   `530 5.7.1 Client was not authenticated`

**Posibles motivos del error**   El servidor de destino no acepta envíos de mensajes anónimos. Recibe este error si intenta utilizar Telnet para enviar un mensaje directamente a un servidor de transporte de concentradores.

## RCPT TO:kate@fabrikam.com NOTIFY=success,failure

**Respuesta correcta**   `250 2.1.5 Recipient OK`

**Respuesta de error**   `550 5.1.1 User unknown`

**Posibles motivos del error**   El destinatario especificado no existe en la organización.

