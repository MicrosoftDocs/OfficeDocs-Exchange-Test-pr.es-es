---
title: 'Simplificar la dirección URL de Outlook Web App para Office 365 híbrido: Exchange 2013 Help'
TOCTitle: Simplificar la dirección URL de Outlook Web App para Office 365 híbrido
ms:assetid: 19449aee-3796-4298-90c6-c7579b8d2f7a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Mt791749(v=EXCHG.150)
ms:contentKeyID: 74259168
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Simplificar la dirección URL de Outlook Web App para Office 365 híbrido

 

_**Última modificación del tema:**2016-11-11_

Obtenga información sobre cómo configurar una dirección URL para Outlook en la web (Outlook Web App) para los usuarios de buzón de correo en la nube en un entorno híbrido.

Una preocupación importante para las organizaciones que se mueven a Office 365 desde Exchange local es la experiencia del usuario. Los usuarios necesitan un acceso ininterrumpido a sus buzones, independientemente de dónde o cuándo se mueve su buzón. Teniendo esto en cuenta, la coexistencia de Outlook en la web (anteriormente denominado Outlook Web App) es importante.

Considere el siguiente escenario: una empresa usa una implementación híbrida para mover algunos de sus buzones de Exchange local a Office 365. El viernes antes del traslado, los usuarios accedieron a sus buzones locales mediante la dirección URL https://mail.contoso.com/owa. El lunes después del traslado, esos mismos usuarios ahora obtienen un error cuando intentan tener acceso a sus buzones mediante esa dirección URL.

Para permitir que los usuarios afectados se conecten a sus buzones con Outlook en la web, tiene dos opciones:

  - **Indique a los usuarios la nueva dirección URL (por ejemplo, https://outlook.com/owa/contoso.com)**   Los problemas con esta opción son:
    
      - La dirección URL es compleja.
    
      - La experiencia puede presentar interrupciones para los usuarios afectados.

  - **Configure la opción de configuración TargetOWAUrl en la relación de la organización**   Los problemas con esta opción son:
    
      - El punto de conexión de los buzones en la nube es externo (no se encuentra en el dominio que los usuarios esperan).
    
      - El punto de conexión requiere el dominio en la dirección URL (para distinguir entre las ofertas para consumidores de Office 365 Empresa y outlook.com).
    
      - El punto de conexión provoca que los usuarios vean advertencias de falta de coincidencia en el certificado.

Para que los usuarios no tengan estos problemas con los buzones en la nube, realice los siguientes pasos:

1.  **Crear un registro CNAME en DNS (por ejemplo, cloudowa.contoso.com) que señale a mail.office365.com**
    
      - Asegúrese de crear este registro CNAME en su DNS interno y externo (público), ya que los usuarios pueden conectarse desde conexiones de Internet internas o externas.
    
      - En nuestro ejemplo, se usa el dominio contoso.com en la solicitud (se quita la parte cloudowa). Esto significa que no necesita especificar el dominio en la dirección URL.

2.  **Configurar el redireccionamiento de Outlook en la web en la relación de la organización local**   Para hacer esto, use la siguiente sintaxis en el Shell de administración de Exchange en Exchange local:
    
        Set-OrganizationRelationship -TargetOWAUrl http://<CNAME value>/owa
    
    Por ejemplo, si el registro CNAME que ha creado en el paso 1 es cloudowa.contoso.com, ejecute el siguiente comando:
    
        Set-OrganizationRelationship -TargetOWAUrl http://cloudowa.contoso.com/owa
    
    **Notas:**
    
      - Use http, no https.
    
      - Se necesita el valor final /owa en la relación de la organización, pero los usuarios no necesitan escribir /owa en la dirección URL.

## Varias solicitudes de autenticación

Los usuarios pueden recibir varias solicitudes de autenticación dependiendo de:

  - Desde dónde se conectan (conexiones de Internet internas o externas).

  - Si el equipo está unido a un dominio o no.

  - Si está usando la federación de identidades en su entorno híbrido.

La experiencia de solicitudes de autenticación que los usuarios pueden esperar se describe en la siguiente tabla.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Método de autenticación</th>
<th>Equipo cliente</th>
<th>Experiencia de solicitudes de autenticación</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Federación de identidades</p></td>
<td><p>Conexión a Internet interna</p></td>
<td><p>Solicitud única</p></td>
</tr>
<tr class="even">
<td><p>Federación de identidades</p></td>
<td><p>Conexión a Internet externa</p></td>
<td><p>Solicitud doble</p></td>
</tr>
<tr class="odd">
<td><p>Sin federación de identidades</p></td>
<td><p>Unido a un dominio (interno o externo)</p></td>
<td><p>Solicitud doble</p></td>
</tr>
<tr class="even">
<td><p>Con o sin federación de identidades</p></td>
<td><p>No está unido a un dominio (interno o externo)</p></td>
<td><p>Solicitud doble</p></td>
</tr>
</tbody>
</table>


**Nota:** La federación de identidades requiere que el punto de conexión de AD FS esté configurado en la zona de intranet de Internet Explorer como se describe en el tema [https://go.microsoft.com/fwlink/p/?linkid=834460](https://go.microsoft.com/fwlink/p/?linkid=83446), y que AD FS esté configurado según las instrucciones generales de Office 365.

