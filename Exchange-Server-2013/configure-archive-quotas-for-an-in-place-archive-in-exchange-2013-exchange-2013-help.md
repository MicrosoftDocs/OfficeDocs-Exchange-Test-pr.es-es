---
title: 'Configurar cuotas de archivo para un archivo local en Exchange 2013'
TOCTitle: Configurar cuotas de archivo para un archivo en contexto (local)
ms:assetid: f10e77c7-e1d4-415a-bef9-cb3f00e74c34
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee633489(v=EXCHG.150)
ms:contentKeyID: 50556907
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar cuotas de archivo para un archivo en contexto (local)

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-12-04_

En las implementaciones locales, los archivos locales se crean con cuotas de almacenamiento ilimitadas de manera predeterminada. Debido a esto, es necesario editar las propiedades de un buzón para establecer cuotas de almacenamiento para el archivo. Puede establecer las siguientes cuotas para un archivo:

  - **Cuota de advertencia de archivo**   Cuando un archivo local supera la cuota de advertencia de archivo especificada, se registra un evento para el administrador de Exchange y se envía un mensaje de advertencia al buzón del usuario.

  - **Cuota de archivo**   Cuando un archivo local supera la cuota de archivo especificada, los mensajes ya no se mueven al archivo y se envía un mensaje de advertencia al buzón del usuario.

Para obtener más información acerca de los archivos locales, consulte [Archivado local en Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  5 minutos.

  - En el Centro de administración de Exchange (EAC), puede usar una lista desplegable con valores fijos para configurar la cuota de archivo y la cuota de advertencia de archivo. Si desea establecer alguna de las cuotas en un valor que no aparezca en el EAC, use el Shell.

  - Configure la cuota de advertencia de archivo en un valor inferior a la cuota de archivo. En función de la tasa de crecimiento de archivo de un usuario, la diferencia entre la cuota de advertencia de archivo y la cuota de archivo debe ser la suficiente como para que el usuario realice las acciones adecuadas, como eliminar elementos del archivo o solicitar que un administrador o personal del departamento de soporte técnico aumenten la cuota de archivo.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Sección "Permisos de aprovisionamiento de destinatarios" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Usar la EAC para configurar la cuota de archivo y la cuota de advertencia de archivo para un buzón

1.  Vaya a **Destinatarios** \> **Buzones de correo**

2.  En la vista de lista, seleccione un buzón,

3.  En el panel de detalles, en **Archivo local**, haga clic en **Ver detalles**.

4.  En **Buzón de correo de archivo**, use las listas **Valor de cuota (GB)** y **Emitir advertencia al llegar a (GB)** para seleccionar los valores deseados.

5.  Haga clic en **Aceptar**.

## Usar el Shell para configurar la cuota de archivo y la cuota de advertencia de archivo para un buzón

En este ejemplo se establece la cuota de archivo del buzón de Chris Ashton en 10 gigabytes (GB) y, una vez alcanzado dicho límite, el usuario recibe un mensaje de advertencia que le informa de que el archivo local está lleno y ya no se podrán mover más elementos al mismo. En este ejemplo también se establece una cuota de advertencia de archivo de 9,5 GB, lo que significa que cuando se alcance esta cifra, el usuario recibirá un mensaje de advertencia que le informará de que el archivo local está prácticamente lleno.

```powershell
Set-Mailbox -Identity "Chris Ashton" -ArchiveQuota 10GB -ArchiveWarningQuota 9.5GB
```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si habilitó un archivo local para un buzón existente correctamente, siga uno de estos procedimientos:

  - En el EAC, vaya a **Destinatarios**  \> **Buzones de correo** y, a continuación, seleccione el buzón que desee. En el panel de detalles, en **Archivo local**, haga clic en **Ver detalles** y compruebe la configuración de cuota del archivo.

  - En el Shell, ejecute el siguiente comando para mostrar la información de cuota del archivo.
    
  ```powershell
  Get-Mailbox <Name> | FL Name,Archive*Quota
  ```