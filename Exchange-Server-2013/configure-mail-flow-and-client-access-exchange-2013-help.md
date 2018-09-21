---
title: 'Configurar el flujo de correo y el acceso de cliente: Exchange 2013 Help'
TOCTitle: Configurar el flujo de correo y el acceso de cliente
ms:assetid: 4acc7f2a-93ce-468c-9ace-d5f7eecbd8d4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ218640(v=EXCHG.150)
ms:contentKeyID: 49116196
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar el flujo de correo y el acceso de cliente

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Tareas posteriores a la instalación de flujo de correo y acceso de cliente de Exchange Server 2013, incluidas cómo configurar un certificado SSL.

Después de instalar Microsoft Exchange Server 2013 en la organización, deberá configurar Exchange Server 2013 para el flujo de correo y el acceso de clientes. Sin estos pasos adicionales, no podrá enviar correo a Internet ni a clientes externos, como Microsoft Office Outlook. Además, los dispositivos de Exchange ActiveSync no podrán conectarse a la organización de Exchange.

En los pasos descritos en este tema se asume el uso de una implementación básica de Exchange con un único sitio de Active Directory y un solo espacio de nombres del protocolo simple de transferencia de correo (SMTP).


> [!IMPORTANT]
> En este tema se utilizan valores de ejemplo, como Ex2013CAS, contoso.com, mail.contoso.com y 172.16.10.11. Reemplace los valores de ejemplo por los nombres del servidor, los FQDN y las direcciones IP de su organización.



Para consultar otras tareas de administración relacionadas con el flujo de correo y los clientes y dispositivos, vea [Flujo de correo](mail-flow-exchange-2013-help.md) y [Clientes y móvil](clients-and-mobile-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar esta tarea: 50 minutos

  - Los procedimientos descritos en este tema requieren permisos específicos. Vea cada procedimiento para ver la información de permisos.

  - Recibirá advertencias de certificado al conectarse con el sitio web del Centro de administración de Exchange (EAC) hasta que configure un certificado de Capa de sockets seguros (SSL) en el servidor de acceso de clientes. Se explicará cómo hacerlo más adelante en este tema.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!IMPORTANT]
> Cada organización requiere, como mínimo, un servidor de acceso de cliente y un servidor de buzones en el bosque de Active Directory. Además, cada sitio de Active Directory que contiene un servidor de buzones deberá también contener, como mínimo, un servidor de acceso de cliente. Si separa sus roles de servidor, le recomendamos instalar el rol del servidor de buzones primero.




> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Cómo realiza esto?

## Paso 1: Crear un conector de envío

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Conectores de envío" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

Para poder enviar correo a Internet, debe crear un conector de envío en el servidor de buzones. Realice lo siguiente.

1.  Para abrir el EAC, vaya a la URL del servidor de acceso de cliente. Por ejemplo, https://Ex2013CAS/ECP.

2.  Escriba su nombre de usuario y contraseña en **Dominio\\nombre de usuario** y **Contraseña** y, a continuación, haga clic en **Iniciar sesión**.

3.  Vaya a **Flujo de correo** \> **Conectores de envío**. En la página **Conectores de envío**, haga clic en **Nuevo**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

4.  En el asistente para **nuevo conector de envío**, especifique un nombre para el conector de envío y, a continuación, elija **Internet**. Haga clic en **Siguiente**.

5.  Compruebe que la opción **Registro MX asociado con el dominio del destinatario** está seleccionada. Haga clic en **Siguiente**.

6.  En **Espacio de direcciones**, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). En la ventana **Agregar dominio**, asegúrese de que **SMTP** está seleccionado en el campo **Tipo**. En el campo **Nombre de dominio completo (FQDN)**, escriba **\***. Haga clic en **Guardar**.

7.  Asegúrese de que la casilla **Conector de envío en el ámbito** está desactivada y, a continuación, haga clic en **Siguiente** .

8.  En **Servidor de origen**, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). En la ventana **Seleccionar un servidor**, seleccione un servidor de buzones. Después de seleccionar el servidor, haga clic en **Agregar** y después en **Aceptar**.

9.  Haga clic en **Finalizar**.


