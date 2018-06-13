---
title: 'Configurar Exchange para admitir permisos de buzón delegada en una implementación híbrida: Exchange 2013 Help'
TOCTitle: Configurar Exchange para admitir permisos de buzón delegada en una implementación híbrida
ms:assetid: a2a10cb3-4557-4ff5-8191-c653522f4512
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Mt784505(v=EXCHG.150)
ms:contentKeyID: 74447329
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar Exchange para admitir permisos de buzón delegada en una implementación híbrida

 

_**Última modificación del tema:**2018-01-30_

Permisos de buzón delegada habilitar a otro usuario administrar parte de buzón de otro usuario. Un ejemplo común de esto es un Ayudante administrativo que necesita para administrar los buzones de correo y el calendario de un ejecutivo. Las implementaciones de híbrido entre una organización de Exchange local y soporte técnico de Office 365 el **Acceso completo** y **Enviar en nombre de** delegar permisos de buzón. Sin embargo, según la versión de Exchange que se ha instalado en la organización local, necesitará realizar una configuración adicional para utilizar permisos de buzón delegada en una implementación híbrida. A continuación enumeran las versiones de Exchange que soporte delegado permisos de buzón en una implementación híbrida y si se necesita una configuración adicional para esa versión.

  - **Intercambio de 2016** No se requiere ninguna configuración adicional.

  - **Intercambio de 2013** A soporta la actualización acumulativa de Exchange 2013 (CU) y se requieren configuración adicional.

  - **Exchange 2010** Una actualización de Exchange 2010 admitida del rodillo (RU) y se requieren configuración adicional.

Para obtener más información acerca de los requisitos específicos para admitir permisos de buzón delegada en una implementación híbrida, eche un vistazo a [Permisos en implementaciones híbridas de Exchange](permissions-in-exchange-hybrid-deployments-exchange-2013-help.md).

En las secciones siguientes le guiará a través de la configuración de 2013 de Exchange y Exchange 2010 implementaciones para habilitar la compatibilidad con permisos de delegado del buzón local. Antes de seguir estos pasos, debe asegurarse de que está en la última CU 2013 de Exchange o Exchange SP3 RU. Para obtener más información, consulte [Requisitos previos de implementación híbrida](hybrid-deployment-prerequisites-exchange-2013-help.md).

## Exchange 2013

Qué debe hacer para habilitar la compatibilidad con los permisos de buzón delegada depende de una serie de factores. Si mueve los buzones a Office 365 y en ese momento:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Se ha instalado...</th>
<th>Y fue ACLable la sincronización del objeto de la organización...</th>
<th>A continuación, necesitará...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Intercambio de 2013 CU9 o anterior</p></td>
<td><p>Esta característica no está disponible en Exchange 2013 CU9 y anteriores.</p></td>
<td><p>Configurar manualmente cada buzón para admitir las ACL</p></td>
</tr>
<tr class="even">
<td><p>Intercambio de 2013 CU10 o posterior</p></td>
<td><p>Deshabilitado</p></td>
<td><ol>
<li><p>Habilitar la sincronización de objeto ACLable en el nivel de organización</p></li>
<li><p>Habilitar manualmente las ACL en cada buzón movido a Office 365 antes de habilita la sincronización de objetos ACLable en el nivel de organización.</p></li>
</ol>
<p>Se necesita ninguna configuración adicional para buzones de correo que se trasladó a Office 365 después de la sincronización del objeto ACLable está habilitada en el nivel de organización.</p></td>
</tr>
<tr class="odd">
<td><p>Intercambio de 2013 CU10 o posterior</p></td>
<td><p>Habilitado</p></td>
<td><p>No es necesaria ninguna configuración adicional</p></td>
</tr>
</tbody>
</table>


## Habilitar la sincronización de objetos ACLable

Para habilitar la sincronización de objeto ACLable en el nivel de organización, haga lo siguiente.

