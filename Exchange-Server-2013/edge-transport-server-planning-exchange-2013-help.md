---
title: 'Planeación de servidores de transporte perimetral: Exchange 2013 Help'
TOCTitle: Planeación de servidores de transporte perimetral
ms:assetid: 3d34de82-58a5-4b30-9978-7d330102eb92
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn641596(v=EXCHG.150)
ms:contentKeyID: 61545100
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Planeación de servidores de transporte perimetral

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-04-07_

El servidor de transporte perimetral se ha introducido de nuevo en Exchange Service Pack 1. El servidor de transporte perimetral proporciona una protección mejorada contra el correo no deseado para la organización de Exchange. El servidor de transporte perimetral, además, aplica directivas a los mensajes que se envían de unas organizaciones a otras. Este rol de servidor se implementa en la red perimetral y fuera del bosque de Active Directory. Los servidores de transporte perimetral no tienen acceso directo a Active Directory para configuración e información de destinatarios de la misma forma que los servidores de acceso de cliente. El servidor de transporte perimetral usa los Servicios de directorio ligero de Active Directory (AD LDS) para almacenar localmente información de configuración y destinatarios.

Puede agregar un servidor de transporte perimetral a una organización existente de Exchange 2013. Tampoco hay que llevar a cabo ninguna preparación adicional de Active Directory al instalar el servidor Transporte perimetral.


> [!NOTE]
> Si va a agregar un servidor de transporte perimetral a una organización existente de Exchange 2010 o Exchange 2007, tendrá que instalar actualizaciones acumulativas específicas en los servidores heredados antes de instalar el servidor de transporte perimetral de Exchange&nbsp;2013. Para más información, vea <A href="exchange-2013-system-requirements-exchange-2013-help.md">Requisitos del sistema para Exchange&nbsp;2013</A>.



Al planear la implementación de servidores Transporte perimetral, debe tener en cuenta lo siguiente:

  - **Capacidad del servidor**   Al planear la capacidad del servidor hay que planificar cómo se realizará la supervisión del rendimiento del servidor Transporte perimetral. La supervisión de rendimiento le ayudará a comprender la carga del servidor. Esta información determinará la capacidad de su configuración de hardware actual.

  - **Características de transporte**   El servidor Transporte perimetral puede proporcionar protección contra correo no deseado en el perímetro de la red. Como parte del proceso de planificación, deberá determinar las características contra correo no deseado que habilitará en el servidor Transporte perimetral y su configuración.

  - **Seguridad   **El rol de servidor Transporte perimetral está diseñado para que tenga una superficie de ataque mínima. Por lo tanto, es importante asegurar y administrar de forma correcta tanto el acceso físico como el acceso de red al servidor. Al planificar la seguridad se asegurará de que las conexiones IP solo se habiliten desde servidores y usuarios autorizados. Para obtener más información, vea [Lista de comprobación de seguridad de la implementación](deployment-security-checklist-exchange-2013-help.md).
    
    Es recomendable poner el servidor Transporte perimetral dentro de una red perimetral. Para garantizar que el servidor pueda enviar y recibir correo electrónico, así como recibir actualizaciones de los datos de destinatario y la configuración desde el servicio EdgeSync de Microsoft Exchange, deberá permitir las comunicaciones a través de los puertos que se enumeran en la tabla siguiente.
    
    ### Configuración de puertos de comunicaciones para servidores Transporte perimetral
    
    <table>
    <colgroup>
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Interfaz de red</th>
    <th>Puerto abierto</th>
    <th>Protocolo</th>
    <th>Nota</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Entrante de Internet y saliente a Internet</p></td>
    <td><p>25/TCP</p></td>
    <td><p>SMTP</p></td>
    <td><p>Este puerto es obligatorio para hacer posible el flujo de correo desde y hacia Internet.</p></td>
    </tr>
    <tr class="even">
    <td><p>Entrante de la red interna y saliente a la red interna</p></td>
    <td><p>25/TCP</p></td>
    <td><p>SMTP</p></td>
    <td><p>Este puerto es obligatorio para hacer posible el flujo de correo desde la organización de Exchange.</p></td>
    </tr>
    <tr class="odd">
    <td><p>Solo local</p></td>
    <td><p>50389/TCP</p></td>
    <td><p>LDAP</p></td>
    <td><p>Este puerto se utiliza para establecer una conexión local con AD LDS.</p></td>
    </tr>
    <tr class="even">
    <td><p>Entrante de la red interna</p></td>
    <td><p>50636/TCP</p></td>
    <td><p>LDAP seguro</p></td>
    <td><p>Este puerto es obligatorio para la sincronización de EdgeSync.</p></td>
    </tr>
    <tr class="odd">
    <td><p>Entrante de la red interna</p></td>
    <td><p>3389/TCP</p></td>
    <td><p>RDP</p></td>
    <td><p>Abrir este puerto es opcional. Ofrece más flexibilidad a la hora de administrar los servidores Transporte perimetral desde la red interna, ya que permite usar una conexión de escritorio remota.</p></td>
    </tr>
    </tbody>
    </table>
    

    > [!NOTE]
    > El rol de servidor Transporte perimetral utiliza puertos LDAP no estándar. Los puertos que se especifican en este tema son los puertos de comunicación LDAP que están configurados cuando se tiene instalado el rol de servidor Transporte perimetral.



  - **EdgeSync** El proceso de implementación recomendado es crear una suscripción perimetral para suscribir el servidor Transporte perimetral a la organización de Exchange. Al crear una suscripción perimetral, los datos de los destinatarios y de la configuración se replican de Active Directory a AD LDS. Se suscribe un servidor Transporte perimetral a un sitio de Active Directory. A continuación, el servicio EdgeSync de Microsoft Exchange que se encuentra en ejecución en los servidores de buzones de correo de dicho sitio actualiza AD LDS de forma periódica mediante la sincronización de datos de Active Directory. El proceso de suscripción perimetral proporciona automáticamente los conectores de envío necesarios para habilitar el flujo de correo desde la organización de Exchange a Internet a través de un servidor Transporte perimetral. Si está utilizando las características de consulta de destinatario o de agregación de lista segura en el servidor Transporte perimetral, es preciso que suscriba este servidor a la organización.

