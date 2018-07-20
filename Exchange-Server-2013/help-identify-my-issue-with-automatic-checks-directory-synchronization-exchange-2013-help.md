---
title: 'Ayudar a identificar mi problema con comprobaciones automáticas: sincronización de directorios: Exchange 2013 Help'
TOCTitle: 'Ayudar a identificar mi problema con comprobaciones automáticas: sincronización de directorios'
ms:assetid: e6ea900a-c382-444c-a8ce-54d392bfeca3
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn793977(v=EXCHG.150)
ms:contentKeyID: 62633070
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ayudar a identificar mi problema con comprobaciones automáticas: sincronización de directorios

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Puede usar las siguientes comprobaciones automáticas para validar la configuración y actualizar su entorno.

Si ya posee una cuenta de usuario de Office 365, seleccione Iniciar sesión. No necesita una cuenta de identificación de Azure. Quizás se le pida una cuenta de usuario nuevamente cuando se ejecutan las comprobaciones. Si es así, la cuenta de usuario está en el formato de nombredeusuario@iniciosesióndeoffice365.dominio y la contraseña.


> [!NOTE]
> Si recibe mensajes de advertencia de sincronización en el portal de Office 365, los errores en los registros de sucesos del servidor de sincronización o correos electrónicos de notificación de sincronización de directorio negativa de Microsoft Online Services, puede que tenga algún tipo de problema de sincronización de directorios. El <A href="https://aka.ms/dsup">Solucionador de problemas de sincronización de directorio</A> es una herramienta de diagnóstico basado en Web diseñada para ayudar a identificar los tipos comunes de errores de sincronización y prescribir soluciones dirigidas a los problemas encontrados. El Solucionador de problemas de sincronización de directorios se debe ejecutar en el servidor de sincronización de directorios.



## Requisitos previos

Comprobaremos si tiene instalados Ayudante para el inicio de sesión de Azure Active Directory y Módulo Azure Active Directory para Windows PowerShell.

El Ayudante para el inicio de sesión de Azure Active Directory viene en dos versiones: [32 bits](https://go.microsoft.com/fwlink/?linkid=286261) y [64 bits](https://go.microsoft.com/fwlink/?linkid=286262).

El Módulo Azure Active Directory para Windows PowerShell viene en dos versiones: [32 bits](https://go.microsoft.com/fwlink/?linkid=286258) y [64 bits](https://go.microsoft.com/fwlink/?linkid=286259).

## Comprobaciones de sincronización de directorios


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Aplicación</p></td>
<td><p>Síntoma</p></td>
<td><p>Comprobación</p></td>
</tr>
<tr class="even">
<td><p>Sincronización de directorios</p></td>
<td><p>No sé si todas mis cuentas de usuario de Active Directory cumplen con los requisitos para la sincronización de directorios.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834884">Ejecutar esta comprobación</a></p></td>
</tr>
<tr class="odd">
<td><p>Sincronización de directorios</p></td>
<td><p>No sé si los niveles funcionales de dominio de Active Directory están correctamente configurados para Windows Server 2003 o versiones posteriores.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834876">Ejecutar esta comprobación</a></p></td>
</tr>
<tr class="even">
<td><p>Sincronización de directorios</p></td>
<td><p>No sé si se llevó a cabo la sincronización de directorios en las últimas tres horas.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834887">Ejecutar esta comprobación</a></p></td>
</tr>
<tr class="odd">
<td><p>Sincronización de directorios</p></td>
<td><p>No sé si Active Directory tiene algún atributo de usuario duplicado que bloqueará la sincronización de directorios.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834883">Ejecutar esta comprobación</a></p></td>
</tr>
<tr class="even">
<td><p>Sincronización de directorios</p></td>
<td><p>No sé si está habilitada la sincronización de directorios en Office 365.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834887">Ejecutar esta comprobación</a></p></td>
</tr>
<tr class="odd">
<td><p>Sincronización de directorios</p></td>
<td><p>No sé si puedo implementar limitaciones de oferta de Office 365.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834920">Ejecutar esta comprobación</a></p></td>
</tr>
<tr class="even">
<td><p>Sincronización de directorios</p></td>
<td><p>No sé si puedo implementar Office 365 y usar la configuración de sincronización de directorios predeterminada.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834876">Ejecutar esta comprobación</a></p></td>
</tr>
<tr class="odd">
<td><p>Sincronización de directorios</p></td>
<td><p>No sé si uso Active Directory y si es compatible con la sincronización de directorios.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834886">Ejecutar esta comprobación</a></p></td>
</tr>
<tr class="even">
<td><p>Sincronización de directorios</p></td>
<td><p>No sé si todos mis grupos de Active Directory cumplen con los requisitos para la sincronización de directorios.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834913">Ejecutar esta comprobación</a></p></td>
</tr>
</tbody>
</table>

