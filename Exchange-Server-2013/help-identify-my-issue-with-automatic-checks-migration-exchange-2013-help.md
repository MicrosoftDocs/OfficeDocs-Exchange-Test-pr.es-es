---
title: 'Ayudar a identificar mi problema con comprobaciones automáticas: migración: Exchange 2013 Help'
TOCTitle: 'Ayudar a identificar mi problema con comprobaciones automáticas: migración'
ms:assetid: c1cd235d-8e8b-44a8-862d-9d36dc3a44c3
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn793980(v=EXCHG.150)
ms:contentKeyID: 62633068
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ayudar a identificar mi problema con comprobaciones automáticas: migración

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

Las comprobaciones de esta página lo ayudarán a identificar algunos de los desafíos más comunes de la configuración. Puede usar las siguientes comprobaciones automáticas para validar la configuración y actualizar su entorno.

Si ya tiene una cuenta de usuario de Office 365, seleccione **Iniciar sesión**. No necesita una cuenta de identificación de Azure. Quizás se le pida una cuenta de usuario nuevamente cuando se ejecutan las comprobaciones. Si es así, la cuenta de usuario está en el formato de nombredeusuario@iniciosesióndeoffice365.dominio y la contraseña.

## Requisitos previos

Comprobaremos si tiene instalados Ayudante para el inicio de sesión de Azure Active Directory y Módulo Azure Active Directory para Windows PowerShell.

El Ayudante para el inicio de sesión de Azure Active Directory viene en dos versiones: [32 bits](https://go.microsoft.com/fwlink/?linkid=286261) y [64 bits](https://go.microsoft.com/fwlink/?linkid=286262).

El Módulo Azure Active Directory para Windows PowerShell viene en dos versiones: [32 bits](https://go.microsoft.com/fwlink/?linkid=286258) y [64 bits](https://go.microsoft.com/fwlink/?linkid=286259).

## Agregar comprobaciones de dominios


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
<td><p>Tamaños de los buzones de correo</p></td>
<td><p>Me gustaría determinar si mis usuarios usan los tamaños predeterminados de los buzones de correo de la organización para poder planear mejor mi migración.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834877">Ejecutar esta comprobación</a></p></td>
</tr>
<tr class="odd">
<td><p>Bosque único</p></td>
<td><p>Estoy intentando evaluar si puedo migrar las cuentas de mis usuarios con la sincronización de directorios.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834875">Ejecutar esta comprobación</a></p></td>
</tr>
<tr class="even">
<td><p>Modo funcional de dominio</p></td>
<td><p>No sé si estoy preparado para integrar ADFS 2.0/Inicio de sesión único</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834876">Ejecutar esta comprobación</a></p></td>
</tr>
<tr class="odd">
<td><p>Carpetas públicas</p></td>
<td><p>No sé si tengo carpetas públicas para migrar a Office 365.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834896">Ejecutar esta comprobación</a></p></td>
</tr>
</tbody>
</table>