> [!NOTE]
> Al instalar Exchange&nbsp;2013 se crea un conector de recepción de entrada predeterminado, que acepta conexiones SMTP anónimas desde servidores externos. No es necesario realizar ninguna configuración adicional si ésta es la funcionalidad que desea. Si desea restringir las conexiones de entrada desde los servidores externos, modifique el conector de recepción <STRONG>frontend predeterminado &lt;servidor de acceso de clientes&gt;</STRONG> en el servidor de acceso de clientes.



## ¿Cómo sabe si este paso se ha completado correctamente?

Para comprobar si el conector de envío de salida se creó correctamente, siga estos pasos:

1.  En el EAC, compruebe si el nuevo conector de envío aparece en **Flujo de correo** \> **Conectores de envío**.

2.  Abra Outlook Web App y envíe un mensaje de correo a un destinatario externo. Si el destinatario recibe el mensaje, habrá configurado el conector de envío correctamente.

## Paso 2: Agregar dominios aceptados adicionales

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Dominios aceptados" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

De forma predeterminada, cuando se implementa una nueva organización de Exchange 2013 en un bosque de Active Directory, Exchange usa el nombre del dominio de Active Directory donde se ejecutó Setup /PrepareAD. Si desea que los destinatarios envíen o reciban mensajes de otro dominio, agregue el dominio como un dominio aceptado. Este dominio también se agrega como la dirección SMTP principal en la directiva de direcciones de correo electrónico predeterminada en el siguiente paso.


> [!IMPORTANT]
> Se necesita un registro de recursos MX del Sistema de nombres de dominio (DNS) para cada dominio SMTP del que desee aceptar correo electrónico de Internet. Deberá resolver los registros MX para el servidor con conexión a Internet que reciba correo electrónico para la organización.



1.  Para abrir el EAC, vaya a la URL del servidor de acceso de cliente. Por ejemplo, https://Ex2013CAS/ECP.

2.  Escriba su nombre de usuario y contraseña en **Dominio\\nombre de usuario** y **Contraseña** y, a continuación, haga clic en **Iniciar sesión**.

3.  Vaya a **Flujo de correo** \> **Dominios aceptados**. En la página **Dominios aceptados**, haga clic en **Nuevo**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

4.  En el asistente para **nuevo dominio aceptado**, especifique un nombre para el dominio aceptado.

5.  En el campo **Dominio aceptado**, especifique el dominio de destinatario SMTP que desea agregar. Por ejemplo, contoso.com.

6.  Seleccione **Dominio autoritativo** y, a continuación, haga clic en **Enviar**.

## ¿Cómo sabe si este paso se ha completado correctamente?

Para comprobar que el dominio aceptado se creó correctamente, siga estos pasos:

  - En el EAC, compruebe si el nuevo dominio aceptado aparece en **Flujo de correo** \> **Dominios aceptados**.

## Paso 3: Configurar la directiva de direcciones de correo electrónico predeterminada

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Directivas de direcciones de correo electrónico" en el tema [Permisos de libreta de direcciones y dirección de correo electrónico](email-address-and-address-book-permissions-exchange-2013-help.md).

Si agregó un dominio aceptado en el paso anterior y desea agregarlo ahora a los destinatarios de la organización, deberá actualizar la directiva de direcciones de correo electrónico predeterminada.

1.  Para abrir el EAC, vaya a la URL del servidor de acceso de cliente. Por ejemplo, https://Ex2013CAS/ECP.

2.  Escriba su nombre de usuario y contraseña en **Dominio\\nombre de usuario** y **Contraseña** y, a continuación, haga clic en **Iniciar sesión**.

3.  Vaya a **Flujo de correo** \> **Directivas de direcciones de correo**. En la página **Directivas de direcciones de correo**, elija **Directiva predeterminada** y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

4.  En la página **Directiva de direcciones de correo predeterminada**, haga clic en **Formato de dirección de correo**.

5.  En **Formato de dirección de correo**, haga clic en la dirección SMTP que desea cambiar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

6.  En la página **Formato de dirección de correo** en el campo **Parámetros de la dirección de correo**, especifique el dominio de destinatario SMTP que desea aplicar a todos los destinatarios de la organización de Exchange. Este dominio debe coincidir con el dominio aceptado que agregó en el paso anterior. Por ejemplo, @contoso.com. Haga clic en **Guardar**.

