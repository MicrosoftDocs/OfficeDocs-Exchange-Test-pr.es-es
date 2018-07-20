---
title: 'Listas de direcciones: Exchange 2013 Help'
TOCTitle: Listas de direcciones
ms:assetid: 8ee2672a-3a45-4897-8cc0-fa23c374dbf9
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb232119(v=EXCHG.150)
ms:contentKeyID: 49895771
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Listas de direcciones

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2014-12-02_

Una *lista de direcciones* es un conjunto de objetos de destinatario y de otros objetos de Active Directory. Cada lista de direcciones puede incluir uno o varios tipos de objetos (por ejemplo, usuarios, contactos, grupos, carpetas públicas, salas y recursos de equipamiento). Puede utilizar listas de direcciones para organizar destinatarios y recursos, lo cual le permitirá encontrar los destinatarios y recursos que desee con mayor facilidad. Las listas de direcciones se actualizan dinámicamente. Por lo tanto, cuando se agregan destinatarios nuevos a la organización, se agregan también automáticamente a las listas de direcciones adecuadas.

Como se muestra en la figura siguiente, las aplicaciones cliente, como Microsoft Outlook, muestran las listas de direcciones disponibles que proporciona Exchange.

**Lista global de direcciones como se muestra en Microsoft Office Outlook 2007**

![Listas de direcciones que se muestran en Outlook 2007](images/Bb232119.54d7729c-2e28-4863-8944-b0c37dabbbb3(EXCHG.150).gif "Listas de direcciones que se muestran en Outlook 2007")

Las listas de direcciones residen en Active Directory. Por lo tanto, los usuarios de dispositivos móviles desconectados de la red están también desconectados de estas listas de direcciones en el lado del servidor. No obstante, puede crear libretas de direcciones sin conexión (OAB) para los usuarios desconectados de la red. Estas OAB se pueden descargar en el disco duro del usuario. A menudo, para economizar recursos, las OAB son subconjuntos de la información contenida en las listas de direcciones propiamente dichas que se ubican en sus servidores. Para obtener más información, consulte [Libretas de direcciones sin conexión](offline-address-books-exchange-2013-help.md).

**Contenido**

Listas predeterminadas de direcciones

Listas de direcciones personalizadas

Prácticas recomendadas para crear listas de direcciones

## Listas predeterminadas de direcciones

