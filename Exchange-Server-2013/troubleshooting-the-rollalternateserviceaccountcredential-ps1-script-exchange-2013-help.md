---
title: 'Solución de problemas del script RollAlternateServiceAccountCredential.ps1'
TOCTitle: Solución de problemas del script RollAlternateServiceAccountCredential.ps1
ms:assetid: 2bbf36d3-eb89-4f92-a8de-259a7cb64d62
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ff808310(v=EXCHG.150)
ms:contentKeyID: 63918677
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Solución de problemas del script RollAlternateServiceAccountCredential.ps1

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-01-14_

Este tema proporciona soluciones e información sobre errores comunes que podrían ocurrir al utilizar la secuencia de comandos RollAlternateServiceAccountPassword.ps1.

## No se pueden actualizar uno o más de los servidores de acceso de clientes con la contraseña

## Problema

Cuando utiliza los parámetros *ToEntireForest* o *ToArrayMembers* con la secuencia de comandos, en algunos casos, es posible que no se actualicen uno o más servidores de acceso de clientes.

## Solución

Compruebe los servidores que la secuencia de comandos tendrán como destino los servidores necesarios; utilice el cmdlet **Get-ClientAccessArray**, como muestra el siguiente ejemplo.

    Get-ClientAccessArray | fl members

Si el servidor que no se puede actualizar pertenece a la matriz de Acceso de clientes y aún no se actualiza correctamente, vuelva a ejecutar la instalación de Exchange y agregue el rol del servidor de acceso de clientes al servidor nuevamente. También puede especificar los servidores individuales al destino mediante el parámetro *ToSpecificServers*.

## Algunos servidores no responden a la secuencia de comandos

## Problema

En algunos casos, los servidores no se pueden actualizar debido a errores transitorios, como una conexión de red incorrecta.

## Solución

Compruebe que los servidores en cuestión se encuentren en red y con conectividad de Active Directory y, a continuación, pruebe la secuencia de comandos nuevamente.

## Algunos miembros de la matriz están fuera de servicio durante un período prolongado

## Problema

Si el servidor está fuera de rotación por un período más prolongado pero aún es miembro de la matriz según lo determina el cmdlet **Get-ClientAccessArray**, es posible que el uso de los parámetros *ToArrayMembers* y *ToEntireForest* afecte la funcionalidad de la secuencia de comandos. El mismo problema ocurrirá si el servidor ha tenido un error permanente pero no se ha quitado correctamente de su implementación.

## Solución

Para resolver este problema, quite el servidor de su implementación mediante la instalación de Exchange o ejecute la secuencia de comandos en modo atendido hasta que se pueda quitar el servidor.

Si el servidor solo estará inactivo durante un breve período de tiempo y no desea quitar Exchange permanentemente, podrá ajustar la secuencia de comandos para que se ejecute con servidores específicos mediante el parámetro *ToSpecificServers*, de modo que solo se destine a servidores activos. Opcionalmente, puede quitar el servicio de acceso de clientes RPC del objeto Active Directory del servidor que no responde mediante el cmdlet **Remove-ClientAccessArray**, como muestra el siguiente ejemplo.

    Remove-RPCClientAccess -Server Server.Contoso.com

Después de haber quitado el servicio de acceso de clientes RPC, el servidor no volverá como un miembro de matriz en [Get-ClientAccessArray](https://technet.microsoft.com/es-es/library/dd297976\(v=exchg.150\)) y la secuencia de comandos no será el destino. En cuanto el servidor esté en funcionamiento nuevamente, podrá volver a agregar el servicio de acceso de clientes RPC mediante el cmdlet **New-RpcClientAccess**. Cuando se vuelva a agregar el servicio de acceso de clientes RPC, asegúrese de reiniciar el servicio de la libreta de direcciones de Microsoft Exchange en el servidor afectado.


> [!WARNING]
> Antes de quitar el servicio de acceso de clientes RPC del servidor, consulte el tema <A href="https://technet.microsoft.com/es-es/library/dd298151(v=exchg.150)">Remove-RPCClientAccess</A>.



## Para obtener más información

Para obtener más información acerca de cómo usar la autenticación Kerberos con una matriz del servidor Acceso de cliente o una solución de equilibrio de carga, consulte los temas siguientes:

  - [Configurar la autenticación de Kerberos para servidores de acceso de cliente con equilibrio de carga](configuring-kerberos-authentication-for-load-balanced-client-access-servers-exchange-2013-help.md)

  - [Uso del script RollAlternateserviceAccountCredential.ps1 en el Shell](using-the-rollalternateserviceaccountcredential-ps1-script-in-the-shell-exchange-2013-help.md)

