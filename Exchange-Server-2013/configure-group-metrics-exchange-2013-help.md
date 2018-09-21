---
title: 'Configurar métricas de grupo: Exchange 2013 Help'
TOCTitle: Configurar métricas de grupo
ms:assetid: 76ccd6a7-e2ec-42f4-9ab3-e8cc257ac896
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ649327(v=EXCHG.150)
ms:contentKeyID: 49895723
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar métricas de grupo

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-04-08_

La información sobre correo que proporciona información acerca del tamaño de los grupos de distribución y los grupos de distribución dinámica confían en los datos de métricas de grupo. Los datos de métricas de grupo se generan en los servidores de buzones designados. Para obtener más información acerca de las métricas de grupos, consulte [Grupo métricas y sugerencias de correo electrónico](group-metrics-and-https://docs.microsoft.com/es-es/exchange/clients-and-mobile-in-exchange-online/mailtips/mailtips).

Puede habilitar o deshabilitar la generación de métricas de grupo en un servidor de buzones.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 10 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Mediciones de grupos" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Los datos de métrica de grupos solamente se utilizan para la información sobre correo. Asegúrese de que la información sobre correo para métricas de grupo esté habilitada en su organización. Para conocer los pasos detallados, consulte [Administrar sugerencias de correo electrónico para las relaciones de la organización](https://docs.microsoft.com/es-es/exchange/clients-and-mobile-in-exchange-online/mailtips/manage-mailtips-for-organization-relationships).

  - Solo puede usar el Shell para realizar este procedimiento.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Usar el Shell para habilitar o deshabilitar la generación de métricas de grupo


> [!NOTE]
> De manera predeterminada, los datos de métricas de grupo se generan en cualquier servidor responsable por la generación de la libreta de direcciones sin conexión (OAB). Estos ejemplos únicamente son necesarios para las organizaciones que no utilizan OAB.



Para habilitar o deshabilitar la generación de métricas de grupo en un servidor de buzones, ejecute el siguiente comando:

```powershell
Set-MailboxServer <ServerIdentity> -ForceGroupMetricsGeneration <$true | $false>
```

En este ejemplo se habilita la generación de métricas de grupo en el servidor de buzones denominado MBX1.

```powershell
Set-MailboxServer MBX1 -ForceGroupMetricsGeneration $true
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para verificar que ha habilitado o deshabilitado correctamente la generación de métricas de grupo en una organización que no utiliza OAB, siga el procedimiento siguiente:

1.  Ejecute el siguiente comando:
    
    ```powershell
Get-MailboxServer <ServerIdentity> | Format-List ForceGroupMetricsGeneration
```

2.  Compruebe que la configuración que se muestra sea la que seleccionó.

