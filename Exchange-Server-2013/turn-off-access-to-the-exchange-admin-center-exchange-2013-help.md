---
title: 'Desactivar acceso al Centro de administración de Exchange: Exchange 2013 Help'
TOCTitle: Desactivar el acceso al Centro de administración de Exchange
ms:assetid: 49f4fa77-1722-4703-81c9-8724ae0334fb
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ218639(v=EXCHG.150)
ms:contentKeyID: 49116194
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Desactivar el acceso al Centro de administración de Exchange

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2013-05-20_

Por motivos de seguridad, puede que algunas organizaciones deseen restringir el acceso al Centro de administración de Exchange (EAC) a los usuarios procedentes de Internet. En este procedimiento se muestra cómo desactivar el acceso al EAC. Este procedimiento no evita que otros usuarios tengan acceso a las Opciones en Outlook Web App.


> [!NOTE]
> Este procedimiento deshabilita el acceso de administrador del EAC completamente en el servidor CAS donde se aplican los pasos. Si habilita el administrador del EAC para usuarios internos, debería instalar un servidor CAS separado y configurarlo para que solo se encargue de solicitudes internas mediante el siguiente comando:<BR><CODE>Set-ECPVirtualDirectory -Identity "InternalCAS\ecp (default web site)" -AdminEnabled $True</CODE>




> [!WARNING]
> El procedimiento se aplica solo a las implementaciones locales de Exchange Server 2013.



## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Conectividad del Centro de administración de Exchange" en el tema [Permisos de infraestructura de la Shell y de Exchange](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - No puede usar la EAC para realizar este proceso. Debe usar el Shell.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Usar el Shell para desactivar el acceso a Internet al EAC

En este ejemplo se desactiva el acceso al Centro de administración de Exchange en el servidor CAS01.

    Set-ECPVirtualDirectory -Identity "CAS01\ecp (default web site)" -AdminEnabled $false

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-EcpVirtualDirectory](https://technet.microsoft.com/es-es/library/dd297991\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que el acceso al EAC se desactivó correctamente, siga estos pasos:

1.  En el explorador de Internet, escriba la dirección URL interna o externa de su organización para tener acceso a Outlook Web App, pero reemplace el identificador **/owa** por **/ecp**. Por ejemplo, si la URL externa para tener acceso a Outlook Web App es https://primary.tailspintoys.com/owa, use https://primary.tailspintoys.com/ecp.

2.  Si el acceso se desactiva, recibirá un error del tipo **404: sitio web no encontrado**.

