---
title: 'Configurar IRM para la búsqueda y la exhibición de documentos electrónicos local de Exchange: Exchange 2013 Help'
TOCTitle: Configurar IRM para la búsqueda y la exhibición de documentos electrónicos local de Exchange
ms:assetid: d96790e9-93ad-4a56-b90f-2dbfa2f2073c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg588319(v=EXCHG.150)
ms:contentKeyID: 49895950
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar IRM para la búsqueda y la exhibición de documentos electrónicos local de Exchange

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-11-16_

En Microsoft Exchange Server 2013, pueden configurar Information Rights Management (IRM) de manera que Exchange Search pueda indizar los mensajes protegidos de IRM.

Cuando los miembros del grupo de roles de administración de detección usa una búsqueda de [Exhibición de documentos electrónicos en contexto](in-place-ediscovery-exchange-2013-help.md), los mensajes protegidos por IRM aparecen en los resultados de búsqueda y se copian en el buzón de correo de detección especificado en la búsqueda. Además, los miembros del grupo de roles de administración de detección pueden usar Outlook Web App para obtener acceso a los mensajes protegidos por IRM que se copiaron en el buzón de detección como resultado de la búsqueda de detección.


> [!NOTE]
> Los miembros del grupo de funciones Administración de detección no pueden obtener acceso a los mensajes protegidos por IRM que se exportaron desde un buzón de detección a otro o a un archivo .pst. Sólo se puede obtener acceso a los mensajes protegidos por IRM en un buzón de detección mediante Outlook Web App.



Para otras tareas de administración relacionadas con IRM, consulte [Procedimientos de Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Protección de derechos" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - IRM debe estar configurado en su organización de Exchange 2013. Para obtener más información, consulte [Habilitar o deshabilitar IRM para mensajes internos](enable-or-disable-irm-for-internal-messages-exchange-2013-help.md).

  - El buzón de federación se debe agregar al grupo de superusuarios de Active Directory Rights Management Services (AD RMS). Para obtener más información, consulte [Agregar el buzón de la federación para el grupo de usuarios de AD RMS Super](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md).

  - No puede utilizar el centro de administración de Exchange (EAC) para configurar IRM para la búsqueda y la detección electrónica local de Exchange. Debe usar el Shell.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Use el Shell para configurar IRM para Exchange Search

En este ejemplo, se configura IRM para permitir que Exchange Search indice los mensajes protegidos por IRM.


> [!NOTE]
> De forma predeterminada, el parámetro <EM>SearchEnabled</EM> se establece en <CODE>$true</CODE>. Para deshabilitar los mensajes protegidos por IRM, configúrelo en <CODE>$false</CODE>. Deshabilitar la indización de los mensajes protegidos por IRM evita que se aparezcan en los resultados de búsqueda cuando los usuarios busquen en el buzón o cuando los administradores de detección usen la detección electrónica local.



    Set-IRMConfiguration -SearchEnabled $true

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Set-IRMConfiguration](https://technet.microsoft.com/es-es/library/dd979792\(v=exchg.150\)).

## Usar el Shell para configurar IRM para la detección electrónica local

En este ejemplo se habilita a los miembros del grupo de roles de administración de detección para que tengan acceso a los mensajes protegidos por IRM que residen en el buzón de detección.


> [!NOTE]
> De forma predeterminada, el parámetro <EM>EDiscoverySuperUserEnabled</EM> se establece en <CODE>$true</CODE>. Para deshabilitar el acceso a los mensajes protegidos por IRM para los miembros del grupo de funciones Administración de detección, configúrelo en <CODE>$false</CODE>.



    Set-IRMConfiguration -EDiscoverySuperUserEnabled $true

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Set-IRMConfiguration](https://technet.microsoft.com/es-es/library/dd979792\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que ha configurado correctamente IRM para la búsqueda y la detección electrónica local de Exchange, use el cmdlet **Get-IRMConfigurtaion** para obtener la información de configuración de IRM. Para ver un ejemplo de cómo obtener la configuración de IRM, consulte [Examples](https://technet.microsoft.com/es-es/e1821219-fe18-4642-a9c2-58eb0aadd61a\(exchg.150\)#examples) en **Get-IRMConfiguration**.

