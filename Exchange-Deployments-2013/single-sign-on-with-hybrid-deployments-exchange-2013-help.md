---
title: 'Inicio de sesión único con implementaciones híbridas: Exchange 2013 Help'
TOCTitle: Inicio de sesión único con implementaciones híbridas
ms:assetid: 050606f9-718d-4a1f-b7a6-50b08c6e9e07
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Hh563846(v=EXCHG.150)
ms:contentKeyID: 48268927
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Inicio de sesión único con implementaciones híbridas

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2016-01-29_

El inicio de sesión único permite a los usuarios acceder tanto a la organización local como a organizaciones de Office 365 con un solo nombre de usuario y contraseña. Ofrece a los usuarios una experiencia de inicio de sesión con la que están familiarizados y permite a los administradores controlar con facilidad las directivas de cuenta para buzones de la organización de Exchange Online mediante herramientas de administración de Active Directory locales. Aunque no tiene que configurar una implementación híbrida con el inicio de sesión único habilitado, se recomienda que lo haga. Sin el inicio de sesión único, los usuarios tendrán que recordar dos conjuntos diferentes de credenciales, uno para la organización local y otro para Office 365. A continuación se indican otras ventajas del inicio de sesión único:

  - **Archivado de Exchange Online**   Cuando se implementa el inicio de sesión único, se solicita a los usuarios de Outlook local sus credenciales cuando acceden por primera vez al contenido archivado en la organización de Exchange Online. Sin embargo, los usuarios pueden evitar temporalmente la solicitud de credenciales en el futuro seleccionando "guardar contraseña". De este modo, solo se volverán a pedir las credenciales cuando se cambie la contraseña de cuenta local. Si el inicio de sesión único no está implementado en las organizaciones de Exchange y el Archivado de Exchange Online está habilitado, el nombre principal de usuario (UPN) local debe coincidir con su cuenta de Exchange Online, y los usuarios siempre deberán introducir las credenciales locales cuando accedan al archivo.

  - **Control de directivas**   Puede controlar las directivas de cuentas mediante Active Directory, que le ofrece la posibilidad de administrar las directivas de contraseñas, restricciones de estación de trabajo, controles de bloqueo y mucho más sin tener que llevar a cabo tareas adicionales en su organización Office 365.

  - **Menor número de llamadas al soporte técnico** en todas las compañías, las contraseñas olvidadas constituyen una fuente habitual de llamadas de soporte técnico. Si los usuarios tienen que recordar menos contraseñas, hay menos probabilidad de que las olviden.

Tiene dos opciones al implementar el inicio de sesión único: la sincronización de contraseña y los Servicios de federación de Active Directory (AD FS). Azure Active Directory Connect proporciona ambas opciones. Se recomienda usar el método de sincronización de contraseña, a menos que existan necesidades específicas que requieran AD FS. La sincronización de contraseña proporciona muchas de las ventajas de AD FS, pero sin la complejidad de su implementación. En la tabla siguiente se muestran algunas ventajas y desventajas de cada opción.


> [!NOTE]
> De forma predeterminada, si implementa AD&nbsp;FS y sus servidores de AD&nbsp;FS locales no son accesibles desde Internet por cualquier motivo, Office 365 volverá a la sincronización de contraseña para autenticar a los usuarios. Esto permite a los usuarios con buzones de correo de Office 365 seguir trabajando sin interrupciones incluso si los servidores locales no están disponibles.



Para obtener más información sobre cada opción, consulte [Opciones para el inicio de sesión de los usuarios en Azure AD Connect](http://go.microsoft.com/fwlink/p/?linkid=723514)


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Método de inicio de sesión único</p></th>
<th><p>Ventajas</p></th>
<th><p>Desventajas</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Sincronización de contraseña (recomendado)</p></td>
<td><ul>
<li><p>Mucho menos complejo que AD FS</p></li>
<li><p>Los usuarios pueden iniciar sesión en Office 365 aunque la implementación local de Active Directory no esté disponible.</p></li>
<li><p>Se requieren menos servidores adicionales para implementar la sincronización de contraseña.</p></li>
<li><p>No se requieren certificados de terceros.</p></li>
<li><p>No se requiere el acceso externo a la implementación local de Active Directory a través de AD FS.</p></li>
<li><p>La implementación a menudo puede realizarse en unas pocas horas.</p></li>
</ul></td>
<td><ul>
<li><p>Si se deshabilita una cuenta de usuario en la implementación local de Active Directory, no se deshabilita en Office 365. Debe deshabilitar manualmente la cuenta en el Portal de administración de Office 365.</p></li>
<li><p>Requiere una implementación local de Active Directory. No se admiten otros servicios de directorio.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>AD FS</p></td>
<td><ul>
<li><p>Los cambios de contraseña son inmediatos.</p></li>
<li><p>Si se deshabilita a un usuario en la implementación local de Active Directory, se deshabilita su acceso a la red local y su cuenta de Office 365.</p></li>
<li><p>Admite servicios de directorio que no sean Active Directory.</p></li>
<li><p>Admite implementaciones de gran tamaño y muy variadas.</p></li>
<li><p>Admite la autenticación en dos fases.</p></li>
</ul></td>
<td><ul>
<li><p>Requiere más servidores, al menos uno de los cuales debe residir en la red perimetral.</p></li>
<li><p>Requiere que una dirección IP pública y el puerto TCP 443 se abran en el firewall.</p></li>
<li><p>Se requiere conectividad con la implementación local de Active Directory para detectar cambios en las contraseñas de cuentas y con una cuenta recientemente habilitada o deshabilitada.</p></li>
</ul></td>
</tr>
</tbody>
</table>

