---
title: 'Centro de administración de Exchange en Exchange 2013: Exchange 2013 Help'
TOCTitle: Centro de administración de Exchange en Exchange 2013
ms:assetid: a9aea11a-6ba3-4f4a-a76e-79072e7cfc7d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150562(v=EXCHG.150)
ms:contentKeyID: 48268533
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Centro de administración de Exchange en Exchange 2013

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-17_

El Centro de Administración de Exchange (EAC) es la consola de administración basada en web en Microsoft Exchange Server 2013 optimizada para las implementaciones de Exchange locales, en línea o híbridas de Exchange. El EAC reemplaza a la Consola de Administración de Exchange (EMC) y al Panel de Control de Exchange (ECP), que eran las dos interfaces que se usaban para administrar Exchange Server 2010.

Una ventaja que ofrece un EAC basada en web es que puede realizar particiones del acceso a Internet y a intranet desde el directorio virtual de ECP IIS. Con esta funcionalidad, puede controlar si los usuarios tienen permiso para tener acceso a Internet al EAC desde fuera de su organización, y continuar permitiendo que un usuario final acceda a las opciones de Outlook Web App. Para obtener más información, consulte [Desactivar el acceso al Centro de administración de Exchange](turn-off-access-to-the-exchange-admin-center-exchange-2013-help.md).

