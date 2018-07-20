---
title: 'P+F: Centro de administración de Exchange: Exchange 2013 Help'
TOCTitle: 'P+F: Centro de administración de Exchange'
ms:assetid: 3de0042f-74a6-458f-947c-3cd6eeacd6ab
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ552409(v=EXCHG.150)
ms:contentKeyID: 49116167
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# P+F: Centro de administración de Exchange

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Este tema proporciona una lista de las preguntas más frecuentes del nuevo Centro de administración de Exchange (EAC) en Microsoft Exchange Server 2013. ¿Tiene otras preguntas acerca de EAC que no se han respondido aquí? Envíenos un correo electrónico a [Ex2013HelpFeedback@microsoft.com](mailto:ex2013helpfeedback@microsoft.com).

## ¿Fue el EAC desarrollado exclusivamente para Exchange Online?

El EAC da servicio a todas las opciones de implementación de Exchange 2013, incluidos clientes que quieren implementar de forma local, en la nube con Exchange Online o una implementación híbrida.

## ¿Eliminó la Consola de Administración de Exchange (EMC) porque crea una interfaz principal para clientes pequeños y medianos?

El EAC se desarrolló para proporcionar una experiencia de administración única e intuitiva a todos nuestros clientes y se diseñó para ayudar a hacer que la ejecución de las tareas de administración más habituales sea más simple.

Hemos creado una sola interfaz que proporcione un superconjunto de cobertura de escenarios en la consola de administración de Exchange (EMC) y en el Panel de control de Exchange (ECP), y una que se ajuste a los desafíos y escenarios principales de los clientes.

Además, hemos escuchado a clientes de todos tamaños y sus preocupaciones principales fueron las siguientes:

  - El mantenimiento y la descarga de revisiones para usar una herramienta administrativa son los gastos generales operativos para los clientes, lo que, a su vez, incrementa los costos operativos.

  - A medida que aumentaba la movilidad del personal de TI, los clientes querían poder administrar sus entornos desde cualquier lugar, no solamente desde escritorios y servidores donde están instaladas sus herramientas administrativas.

  - Usar varias herramientas para las diferentes opciones de implementación se hace cada vez más complicado e implica un aumento en los costos operativos y de aprendizaje

## ¿El registro de PowerShell y la exposición de cmdlets vuelven a EAC?

Hemos recopilado los comentarios anteriores de los clientes sobre este tema y estamos evaluando la posibilidad de solventarlo en una actualización en el futuro.

## ¿Se reintroducirá la EMC en un próximo Service Pack?

No. Damos un soporte total a la experiencia de EAC.

## ¿Se puede usar la EMC de Exchange 2010 para administrar los objetos de Exchange 2013?

No. No se puede usar la EMC de Exchange 2010 para administrar objetos y servidores Exchange 2013. Mientras que los clientes se actualizan a Exchange 2013, los animamos a que usen el EAC para:

1.  Administrar buzones de correo, servidores y los servicios correspondientes de Exchange 2013.

2.  Ver y actualizar las propiedades y los buzones de Exchange 2010.

3.  Ver y actualizar las propiedades y los buzones de Exchange 2007.

Se recomienda a los clientes usar el EMC de Exchange 2010 para crear y administrar buzones de correo de Exchange 2010.

Se recomienda a los clientes usar el EMC de Exchange 2007 para crear y administrar buzones de correo de Exchange 2007.

Los clientes pueden continuar realizando tareas de administración con el Shell de administración de Exchange y tareas de script.

## ¿Por qué la casilla de búsqueda no está siempre visible?

Como parte de nuestros principios de diseño de Exchange 2013, queríamos ayudar a garantizar que nada le moleste hasta que lo necesite. Esta sencillez está representada en todas nuestras experiencias de usuario final (incluido el EAC). El cuadro de búsqueda se desliza después de hacer clic en el icono. Esto permite más espacio para que el usuario escriba su consulta en el cuadro de texto y también proporciona cuadros desplegables de escritura que aparecen cuando se realiza la concordancia de consulta en tiempo real. Esta mejora nos permite ocultar la complejidad innecesaria sin interceder en la experiencia de administración. Continuaremos mejorando todas nuestras experiencias en base a sus comentarios.

