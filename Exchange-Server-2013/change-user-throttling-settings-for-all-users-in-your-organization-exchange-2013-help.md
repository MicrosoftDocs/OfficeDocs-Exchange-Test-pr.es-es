---
title: 'Cambiar configuración de limitación para todos usuarios de organización'
TOCTitle: Cambiar la configuración de limitación para todos los usuarios de la organización
ms:assetid: c45cacfc-768d-4605-9bb0-53e30273fe4d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ863578(v=EXCHG.150)
ms:contentKeyID: 50556879
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Cambiar la configuración de limitación para todos los usuarios de la organización

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-08-05_

Puede controlar el modo en que los usuarios individuales de una organización de Exchange consumen recursos mediante la modificación de la configuración de limitación predeterminada.

El control de cómo los usuarios individuales consumían los recursos era posible en Exchange Server 2010, y esta capacidad se ha ampliado para Exchange Server 2013. La directiva llamada GlobalThrottlingPolicy define la configuración de limitación predeterminada para los usuarios nuevos y existentes de la organización a menos que haya personalizado las directivas de limitación. En muchos casos de implementación típicos de Exchange, la directiva GlobalThrottlingPolicy es la correcta para administrar usuarios.

Para personalizar la configuración de limitaciones que se aplican a todos los usuarios de la organización, cree una nueva directiva de limitación con la asignación del ámbito Organization. Solo se puede cambiar la configuración de limitación predeterminada mediante el uso del Shell.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  10 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el entrada "Limitación de usuario" en el tema [Permisos de rendimiento y estado del servidor](server-health-and-performance-permissions-exchange-2013-help.md).

  - En las nuevas directivas de ámbito Organization, solo debe establecer configuraciones de limitación diferentes a las de la directiva llamada GlobalThrottlingPolicy y a otras directivas de organización. De este modo, se hereda el resto de la configuración de la directiva llamada GlobalThrottlingPolicy, al igual que las actualizaciones a las directivas de limitación que se agreguen en futuras actualizaciones de Exchange. Se recomienda que revise la sección sobre administración de directivas de limitación mediante ámbitos en el tema [Administración de carga de trabajo de Exchange](exchange-workload-management-exchange-2013-help.md) antes de continuar con este procedimiento.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Uso del Shell para cambiar el modo en que los usuarios usan los recursos en toda la organización

En este ejemplo se crea una directiva de limitación que se aplica a todos los usuarios de la organización. Los parámetros que se omiten heredan los valores de la directiva de limitación predeterminada GlobalThrottlingPolicy.

    New-ThrottlingPolicy -Name AllUsersEWSPolicy EwsMaxConcurrency 4 -ThrottlingPolicyScope Organization

Para obtener más información sobre sintaxis y parámetros, consulte [New-ThrottlingPolicy](https://technet.microsoft.com/es-es/library/dd351045\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la directiva de limitación Organization se creó correctamente, siga estos pasos:

1.  Ejecute el siguiente comando.
    
        Get-ThrottlingPolicy | Format-List

2.  Compruebe que la directiva de limitación Organization que acaba de crear aparece en la columna que muestra el objeto GlobalThrottlingPolicy.

3.  Ejecute el siguiente comando.
    
        Get-ThrottlingPolicy | Format-List

4.  Compruebe que las propiedades de la nueva directiva Organization coinciden con el valor o valores configurados.

