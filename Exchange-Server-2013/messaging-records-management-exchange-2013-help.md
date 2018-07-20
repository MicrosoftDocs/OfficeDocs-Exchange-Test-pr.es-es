---
title: 'Administración de registros de mensajes: Exchange 2013 Help'
TOCTitle: Administración de registros de mensajes
ms:assetid: 0dd92e9c-881e-43c0-9bbf-f41fdc9dfd87
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd335093(v=EXCHG.150)
ms:contentKeyID: 49895460
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Administración de registros de mensajes

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2016-02-01_

Los usuarios envían y reciben correos electrónicos todos los días. Si no se administra, el volumen de correo electrónico generado y recibido cada día puede inundar a los usuarios, tener un impacto en la productividad del usuario y exponer la organización a riesgos. Como resultado, la administración del ciclo de vida del correo electrónico es un componente fundamental para muchas organizaciones.

La administración de registros de mensajes (MRM) es la tecnología de administración de registros de Exchange Server 2013 y Exchange Online que ayuda a las organizaciones a administrar el ciclo de vida del correo electrónico y a reducir los riesgos legales asociados al correo electrónico. La implementación de MRM puede ayudar a su organización de varias maneras:

  - **Cumplir con los requisitos empresariales**   Según las directivas de mensajería de su organización, es posible que necesite conservar mensajes de correo electrónico importantes durante un período determinado. Por ejemplo, el buzón de correo de un usuario puede contener mensajes fundamentales relacionados con la estrategia empresarial, las transacciones, el desarrollo de los productos o las interacciones con clientes.

  - **Cumplir con los requisitos legales y las normas de regulación**   Muchas organizaciones tienen un requisito legal o una norma de regulación para almacenar mensajes durante un período de tiempo concreto y eliminarlos pasado este. El almacenamiento de mensajes durante un período más largo del necesario puede incrementar los riesgos legales y financieros de su organización.

  - **Aumentar la productividad del usuario**   Si se deja sin administrar, el volumen del correo electrónico que incrementa constantemente los buzones de correo de los usuarios también puede tener un impacto en la productividad del usuario. Por ejemplo, si bien las suscripciones a boletines y las notificaciones automáticas pueden tener valor informativo cuando se reciben, es posible que los usuarios no las eliminen después de leerlas (a menudo, jamás las leen). No tiene valor retener muchos de estos tipos de mensajes después de un par de días. El uso de MRM para eliminarlos puede ayudar a disminuir el desorden de otros correos en la información de los buzones de los usuarios y, por lo tanto, aumentar la productividad.

  - **Mejorar la administración de almacenamiento**   Debido a las expectativas de los servicios de correo electrónico gratuitos para clientes, muchos usuarios conservan mensajes antiguos durante un largo período antes de eliminarlos. Mantener grandes buzones de correo se está convirtiendo en una práctica estándar, y no se debería forzar a los usuarios a cambiar sus hábitos de trabajo en base a las cuotas restrictivas del buzón de correo. Sin embargo, la retención de mensajes pasado el período necesario por razones empresariales, legales o normativas también incrementa los costos de almacenamiento.

MRM ofrece la flexibilidad de implementar las directivas de administración de registros que mejor se adapten a los requisitos de su organización. Con una buena comprensión de MRM, Archivo local y Conservación local, puede ayudar a cumplir con los objetivos de la administración del almacenamiento de buzones de correo y cumplir con los requisitos de retención normativos.

¿Está buscando las tareas de administración relacionadas con MRM? Vea [Procedimientos de administración de registros de mensajería](messaging-records-management-procedures-exchange-2013-help.md).

## MRM en Exchange Server 2013 y Exchange Online

