---
title: 'Habilitar o deshabilitar el servicio de IRM en servidores de acceso de cliente'
TOCTitle: Habilitar o deshabilitar el servicio Information Rights Management en los servidores de acceso de cliente
ms:assetid: c7ce069b-a572-4755-90a3-7105472e4c83
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd876938(v=EXCHG.150)
ms:contentKeyID: 49895903
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Habilitar o deshabilitar el servicio Information Rights Management en los servidores de acceso de cliente

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Cuando se habilita Information Rights Management (IRM) en los servidores de acceso de cliente, se activan las siguientes características:

  - Microsoft Office Outlook Web App

  - IRM en Microsoft Exchange ActiveSync

Cuando IRM está habilitado en los servidores de acceso de cliente, los usuarios de Outlook Web App pueden proteger los mensajes por IRM aplicando una plantilla de [Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/es-es/library/hh831364.aspx) creada en su clúster de AD RMS. Los usuarios de Outlook Web App también pueden ver mensajes protegidos por IRM y documentos adjuntos admitidos. Antes de habilitar IRM en los servidores Acceso de cliente, debe agregar el buzón de correo de la federación al grupo de superusuarios en el clúster de AD RMS.


> [!IMPORTANT]
> Los miembros del grupo de superusuarios obtienen una licencia de uso de propietario cuando solicitan una licencia al clúster de AD&nbsp;RMS. Esto les permite descifrar todo el contenido protegido de RMS por ese clúster.



Para obtener información acerca de otras tareas de administración relacionadas con IRM, consulte [Procedimientos de Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Configuración de Information Rights Management (IRM)" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Un clúster de AD RMS se debe instalar en el bosque de Active Directory.

  - El buzón Federación se ha agregado al grupo de superusuarios AD RMS. Para obtener instrucciones detalladas, consulte [Agregar el buzón de la federación para el grupo de usuarios de AD RMS Super](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md).

  - Las características de IRM se deben habilitar para la organización. Para obtener instrucciones detalladas, consulte [Habilitar o deshabilitar IRM para mensajes internos](enable-or-disable-irm-for-internal-messages-exchange-2013-help.md).

  - Puede utilizar el cmdlet **Set-IRMConfiguration** para habilitar o deshabilitar IRM en Outlook Web App e IRM en Exchange ActiveSync para toda la organización de Exchange o en niveles específicos.
    
    Puede controlar IRM en Outlook Web App en los siguientes niveles:
    
      - **Directorio virtual de Per-Outlook Web App**   Para habilitar o deshabilitar IRM en Outlook Web App para un directorio virtual de Outlook Web App, use el cmdlet **Set-OWAVirtualDirectory** y establezca el parámetro *IRMEnabled* en `$false` o `$true` (predeterminado). Este permite deshabilitar IRM en Outlook Web App para un directorio virtual en un servidor de acceso de cliente Exchange 2013, mientras está habilitado en otro directorio virtual en un servidor de acceso de cliente distinto.
    
      - **Directiva de buzón de Per-Outlook Web App**   Para habilitar o deshabilitar IRM en Outlook Web App para una directiva de buzón de Outlook Web App, use el cmdlet **Set-OWAMailboxPolicy** y establezca el parámetro *IRMEnabled* en `$false` o `$true` (predeterminado). Esto permite habilitar IRM en Outlook Web App para un grupo de usuarios y deshabilitarlo para otro grupo de usuarios mediante la asignación de una directiva de buzón de Outlook Web App diferente.
    
    También puede controlar IRM en Exchange ActiveSync mediante la directiva de buzón de Exchange ActiveSync. Para deshabilitar o habilitar IRM en Exchange ActiveSync para una directiva de buzón de Exchange ActiveSync, utilice el cmdlet **Set-ActiveSyncMailboxPolicy** y establezca el parámetro *IRMEnabled* en `$false` o `$true` (opción predeterminada). Esto permite habilitar IRM en Exchange ActiveSync para un grupo de usuarios y deshabilitarlo para otro grupo de usuarios mediante la asignación de una directiva de buzón de Exchange ActiveSync.

  - No puede usar el Centro de Administración de Exchange (EAC) para habilitar o deshabilitar IRM en los servidores de acceso de cliente. Debe usar el Shell.

## ¿Qué desea hacer?

## Uso del shell para habilitar IRM en los servidores de acceso de cliente

Este ejemplo habilita IRM en un servidor de acceso de cliente para una organización de Exchange.

```powershell
Set-IRMConfiguration -ClientAccessServerEnabled $true
```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-IRMConfiguration](https://technet.microsoft.com/es-es/library/dd979792\(v=exchg.150\)).

## Utilice el shell para deshabilitar IRM en los servidores de acceso de cliente

Este ejemplo deshabilita IRM en un servidor de acceso de cliente para una organización de Exchange.

```powershell
Set-IRMConfiguration -ClientAccessServerEnabled $false
```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-IRMConfiguration](https://technet.microsoft.com/es-es/library/dd979792\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para verificar que haya habilitado o deshabilitado correctamente IRM en los servidores de acceso de cliente, realice lo siguiente:

  - Ejecute el cmdlet **Get-IRMConfiguration** y verifique el valor de la propiedad *ClientAccessServerEnabled*.
    
    Para conocer un ejemplo para recuperar la configuración IRM, consulte [Examples](https://technet.microsoft.com/es-es/e1821219-fe18-4642-a9c2-58eb0aadd61a\(exchg.150\)#examples) en **Get-IRMConfiguration**.

  - Uso de Outlook Web App para crear o leer un mensaje protegido por IRM.

