---
title: 'Administrar dominios remotos: Exchange 2013 Help'
TOCTitle: Administrar dominios remotos
ms:assetid: 41a86907-bd9e-40d0-94d3-6deb95a0bffa
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997639(v=EXCHG.150)
ms:contentKeyID: 52061814
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.NewRemoteDomainWizardForm.NewRemoteDomainWizardPage
ms.translationtype: HT
---

# Administrar dominios remotos

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-04-13_

Los dominios remotos son dominios SMTP externos a la organización de Microsoft Exchange. Puede crear entradas de dominio remoto para definir la configuración de mensajes transferidos entre la organización de Exchange y dominios externos específicos. La configuración de la entrada de dominio remota de un dominio externo concreto sustituye la configuración del dominio remoto predeterminado que se aplica normalmente a todos los destinatarios externos. La configuración de dominio remoto es global para la organización de Exchange.

Si quita una entrada de dominio remoto, la configuración de transferencia de mensajes se deja de aplicar a los mensajes enviados al dominio remoto. La eliminación de una entrada de dominio remoto no deshabilita el flujo de correo para el dominio remoto. Una vez quitada una entrada de dominio remoto, la configuración del dominio remoto predeterminado se aplica a los mensajes nuevos enviados a dicho dominio. No puede quitar el dominio remoto predeterminado.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  10 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Dominios remotos" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Solo puede usar el Shell para realizar este procedimiento.

  - No puede crear un dominio remoto para un espacio de dirección configurado como dominio aceptado para la organización. Por ejemplo, si la organización acepta correo para fabrikam.com, no se puede crear un dominio remoto para fabrikam.com.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Uso del Shell para crear un dominio remoto

Para crear una nueva entrada de dominio remoto, utilice la siguiente sintaxis.

    New-RemoteDomain -Name <Descriptive Name> -DomainName <SMTP address space>

En este ejemplo se crea una entrada de dominio remoto para mensajes enviados al dominio contoso.com.

    New-RemoteDomain -Name Contoso -DomainName contoso.com

En este ejemplo se crea una entrada de dominio remoto para mensajes enviados al dominio fabrikam.com y todos sus subdominios.

    New-RemoteDomain -Name Fabrikam -DomainName *.fabrikam.com

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que el dominio remoto se creó correctamente, siga estos pasos:

1.  Ejecute el comando **Get-RemoteDomain** y compruebe que dicho dominio aparece en la lista.

2.  Ejecute el comando `Get-RemoteDomain <Remote Domain Name> | Format-List` para comprobar la configuración del nuevo dominio remoto. Envíe un mensaje de prueba a un destinatario en el espacio de direcciones especificado en la nueva entrada de dominio remoto y compruebe que la configuración del mensaje coincide con la especificada por la nueva entrada de dominio remoto.

## Uso del Shell para configurar un dominio remoto

Para establecer la configuración de una entrada de dominio remoto, se usa el cmdlet **Set-RemoteDomain**. Hay muchas configuraciones diferentes relacionadas con las respuestas automáticas, el formato y la codificación de mensajes y otros tipos de configuración de mensajes. Para obtener más información, consulte [Set-RemoteDomain](https://technet.microsoft.com/es-es/library/aa997857\(v=exchg.150\)).

Para configurar dominios remotos para casos concretos, consulte los siguientes temas:

  - [Configurar las respuestas “fuera de la oficina” desde dominios remotos](configure-remote-domain-out-of-office-replies-exchange-2013-help.md)

  - [Configurar respuestas automáticas de dominio remoto](configure-remote-domain-automatic-replies-exchange-2013-help.md)

  - [Configurar informes de mensajes de dominio remoto](configure-remote-domain-message-reporting-exchange-2013-help.md)

## Uso del Shell para quitar un dominio remoto

Para quitar una entrada de dominio remoto, utilice la siguiente sintaxis.

    Remove-RemoteDomain <RemoteDomainName>

En este ejemplo se quita la entrada de dominio remoto denominada Contoso

    Remove-RemoteDomain Contoso

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que el dominio remoto se eliminó correctamente, siga estos pasos:

1.  Ejecute el comando **Get-RemoteDomain** y compruebe que dicho dominio no aparece en la lista.

2.  Ejecute el comando `Get-RemoteDomain Default | Format-List` para comprobar la configuración del dominio remoto predeterminado. Envíe un mensaje de prueba a un destinatario en el espacio de direcciones especificado en el dominio remoto eliminado y compruebe que la configuración del mensaje coincide con la especificada por el dominio remoto predeterminado.

