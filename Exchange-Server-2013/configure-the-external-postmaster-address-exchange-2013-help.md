---
title: 'Configurar la dirección externa del postmaster: Exchange 2013 Help'
TOCTitle: Configurar la dirección externa del postmaster
ms:assetid: 6b0c8675-3238-462d-8973-b52305fb90d2
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb430765(v=EXCHG.150)
ms:contentKeyID: 52062034
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar la dirección externa del postmaster

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

La dirección externa del administrador de correo se usa como remitente de los mensajes y las notificaciones generados por el sistema que se envían a remitentes externos a su organización de Microsoft Exchange Server 2013. Un remitente externo es cualquier remitente que tenga una dirección de correo electrónico en un dominio que no esté configurado como un dominio aceptado en su organización.

De forma predeterminada, el valor de la configuración de la dirección del administrador de correo externo está en blanco. Este valor predeterminado provoca el comportamiento siguiente en la organización Exchange:

  - La dirección externa del administrador de correo es postmaster@\<*Dominio aceptado predeterminado*\> para todos los servidores de buzones y servidores de transporte perimetral suscritos.

  - La dirección externa del administrador de correo es postmaster@\<*Edge Transport server FQDN*\> para todos los servidores de transporte perimetral no suscritos.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 15 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Configuración de transporte" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Al configurar una dirección externa del administrador de correo personalizada, dicho valor se aplica a todos los servidores de buzones Exchange 2013 y los servidores de transporte de concentradores Exchange 2010 en la organización de Exchange. Sin embargo, ese valor no se replica a los servidores de transporte perimetral. Si especifica un valor personalizado para la dirección externa del administrador de correo, debe configurar de forma manual esa dirección en cualquier servidor de transporte perimetral.

  - Si tiene algún servidor de transporte de concentradores o de transporte perimetral de Exchange 2007 en la organización, debe configurar la dirección externa del administrador de correo en cada servidor usando el cmdlet **Set-TransportServer**. Para más información, consulte [Administración de la dirección externa del administrador de correo](https://go.microsoft.com/fwlink/?linkid=279922).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## ¿Qué desea hacer?

## Usar el EAC para configurar la dirección externa del administrador de correo

1.  En el EAC, vaya a **Flujo de correo** \> **Conectores de recepción** \> **Más opciones** ![Icono Más opciones](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icono Más opciones") \> **Configuración de transporte de la organización** \> **Entrega**.

2.  En el campo **Dirección externa del administrador de correo**, escriba la dirección de correo SMTP, por ejemplo, `postmaster@contoso.com`. Si quiere devolver la dirección externa del administrador de correo a su valor predeterminado, elimine cualquier valor existente y deje el campo el blanco.

3.  Cuando haya terminado, haga clic en **Guardar**.

## Usar el Shell para configurar la dirección del administrador de correo externo

Para configurar la dirección del administrador de correo externo, utilice la siguiente sintaxis.

```powershell
Set-TransportConfig -ExternalPostmasterAddress <postmaster address>
```

Por ejemplo, para establecer la dirección del administrador de correo externo en el valor `postmaster@contoso.com`, ejecute el siguiente comando:

```powershell
Set-TransportConfig -ExternalPostmasterAddress postmaster@contoso.com
```

Para restablecer la dirección del administrador de correo externo al valor predeterminado, ejecute el siguiente comando:

```powershell
Set-TransportConfig -ExternalPostmasterAddress $null
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la dirección del administrador de correo externo se configuró correctamente, siga estos pasos:

1.  Ejecute el comando siguiente en el servidor de buzones para comprobar el valor de la dirección externa del administrador de correo:
    
    ```powershell
    Get-TransportConfig | Format-List ExternalPostmasterAddress
    ```

2.  Desde una cuenta de correo electrónico externa, envíe un mensaje a su organización de Exchange que generará una notificación de estado de entrega (DSN). Por ejemplo, puede configurar una regla de transporte para enviar un informe de no entrega (NDR) para un mensaje de ese remitente que contenga determinadas palabas clave. Compruebe que la dirección de correo del remitente en el DSN coincide con el valor que ha especificado.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