Si los usuarios usan su aplicación de cliente para buscar información de destinatario, pueden elegir entre las listas de direcciones disponibles. De forma predeterminada, se crean varias listas de direcciones, como la lista global de direcciones (GAL). Exchange contiene las listas de direcciones predeterminadas siguientes, que se completan automáticamente con usuarios, contactos, grupos o salas nuevos a medida que se agregan a la organización:

  - **Todos los contactos**   Esta lista de direcciones contiene todos los contactos con correo habilitado en su organización. Los contactos con correo habilitado son los destinatarios que tienen una dirección de correo electrónico externa. Si desea que haya información sobre un contacto con correo habilitado a disposición de todos los usuarios de su organización, incluya el contacto en la GAL. Para obtener más información acerca de los contactos con correo habilitado, consulte [Destinatarios](recipients-exchange-2013-help.md).

  - **Todas las listas de distribución**   Esta lista de direcciones contiene grupos habilitados para correo electrónico, como grupos de seguridad habilitados para correo electrónico, grupos de distribución y grupos de distribución dinámicos en su organización. Los grupos habilitados para correo electrónico son listas de destinatarios creadas para acelerar el envío masivo de mensajes de correo electrónico y otra información. Cuando se envía un mensaje de correo electrónico a un grupo con correo habilitado, todos los miembros de esa lista reciben una copia del mensaje. Para obtener más información acerca de los grupos con correo habilitado, consulte [Destinatarios](recipients-exchange-2013-help.md).

  - **Todas las salas**   Esta lista de direcciones contiene todos los recursos designados como sala en su organización. Las salas son recursos en su organización que se pueden programar mediante el envío de una convocatoria de reunión desde una aplicación cliente. La cuenta de usuario asociada a una sala está deshabilitada. Para conocer más detalles acerca de los buzones de recursos, consulte [Destinatarios](recipients-exchange-2013-help.md).

  - **Todos los usuarios**   Esta lista de direcciones contiene todos los usuarios con correo habilitado en su organización. Un usuario habilitado para correo es un usuario externo a la organización de Exchange. Cada usuario con correo habilitado tiene una dirección de correo electrónico externa. Todos los mensajes enviados a usuarios con correo habilitado se enrutan a esta dirección de correo electrónico externa. Un usuario con correo habilitado es parecido a un contacto de correo, excepto que un usuario con correo habilitado tiene credenciales de inicio de sesión de Active Directory y puede tener acceso a los recursos. Para obtener más información acerca de los usuarios con correo habilitado, consulte [Destinatarios](recipients-exchange-2013-help.md).

  - **Lista de direcciones global predeterminada**   Esta lista de direcciones contiene todos los usuarios, contactos, grupos o salas con correo habilitado en la organización. Durante la instalación, Exchange crea varias listas de direcciones predeterminadas. La lista de direcciones más conocida es la GAL. De forma predeterminada, la GAL contiene todos los destinatarios de una organización de Exchange. Dicho de otro modo, cualquier objeto habilitado para correo o buzón de correo en un bosque de Active Directory que tenga instalado Exchange aparecerá en la GAL. Para facilitar el uso, la GAL está organizada por nombre, no por dirección de correo electrónico. Para obtener más información, consulte [Crear una lista global de direcciones](create-a-global-address-list-exchange-2013-help.md).

  - **Carpetas públicas**   Esta lista de direcciones contiene todas las carpetas públicas de la organización. Los permisos de acceso determinan quién puede ver y usar las carpetas. Las carpetas públicas se almacenan en equipos que ejecutan Exchange. Para obtener más información sobre la administración de carpetas públicas en Exchange 2013, consulte [Carpetas públicas](public-folders-exchange-2013-help.md). Para obtener más información sobre la administración de carpetas públicas en Exchange Online, consulte [Carpetas públicas de Office 365 y Exchange Online](https://technet.microsoft.com/es-es/library/jj200758\(v=exchg.150\)).

## Listas de direcciones personalizadas

Una organización de Exchange puede contener miles de destinatarios. Si compila todos los destinatarios en las listas de direcciones predeterminadas, dichas listas podrían llegar a ser muy grandes. Para evitarlo, puede crear listas de direcciones personalizadas que ayuden a los usuarios de su organización a encontrar lo que buscan con mayor facilidad.

Por ejemplo, imagínese una compañía compuesta por dos grandes divisiones y una organización de Exchange. Una de las divisiones, llamada Fourth Coffee, importa y vende granos de café. La otra división, Contoso, Ltd, vende pólizas de seguros. Para la mayoría de las actividades diarias, los empleados de Fourth Coffee no se comunican con los de Contoso Ltd. Por ello, para que los empleados puedan encontrar destinatarios que solo existen en su división con mayor facilidad, puede crear dos listas de direcciones personalizadas, una para Fourth Coffee y otra para Contoso Ltd. Cuando los empleados buscan destinatarios en su división, estas listas de direcciones personalizadas les permiten seleccionar solo la lista de direcciones específica de su división. No obstante, si un empleado no está seguro de en qué división existe el destinatario, puede buscar en la GAL, que contiene todos los destinatarios de ambas divisiones.

También puede crear subcategorías de listas de direcciones, llamadas listas de direcciones jerárquicas. Por ejemplo, puede crear una lista de direcciones que contenga todos los destinatarios de Manchester y otra que contenga todos los destinatarios de Stuttgart.

## Prácticas recomendadas para crear listas de direcciones

A pesar de que las listas de direcciones son herramientas útiles para los usuarios, si están mal diseñadas, pueden resultar frustrantes. Para asegurarse de que sus listas de direcciones resultan prácticas a los usuarios, tenga en cuenta estas prácticas recomendadas:

  - Evite crear tantas listas de direcciones que los usuarios duden en cuál de ellas deben buscar los destinatarios.

  - Las listas de direcciones hacen que los usuarios encuentren con mayor facilidad direcciones en la LGD.

  - Asigne nombres a las listas de direcciones que permitan saber a los usuarios qué tipos de destinatarios contienen con solo leerlos. Si tiene problemas para asignar nombres a sus listas de direcciones, cree menos listas y recuerde a los usuarios que pueden encontrar a cualquiera en la organización en la GAL.
    

    > [!NOTE]
    > De manera predeterminada, en Exchange Online, el rol Lista de direcciones no se asigna a ningún grupo de roles. Para usar algún cmdlet que requiera el rol Lista de direcciones, es necesario agregar el rol a un grupo de roles. Para obtener más información, consulte la sección "Agregar un rol a un grupo de roles" del tema <A href="manage-role-groups-exchange-2013-help.md">Administrar grupos de roles</A>.



Para obtener instrucciones detalladas a fin de crear una lista de direcciones en Exchange 2013, consulte [Crear una lista de direcciones](create-an-address-list-exchange-2013-help.md). Para obtener instrucciones detalladas a fin de crear una lista de direcciones en Exchange Online, consulte [Administrar listas de direcciones en Exchange Online](https://technet.microsoft.com/es-es/library/jj983798\(v=exchg.150\)).

