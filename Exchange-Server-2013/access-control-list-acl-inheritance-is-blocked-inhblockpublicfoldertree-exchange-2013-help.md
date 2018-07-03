---
title: 'La herencia de la lista de control de acceso (ACL) está bloqueada_InhBlockPublicFolderTree: Exchange 2013 Help'
TOCTitle: La herencia de la lista de control de acceso (ACL) está bloqueada_InhBlockPublicFolderTree
ms:assetid: e3b89c8a-d6f8-4864-8bf0-35a78ce87cc4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.inhblockpublicfoldertree(v=EXCHG.150)
ms:contentKeyID: 48268810
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# La herencia de la lista de control de acceso (ACL) está bloqueada\_InhBlockPublicFolderTree

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2015-03-09_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Microsoft Exchange Server 2007 o Exchange Server 2010 Setup no puede continuar porque no se han podido propagar los permisos necesarios.

El programa de instalación de Exchange requiere que se habilite la herencia para los permisos en los siguientes objetos de Exchange:

  - Objeto de organización de Exchange

  - Objeto de grupo administrativo de Exchange

  - Objeto de contenedor de servidores de Exchange

  - Objeto de lista de direcciones de Exchange

  - Objeto de carpeta pública de Exchange

  - Objeto de árbol de carpetas públicas de Exchange

Si no se habilita la herencia para los permisos en estos objetos se pueden producir problemas de flujo del correo, problemas de montaje de almacenes y otras interrupciones de servicios.

Para resolver este problema, asegúrese de que la configuración "Permitir que los permisos heredables del primario se propaguen a este objeto y a todos los objetos secundarios" esté habilitada para el objeto y vuelva a ejecutar Exchange Server 2007 Setup o Exchange 2010 Setup.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Para volver a habilitar la herencia de los permisos para un objeto de configuración de Exchange con el Administrador del sistema de Exchange Server 2003</p></td>
</tr>
<tr class="even">
<td><ol>
<li><p>Habilite la ficha <strong>Seguridad</strong> del recuadro de propiedades del objeto del Administrador del sistema de Exchange definiendo un parámetro del Registro.</p>
<ol>
<li><p>Inicie el editor del Registro (Regedt32.exe).</p></li>
<li><p>Busque la siguiente clave en el Registro:</p>
<p><strong>HKEY_CURRENT_USER\Software\Microsoft\Exchange\EXAdmin</strong></p></li>
<li><p>En el menú <strong>Editar</strong>, haga clic en <strong>Nuevo</strong> y, a continuación, agregue el siguiente valor.</p>
<p><strong>Nombre de valor</strong>: ShowSecurityPage</p>
<p><strong>Tipo de datos</strong>: REG_DWORD</p>
<p><strong>Base</strong>: Binario</p>
<p><strong>Valor</strong>: 1</p></li>
<li><p>Salga del editor del Registro.</p></li>
</ol>

> [!NOTE]
> De manera predeterminada, la ficha <STRONG>Seguridad</STRONG> no está habilitada en el recuadro de propiedades del objeto de configuración.


</li>
<li><p>Abra el Administrador del sistema de Exchange, busque el objeto en cuestión, haga clic en el objeto con el botón secundario y seleccione <strong>Propiedades</strong>.</p></li>
<li><p>Seleccione la ficha <strong>Seguridad</strong> y, a continuación, haga clic en <strong>Avanzada</strong>.</p></li>
<li><p>Active <strong>Permitir que los permisos heredables del primario se propaguen a este objeto y a todos los objetos secundarios</strong> para volver a habilitar la herencia de permisos.</p></li>
<li><p>Reinicie Exchange Server.</p></li>
</ol></td>
</tr>
</tbody>
</table>



> [!WARNING]
> Si modifica los atributos de los objetos de Active Directory de manera incorrecta al usar el Editor ADSI, la herramienta LDP u otro cliente de la versión 3 de LDAP, puede provocar graves problemas. Estos problemas pueden exigir que vuelva a instalar Microsoft Windows&nbsp;Server™ 2003, Exchange&nbsp;Server o ambos. Si modifica atributos de objeto de Active Directory, es bajo su propia responsabilidad.




<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Para volver a habilitar la herencia de permisos para un objeto de configuración de Exchange utilizando ADSIEdit en Exchange Server 2007 o Exchange Server 2010</p></td>
</tr>
<tr class="even">
<td><ol>
<li><p>Instale ADSI Edit.</p></li>
<li><p>Inicie ADSI Edit. Haga clic en <strong>Inicio</strong>, <strong>Ejecutar</strong>, escriba <strong>adsiedit.msc</strong> en el cuadro de texto y, a continuación, haga clic en Aceptar.</p></li>
<li><p>Busque el objeto en cuestión, haga clic con el botón secundario y seleccione <strong>Propiedades</strong>.</p></li>
<li><p>Seleccione la ficha <strong>Seguridad</strong> y, a continuación, haga clic en <strong>Avanzada</strong>.</p></li>
<li><p>Active <strong>Permitir que los permisos heredables del primario se propaguen a este objeto y a todos los objetos secundarios</strong> para volver a habilitar la herencia de permisos.</p></li>
<li><p>Haga clic en <strong>Aceptar</strong> dos veces para aplicar el cambio.</p></li>
<li><p>Espere a que la replicación de Active Directory propague los cambios o fuércela siguiendo las instrucciones descritas en el artículo 232072 de Microsoft Knowledge Base, &quot;Iniciar la replicación entre Active Directory Direct Replication Partners&quot; (<a href="http://go.microsoft.com/fwlink/?linkid=3052&kbid=232072" class="uri">http://go.microsoft.com/fwlink/?linkid=3052&amp;kbid=232072</a>).</p></li>
</ol></td>
</tr>
</tbody>
</table>