7.  Haga clic en **Guardar**

8.  En el panel de detalles **Directiva predeterminada**, haga clic en **Aplicar**.


> [!NOTE]
> Se recomienda configurar un nombre principal de usuario (UPN) que coincida con la dirección de correo principal de cada usuario. Si no especifica ningún UPN que coincida con la dirección de correo de un usuario, éste deberá especificar manualmente un dominio\nombre de usuario o UPN además de la dirección de correo electrónico. Si el UPN coincide con la dirección de correo electrónico, Outlook Web App, ActiveSync y Outlook harán coincidir la dirección de correo automáticamente con el UPN.



## ¿Cómo sabe si este paso se ha completado correctamente?

Para comprobar que la directiva de direcciones de correo electrónico predeterminada se configuró correctamente, siga estos pasos:

1.  En el EAC, vaya a **Destinatarios** \> **Buzones de correo**.

2.  Seleccione un buzón y, a continuación, en el panel de detalles del destinatario, compruebe que el campo **Buzón del usuario** se estableció en *\<alias\>*@*\<nuevo dominio aceptado\>*. Por ejemplo, david@contoso.com.

3.  De manera opcional, cree un nuevo buzón y compruebe que se le concede una dirección de correo electrónico con el nuevo dominio aceptado. Para ello, siga estos pasos:
    
    1.  Vaya a **Destinatarios** \> **Buzones de correo**, haga clic en **Nuevo**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") y, a continuación, seleccione **Buzón de correo de usuario**.
    
    2.  En la página de nuevo buzón de correo de usuario, especifique la información necesaria para crear un buzón nuevo. Haga clic en **Guardar**.
    
    3.  Seleccione el buzón nuevo y, a continuación, en el panel de detalles del destinatario, compruebe que el campo **Buzón del usuario** se estableció en *\<alias\>*@*\<nuevo dominio aceptado\>*. Por ejemplo, david@contoso.com.

## Paso 4: Configurar direcciones URL externas

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Configuración de directorio virtual de *\<servicio\>*" en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

Antes de que los clientes puedan conectarse al nuevo servidor desde Internet es necesario configurar los dominios externos, o las URL, en los directorios virtuales del servidor de acceso de clientes. A continuación, deberá configurar los registros públicos del servicio de nombres de dominio (DNS). Siga los pasos a continuación para configurar el mismo dominio externo en la dirección URL externa de cada directorio virtual. Si desea configurar varios dominios externos en una o más direcciones URL externas de los directorios virtuales, deberá configurar las URL externas manualmente. Para obtener más información, consulte [Administración de directorios virtuales](virtual-directory-management-exchange-2013-help.md).

1.  Para abrir el EAC, vaya a la URL del servidor de acceso de cliente. Por ejemplo, https://Ex2013CAS/ECP.

2.  Escriba su nombre de usuario y contraseña en **Dominio\\nombre de usuario** y **Contraseña** y, a continuación, haga clic en **Iniciar sesión**.

3.  Vaya a **Servidores** \> **Servidores**, seleccione el nombre del servidor de acceso de clientes con conexión a Internet y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

4.  Haga clic en **Outlook Anywhere**.

5.  En el campo **Nombre de host externo**, especifique el FQDN accesible externamente del servidor de acceso de clientes. Por ejemplo, mail.contoso.com.

6.  De paso, configuremos también el FQDN accesible de manera interna del servidor de acceso de cliente. En el campo **Especificar el nombre de host interno**, especifique el FQDN que utilizó en el paso anterior. Por ejemplo, mail.contoso.com.

7.  Haga clic en **Guardar**.

8.  Vaya a **Servidores** \> **Servidores virtuales** y, a continuación, haga clic en **Configurar dominio de acceso externo** ![Configurar icono](images/JJ218640.a9c33f23-3d44-44e7-a5d0-8446200c746e(EXCHG.150).gif "Configurar icono").

9.  En **Seleccione los servidores de acceso de cliente para utilizar con la dirección URL externa**, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono")

10. Seleccione los servidores de acceso de clientes que desea configurar y, a continuación, haga clic en **Agregar**. Después de agregar todos los servidores de acceso de clientes que desea configurar, haga clic en **Aceptar**.