1.  Instalar la versión más reciente de Azure Active Directory Connect (conectar DAA) en todos los servidores de DAA conectarse. Esto es necesario para permitir DAA conectarse sincronizar los atributos necesarios para admitir permisos híbrido. Puede descargar DAA conectarse desde [Microsoft Azure Active Directory Connect](http://go.microsoft.com/fwlink/p/?linkid=510956).

2.  Abra el Shell de administración de Exchange en un servidor que ejecute la última CU disponible del 2013 Exchange o el CU inmediatamente anterior.

3.  Ejecute el comando siguiente.
    
        Set-OrganizationConfig -ACLableSyncedObjectEnabled $True

Una vez hecho esto, todos los buzones que se desplaza a Office 365 se configurará correctamente para admitir permisos de delegado del buzón. Si los buzones se han movido a Office 365 antes de completar estos pasos, debe habilitar manualmente las ACL en dichos buzones siguiendo los pasos de Habilitar las listas ACL de buzones de correo remotos.


> [!IMPORTANT]
> ACL no están habilitadas en buzones remotos creados en Office 365. Si crea un buzón de correo remoto en Office 365, debe seguir los pasos en la ACL de habilitar en la sección de buzones de correo remoto para habilitar las ACL en ese buzón de correo remoto. Para evitar este paso adicional, recomendamos que cree el buzón en un servidor de Exchange local y, a continuación, mover el buzón a Office 365.



## Habilitar las ACL de buzones de correo remotos

Para habilitar las ACL de buzones de correo que se trasladó a Office 365 antes de habilita la sincronización de objetos ACLable en el nivel de organización, haga lo siguiente.

1.  Abra el Shell de administración de Exchange en un servidor que ejecute la última CU disponible del 2013 Exchange o el CU inmediatamente anterior.

2.  Para habilitar las ACL en un único buzón, ejecute el siguiente comando.
    
        Get-AdUser <Identity> | Set-AdObject -Replace @{msExchRecipientDisplayType=-1073741818}

3.  Para habilitar las ACL en todos los buzones que se trasladó a Office 365, ejecute el siguiente comando.
    
        Get-RemoteMailbox | ForEach { Get-AdUser -Identity $_.Guid | Set-ADObject -Replace @{msExchRecipientDisplayType=-1073741818}}

4.  Para comprobar que los buzones se han actualizado correctamente, ejecute el siguiente comando.
    
        Get-RemoteMailbox | ForEach { Get-AdUser -Identity $_.Guid -Properties msExchRecipientDisplayType | Format-Table -AutoSize DistinguishedName, msExchRecipientDisplayType}

## Exchange 2010

Servidores de Exchange 2010 SP3 admiten la configuración de las ACL de buzones de correo remotos, sin embargo, esta configuración debe establecerse manualmente en cada buzón. A diferencia de las versiones más recientes de Exchange, Exchange 2010 no ofrece la capacidad de establecer esta característica en el nivel de organización. Debe seguir los pasos indicados en los buzones que se hayan colocado previamente a Office 365 y en todos los buzones que se moverán desde un servidor de Exchange 2010 Service Pack 3 para Office 365 en el futuro.

## Habilitar las ACL de buzones de correo remotos

Para habilitar las ACL de buzones de correo que se trasladó a Office 365, haga lo siguiente.

1.  Abra el Shell de administración de Exchange en un servidor que ejecute la última disponible Exchange 2010 SP3 RU o el RU inmediatamente anterior.

2.  Para habilitar las ACL en un único buzón, ejecute el siguiente comando.
    
        Get-AdUser <Identity> | Set-AdObject -Replace @{msExchRecipientDisplayType=-1073741818}

3.  Para habilitar las ACL en todos los buzones que se trasladó a Office 365, ejecute el siguiente comando.
    
        Get-RemoteMailbox | ForEach { Get-AdUser -Identity $_.Guid | Set-ADObject -Replace @{msExchRecipientDisplayType=-1073741818}}

4.  Para comprobar que los buzones se han actualizado correctamente, ejecute el siguiente comando.
    
        Get-RemoteMailbox | ForEach { Get-AdUser -Identity $_.Guid -Properties msExchRecipientDisplayType | Format-Table -AutoSize DistinguishedName, msExchRecipientDisplayType}

