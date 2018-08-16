---
title: 'Configurar propiedad distribuír libreta dirección conexión: Exchange 2013 Help'
TOCTitle: Configurar propiedades de distribución de libreta de direcciones sin conexión
ms:assetid: 8df985e9-75ba-47ea-9cc3-aa98a5d8acf4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb123710(v=EXCHG.150)
ms:contentKeyID: 49895766
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.ClientAccess.OabDistributionGeneralPage
ms.translationtype: MT
---

# Configurar propiedades de distribución de libreta de direcciones sin conexión

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2012-10-14_

Para cada punto de distribución de libreta de direcciones sin conexión (OAB) en Exchange, es posible configurar dos direcciones URL: una dirección URL interna a la que solo se puede obtener acceso desde la red corporativa interna y una dirección URL externa a la que se puede obtener acceso desde Internet.

Para otras tareas de administración relacionadas con las OAB, consulte [Procedimientos de libretas de direcciones sin conexión](offline-address-book-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Libreta de direcciones sin conexión" en el tema [Permisos de libreta de direcciones y dirección de correo electrónico](email-address-and-address-book-permissions-exchange-2013-help.md).

  - No puede usar el Centro de Administración de Exchange (EAC) para realizar este procedimiento. Debe usar el Shell.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Uso de Shell para configurar las propiedades de distribución de la OAB

En este ejemplo se establece el intervalo de sondeo para la distribución de la OAB en el directorio virtual de la OAB llamado OAB (sitio web predeterminado) en seis horas.

    Set-OABVirtualDirectory "OAB (Default Web Site)" -PollInterval 360

En este ejemplo se establece el punto de distribución externa en https://contoso.com/OAB para el directorio virtual de la OAB predeterminado denominado OAB (sitio web predeterminado).

    Set-OABVirtualDirectory "OAB (Default Web Site)" -ExternalUrl https://contoso.com/OAB

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-OabVirtualDirectory](https://technet.microsoft.com/es-es/library/bb124707\(v=exchg.150\)).

## Para obtener más información

[Libretas de direcciones sin conexión](offline-address-books-exchange-2013-help.md)

