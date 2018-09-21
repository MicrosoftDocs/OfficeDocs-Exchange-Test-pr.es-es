---
title: 'Quitar una relación de la organización: Exchange 2013 Help'
TOCTitle: Quitar una relación de la organización
ms:assetid: ff211394-f58b-4da7-bb3a-df6abcb5950e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ657513(v=EXCHG.150)
ms:contentKeyID: 49896041
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Quitar una relación de la organización

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-01-04_

Con una relación de organización, los usuarios de la organización de Exchange pueden compartir la información de disponibilidad del calendario con una organización de Office 365 o con otra organización de Exchange local. Una relación de organización se puede quitar para deshabilitar el uso compartido de calendario con esa otra organización.

Para poder compartir calendarios con otra organización, debe configurar una relación de autenticación con el sistema de autenticación de Azure Active Directory (también conocida como "federación") y debe cumplir unos requisitos de software mínimos. Para obtener más información acerca del uso compartido federado, consulte [Uso compartido](sharing-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Sección "Permisos de uso compartido y Calendario" del tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## ¿Qué desea hacer?

## Usar el Centro de administración de Exchange para quitar una relación de la organización

1.  En un servidor de Exchange 2013 de la organización local, vaya a **organización** \> **uso compartido**.

2.  En **Uso compartido de la organización**, seleccione una relación de organización y, luego, haga clic en **Eliminar**![Eliminar icono](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Eliminar icono") para quitar la relación de la organización.

3.  En la advertencia que aparece, haga clic en **sí**.

## Usar el Shell para quitar una relación de la organización

En este ejemplo se quita la relación de la organización Contoso de la organización de Exchange

```powershell
Remove-OrganizationRelationship -Identity "Contoso"
```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Remove-OrganizationRelationship](https://technet.microsoft.com/es-es/library/ee332362\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la relación de la organización se eliminó correctamente, siga uno de estos pasos:

  - En el Centro de administración de Exchange, vaya a **Organización** \> **Uso compartido** y compruebe que no se muestre la relación de la organización en la vista de la lista en **Uso compartido de la organización**.

  - Ejecute el siguiente comando de Shell para comprobar que se quitó la información de la relación de la organización.
    
    ```powershell
Get-OrganizationRelationship | Format-List
```


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