## ¿EAC funcionará en tabletas?

En estos momentos la administración mediante tabletas y dispositivos móviles no es compatible.

## ¿Por qué se abre Exchange 2010 ECP cuando intento acceder a Exchange 2013 EAC?

Si su buzón de correo se encuentra en un servidor de buzones de correo de Exchange 2010, Exchange 2010 ECP se cargará automáticamente en su explorador. Esto es así por diseño. Puede obtener acceso al EAC agregando la versión de Exchange a la dirección URL. Por ejemplo, para acceder al EAC cuyo directorio virtual se aloja en el servidor de acceso de clientes CAS01-NA, use la siguiente dirección URL: `https://CAS01-NA/ecp?ExchClientVer=15`.

## ¿Cómo se limita donde se puede usar el EAC?

Para limitar el acceso de los virus de Internet a la intranet, Exchange proporciona particiones en el nivel del directorio virtual en IIS. Los administradores pueden permitir o denegar explícitamente que los escenarios de administración de TI se realicen desde clientes de Internet externos (por ejemplo, desde clientes que no se unieron a un dominio dentro del firewall corporativo). Para obtener más información, vea [Desactivar el acceso al Centro de administración de Exchange](turn-off-access-to-the-exchange-admin-center-exchange-2013-help.md).

## ¿Qué ha cambiado para el cuadro de herramientas de Exchange 2013?

En Exchange 2007 y Exchange 2010, la EMC contenía el cuadro de herramientas, que proporcionaba acceso a varias herramientas para administrar su organización de Exchange. El cuadro de herramientas de Exchange 2013 se ha recortado considerablemente frente a las versiones anteriores. El Editor de plantillas de detalles, el Analizador de conectividad remota y el Visor de cola continúan disponibles en el cuadro de herramientas de Exchange 2013. Las herramientas restantes se han reciclado o desplazado al EAC.

La tabla siguiente muestra los cambios en el cuadro de herramientas de Exchange 2013:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Herramienta</th>
<th>¿Dónde está ahora?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Best Practices Analyzer (ExBPA)</p></td>
<td><p>El ExBPA se ha retirado. Las comprobaciones de disponibilidad han sustituido al ExBPA para garantizar que su bosque de Active Directory y servidores de Exchange estén preparados para Exchange 2013. Cada tema de comprobación de disponibilidad describe las acciones que puede realizar para solucionar los problemas que se encuentren al ejecutarse las comprobaciones de disponibilidad. Solo debe realizar los pasos detallados en un tema de comprobación de disponibilidad si dicha comprobación de disponibilidad se mostró durante la instalación.</p></td>
</tr>
<tr class="even">
<td><p>Solucionador de problemas del flujo de correo</p></td>
<td><p>El solucionador de problemas de flujo de correo se ha retirado. Ahora puede utilizar la característica de seguimiento de mensajes en el EAC. Vaya a <strong>Flujo de correo</strong>&gt;<strong>Informes de entrega</strong>.</p></td>
</tr>
<tr class="odd">
<td><p>Monitor de rendimiento</p></td>
<td><p>El monitor de rendimiento se ha retirado del cuadro de herramientas. Todavía puede encontrar el monitor de rendimiento en <strong>Herramientas administrativas</strong> en Windows Server 2008 y Windows Server 2012.</p></td>
</tr>
<tr class="even">
<td><p>Solucionador de problemas de rendimiento</p></td>
<td><p>El Solucionador de problemas de rendimiento se ha retirado del cuadro de herramientas.</p></td>
</tr>
<tr class="odd">
<td><p>Visor de registro de enrutamiento</p></td>
<td><p>El Visor de registro de enrutamiento se ha retirado.</p></td>
</tr>
<tr class="even">
<td><p>Consola de administración de carpetas públicas</p></td>
<td><p>Las carpetas públicas ahora se administran desde dentro del EAC. En el EAC, vaya a <strong>Carpetas públicas</strong>.</p></td>
</tr>
<tr class="odd">
<td><p>Editor de usuarios de control de acceso basado en roles (RBAC)</p></td>
<td><p>RBAC ahora se administra desde dentro del EAC. En el EAC, vaya a <strong>Permisos</strong>.</p></td>
</tr>
</tbody>
</table>