## Configuración del DNS para el rol de servidor Transporte perimetral

El rol de servidor Transporte perimetral se implementa fuera de la organización de Exchange como un servidor independiente de la red perimetral o como miembro de un dominio de Active Directory de la red perimetral. Debe configurar manualmente el sufijo DNS correcto para el rol de servidor Transporte perimetral antes de instalar Exchange 2013. Si el sufijo DNS no está configurado, la actualización dará error.

Como el servidor Transporte perimetral se implementa en la red perimetral, este tiene interfaces de red que se conectan a múltiples segmentos de red. Cada segmento de red tiene una única configuración IP. La interfaz de red conectada al segmento de red externo o público debe configurarse para que use un servidor de sistema de nombres de dominio (DNS) público para la resolución de nombres. Esto permite al servidor resolver los nombres de dominio SMTP a los registros de los recursos de MX y enrutar el correo a Internet.

La interfaz de red que está conectada al segmento de red interno o privado debe configurarse para que use un servidor DNS en la red perimetral que pueda resolver los nombres de los servidores de buzones de correo de su organización, o bien debe tener habilitado un archivo Hosts. Los servidores de transporte perimetral y los servidores de buzones de correo deben estar habilitados para utilizar la resolución host de DNS para localizarse.

Para habilitar la resolución de nombres de servidores de buzones de correo por los servidores Transporte perimetral, use uno de los siguientes métodos:

  - Cree manualmente un registro de recursos A para servidores de buzones de correo en una zona de búsqueda directa del servidor DNS que está configurado en el adaptador de red interno del servidor Transporte perimetral.

  - Edite el archivo Hosts en el servidor de transporte perimetral para incluir los registros de Host para los servidores de buzones de correo. El archivo Hosts es un archivo de texto local con el mismo formato que el archivo UNIX/etc/hosts de 4.3 Berkeley Software Distribution (BSD). Este archivo asigna un nombre host a las direcciones IP y el archivo se almacena en la carpeta \\%Systemroot%\\System32\\Drivers\\Etc.

Para habilitar la resolución de nombres de servidores de buzones de correo de transporte perimetral por los servidores de buzones de correo, use uno de los siguientes métodos:

  - Cree manualmente registros de recursos A para servidores Transporte perimetral en una zona de búsqueda directa del servidor DNS que está configurado en el servidor de buzones de correo.

  - Para incluir los registros del host para los servidores de transporte perimetral, edite el archivo Hosts en los servidores de buzones de correo que se encuentran en el sitio de Active Directory con suscripción.

Siga estos pasos para configurar el DNS para el servidor Transporte perimetral:

1.  Compruebe que la configuración del servidor DNS para cada interfaz de red es correcta para el segmento de red.

2.  Configure el sufijo DNS para el nombre del servidor Transporte perimetral siguiendo los pasos siguientes:
    
    1.  Abra el Panel de control y, a continuación, elija **Propiedades del sistema**.
    
    2.  Elija la ficha **Nombre del equipo**.
    
    3.  Elija **Cambiar**.
    
    4.  En la página **Cambios en el nombre de equipo**, haga clic en **Más**.
    
    5.  En el campo **Sufijo DNS principal de este equipo**, escriba un sufijo y nombre de dominio DNS para el servidor de transporte perimetral.
    
    Este nombre no se puede cambiar una vez que se ha instalado el rol de servidor Transporte perimetral.

## Invalidación de la configuración de DNS

Puede que tenga que invalidar la configuración predeterminada de DNS en el servidor de Exchange para que el correo se pueda enrutar y entregar correctamente. Para ello, modifique las configuraciones de **búsquedas DNS internas** y **externas** de las propiedades del servidor de transporte. Esta configuración invalida la configuración del adaptador de red para distribuir mensajes de correo electrónico.

