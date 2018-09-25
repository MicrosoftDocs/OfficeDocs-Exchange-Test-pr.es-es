---
title: 'Configurar cuotas de almacenamiento para un buzón: Exchange 2013 Help'
TOCTitle: Configurar cuotas de almacenamiento para un buzón
ms:assetid: 5f5fe292-c80e-4a0b-b3e6-e193ea5171d0
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998353(v=EXCHG.150)
ms:contentKeyID: 50556795
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar cuotas de almacenamiento para un buzón

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-07-07_

**Resumen:**  Use el CEF o el shell para configurar las cuotas de almacenamiento de buzones específicos.

Las cuotas de almacenamiento le permiten controlar el tamaño de los buzones de correo y administrar el crecimiento de las bases de datos de buzones de correo. Cuando un buzón alcanza o excede una cuota de almacenamiento específica, Exchange envía una notificación descriptiva al propietario del buzón.


> [!NOTE]
> Las cuotas de almacenamiento se aplican al tamaño de un buzón determinado según lo definido en la propiedad <CODE>TotalItemSize</CODE> al ejecutar el cmdlet <CODE>Get-MailboxStatistics</CODE>. Para obtener más información, consulte <A href="https://technet.microsoft.com/es-es/library/bb124612(v=exchg.150)">Get-MailboxStatistics</A>.



Normalmente, las cuotas de almacenamiento se configuran por base de datos. Esto significa que las cuotas configuradas para una base de datos de buzones de correo se aplican a todos los buzones de correo en esa base de datos. Para obtener más información sobre cómo administrar la configuración de buzones por base de datos, consulte [Administrar bases de datos de buzones en Exchange 2013](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md).

En este tema, se muestra cómo personalizar la configuración de almacenamiento para un buzón de correo específico en vez de usar la configuración de almacenamiento desde la base de datos de buzones de correo. Para otras tareas de administración relacionadas con los buzones de usuario, consulte [Administrar los buzones de usuario](https://technet.microsoft.com/es-es/library/bb123809(v=exchg.150)).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 2 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Sección "Permisos de aprovisionamiento de destinatarios" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso del EAC para configurar las cuotas de almacenamiento de un buzón de correo

1.  En el EAC, vaya a **Destinatarios** \> **Buzones de correo**.

2.  En la lista de buzones de usuario, haga clic en el buzón cuyas cuotas de almacenamiento desea cambiar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades del buzón, haga clic en **Uso del buzón de correo** y, luego, haga clic en **Más opciones**.

4.  Haga clic en **Personalizar la configuración de este buzón** y, luego, configure los siguientes cuadros. El intervalo de valor para la configuración de cuotas de almacenamiento oscila entre 0 y 2047 gigabytes (GB).
    
      - **Emitir una advertencia al llegar a (GB)**: este cuadro muestra el límite máximo de almacenamiento antes de que se emita una advertencia al usuario. Si el tamaño del buzón alcanza o supera el valor especificado, Exchange envía un mensaje de advertencia al usuario.
        

        > [!IMPORTANT]
        > El mensaje asociado a la cuota para <STRONG>Emitir advertencia</STRONG> no se enviará al usuario a menos que el valor de este ajuste sea superior al 50% del valor especificado en la cuota para <STRONG>Prohibir envío</STRONG>. Por ejemplo, si establece la cuota de <STRONG>Prohibir envío</STRONG> en 8 MB, debe establecer la cuota de <STRONG>Emitir advertencia</STRONG> en 4 MB como mínimo. Si no lo hace, el mensaje de la cuota <STRONG>Emitir advertencia</STRONG> no se enviará.

    
      - **Prohibir envío al llegar a (GB)**: este cuadro muestra el límite de *Prohibir envío* del buzón. Si el tamaño del buzón alcanza o supera el límite especificado, Exchange impide que el usuario envíe nuevos mensajes y muestra un mensaje de error descriptivo.
    
      - **Prohibir envío y recepción al llegar a (GB)**: este cuadro muestra el límite de *Prohibir envío y recepción* del buzón. Si el tamaño del buzón alcanza o supera el límite especificado, Exchange impide que el usuario del buzón envíe mensajes nuevos y no entregará ningún mensaje nuevo en el buzón. Todos los mensajes que se envíen al buzón se devolverán al remitente con un mensaje de error descriptivo.

5.  Haga clic en **Guardar** para guardar los cambios.

## Usar el Shell para configurar las cuotas de almacenamiento de un buzón de correo

En este ejemplo, se establecen la cuota de emisión de advertencia, de prohibición de envío y de prohibición de envío y recepción del buzón de correo de Joe Healy en 24.5 GB, 24.75 GB y 25 GB, respectivamente.


> [!NOTE]
> Para garantizar que se use la configuración personalizada del buzón de correo en lugar de los valores predeterminados de la base de datos de buzones de correo, debe establecer el parámetro <EM>UseDatabaseQuotaDefaults</EM> en <CODE>$false</CODE>.


```powershell
Set-Mailbox -Identity "Joe Healy" -IssueWarningQuota 24.5gb -ProhibitSendQuota 24.75gb -ProhibitSendReceiveQuota 25gb -UseDatabaseQuotaDefaults $false
```

En este ejemplo, se establecen la cuota de emisión de advertencia, de prohibición de envío y de prohibición de envío y recepción del buzón de correo de Ayla Kol en 900 megabytes (MB), 950 MB y 1 GB, respectivamente, y se configura el buzón para que use la configuración personalizada.

```powershell
Set-Mailbox -Identity "Ayla Kol" -IssueWarningQuota 900mb -ProhibitSendQuota 950mb -ProhibitSendReceiveQuota 1gb -UseDatabaseQuotaDefaults $false
```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que haya establecido las cuotas de almacenamiento para un buzón correctamente, siga uno de estos procedimientos:

1.  En el EAC, vaya a **Destinatarios** \> **Buzones de correo**.

2.  En la lista de buzones de usuario, haga clic en el buzón cuyas cuotas de almacenamiento desea comprobar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades del buzón, haga clic en **Uso del buzón de correo** y, luego, haga clic en **Más opciones**.

4.  Compruebe que **Personalizar la configuración para este buzón** esté seleccionado.

5.  Compruebe la configuración de las cuotas de almacenamiento.

O bien

Ejecute el siguiente comando en el Shell.

```powershell
Get-Mailbox <identity> | fl IssueWarningQuota,ProhibitSendQuota,ProhibitSendReceiveQuota,UseDatabaseQuotaDefaults
```
