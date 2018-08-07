---
title: 'Mensajería registro terminología administrar Exchange 2013: Exchange 2013 Help'
TOCTitle: Mensajería de registros terminología de administración de Exchange de 2013
ms:assetid: de3e3503-6de3-4666-aeb9-cd877efb93bb
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb408414(v=EXCHG.150)
ms:contentKeyID: 49895962
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Mensajería de registros terminología de administración de Exchange de 2013

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-30_

Este tema definen los componentes principales asociados de mensajería (MRM) de administración de registros en Microsoft Exchange Server 2013. MRM es una tecnología de administración de registros en Exchange 2013 que ayuda a las organizaciones a reducir los riesgos asociados con el correo electrónico y otras comunicaciones. MRM hace que sea más fácil mantener los mensajes que se necesitan para cumplir con la directiva de empresa, las regulaciones del gobierno o necesidades legales y quitar el contenido que tiene no legal o valor para el negocio.

  - **etiqueta de directiva predeterminada (DPT)**  
    Una DPT es una etiqueta de retención que se aplica a todos los elementos de un buzón de correo que no tienen una etiqueta de retención aplicada. Solo puede tener una etiqueta de directiva predeterminada en una directiva de retención.

<!-- end list -->

  - **usuario archivador o archivador**  
    Un usuario que archiva con regularidad elementos de buzones en carpetas.
    
    Comparar con usuario acumulador o acumulador.

<!-- end list -->

  - **tareas de diario**  
    Capacidad de registrar comunicaciones de una organización, incluyendo comunicaciones de correo electrónico, que se van a usar en la retención de correo electrónico de la organización o en la estrategia de archivado. EN MRM, las tareas de diario se refieren generalmente al proceso de enviar un informe de diario de mensajes de una carpeta administrada a una dirección SMTP especificada. Este proceso se realiza mediante el Asistente para carpetas administradas.

<!-- end list -->

  - **configuración de contenido administrado**  
    La información de retención creada para las carpetas gestionadas. La característica MRM disponible en Exchange Server 2007 y Exchange Server 2010. Una carpeta administrada puede tener varias configuraciones de contenido para distintos tipos de mensajes, como mensajes de correo electrónico, correo de voz, elementos de calendario y contactos. La configuración de retención de mensajes que se define en la configuración de contenido de una carpeta administrada se aplica a los mensajes de dicha carpeta administrada.

<!-- end list -->

  - **carpeta administrada**  
    Una carpeta administrada se utiliza para la funcionalidad MRM en Exchange Server 2007 y Exchange Server 2010, y es un objeto Active Directory que representa una carpeta del buzón de correo a fin de aplicarle una configuración de contenido administrado. En un buzón, una carpeta administrada es una carpeta a la que se ha aplicado configuración de contenido administrado.

<!-- end list -->

  - **Asistente para carpetas administradas**  
    Uno de los asistentes de buzón de Microsoft Exchange en Exchange 2013. El Asistente para carpetas administradas es responsable del archivado, la caducidad del mensaje y el cumplimiento. Procesa los buzones de correo y aplica directivas de retención.

<!-- end list -->

  - **directiva de buzones de carpetas administradas**  
    Agrupación lógica de carpetas administradas. En Exchange 2010 y Exchange 2007, cuando se aplica una directiva de buzones de correo de carpetas administradas al buzón de correo de un usuario, todas las carpetas administradas vinculadas a la directiva se implementan en una sola operación.

<!-- end list -->

  - **etiqueta personal**  
    Una etiqueta personal es una etiqueta de retención disponible para Outlook Web App y Outlook 2010, y usuarios posteriores, para aplicar una configuración de retención a carpetas personalizadas y elementos individuales, como mensajes de correo electrónico.

<!-- end list -->

  - **usuario acumulador o acumulador**  
    Un usuario que no archiva con regularidad los elementos del buzón. Los acumuladores tienden a tener la bandeja de entrada llena y confían en las opciones de búsqueda para encontrar mensajes.
    
    Comparar con un usuario archivador o archivador.

<!-- end list -->

  - **directiva**  
    Consulte *directiva de retención* o *directiva de buzones de correo de carpetas administradas*.

<!-- end list -->

  - **etiqueta de directiva de retención (RPT)**  
    Una RPT es una etiqueta de retención que se aplica a carpetas predeterminadas, como Bandeja de entrada y Elementos eliminados.

<!-- end list -->

  - **directiva de retención**  
    Una directiva de retención es una agrupación lógica de etiquetas de retención. Cuando se aplica una directiva de retención al buzón de un usuario, todas las etiquetas de retención vinculadas a la directiva se implementan en una única operación.

<!-- end list -->

  - **etiqueta de retención**  
    Las etiquetas de retención se usan para aplicar una configuración de retención a mensajes y carpetas en buzones de correo de usuarios. Existen tres tipos de etiquetas de retención:
    
      - Etiquetas de directivas predeterminadas (DPT)
    
      - Etiquetas de directivas de retención (RPT)
    
      - Etiquetas personales