En Exchange Server 2013 y Exchange Online, MRM se logra mediante el uso de etiquetas y directivas de retención. Las etiquetas de retención se usan para aplicar los ajustes de retención a un buzón de correo entero y a carpetas de buzones de correo predeterminados como los elementos eliminados y de la bandeja de entrada. También puede crear e implementar etiquetas de retención que los usuarios de Outlook 2010 y posteriores y Outlook Web App pueden usar para aplicar a las carpetas o a los mensajes individuales. Una vez creadas, se agregan etiquetas de retención a una directiva de retención y, luego, se aplica la directiva a los usuarios. El Asistente para carpetas administradas, procesa buzones de correo y aplica configuraciones de retención a la directiva de retención del usuario. Para obtener más información sobre las directivas de retención, vea [Etiquetas de retención y directivas de retención](retention-tags-and-retention-policies-exchange-2013-help.md).

Cuando un mensaje alcanza su antigüedad de retención especificada en la etiqueta de retención aplicable, el Asistente para carpetas administradas realiza la acción de retención especificada en la etiqueta. Entonces, es posible eliminar los mensajes con la capacidad de recuperarlos o de forma permanente. Si se aprovisiona un archivo para el usuario, también es posible usar etiquetas de retención para mover elementos al Archivo local.

## Estrategias de MRM

Puede usar directivas de retención para aplicar la retención de mensajes básica para todo el buzón de correo o carpetas predeterminadas específicas. Si bien existen varias estrategias para implementar MRM, estas son algunas de las más comunes:

**Eliminar todos los mensajes después de un período especificado**   En esta estrategia, implementa una única directiva de MRM que elimina todos los mensajes después de un período determinado. En esta estrategia, no hay clasificación de mensajes. Puede implementar esta directiva creando una única etiqueta de directiva predeterminada (DPT) para el buzón de correo. Sin embargo, esto no garantiza que todos los mensajes se retengan durante el período especificado. Los usuarios aún pueden eliminar mensajes antes de alcanzar el período de retención.

