---
title: 'Instalar o eliminar de aplicaciones para Outlook en la organización'
TOCTitle: Instalación o eliminación de aplicaciones para Outlook en la organización
ms:assetid: 112f3ef7-9943-4a1e-8a42-e08e8e9f67f4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ943752(v=EXCHG.150)
ms:contentKeyID: 52062005
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Instalación o eliminación de aplicaciones para Outlook en la organización

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2017-02-03_

Puede instalar o eliminar complementos de Outlook de la organización usando el EAC o el Shell.


> [!NOTE]
> De forma predeterminada, después de instalar un complemento en la organización, este estará disponible para todos sus usuarios. Después de la instalación, puede usar el EAC o el Shell para hacer que el complemento sea opcional u obligatorio para todos los usuarios, así como especificar si quiere que esté habilitado o deshabilitado. Para obtener más información sobre cómo cambiar la configuración predeterminada de un complemento, consulte <A href="manage-user-access-to-add-ins-for-outlook-exchange-online-help.md">Administrar el acceso del usuario a aplicaciones para Outlook</A>. Si quiere limitar la disponibilidad de los complementos para determinados usuarios de la organización, use el Shell. Para obtener más información, consulte <A href="manage-user-access-to-add-ins-for-outlook-exchange-online-help.md">Administrar el acceso del usuario a aplicaciones para Outlook</A>.



Para otras tareas de administración, consulte [Aplicaciones para Outlook](add-ins-for-outlook-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada “Aplicaciones para Outlook” en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Puede asignar permisos de administrador para instalar y administrar los complementos de la organización. También puede asignar permisos a los usuarios para que instalen y administren los complementos para su propio uso. Para obtener más información, consulte [Especifique los administradores y los usuarios que pueden instalar y administrar complementos para Outlook](specify-the-administrators-and-users-who-can-install-and-manage-add-ins-for-outlook-exchange-2013-help.md).

  - El acceso a la Tienda Office no se admite para buzones y organizaciones de ciertas regiones. Si no puede ver la opción **Agregar desde la Tienda Office** en el **Centro de administración de Exchange**, que encontrará en **Organización** \> **Complementos** \> ![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"), es posible que no pueda instalar un complemento de Outlook desde una URL o una ubicación de archivo. Para obtener más información, póngase en contacto con su proveedor de servicios.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué quiere hacer?

## Instalación de un complemento de Outlook

## Uso del EAC para agregar un complemento

1.  En el EAC, vaya a **Organización** \> **Complementos**.

2.  Haga clic en **Nuevo**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") y seleccione la ubicación donde quiera instalarlo.
    
      - **Agregar desde la Tienda Office**. En la Tienda Office, seleccione la aplicación que quiera instalar y haga clic en **Agregar**. Las aplicaciones que funcionan con Outlook Web App aparecen en **Complementos para Office y SharePoint** \> **Outlook**.
        

        > [!NOTE]
        > El acceso a la Tienda Office no se admite para buzones y organizaciones de ciertas regiones. Si no puede ver la opción <STRONG>Agregar desde la Tienda Office</STRONG> en el <STRONG>Centro de administración de Exchange</STRONG>, que encontrará en <STRONG>Organización</STRONG> &gt; <STRONG>Complementos</STRONG> &gt; <IMG title="Agregar icono" alt="Agregar icono" src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif">, es posible que no pueda instalar un complemento de Outlook desde una URL o una ubicación de archivo. Para obtener más información, póngase en contacto con su proveedor de servicios.

    
      - **Agregar desde URL**. En **URL**, escriba la URL completa del archivo de manifiesto del complemento que quiera instalar.
    
      - **Agregar desde archivo**. Seleccione **Examinar** y vaya a la ubicación del archivo de manifiesto del complemento que quiera instalar.

3.  Haga clic en **Guardar**.

## Uso del Shell para agregar un complemento

En este ejemplo se muestra cómo agregar un complemento desde una URL.

    New-App -OrganizationApp -Url <URL location for add-in manifest file>

En este ejemplo se muestra cómo agregar un complemento desde un archivo.

    New-App -OrganizationApp -FileData <File location for add-in manifest file>


> [!TIP]
> Al usar el Shell para instalar un complemento en la organización, puede instalarlo y configurar los parámetros al mismo tiempo.



Para información sobre la sintaxis y los parámetros, vea [New-App](https://technet.microsoft.com/es-es/library/jj218722\(v=exchg.150\)).

## Eliminación de un complemento de Outlook

## Uso del EAC para eliminar un complemento

1.  En el EAC, vaya a **Organización** \> **Complementos**.

2.  En la vista de lista, seleccione la aplicación que quiere quitar y haga clic en **Eliminar**![Eliminar icono](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Eliminar icono").

## Uso del Shell para eliminar un complemento

Puede usar el Shell para eliminar un complemento de la organización.


> [!NOTE]
> Ejecute el siguiente comando para buscar los nombres para mostrar y los identificadores de todos los complementos de Outlook instalados en su organización.



    Get-App -OrganizationApp |FL DisplayName,AppID

Ejecute el comando siguiente para eliminar el complemento personalizado Finance Test de la organización.

    Remove-App -OrganizationApp -Identity <GUID for Finance Test Add-in>

Para información sobre la sintaxis y los parámetros, vea [Remove-App](https://technet.microsoft.com/es-es/library/jj218709\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para ver los complementos instalados en la organización, siga uno de estos pasos:

  - En el EAC, vaya a **Organización** \> **Complementos** y consulte la lista de complementos instalados.

  - En el Shell, ejecute `Get-App` y consulte la lista de complementos instalados.

