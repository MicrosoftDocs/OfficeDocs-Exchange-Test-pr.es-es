---
title: 'Crear directorio virtual libreta direcciones sin conexión: Exchange 2013 Help'
TOCTitle: Crear un directorio virtual de la libreta de direcciones sin conexión
ms:assetid: 2c70e21f-2b12-414a-9e8c-65634a767c72
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa996917(v=EXCHG.150)
ms:contentKeyID: 49895540
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Crear un directorio virtual de la libreta de direcciones sin conexión

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-16_

El directorio virtual OAB es la distribución de OAB. De forma predeterminada, cuando se instala Microsoft Exchange Server 2013, un directorio virtual nuevo denominado OAB se crea en el sitio web predeterminado interno en Internet Information Services (IIS). Si tiene usuarios de cliente que se conectan a Microsoft Outlook desde fuera del firewall de la organización, puede agregar un sitio web externo. Como alternativa, al ejecutar el cmdlet **New-OABVirtualDirectory** en el Shell, se crea un directorio virtual nuevo denominado OAB en el sitio web predeterminado IIS en el servidor Exchange local.

La creación de un directorio virtual de OAB no es una tarea habitual. Exchange permite un directorio virtual de OAB denominado OAB, y sólo debería crear un directorio virtual de OAB si hay algún problema con el directorio virtual de OAB existente, y se eliminó el directorio virtual de OAB anterior.

Para otras tareas de administración relacionadas con las OAB, consulte [Procedimientos de libretas de direcciones sin conexión](https://docs.microsoft.com/es-es/exchange/address-books/offline-address-books/offline-address-book-procedures).


> [!IMPORTANT]
> Antes de crear un directorio virtual OAB, asegúrese de que los usuarios conocen los cambios realizados. Este procedimiento puede interrumpir el proceso de descarga de la OAB para los usuarios.



## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Libreta de direcciones sin conexión" en el tema [Permisos de libreta de direcciones y dirección de correo electrónico](email-address-and-address-book-permissions-exchange-2013-help.md).

  - El servidor local de Exchange debe tener instalado el rol de servidor Acceso de cliente.

  - Debe existir un sitio web de IIS predeterminado (por ejemplo, /w3svc/1/root).

  - No debe existir un directorio virtual denominado OAB.

  - Aunque la distribución basada en web está habilitada de manera predeterminada y no requiere configuración adicional, se recomienda habilitar capas de sockets seguros (SSL) para el punto de distribución de la OAB.

  - No puede usar el Centro de Administración de Exchange (EAC) para realizar este procedimiento. Debe usar el Shell.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Use el Shell para crear un directorio virtual OAB

Para crear un directorio virtual OAB con todas las configuraciones predeterminadas, puede ejecutar el cmdlet **New-OABVirtualDirectory** sin ningún parámetro. Use el siguiente procedimiento para crear un directorio virtual OAB con la configuración personalizada.


> [!NOTE]
> Al crear un directorio virtual OAB, se recomienda tener habilitado SSL.



En este ejemplo, se crea un directorio virtual OAB en el servidor de acceso de clientes denominado "CASServer01" que tiene habilitado la SSL y una dirección URL externa.

    New-OABVirtualDirectory -Server CASServer01 -RequireSSL $true -ExternalURL "https://www.contoso.com/OAB"

Una vez creado un nuevo directorio virtual OAB, deberá editar la configuración en cada OAB que use la distribución basada en Web para volver a conectarse al directorio virtual OAB. Para obtener más información, consulte [Cambiar el programa de generación de libretas de direcciones sin conexión](https://docs.microsoft.com/es-es/exchange/address-books/offline-address-books/change-address-book-generation-schedule).

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [New-OabVirtualDirectory](https://technet.microsoft.com/es-es/library/bb123735\(v=exchg.150\)).