¿Busca la versión de Exchange Online de este tema? Vea [Centro de administración de Exchange en Exchange Online](https://technet.microsoft.com/es-es/library/jj200743\(v=exchg.150\)).

¿Busca la versión de Protección en línea de Exchange de este tema? Vea [Centro de administración de Exchange en Exchange Online Protection](https://technet.microsoft.com/es-es/library/jj723141\(v=exchg.150\)).

Contenido

Acceso a EAC

Elementos comunes de la interfaz de usuario en EAC

Exploradores compatibles

## Acceso a EAC

Debido a que EAC ahora es una consola de administración basada en web, necesitará acceder a ella mediante el uso de su explorador web usando la dirección URL del directorio virtual de ECP. En la mayoría de los casos la URL del EAC será similar a:

  - **Dirección URL interna: `https://<CASServerName>/ecp`**   La URL interna se usa para acceder al EAC desde dentro del firewall de la organización.

  - **Dirección URL externa: `https://mail.contoso.com/ecp`**   La URL externa se usa para acceder al EAC desde fuera del firewall de la organización. Algunas organizaciones pueden desactivar el acceso externo a EAC. Para obtener información más detallada, consulte [Desactivar el acceso al Centro de administración de Exchange](turn-off-access-to-the-exchange-admin-center-exchange-2013-help.md).

Para ubicar la URL interna o externa del EAC, puede usar el cmdlet [Get-EcpVirtualDirectory](https://technet.microsoft.com/es-es/library/dd351058\(v=exchg.150\)). Para obtener información más detallada, consulte [Encontrar las direcciones URL internas y externas para el Centro de Administración de Exchange](find-the-internal-and-external-urls-for-the-exchange-admin-center-exchange-2013-help.md).

Si se encuentra en un escenario de coexistencia, donde ejecute Exchange Server 2010 y Exchange Server 2013 en la misma organización y su buzón de correo todavía se encuentra alojado en el servidor de buzones de correo de Exchange 2010, el explorador utilizará de manera predeterminada el ECP de Exchange Server 2010. Puede acceder al EAC al agregar la versión de Exchange a la dirección URL. Por ejemplo, para acceder a EAC cuyo directorio virtual está hospedado en el servidor Acceso de cliente CAS15-NA, utilice la siguiente dirección URL: `https://CAS15-NA/ecp/?ExchClientVer=15`. Por el contrario, si desea acceder a Exchange 2010 ECP y su buzón de correo reside en un servidor de buzones de correo Exchange 2013, use la siguiente URL: `https://CAS14-NA/ecp/?ExchClientVer=14`.

## Elementos comunes de la interfaz de usuario en EAC

Esta sección describe los elementos de la interfaz de usuario que son comunes en EAC.

![Centro de administración de Exchange](images/JJ150562.cd617bc0-19ef-47d2-bba1-4e9546b12e0c(EXCHG.150).gif "Centro de administración de Exchange")

## Navegación entre sitios

La navegación entre empresas le permite intercambiar fácilmente entre su organización Exchange Online y sus implementaciones de Exchange local. Si no desea tener una organización Exchange Online, el enlace lo llevará a la página de suscripción de Office 365. Para obtener más información, consulte [Implementaciones híbridas de Exchange Server](https://technet.microsoft.com/es-es/library/jj200581\(v=exchg.150\)).

## Panel de características

Este es el primer nivel de la navegación para la mayoría de las tareas que realizará en EAC. El panel de características es similar al árbol de la consola de EMC en Exchange 2010. Sin embargo, en Exchange 2013 el panel de características está organizado por áreas de características a diferencia de los roles del servidor y hay menos clics para encontrar lo que necesita.

  - **Destinatarios** Es donde administrará los buzones de correo, grupos, buzones de recursos, contactos, buzones de correo compartidos y migraciones y movimientos de buzones de correo.

  - **Permisos** Es donde podrá administrar los roles de administrador, los roles de usuario y las directivas de Outlook Web App.

  - **Administración de cumplimiento** Es donde administrará la búsqueda de exhibición de documentos electrónicos local, la retención local, las auditorías, la prevención contra la pérdida de datos (DLP), las directivas de retención, las etiquetas de retención y las reglas del diario.

  - **Organización** Es donde administrará las tareas correspondientes a la organización de Exchange, incluso el uso compartido federado, las aplicaciones de Outlook y las listas de direcciones.

  - **Protección** Es donde administrará la protección antimalware de su organización.

  - **Flujo de correo** Es donde administrará las reglas, informes de entrega, dominios aceptados, directivas de dirección de correo electrónico y conectores de envío y recepción.

  - **Móvil** Es donde administrará los dispositivos móviles que le permiten conectarse a su organización. Puede administrar las directivas de acceso a dispositivos móviles y de buzones de dispositivos móviles.

  - **Carpetas públicas** En Exchange 2010, debe administrar las carpetas públicas mediante el uso de la Consola de Administración de Carpetas Públicas, que está ubicada fuera de la EMC en el cuadro de herramientas. En Exchange 2013, las carpetas públicas se pueden administrar desde dentro del área de funciones **carpetas públicas**.

  - **Mensajería unificada** Es donde administrará los planes de marcado de mensajería unificada y las puertas de enlace IP de mensajería unificada.

  - **Servidores** Es donde administrará los servidores de buzón de correo y de acceso de cliente, las bases de datos, los grupos de disponibilidad de bases de datos (DAG), los directorios virtuales y los certificados.

  - **Híbrido** Es donde establecerá y configurará una organización híbrida.

## Fichas

Las pestañas son el segundo nivel de navegación. Cada una de las áreas de características contiene varias pestañas, representando cada una una característica completa. La única excepción a esta regla es el área de características híbrida. Primero debe habilitar su organización para una implementación híbrida mediante el uso del asistente de configuración híbrida.

## Barra de herramientas

Al hacer clic en la mayoría de las pestañas, verá una barra de herramientas. La barra de herramientas tiene iconos que realizan una acción específica. La siguiente tabla describe los iconos más comunes y sus acciones. Para mostrar la acción asociada con un icono, pase el ratón por encima del mismo.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Icono</th>
<th>Nombre</th>
<th>Action</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="Agregar icono" alt="Agregar icono" /></p></td>
<td><p>Agregar, nuevo</p></td>
<td><p>Use este icono para crear un nuevo objeto. Algunos de estos iconos tienen una flecha hacia abajo asociada donde puede hacer clic para mostrar objetos adicionales que puede crear. Por ejemplo, en <strong>Destinatarios</strong> &gt; <strong>Buzones de correo</strong>, al hacer clic en la flecha hacia abajo se muestra el <strong>Buzón de usuario</strong> y el <strong>Buzón vinculado</strong> como opciones adicionales.</p></td>
</tr>
<tr class="even">
<td><p><img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Icono Editar" alt="Icono Editar" /></p></td>
<td><p>Editar</p></td>
<td><p>Utilice este icono para editar un objeto.</p></td>
</tr>
<tr class="odd">
<td><p><img src="images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif" title="Eliminar icono" alt="Eliminar icono" /></p></td>
<td><p>Eliminar</p></td>
<td><p>Utilice este icono para eliminar un objeto. Algunos iconos eliminados tienen una flecha hacia abajo donde puede hacer clic para mostrar opciones adicionales.</p></td>
</tr>
<tr class="even">
<td><p><img src="images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif" title="icono de Buscar" alt="icono de Buscar" /></p></td>
<td><p>Búsqueda</p></td>
<td><p>Use este icono para abrir una casilla de búsqueda donde puede escribir una frase de búsqueda para el objeto que desee encontrar. Consulte <a href="https://technet.microsoft.com/es-es/library/jj156853(v=exchg.150)">Destinatarios &gt; Búsqueda avanzada</a> para obtener más opciones de búsqueda.</p></td>
</tr>
<tr class="odd">
<td><p><img src="images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif" title="Icono Actualizar" alt="Icono Actualizar" /></p></td>
<td><p>Actualizar</p></td>
<td><p>Utilice este icono para actualizar la vista de lista.</p></td>
</tr>
<tr class="even">
<td><p><img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="Icono Más opciones" alt="Icono Más opciones" /></p></td>
<td><p>Más opciones</p></td>
<td><p>Use este icono para ver más acciones que puede realizar para los objetos de la pestaña. Por ejemplo, en <strong>Destinatarios</strong> &gt; <strong>Buzones de correo</strong> si hace clic en este icono se muestran las siguientes opciones: <strong>Deshabilitar</strong>, <strong>Agregar o quitar columnas</strong>, <strong>Exportar datos a un archivo CSV</strong> , <strong>Conectar un Buzón de correo</strong> y <strong>Búsqueda avanzada</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><img src="images/JJ150576.1732c727-328b-4a1a-b84d-6d7252c7dcab(EXCHG.150).gif" title="Icono flecha arriba" alt="Icono flecha arriba" />   <img src="images/JJ150576.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif" title="Icono flecha abajo" alt="Icono flecha abajo" /></p></td>
<td><p>Flecha hacia arriba y flecha hacia abajo</p></td>
<td><p>Use estos iconos para mover la prioridad de un objeto hacia arriba o hacia abajo. Por ejemplo, en <strong>Flujo del correo</strong> &gt; <strong>Directivas de direcciones de correo electrónico</strong> haga clic en la flecha hacia arriba para elevar la prioridad de una directiva de dirección de correo electrónico. También puede usar estas flechas para navegar por la jerarquía de la carpeta pública y hacer subir o bajar las reglas en la vista de la lista.</p></td>
</tr>
<tr class="even">
<td><p><img src="images/JJ657480.ed7f7abf-39d8-4f43-a918-ccb3bff87ef5(EXCHG.150).gif" title="Copiar icono" alt="Copiar icono" /></p></td>
<td><p>Copiar</p></td>
<td><p>Use este icono para copiar un objeto para que pueda realizar cambios sin cambiar el objeto original. Por ejemplo, en <strong>Permisos</strong>&gt;<strong>Roles de administrador</strong>, seleccione un rol de administrador en la vista de lista y haga clic en este icono para crear un nuevo grupo de roles basado en uno existente.</p></td>
</tr>
<tr class="odd">
<td><p><img src="images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif" title="Icono de quitar" alt="Icono de quitar" /></p></td>
<td><p>Quitar</p></td>
<td><p>Utilice este icono para quitar un elemento de la lista. Por ejemplo, en el cuadro de diálogo <strong>Permisos de carpeta pública</strong>, puede quitar usuarios de la lista de usuarios con permiso para acceder a la carpeta pública seleccionando el usuario y haciendo clic en este icono.</p></td>
</tr>
</tbody>
</table>


## Vista de lista

Cuando seleccione una pestaña, en la mayoría de los casos verá la vista de lista. La vista de lista de EAC se ha diseñado para eliminar las limitaciones que existían en ECP. EMC solo puede mostrar hasta 500 objetos y si desea ver los objetos que no están en la lista del panel de detalles, debe usar las opciones de búsqueda y filtrado para encontrar esos objetos específicos. En Exchange 2013, el límite de visualización desde el interior de la vista de lista de EAC es de aproximadamente 20.000 objetos en implementaciones locales y 10.000 objetos en Exchange Online. Además, la paginación se incluye para que usted puede paginar los resultados. En la vista de lista de **Destinatarios** también puede configurar el tamaño de la página y exportar los datos a un archivo CSV.

## Panel de detalles

Cuando seleccione un objeto de la vista de lista, la información acerca del objeto se muestra en el panel de detalles. En algunos casos (por ejemplo, con objetos de destinatarios) el panel de detalles incluye tareas de gestión rápidas. Por ejemplo, si va a **Destinatarios** \> **Buzones de correo** y selecciona un buzón de correo de la vista de lista, el panel de detalles muestra una opción para habilitar o deshabilitar el archivo del buzón de correo. El panel de detalles también puede utilizarse para editar masivamente varios objetos. Simplemente pulse la tecla CTRL, seleccione los objetos que desee editar masivamente y use las opciones en el panel de detalles. Por ejemplo, la selección de varios buzones de correo le permite actualizar masivamente la información de contacto, la organización, los atributos personalizados, la cuota del buzón, las configuraciones de Outlook Web App y mucho más del usuario.

## Notificaciones

El EAC incluye un visor de notificaciones que muestra el estado de procesos de larga ejecución y proporciona notificaciones cuando se completa el proceso. Además, para los procesos de ejecución especialmente largos como las solicitudes de movimiento, puede suscribirse para recibir notificaciones por correo electrónico.

## Mosaico Yo y Ayuda

El *Mosaico* le permite cerrar sesión en EAC e iniciar sesión como un usuario diferente. Desde el menú desplegable en Ayuda ![Icono de ayuda](images/JJ150562.a32eac4e-345d-4236-a284-204390aff4ee(EXCHG.150).gif "Icono de ayuda"), puede realizar las siguientes acciones:

  - **Ayuda**   Haga clic en ![Icono de ayuda](images/JJ150562.a32eac4e-345d-4236-a284-204390aff4ee(EXCHG.150).gif "Icono de ayuda") para ver el contenido de la ayuda en línea.

  - **Deshabilitar el globo de Ayuda**   El globo de Ayuda muestra la ayuda contextual de los campos cuando crea o edita un objeto. Puede desactivar la ayuda del globo de Ayuda o activarlo si estaba deshabilitado.

  - **Copyright y privacidad** Haga clic en el enlace de privacidad o copyright para leer la información del copyright y de privacidad de Exchange 2013.

## Exploradores compatibles

Para tener la mejor experiencia con EAC, use una de las combinaciones de sistema operativo y navegación denominados "Premium".


> [!NOTE]  
> Las combinaciones de sistema operativo y navegador que no aparezcan en la tabla anterior no son compatibles, incluidas las táctiles.



  - **Premium:**  Todas las características funcionales son compatibles y probadas en su totalidad.

  - **Admitidos:**  Tiene el mismo soporte de característica funcional que Premium. Sin embargo, a los navegadores admitidos le faltarán ciertas características que no admite la combinación de sistema operativo y navegador.

  - **No admitido:**  El navegador y sistema operativo no están admitidos o no fueron probados.


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Explorador web</p></td>
<td><p>Windows XP y Windows Server 2003</p></td>
<td><p>Windows Vista</p></td>
<td><p>Windows 7 y Windows Server 2008</p></td>
<td><p>Windows 8 y Windows Server 2012</p></td>
<td><p>Mac SOX</p></td>
<td><p>Linux</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 8</p></td>
<td><p>Compatible</p></td>
<td><p>Compatible</p></td>
<td><p>Premium</p></td>
<td><p>No compatible</p></td>
<td><p>No compatible</p></td>
<td><p>No compatible</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 9</p></td>
<td><p>No compatible</p></td>
<td><p>Compatible</p></td>
<td><p>Premium</p></td>
<td><p>No compatible</p></td>
<td><p>No compatible</p></td>
<td><p>No compatible</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 10 o posterior</p></td>
<td><p>No compatible</p></td>
<td><p>Compatible</p></td>
<td><p>Premium</p></td>
<td><p>Premium</p></td>
<td><p>No compatible</p></td>
<td><p>No compatible</p></td>
</tr>
<tr class="odd">
<td><p>Firefox 11 o posterior</p></td>
<td><p>Compatible</p></td>
<td><p>Compatible</p></td>
<td><p>Premium</p></td>
<td><p>Premium</p></td>
<td><p>Premium</p></td>
<td><p>Compatible</p></td>
</tr>
<tr class="even">
<td><p>Safari 5,1 o posterior</p></td>
<td><p>No compatible</p></td>
<td><p>No compatible</p></td>
<td><p>No compatible</p></td>
<td><p>No compatible</p></td>
<td><p>Premium</p></td>
<td><p>No compatible</p></td>
</tr>
<tr class="odd">
<td><p>Chrome 18 o posterior</p></td>
<td><p>Compatible</p></td>
<td><p>Compatible</p></td>
<td><p>Premium</p></td>
<td><p>Premium</p></td>
<td><p>Premium</p></td>
<td><p>No compatible</p></td>
</tr>
</tbody>
</table>