11. En **Escriba el nombre de dominio que usará con los servidores de acceso de clientes externos**, escriba el dominio externo que desee aplicar. Por ejemplo, mail.contoso.com. Haga clic en **Guardar**.
    

    > [!NOTE]
    > Algunas organizaciones hacen el FQDN de Outlook Web App único para proteger a los usuarios de los cambios al FQDN del servidor subyacente. Muchas organizaciones usan owa.contoso.com para su FQDN de Outlook Web App en vez de mail.contoso.com. Si desea configurar un FQDN de Outlook Web App único, realice lo siguiente después de finalizar el paso anterior. Esta lista de comprobación asume que ha configurado un FQDN de Outlook Web App único. 
    > <OL>
    > <LI>
    > <P>Seleccione <STRONG>owa (Sitio web predeterminado)</STRONG> y haga clic en <STRONG>Editar</STRONG>&nbsp;<IMG title="Icono Editar" alt="Icono Editar" src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif">.</P>
    > <LI>
    > <P>En <STRONG>URL externa</STRONG>, escriba <STRONG>https://</STRONG>, luego, el FQDN de Outlook Web App único que desea usar y, luego, agregue <STRONG>/owa</STRONG>. Por ejemplo, https://owa.contoso.com/owa.</P>
    > <LI>
    > <P>Haga clic en <STRONG>Guardar</STRONG>.</P>
    > <LI>
    > <P>Seleccione <STRONG>ecp (Sitio web predeterminado)</STRONG> y haga clic en <STRONG>Editar</STRONG>&nbsp;<IMG title="Icono Editar" alt="Icono Editar" src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif">.</P>
    > <LI>
    > <P>En <STRONG>URL externa</STRONG>, escriba <STRONG>https://</STRONG>, luego, el mismo FQDN de Outlook Web App que especificó en el paso anterior y, luego, agregue <STRONG>/ecp</STRONG>. Por ejemplo, https://owa.contoso.com/ecp.</P>
    > <LI>
    > <P>Haga clic en <STRONG>Guardar</STRONG>.</P></LI></OL>



Después de configurar la dirección URL externa en los directorios virtuales del servidor de acceso de cliente, deberá configurar los registros DNS públicos para la detección automática, Outlook Web App y el flujo de correo. Los registros DNS públicos deben apuntar a la dirección IP externa o FQDN del servidor de acceso de cliente con conexión a Internet, y debe utilizar los FQDN accesibles externamente que configuró en el servidor de acceso de cliente. A continuación se muestran algunos ejemplos de registros DNS recomendados que debe crear para habilitar el flujo de correo y la conectividad de clientes externos.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>FQDN</th>
<th>Tipo de registro de DNS</th>
<th>Valor</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Contoso.com</p></td>
<td><p>MX</p></td>
<td><p>Mail.contoso.com</p></td>
</tr>
<tr class="even">
<td><p>Mail.contoso.com</p></td>
<td><p>A</p></td>
<td><p>172.16.10.11</p></td>
</tr>
<tr class="odd">
<td><p>Owa.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Mail.contoso.com</p></td>
</tr>
<tr class="even">
<td><p>Autodiscover.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Mail.contoso.com</p></td>
</tr>
</tbody>
</table>


## ¿Cómo sabe si este paso se ha completado correctamente?

Para comprobar que la dirección URL externa se configuró correctamente en los directorios virtuales del servidor de acceso de clientes, siga estos pasos:

1.  En el EAC, vaya a **Servidores** \> **Directorios virtuales**.

2.  En el campo **Seleccionar servidor**, elija el servidor de acceso de clientes con conexión a Internet.

3.  Seleccione un directorio virtual y, a continuación, en el panel de detalles del directorio, compruebe que el campo **Dirección URL externa** contiene el FQDN y el servicio correctos, según se muestra a continuación:
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Directorio virtual</th>
    <th>Valor de dirección URL externa</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Detección automática</strong></p></td>
    <td><p>No se muestra ninguna dirección URL externa</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ECP</strong></p></td>
    <td><p>https://owa.contoso.com/ecp</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>EWS</strong></p></td>
    <td><p>https://mail.contoso.com/EWS/Exchange.asmx</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Microsoft-Server-ActiveSync</strong></p></td>
    <td><p>https://mail.contoso.com/Microsoft-Server-ActiveSync</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>OAB</strong></p></td>
    <td><p>https://mail.contoso.com/OAB</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OWA</strong></p></td>
    <td><p>https://owa.contoso.com/owa</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>PowerShell</strong></p></td>
    <td><p>http://mail.contoso.com/PowerShell</p></td>
    </tr>
    </tbody>
    </table>


