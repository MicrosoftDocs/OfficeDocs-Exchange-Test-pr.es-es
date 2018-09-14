---
title: 'Direcciones de correo electrónico y libretas de direcciones Exchange 2013 Help'
TOCTitle: Direcciones de correo electrónico y libretas de direcciones
ms:assetid: b97d0f68-691a-42af-9a6c-4dcc37b28a42
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ657488(v=EXCHG.150)
ms:contentKeyID: 49895866
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Direcciones de correo electrónico y libretas de direcciones

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

En Active Directory, los destinatarios (incluidos los usuarios, recursos, contactos y grupos) son cualquier objeto habilitado para correo al que Microsoft Exchange puede entregar o enrutar mensajes. Para que un destinatario reciba o envíe mensajes de correo electrónico, debe disponer de una dirección de correo electrónico. Las libretas de direcciones son el método por el cual los usuarios se encuentran para poder enviar correos electrónicos. Hay muchos métodos diferentes para organizar las libretas de direcciones. Vea Terminología básica para obtener descripciones detalladas de las características de las libretas de direcciones en Exchange Server 2013.

## Terminología básica

Los siguientes términos definen los componentes centrales asociados con las direcciones de correo electrónico y las libretas de direcciones en Exchange 2013.

  - **directivas de la libreta de direcciones**  
    Las directivas de libreta de direcciones (ABP) permiten clasificar a los usuarios en grupos específicos para proporcionar vistas personalizadas de la lista global de direcciones (LGD) de una organización. Al crear una ABP, asigna una GAL, una libreta de direcciones sin conexión (OAB), una lista de sala y una o varias listas de direcciones a la directiva. A continuación, puede asignar la ABP a usuarios de los buzones y proporcionarles acceso a una GAL personalizada en Outlook y Outlook Web App. El objetivo es proporcionar un mecanismo más sencillo para cumplir la segmentación de GAL para organizaciones locales que necesiten varias GAL.

<!-- end list -->

  - **listas de direcciones**  
    Una lista de direcciones es un subconjunto de LGD. Cada lista de direcciones es una colección de uno o más tipos de destinatarios habilitados para correo (por ejemplo: usuarios, contactos, grupos, carpetas públicas, conferencias y otros recursos). Puede utilizar las listas de direcciones para organizar destinatarios y recursos, lo cual le permitirá encontrar los destinatarios y recursos que desee con mayor facilidad. Las listas de direcciones se actualizan dinámicamente. Por lo tanto, cuando se agregan destinatarios nuevos a la organización, se agregan también automáticamente a las listas de direcciones adecuadas.

<!-- end list -->

  - **directivas de direcciones de correo electrónico**  
    Las directivas de direcciones de correo electrónico generan direcciones primarias y secundarias para sus destinatarios a fin de que puedan recibir y enviar mensajes de correo electrónico. De manera predeterminada, Exchange contiene una directiva de direcciones de correo electrónico para cada usuario habilitado para correo.

<!-- end list -->

  - **libretas jerárquicas de direcciones**  
    La libreta jerárquica de direcciones (HAB) permite a los usuarios buscar destinatarios en sus libretas de direcciones usando una jerarquía organizativa, como la antigüedad o la estructura administrativa. Normalmente, los usuarios están limitados a la GAL y sus propiedades de destinatario asociadas, y la estructura de la GAL no suele reflejar de forma precisa las relaciones de administración y antigüedad de los destinatarios de la organización. Poder personalizar una HAB que asigne a la organización una estructura empresarial exclusiva dota a los usuarios de un método eficiente para buscar destinatarios internos.

<!-- end list -->

  - **libretas de direcciones sin conexión**  
    Una libreta de direcciones sin conexión (OAB) es una copia de un conjunto de listas de direcciones que se descarga para que un usuario de Microsoft Outlook pueda tener acceso a la información que contiene la libreta cuando no tiene conexión con el servidor.

## Documentación de libreta de direcciones y direcciones de correo electrónico

La siguiente tabla contiene vínculos a los temas que lo ayudarán a aprender y a administrar las direcciones de correo electrónico y las libretas de direcciones en Exchange 2013.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tema</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/es-es/exchange/address-books/address-lists/address-lists">Listas de direcciones</a></p></td>
<td><p>Conozca más acerca de las listas de direcciones y GAL como métodos para organizar los destinatarios para obtener un acceso de usuario final más sencillo.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/es-es/exchange/address-books/address-book-policies/address-book-policies">Directivas de la libreta de direcciones</a></p></td>
<td><p>Conozca más acerca de cómo separar las listas de direcciones y GAL en organizaciones virtuales separadas.</p></td>
</tr>
<tr class="odd">
<td><p><a href="details-templates-exchange-2013-help.md">Plantillas de detalles</a></p></td>
<td><p>Conozca más acerca de la personalización de las tarjetas de direcciones en Outlook.</p></td>
</tr>
<tr class="even">
<td><p><a href="email-address-policies-exchange-2013-help.md">Directivas de dirección de correo electrónico</a></p></td>
<td><p>Conozca más acerca de las direcciones de correo electrónico de proxy para que los destinatarios sean más fáciles de detectar.</p></td>
</tr>
<tr class="odd">
<td><p><a href="hierarchical-address-books-exchange-2013-help.md">Libretas de direcciones jerárquicas</a></p></td>
<td><p>Conozca más acerca de cómo personalizar las LGD y las listas de direcciones para que cumplan con la estructura comercial única de su organización.</p></td>
</tr>
<tr class="even">
<td><p><a href="offline-address-books-exchange-2013-help.md">Libretas de direcciones sin conexión</a></p></td>
<td><p>Conozca más acerca de cómo proporcionar usuarios con acceso sin conexión a las listas de direcciones de su organización.</p></td>
</tr>
</tbody>
</table>

