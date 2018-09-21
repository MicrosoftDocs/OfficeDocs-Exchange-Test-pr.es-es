---
title: 'Configurar retención de elementos eliminados y cuotas elementos recuperables'
TOCTitle: Configurar la retención de elementos eliminados y las cuotas de elementos recuperables
ms:assetid: de7d667a-1c93-4364-a4f9-2aa5e3678b12
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee364752(v=EXCHG.150)
ms:contentKeyID: 50556896
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar la retención de elementos eliminados y las cuotas de elementos recuperables

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Cuando un usuario elimina elementos de la carpeta predeterminada Elementos eliminados utilizando las acciones Eliminar, Mayús+Eliminar o **Vaciar carpeta de elementos eliminados**, los elementos se mueven a la carpeta **Elementos recuperables\\Eliminaciones**. El tiempo que los elementos eliminados permanecen en esta carpeta se basa en la configuración de la retención de elementos eliminados establecida para la base de datos del buzón o para el buzón. De forma predeterminada, una base de datos de buzones está configurada para retener los elementos eliminados durante 14 días, y la cuota de advertencia de elementos recuperables y la cuota de elementos recuperables están configuradas a 20 gigabytes (GB) y 30 GB respectivamente.


> [!NOTE]
> Antes del tiempo de retención de elementos eliminados transcurre, Outlook de Microsoft y Microsoft OfficeOutlook Web App, los usuarios pueden recuperar elementos eliminados mediante la característica recuperar elementos eliminados. Para obtener más información acerca de estas características, vea el tema "Recuperar elementos eliminados" para <A href="https://go.microsoft.com/fwlink/p/?linkid=198206">Outlook</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=198207">Outlook Web App</A>.



Puede utilizar el Shell para configurar la retención de los elementos eliminados y las cuotas de elementos recuperables para un buzón o una base de datos de buzones. La configuración de retención de elementos eliminados se omite cuando un buzón se coloca en retención local o en retención por juicio.

Para obtener más información acerca de la retención de elementos eliminados, la carpeta Elementos recuperables, la retención local y la retención por juicio, consulte [Carpeta Elementos recuperables](recoverable-items-folder-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Administración de registros de mensajes" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Configurar la retención de elementos eliminados para un buzón

**Uso de la EAC para configurar la retención de elementos eliminados para un buzón**

1.  Vaya a **Destinatarios** \> **Buzones de correo**.

2.  En la vista de lista, seleccione un buzón y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades del buzón, haga clic en **Uso del buzón**, **Más opciones** y, a continuación, seleccione una de las siguientes opciones
    
      - **Usar la configuración de retención predeterminada de la base de datos del buzón**   Elija esta configuración para usar los valores de retención de elementos eliminados configurados para la base de datos de buzones.
    
      - **Personalizar la configuración para este buzón**   Use esta opción para configurar los valores de retención de elementos eliminados para el buzón.
        
        **Guardar los elementos eliminados durante (días)**   Este cuadro muestra la cantidad de tiempo que se retienen los elementos eliminados antes de que se eliminen permanentemente y el usuario no pueda recuperarlos. Al crear el buzón, este valor se basa en los valores de retención de elementos eliminados configurados para la base de datos de buzones. De manera predeterminada, se configura una base de datos de buzón para que retenga los elementos eliminados por 14 días. El intervalo de valores para esta propiedad oscila entre 0 y 24.855 días.
    
      - **No eliminar permanentemente los elementos hasta después de realizada la copia de seguridad de la base de datos**   Seleccione esta casilla de verificación para evitar que los buzones y los mensajes de correo electrónico se eliminen hasta que se haya realizado la copia de seguridad de la base de datos de buzones en la que está ubicado el buzón.

**Uso del Shell para configurar la retención de elementos eliminados de un buzón**

En este ejemplo se configura el buzón de April Stewart para retener los elementos eliminados durante 30 días.

```powershell
Set-Mailbox -Identity - "April Stewart" -RetainDeletedItemsFor 30
```

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)).

## Uso del Shell para configurar las cuotas de elementos recuperables para un buzón


> [!NOTE]
> No se puede usar la EAC para configurar las cuotas de elementos recuperables para un buzón.



En este ejemplo se configura una cuota de advertencia de elementos recuperables de 12 GB y una cuota de elementos recuperables de 15 GB para el buzón de April Stewart.

    Set-Mailbox -Identity "April Stewart" -RecoverableItemsWarningQuota 12GB -RecoverableItemsQuota 15GB -UseDatabaseQuotaDefaults $false


> [!NOTE]
> Para configurar un buzón de modo que utilice cuotas de elementos recuperables diferentes a la base de datos de buzones en la que se encuentra, se deberá establecer el parámetro <EM>UseDatabaseQuotaDefaults</EM> en <CODE>$false</CODE>.



Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)).

## Uso del Shell para configurar la retención de elementos eliminados de una base de datos de buzones


> [!NOTE]
> No se puede usar la EAC para configurar la retención de elementos eliminados para una base de datos de buzones.



En este ejemplo se configura un período de retención de elementos eliminados de 10 días para la base de datos de buzones MDB2.

```powershell
Set-MailboxDatabase -Identity MDB2 -DeletedItemRetention 10
```

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Set-MailboxDatabase](https://technet.microsoft.com/es-es/library/bb123971\(v=exchg.150\)).

## Uso del Shell para configurar las cuotas de elementos recuperables para una base de datos de buzones


> [!NOTE]
> No se puede usar la EAC para configurar las cuotas de elementos recuperables para una base de datos de buzones



En este ejemplo se configura una cuota de advertencia de elementos recuperables de 15 GB y una cuota de elementos recuperables de 20 GB en la base de datos de buzones MDB2.

```powershell
Set-MailboxDatabase -Identity MDB2 -RecoverableItemsWarningQuota 15GB -RecoverableItemsQuota 20GB
```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-MailboxDatabase](https://technet.microsoft.com/es-es/library/bb123971\(v=exchg.150\)).

