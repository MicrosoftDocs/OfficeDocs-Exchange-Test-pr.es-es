---
title: 'Modificar la configuración de AD LDS: Exchange 2013 Help'
TOCTitle: Modificar la configuración de AD LDS
ms:assetid: 381f582c-15ec-43bc-b674-5399fad72c97
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997269(v=EXCHG.150)
ms:contentKeyID: 61183324
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Modificar la configuración de AD LDS

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-04-08_

Puede usar el script **ConfigureAdam.ps1** (ubicado en $env:ExchangeInstallPath\\Scripts) para modificar la configuración predeterminada de Active Directory Lightweight Directory Services (AD LDS) en los servidores de transporte perimetral antes de suscribir el servidor de transporte perimetral a su organización de Exchange.


> [!IMPORTANT]
> El script <STRONG>ConfigureAdam.ps1</STRONG> invoca el comando <STRONG>dsdbutil</STRONG> para cambiar la configuración del Registro para AD LDS. El comando <STRONG>dsdbutil</STRONG> es una herramienta de administración de AD&nbsp;LDS destinada solo a administradores experimentados; la manera recomendada de cambiar la configuración de AD&nbsp;LDS es usar <STRONG>ConfigureAdam.ps1</STRONG>.



Los parámetros de la siguiente tabla están disponibles para el script **ConfigureAdam.ps1**. Puede usar uno, todos o cualquier combinación de estos parámetros para modificar AD LDS.

### Parámetros disponibles para el script ConfigureAdam.ps1

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parámetro</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Ldapport</em></p></td>
<td><p>Modifica el puerto usado para la comunicación de LDAP. De forma predeterminada, el servidor de transporte perimetral usa el puerto 50389 no estándar.</p></td>
</tr>
<tr class="even">
<td><p><em>Sslport</em></p></td>
<td><p>Modifica el puerto usado para la comunicación segura de LDAP. De forma predeterminada, el servidor de transporte perimetral usa el puerto 50636 no estándar.</p></td>
</tr>
<tr class="odd">
<td><p><em>LogPath</em></p></td>
<td><p>Modifica la ubicación del archivo de registro. De forma predeterminada, el servidor de transporte perimetral crea archivos de registro en la ruta de acceso %ExchangeInstallPath%Transport Roles\Data\adam</p></td>
</tr>
<tr class="even">
<td><p><em>DataPath</em></p></td>
<td><p>Modifica la ubicación del archivo de la base de datos del directorio. De forma predeterminada, el servidor de transporte perimetral almacena la base de datos del directorio en la ruta de acceso %ExchangeInstallPath%Transport Roles\Data\adam</p></td>
</tr>
</tbody>
</table>


## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: cinco minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Sección "Servidores de transporte perimetral" en [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Si necesita realizar modificaciones en la configuración de AD LDS de los servidores de transporte perimetral, hágalo antes de suscribir el servidor de transporte perimetral a su organización de Exchange. Si modifica la configuración de AD LDS de un servidor de transporte perimetral, tendrá que volver a suscribirlo a la organización de Exchange.

  - Use siempre el script para modificar la configuración del Registro. Realizar cambios manuales en la configuración de AD LDS del Registro podría hacer que la instancia de AD LDS no esté disponible.

  - Si necesita modificar el puerto LDAP o el puerto SSL que AD LDS utiliza, compruebe primero que el puerto seleccionado no está siendo utilizado por otra aplicación. Puede utilizar el comando **netstat** para ver los puertos que se están utilizando en el servidor de transporte perimetral.

  - Solo puede usar el Shell para realizar este procedimiento.


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Modificar la configuración de AD LDS en un servidor de transporte perimetral

Este ejemplo cambia el puerto LDAP que AD LDS utiliza a 5000. El símbolo "y" comercial (&) forma parte de la sintaxis del comando.

    & $env:ExchangeInstallPath\Scripts\ConfigureAdam.ps1 -LdapPort:5000

Este ejemplo realiza los siguientes cambios en la configuración de AD LDS. El símbolo de "y" comercial (&) forma parte de la sintaxis del comando. Tenga en cuenta los dos puntos (:) que se utilizan entre cada parámetro y su valor:

  - Cambia el puerto LDAP a 5000

  - Cambia el puerto SSL a 500

  - Cambia la ruta de acceso de registro a D:\\Exchange Server\\Data\\ADLDS

  - Cambia la ruta de acceso a los datos a D:\\Exchange Server\\Data\\ADLDS

<!-- end list -->

    & $env:ExchangeInstallPath\Scripts\ConfigureAdam.ps1 -LdapPort:5000 -SslPort:5001 -LogPath:"D:\Exchange Server\Data\ADLDS" -DataPath:"D:\Exchange Server\Data\ADLDS"

