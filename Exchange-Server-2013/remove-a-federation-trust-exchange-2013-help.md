---
title: 'Quitar las confianzas de federación: Exchange 2013 Help'
TOCTitle: Quitar las confianzas de federación
ms:assetid: dc4d126d-b567-470d-a5d0-e1402bf8f369
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ657500(v=EXCHG.150)
ms:contentKeyID: 49895959
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Quitar las confianzas de federación

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-01-04_

Una confianza de federación establece una relación de confianza entre una organización de Microsoft Exchange 2013 y el sistema de autenticación de Azure Active Directory y admite el uso compartido con otras organizaciones federadas de Exchange. Al quitar una confianza de federación de la organización de Exchange local, se deshabilitará el uso compartido federado con otras organizaciones de Exchange y con organizaciones de Office 365 conectadas a su organización como parte de una implementación híbrida. Debe evaluar detenidamente el impacto general para su organización antes de quitar una confianza de federación.

Para conocer tareas de administración adicionales relacionadas con las confianzas de federación, consulte [Procedimientos de la Federación](federation-procedures-exchange-2013-help.md).


> [!IMPORTANT]
> Esta característica de Exchange Server 2013 no es totalmente compatible con Office 365 operado por 21Vianet en China y pueden aplicarse ciertas limitaciones en las características. Para obtener más información, consulte <A href="https://go.microsoft.com/fwlink/?linkid=313640">Acerca de Office 365 operado por 21Vianet</A>.



## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el entrada "Permisos de certificados y federación" en el tema [Permisos de infraestructura de la Shell y de Exchange](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Después de quitar una confianza de federación, puede quitar los registros TXT del servidor DNS público para cada dominio federado. Revise los requisitos para quitar un registro TXT con la organización que aloja sus registros DNS públicos.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## ¿Qué desea hacer?

## Uso del EAC para quitar una confianza de federación

1.  En un servidor de Exchange 2013 de la organización local, vaya a **organización** \> **uso compartido**.

2.  En la sección **Confianza de federación**, haga clic en **Quitar**.

3.  En la advertencia, haga clic en **sí** para confirmar que quiere quitar la confianza de federación.

4.  Después de quitar la confianza de federación, haga clic en **Cerrar**.

## Uso del Shell para quitar una confianza de federación

En este ejemplo, se quita la confianza de federación.

```powershell
Remove-FederationTrust
```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Remove-FederationTrust](https://technet.microsoft.com/es-es/library/dd351153\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la confianza de federación se quitó correctamente, realice una de las siguientes acciones:

  - En EAC, vaya a **organización** \> **uso compartido**. Si la confianza de federación se quitó correctamente, únicamente el botón **Habilitar** estará disponible debajo de **Confianza de federación**.

  - En el Shell, ejecute el siguiente comando para comprobar que la información de la confianza de federación no se devuelva para su organización de Exchange.
    
    ```powershell
    Get-FederationTrust
    ```
    
    Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-FederationTrust](https://technet.microsoft.com/es-es/library/dd351262\(v=exchg.150\)).

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