**Mover mensajes a buzones de archivo**   En esta estrategia, se implementan directivas de MRM que mueven elementos al buzón de archivo del usuario. Un buzón de archivo proporciona almacenamiento adicional para que los usuarios conserven contenidos antiguos y a los cuales se obtiene acceso poco frecuentemente. Las etiquetas de retención que mueven elementos también se conocen como *directivas de archivo*. En la misma directiva de retención, puede combinar una DPT y etiquetas personales para mover elementos, y una DPT, RPT y etiquetas personales para eliminar elementos. Para obtener más información acerca de las directivas de archivo, vea:

  - **Exchange Server 2013:**  [Archivado local en Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md)

  - **Exchange Online:**  [Buzones de archivo en Exchange Online](https://technet.microsoft.com/es-es/library/dn922147\(v=exchg.150\))


> [!NOTE]
> En una implementación híbrida de Exchange, puede habilitar un buzón de archivo basado en la nube para un buzón principal local. Si asigna una directiva de archivo a un buzón local, los elementos se mueven al archivo basado en la nube. Si un elemento se mueve al buzón de archivo, no se conserva una copia del elemento en el buzón local. Si el buzón local se coloca en retención, una directiva de archivo moverá igualmente los elementos al buzón de archivo basado en la nube, donde se conservarán durante el tiempo especificado por la retención.



**Eliminar mensajes según la ubicación de la carpeta**   En esta estrategia, debe implementar directivas de MRM basadas en la ubicación del correo electrónico. Por ejemplo, puede especificar que los mensajes en la Bandeja de entrada se retengan durante un año y los mensajes en la carpeta Correo no deseado se retengan durante 60 días. Puede implementar esta directiva usando una combinación de etiquetas de directiva de retención (RPT) para cada carpeta predeterminada que desee configurar y una DPT para todo el buzón de correo. La DPT se aplica a las carpetas predeterminadas y todas las carpetas predeterminadas que no tengan una RPT aplicada.


> [!NOTE]
> En Exchange 2013, puede crear RPTs para las carpetas Calendario y Tareas. Si no desea que los elementos de estas carpetas o de otras carpetas predeterminadas expiren, puede crear una etiqueta de retención deshabilitada para dicha carpeta predeterminada.



**Permitir a los usuarios clasificar mensajes**   En esta estrategia, se implementan directivas de MRM que incluyen una configuración de retención básica para todos los mensajes pero permiten a los usuarios clasificar mensajes según requisitos de regulación o empresariales. En este caso, los usuarios se convierten en una parte importante de su estrategia de administración de registros ya que, a menudo, son los que mejor entienden el valor de la retención de un mensaje.

Los usuarios pueden aplicar diferentes configuraciones de retención a los mensajes que se deben conservar durante un período superior o inferior. Puede implementar esta directiva mediante una combinación de lo siguiente:

  - Una DPT para el buzón de correo

  - Etiquetas personales que los usuarios pueden aplicar a carpetas personalizadas o mensajes individuales

  - (Opcional) Agregue RPT para que elementos en carpetas específicas predeterminadas expiren

Por ejemplo, puede usar una directiva de retención con etiquetas personales que tienen un período de retención más corto (como dos días, una semana o un mes), además de etiquetas personales con un período de retención más largo (como un año, dos años o cinco años). Los usuarios pueden aplicar etiquetas personales con períodos de retención más cortos para elementos como suscripciones a boletines que pueden perder su valor dos días después de recibidos, y aplicar las etiquetas con períodos más largos para conservar los elementos de mayor valor empresarial. También pueden automatizar el proceso usando reglas de la Bandeja de entrada en Outlook para aplicar una etiqueta personal a los mensajes que coinciden con las condiciones de la regla.

**Retener mensajes para propósitos de exhibición de documentos electrónicos**   En esta estrategia, se implementan directivas de MRM que eliminan mensajes de buzones después de un período específico, pero también los retienen en la carpeta de Elementos recuperables para propósitos de [Exhibición de documentos electrónicos en contexto](in-place-ediscovery-exchange-2013-help.md), incluso si otro usuario u otro proceso eliminaron los mensajes.

Para cumplir este requisito, puede usar una combinación de directivas de retención y [Conservación local y retención por juicio](in-place-hold-and-litigation-hold-exchange-2013-help.md) o Retención por juicio. Las directivas de retención eliminan los mensajes del buzón de correo después del período especificado. Una Conservación local o una Retención por juicio basada en tiempo preserva los mensajes eliminados o modificados antes de dicho período. Por ejemplo, para retener mensajes durante siete años, puede crear una directiva de retención con una DPT que elimina mensajes en siete años y una Retención por juicio para retener los mensajes durante siete años. Los mensajes que los usuarios no han eliminado, se eliminarán a los siete años, los mensajes eliminados por los usuarios antes de siete años se retendrán en la carpeta Elementos recuperables durante siete años. Para obtener más información acerca de esta carpeta, vea [Carpeta Elementos recuperables](recoverable-items-folder-exchange-2013-help.md).

Como alternativa, puede usar etiquetas personales y RPT para permitir a los usuarios limpiar sus buzones de correo. Sin embargo, la Retención local y la Retención por juicio siguen reteniendo los mensajes eliminados hasta el vencimiento del período de retención.


> [!NOTE]
> Una Retención local o Retención por juicio basada en tiempo es similar a lo que se conocía de forma informal como <EM>retención legal gradual</EM> en Exchange 2010. La Retención legal gradual se implementó configurando el período de retención del elemento eliminado de una base de datos de buzones de correo o buzón de correo individual. Sin embargo, la retención del elemento eliminado retiene los elementos eliminados y modificados en la fecha eliminada. La Retención local y la Retención por juicio conservan los elementos según la fecha de recepción o creación. Esto garantiza que los mensajes se conserven durante, al menos, el período especificado.



## Más información

[Mensajería de registros terminología de administración de Exchange de 2013](messaging-records-management-terminology-in-exchange-2013-exchange-2013-help.md)

[Etiquetas de retención y directivas de retención](retention-tags-and-retention-policies-exchange-2013-help.md)

