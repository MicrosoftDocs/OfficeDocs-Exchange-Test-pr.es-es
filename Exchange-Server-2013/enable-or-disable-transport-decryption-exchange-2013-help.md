---
title: 'Habilitar o deshabilitar el descifrado de transporte: Exchange 2013 Help'
TOCTitle: Habilitar o deshabilitar el descifrado de transporte
ms:assetid: 4663f54e-dd0a-4a42-983e-8765e2adc412
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd638126(v=EXCHG.150)
ms:contentKeyID: 49895603
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar o deshabilitar el descifrado de transporte

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Descifrado de transporte habilitación permite al agente de reglas de transporte en Microsoft Exchange Server 2013 servidores de buzón para tener acceso al contenido de los mensajes protegidos por Information Rights Management (IRM). Como resultado, otros agentes de transporte pueden tener acceso al contenido del mensaje y posiblemente realizar cambios en él. Por ejemplo, el agente de reglas de transporte que necesite inspeccionar el contenido del mensaje y aplicar reglas de transporte (por ejemplo, las reglas que se aplican una renuncia al mensaje). Para descifrar los mensajes protegidos mediante IRM correctamente, debe agregar el buzón de entrega federada al grupo de superusuarios configurado en el servidor de [Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx) .


> [!IMPORTANT]
> Los miembros del grupo de superusuarios obtienen una licencia de uso de propietario cuando solicitan una licencia al clúster de AD&nbsp;RMS. Esto les permite descifrar todos los contenidos protegidos por RMS que fueron creados por ese clúster de AD&nbsp;RMS.



Al habilitar el descifrado de transporte, puede especificar la siguiente configuración:

  - **Obligatorio**   Se rechazan los mensajes que no pueden descifrarse y se devuelve un informe de no entrega (NDR) al remitente.

  - **Opcional**   Utiliza un enfoque de mayor esfuerzo con respecto al descifrado. Los mensajes se descifran si es posible, pero se entregan incluso si no se pueden descifrar. Esta es la configuración predeterminada.

Para obtener más información acerca del descifrado de transporte, consulte [Descifrado de transporte](transport-decryption-exchange-2013-help.md).

Para otras tareas de administración relacionadas con IRM, consulte [Procedimientos de Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Protección de derechos" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Existe un servidor AD RMS en el bosque de Active Directory y es accesible.

  - Debe agregar el buzón de entrega federada al grupo de superusuarios en el clúster de AD RMS. Para obtener información detallada, consulte [Agregar el buzón de la federación para el grupo de usuarios de AD RMS Super](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md).

  - No puede usar el Centro de administración de Exchange (EAC) para habilitar el descifrado de transporte. Debe usar el Shell.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Usar el Shell para habilitar el descifrado de transporte

En este ejemplo, se habilita el descifrado de transporte de la organización de Exchange 2013. Los mensajes que no se pueden descifrar se rechazan y se devuelve un NDR al remitente.

```powershell
Set-IRMConfiguration -TransportDecryptionSetting Mandatory
```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-IRMConfiguration](https://technet.microsoft.com/es-es/library/dd979792\(v=exchg.150\)).

## Usar el Shell para deshabilitar el descifrado de transporte

En este ejemplo, se deshabilita el descifrado de transporte de la organización de Exchange 2013.

```powershell
Set-IRMConfiguration -TransportDecryptionSetting Disabled
```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-IRMConfiguration](https://technet.microsoft.com/es-es/library/dd979792\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que ha habilitado o deshabilitado el descifrado de transporte, use el cmdlet **Get-IRMConfiguration** y compruebe el valor de la propiedad *JournalDecryptionEnabled*.

Para ver un ejemplo sobre cómo comprobar la configuración de IRM, consulte [Examples](https://technet.microsoft.com/es-es/e1821219-fe18-4642-a9c2-58eb0aadd61a\(exchg.150\)#examples) en **Get-IRMConfiguration**.

