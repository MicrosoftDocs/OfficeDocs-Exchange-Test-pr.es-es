---
title: 'Consideraciones a la hora de implementar carpetas públicas: Exchange 2013 Help'
TOCTitle: Consideraciones a la hora de implementar carpetas públicas
ms:assetid: 2e416eed-b88f-45db-a482-1232fd2610fa
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn957481(v=EXCHG.150)
ms:contentKeyID: 64966457
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Consideraciones a la hora de implementar carpetas públicas

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2016-07-12_

Aunque el uso de carpetas públicas de Exchange 2013 tiene muchas ventajas, deben tenerse en cuenta varias cosas antes de implementarlas en su organización.

## Consideraciones sobre la implementación de carpetas públicas

Este artículo contiene factores para considerar antes de implementar carpetas públicas en la organización, especialmente si planea tener un gran número de carpetas públicas. Exchange 2013 ahora admite hasta un millón de carpetas públicas.

  - La actividad en una carpeta pública tiene un impacto directo en la carga que se coloca en el buzón de correo de carpeta pública donde se localiza la carpeta. Para evitar problemas de conectividad de cliente, como alta latencia o la incapacidad para obtener acceso a una carpeta pública, se recomienda lo siguiente:
    
      - No deje que los buzones de correo de carpeta pública superen el 50 % del límite de tamaño de buzón. Si esto sucede, considere la posibilidad de usar el script `Split-PublicFolderMailbox.ps1` que se encuentra en la carpeta C:\\Archivos de programa\\Microsoft\\Exchange Server\\V15\\Scripts en el servidor de Exchange 2013 para mover algunas carpetas públicas a un nuevo buzón de correo de carpeta pública.
    
      - Considere la posibilidad de mover carpetas públicas de uso intensivo a un buzón de correo de carpeta pública dedicado.
    
      - Excluya las carpetas públicas de uso intensivo de la jerarquía de carpetas públicas de servicio. Para ello, puede establecer la propiedad *IsExcludedFromServingHierarchy* en el buzón de correo de carpeta pública mediante el cmdlet **Set-Mailbox**.
    
      - Para organizaciones grandes con varias carpetas públicas, considere la posibilidad de agregar buzones de correo de carpeta pública adicionales para distribuir la carga de solicitudes de jerarquía de carpetas públicas de servicio.

  - Coloque el buzón de correo de carpeta pública principal en un DAG para mejorar la disponibilidad del buzón. El buzón de correo de carpeta pública principal contiene la copia de autoridad de la jerarquía de carpetas públicas.

  - Coloque los buzones de correo de carpeta pública secundarios en un DAG o cree copias de seguridad de los buzones con frecuencia.

  - Coloque los buzones de correo de carpeta pública en la ubicación geográfica más cercana a los usuarios que tendrán acceso al contenido de carpetas públicas en ellos.

  - Mejore los tiempos de acceso a la jerarquía de carpetas públicas mediante la propiedad DefaultPublicFolderMailbox en los buzones de los usuarios para especificar un buzón de correo de carpeta pública cercano a ellos. Esto impedirá que dichos usuarios recuperen la jerarquía de carpetas públicas desde un buzón de correo de carpeta pública en otras ubicaciones geográficas.

  - En implementaciones con más de 50 buzones de correo de carpeta pública secundarios, se recomienda no almacenar contenido de carpeta pública en el buzón de correo de carpeta pública principal. Esto dedica el buzón de correo de carpeta pública principal para sincronizar la jerarquía con los buzones de correo de carpeta pública secundarios.

  - Exchange 2013 ya no admite las bases de datos de carpetas públicas. Por lo tanto, los usuarios de Outlook Web App que tienen buzones de Exchange 2013 no podrán obtener acceso a las carpetas públicas de Exchange 2010 ni de Exchange 2007. Los usuarios de Exchange 2013 sí pueden obtener acceso a las carpetas públicas de Exchange 2010 o Exchange 2007 con Outlook o Outlook para Mac.

  - Outlook Web App es compatible, pero con limitaciones. Puede agregar y eliminar carpetas públicas favoritas y realizar operaciones de nivel de elemento, como crear, editar, eliminar y responder mensajes. Sin embargo, no puede crear o borrar carpetas públicas de Outlook Web App. Además, solo las carpetas públicas de correo, publicación, calendario y contactos se pueden agregar a la lista de favoritos en Outlook Web App.

  - Si bien se encuentra disponible una búsqueda de texto completo del contenido de las carpetas públicas, no se puede buscar contenido de carpetas públicas entre carpetas públicas y Exchange Search no lo indiza.

  - Debe usar Outlook 2007 o superior para acceder a carpetas públicas en servidores Exchange 2013.

  - Las directivas de retención no son compatibles para los buzones de correo de carpeta pública.