Para comprobar si ha configurado correctamente sus registros DNS públicos, haga lo siguiente:

1.  Abra un símbolo del sistema y ejecute `nslookup.exe`.

2.  Cambie a un servidor DNS que pueda consultar a su zona DNS pública.

3.  En `nslookup`, busque el registro de todos los FQDN que creó. Compruebe que el valor que se devuelve para cada FQDN es correcto.

4.  En `nslookup`, escriba `set type=mx` y, a continuación, busque el dominio aceptado que agregó en el paso 1. Compruebe que el valor devuelto coincide con el FQDN del servidor de acceso de clientes.

## Paso 5: Configurar las URL internas

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Configuración de directorio virtual de *\<servicio\>*" en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

Antes de que los clientes puedan conectarse al nuevo servidor desde su intranet es necesario configurar los dominios internos, o las URL, en los directorios virtuales del servidor de acceso de clientes. A continuación, deberá configurar los registros privados del servicio de nombres de dominio (DNS).

El siguiente procedimiento le permite elegir si quiere que los usuarios utilicen la misma URL en la intranet y en Internet para acceder el servidor Exchange o bien si deben utilizar una URL distinta. Su elección dependerá del esquema de direccionamiento que ya se haya instaurado o que desee implementar. Si está implementando un nuevo esquema de direccionamiento, le recomendamos que use la misma dirección URL para las URL internas y externas. El uso de la misma URL les facilita a los usuarios el acceso a su servidor Exchange porque solo tienen que recordar una dirección. Independientemente de la elección que realice, debe asegurarse de configurar una zona DNS privada para el espacio de direcciones que configure. Para obtener más información acerca de la administración de zonas DNS, consulte [Administración del servidor DNS](http://go.microsoft.com/fwlink/p/?linkid=190631).

Para más información acerca de las URL internas y externas en los directorios virtuales, consulte [Administración de directorios virtuales](virtual-directory-management-exchange-2013-help.md).

## Configurar direcciones URL internas y externas iguales

1.  Abrir el Shell de administración de Exchange en el servidor de acceso de cliente.

2.  Almacenar el nombre del host de su servidor de acceso de cliente en una variable que se usará en el próximo paso. Por ejemplo, Ex2013CAS.
    
    ```powershell
$HostName = "Ex2013CAS"
```

3.  Ejecute cada uno de los siguientes comandos en el Shell para configurar cada URL interna a fin de que coincida con la URL externa del directorio virtual.
    
        Set-EcpVirtualDirectory "$HostName\ECP (Default Web Site)" -InternalUrl ((Get-EcpVirtualDirectory "$HostName\ECP (Default Web Site)").ExternalUrl)
        
        Set-WebServicesVirtualDirectory "$HostName\EWS (Default Web Site)" -InternalUrl ((get-WebServicesVirtualDirectory "$HostName\EWS (Default Web Site)").ExternalUrl)
        
        Set-ActiveSyncVirtualDirectory "$HostName\Microsoft-Server-ActiveSync (Default Web Site)" -InternalUrl ((Get-ActiveSyncVirtualDirectory "$HostName\Microsoft-Server-ActiveSync (Default Web Site)").ExternalUrl)
        
        Set-OabVirtualDirectory "$HostName\OAB (Default Web Site)" -InternalUrl ((Get-OabVirtualDirectory "$HostName\OAB (Default Web Site)").ExternalUrl)
        
        Set-OwaVirtualDirectory "$HostName\OWA (Default Web Site)" -InternalUrl ((Get-OwaVirtualDirectory "$HostName\OWA (Default Web Site)").ExternalUrl)
        
        Set-PowerShellVirtualDirectory "$HostName\PowerShell (Default Web Site)" -InternalUrl ((Get-PowerShellVirtualDirectory "$HostName\PowerShell (Default Web Site)").ExternalUrl)

4.  Mientras estamos en el Shell, vamos a configurar también la Libreta de direcciones sin conexión (OAB) para permitir que Detección automática seleccione el directorio virtual correcto para distribuir la OAB. Ejecute los siguientes comandos para hacerlo.
    
        Get-OfflineAddressBook | Set-OfflineAddressBook -GlobalWebDistributionEnabled $True -VirtualDirectories $Null

Después de configurar la dirección URL interna en los directorios virtuales del servidor de acceso de clientes, deberá configurar los registros DNS privados para Outlook Web App y otra conectividad. En función de su configuración, deberá modificar los registros DNS privados para que apunten a la dirección IP interna o externa o al nombre de dominio completo (FQDN) del servidor de acceso de clientes. A continuación, se muestran algunos ejemplos de registros DNS recomendados que debe crear para habilitar la conectividad de clientes internos.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>FQDN</th>
<th>Tipo de registro de DNS</th>
<th>Valor</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mail.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Ex2013CAS.corp.contoso.com</p></td>
</tr>
<tr class="even">
<td><p>Owa.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Ex2013CAS.corp.contoso.com</p></td>
</tr>
</tbody>
</table>


## ¿Cómo sabe si este paso se ha completado correctamente?

Para comprobar que la dirección URL interna se configuró correctamente en los directorios virtuales del servidor de acceso de clientes, siga estos pasos:

1.  En el EAC, vaya a **Servidores** \> **Directorios virtuales**.

2.  En el campo **Seleccionar servidor**, elija el servidor de acceso de clientes con conexión a Internet.

3.  Seleccione un directorio virtual y, a continuación, haga clic en **Editar** ![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

4.  Verifique que el campo **URL interna** se haya rellenado con el servicio y el FQDN correctos, tal como se muestra a continuación:
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Directorio virtual</th>
    <th>Valor de URL interna</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Detección automática</strong></p></td>
    <td><p>No se muestra ninguna dirección URL interna</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ECP</strong></p></td>
    <td><p>https://owa.contoso.com/ecp</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>EWS</strong></p></td>
    <td><p>https://mail.contoso.com/EWS/Exchange.asmx</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Microsoft-Server-ActiveSync</strong></p></td>
    <td><p>https://mail.contoso.com/Microsoft-Server-ActiveSync</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>OAB</strong></p></td>
    <td><p>https://mail.contoso.com/OAB</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OWA</strong></p></td>
    <td><p>https://owa.contoso.com/owa</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>PowerShell</strong></p></td>
    <td><p>http://mail.contoso.com/PowerShell</p></td>
    </tr>
    </tbody>
    </table>


Para comprobar que ha configurado correctamente sus registros DNS privados, haga lo siguiente:

1.  Abra un símbolo del sistema y ejecute `nslookup.exe`.

2.  Cambie a un servidor DNS que pueda consultar su zona DNS privada.

3.  En `nslookup`, busque el registro de todos los FQDN que creó. Compruebe que el valor que se devuelve para cada FQDN es correcto.

## Configurar diferentes URL internas y externas

1.  Abra el EAC. Para ello, examine la URL del servidor de acceso de cliente. Por ejemplo, https://Ex2013CAS/ECP.

2.  Vaya a **Servidores** \> **Directorios virtuales**.

3.  En el campo **Seleccionar servidor**, elija el servidor de acceso de clientes con conexión a Internet.

4.  Seleccione el directorio virtual que quiera modificar y haga clic en **Editar** ![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

5.  En **URL interna**, reemplace el nombre de host entre **https://** y la primera barra diagonal (**/**) con el nuevo FQDN que desea usar. Por ejemplo, si desea cambiar el FQDN del directorio virtual EWS de Ex2013CAS.corp.contoso.com a internal.contoso.com, cambie la URL interna de https://Ex2013CAS.corp.contoso.com/ews/exchange.asmx a https://internal.contoso.com/ews/exchange.asmx.

6.  Haga clic en **Guardar**.

7.  Repita los pasos 5 y 6 para cada directorio virtual que desee cambiar.
    

    > [!NOTE]
    > Las URL internas del directorio virtual de ECP y OWA deben ser las mismas.<BR>No se puede establecer una URL interna en el directorio virtual de Detección automática.



8.  Por último, necesitamos abrir el Shell y configurar la Libreta de direcciones sin conexión (OAB) para permitir que Detección automática seleccione el directorio virtual correcto para distribuir la OAB. Ejecute los siguientes comandos para hacerlo.
    
        Get-OfflineAddressBook | Set-OfflineAddressBook -GlobalWebDistributionEnabled $True -VirtualDirectories $Null

Después de configurar la dirección URL interna en los directorios virtuales del servidor de acceso de clientes, deberá configurar los registros DNS privados para Outlook Web App y otra conectividad. Según la configuración, necesitará establecer sus registros DNS privados para que apunten a la dirección IP interna y externa o al FQDN de su servidor de acceso de cliente. A continuación puede ver un ejemplo de registro DNS recomendado que debería crear para que el cliente interno tenga conectividad si ha configurado las URL internas del directorio virtual para que usen internal.contoso.com.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>FQDN</th>
<th>Tipo de registro de DNS</th>
<th>Valor</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>internal.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Ex2013CAS.corp.contoso.com</p></td>
</tr>
</tbody>
</table>


## ¿Cómo sabe si este paso se ha completado correctamente?

Para comprobar que la dirección URL interna se configuró correctamente en los directorios virtuales del servidor de acceso de clientes, siga estos pasos:

1.  En el EAC, vaya a **Servidores** \> **Directorios virtuales**.

2.  En el campo **Seleccionar servidor**, elija el servidor de acceso de clientes con conexión a Internet.

3.  Seleccione un directorio virtual y, a continuación, haga clic en **Editar** ![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

4.  Verifique que el campo **URL interna** se haya rellenado con el FQDN correcto. Por ejemplo, es posible que haya definido las URL internas para usar internal.contoso.com.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Directorio virtual</th>
    <th>Valor de URL interna</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Detección automática</strong></p></td>
    <td><p>No se muestra ninguna dirección URL interna</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ECP</strong></p></td>
    <td><p>https://internal.contoso.com/ecp</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>EWS</strong></p></td>
    <td><p>https://internal.contoso.com/EWS/Exchange.asmx</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Microsoft-Server-ActiveSync</strong></p></td>
    <td><p>https://internal.contoso.com/Microsoft-Server-ActiveSync</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>OAB</strong></p></td>
    <td><p>https://internal.contoso.com/OAB</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OWA</strong></p></td>
    <td><p>https://internal.contoso.com/owa</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>PowerShell</strong></p></td>
    <td><p>http://internal.contoso.com/PowerShell</p></td>
    </tr>
    </tbody>
    </table>


Para comprobar que ha configurado correctamente sus registros DNS privados, haga lo siguiente:

1.  Abra un símbolo del sistema y ejecute `nslookup.exe`.

2.  Cambie a un servidor DNS que pueda consultar su zona DNS privada.

3.  En `nslookup`, busque el registro de todos los FQDN que creó. Compruebe que el valor que se devuelve para cada FQDN es correcto.

## Paso 6: Configurar un certificado SSL

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el contenido "Administración de certificados" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

Algunos servicios, como Outlook en cualquier lugar y Exchange ActiveSync, requieren que se configuren certificados en el servidor Exchange 2013. En los siguientes pasos se describe cómo configurar un certificado SSL de una entidad de certificación (CA) de terceros:

1.  Para abrir el EAC, vaya a la URL del servidor de acceso de cliente. Por ejemplo, https://Ex2013CAS/ECP.

2.  Escriba su nombre de usuario y contraseña en **Dominio\\nombre de usuario** y **Contraseña** y, a continuación, haga clic en **Iniciar sesión**.

3.  Vaya a **Servidores** \> **Certificados**. En la página **Certificados**, asegúrese de que su servidor de acceso de clientes está seleccionado en el campo **Seleccionar servidor** y, a continuación, haga clic en **Nuevo**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

4.  En el asistente para **nuevo certificado de Exchange**, seleccione **Crear una solicitud para un certificado desde una entidad de certificación** y, a continuación, haga clic en **Siguiente**.

5.  Especifique un nombre para este certificado y haga clic en **Siguiente**.

6.  Si desea solicitar un certificado de comodín, seleccione **Solicitar un certificado de comodín** y, a continuación, especifique el dominio raíz de todos los subdominios en el campo **Dominio raíz**. Si no desea solicitar ningún certificado de comodín pero sí especificar los dominios que desea agregar al certificado, deje esta página en blanco. Haga clic en **Siguiente**.

7.  Haga clic en **Examinar** y especifique el servidor Exchange en el que desea almacenar los certificados. El servidor que seleccione debe ser el servidor de acceso de clientes con conexión a Internet. Haga clic en **Siguiente**.

8.  Para cada servicio mostrado en la lista, compruebe que los nombres de servidor interno o externo que los usuarios utilizarán para conectarse al servidor Exchange sean correctos. Por ejemplo:
    
      - Si configuró las URL internas y externas para que sean las mismas, **Outlook Web App (cuando se accede desde Internet)** y **Outlook Web App (cuando se accede desde la intranet)** deben mostrar owa.contoso.com. **OAB (cuando se accede desde Internet)** y **OAB (cuando se accede desde la intranet)** deben mostrar mail.contoso.com.
    
      - Si configura las URL internas para que sean internal.contoso.com, **Outlook Web App (cuando se accede desde Internet)** debe mostrar owa.contoso.com y **Outlook Web App (cuando se accede desde la intranet)** debe mostrar internal.contoso.com.
    
    Estos dominios se utilizarán para crear la solicitud de certificado SSL. Haga clic en **Siguiente**.

9.  Agregue cualquier otro dominio que desee incluir en el certificado SSL.

10. Seleccione el dominio que quiere utilizar como nombre común para el certificado y, a continuación, haga clic en **Establecer como nombre común**. Por ejemplo, contoso.com. Haga clic en **Siguiente**.

11. Proporcione información acerca de la organización. Esta información se incluirá en el certificado SSL. Haga clic en **Siguiente**.

12. Especifique la ubicación de red en la que desea guardar la solicitud de certificado. Haga clic en **Finalizar**.

Después de guardar la solicitud de certificado, envíela a la entidad de certificación (CA), que puede ser una CA interna o de terceros, en función de la organización. Los clientes que se conecten al servidor de acceso de clientes deben confiar en la CA que utilice. Después de recibir el certificado de la CA, complete los siguientes pasos:

1.  En la página **Servidor** \> **Certificados** en el EAC, seleccione la solicitud de certificado que creó en los pasos anteriores.

2.  En el panel de detalles de la solicitud de certificado, haga clic en **Completo** en **Estado**.

3.  En la página para completar solicitudes pendientes, especifique la ruta de acceso al archivo del certificado SSL y, a continuación, haga clic en **Aceptar**.

4.  Seleccione el nuevo certificado que acaba de agregar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

5.  En la página del certificado, haga clic en **Servicios**.

6.  Seleccione los servicios que desea asignar a este certificado. Como mínimo, debe seleccionar **SMTP** e **IIS**. Haga clic en **Guardar**.

7.  Si recibe la advertencia **¿Desea sobrescribir el certificado SMTP predeterminado existente?**, haga clic en **Sí**.

## ¿Cómo sabe si este paso se ha completado correctamente?

Para comprobar que el nuevo certificado se agregó correctamente, siga estos pasos:

1.  En el EAC, vaya a **Servidores** \> **Certificados**.

2.  Seleccione el certificado nuevo y, a continuación, en el panel de detalles del certificado, compruebe que se cumple lo siguiente:
    
      - El **Estado** está establecido en **Válido**
    
      - **Asignado a servicios** muestra, como mínimo, **IIS** y **SMTP**.

## ¿Cómo sabe si esta tarea se ha completado correctamente?

Para comprobar que el flujo de correo y el acceso de clientes externos se configuró correctamente, siga estos pasos:

1.  En Outlook, en un dispositivo de Exchange ActiveSync o en ambos, cree un perfil nuevo. Compruebe que Outlook o el dispositivo móvil crean el perfil nuevo correctamente.

2.  En Outlook o en el dispositivo móvil, envíe un mensaje nuevo a un destinatario externo. Compruebe que el destinatario externo recibe el mensaje.

3.  En el buzón del destinatario externo, responda al mensaje que acaba de enviar desde el buzón de Exchange. Compruebe que el buzón de Exchange recibe el mensaje.

4.  Vaya a https://owa.contoso.com/owa y compruebe que no hay ninguna advertencia de certificado.

