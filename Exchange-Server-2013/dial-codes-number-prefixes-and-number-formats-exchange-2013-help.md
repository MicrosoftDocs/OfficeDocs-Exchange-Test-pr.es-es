---
title: 'Códigos de marcado, prefijos numéricos y formatos de número: Exchange 2013 Help'
TOCTitle: Códigos de marcado, prefijos numéricos y formatos de número
ms:assetid: 26d61e55-f8dd-4d25-81f1-78a87cf88bad
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb266967(v=EXCHG.150)
ms:contentKeyID: 51406486
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Códigos de marcado, prefijos numéricos y formatos de número

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2016-05-04_

Puede configurar varios códigos de marcado de los que usa la mensajería unificada (UM) para hacer llamadas internas y externas para usuarios habilitados para UM. Con frecuencia, querrá configurar un plan de marcado con los códigos de marcado o de acceso, un prefijo numérico nacional o los formatos de número nacionales o internacionales para poder controlar las llamadas externas de los usuarios de la organización. En este tema se tratan los códigos de marcado, los prefijos numéricos y los formatos de número, y cómo se pueden usar para controlar las llamadas externas en una organización.

**Contenido**

Introducción

Código de acceso a línea externa

Prefijo de número nacional

Código de acceso nacional o regional

Código de acceso internacional

Formatos de número nacionales o regionales e internacionales

## Introducción

La *llamada externa* es un proceso en el que los usuarios llaman a un plan de marcado de UM o a un operador automático de UM y luego hacen una llamada a un número de teléfono interno o externo. Si un usuario llama a un plan de marcado de UM o a un operador automático de UM y luego realiza una llamada, Mensajería unificada usará la configuración establecida en el plan de marcado, el operador automático y las directivas de buzón de UM para hacer la llamada. Mensajería unificada hace una llamada saliente en las siguientes situaciones:

  - Cuando realiza una llamada a un número de teléfono externo para un llamador

  - Cuando transfiere una llamada a un operador automático

  - Cuando transfiere una llamada a un usuario (ya sea un usuario habilitado para UM o no) de la organización

  - Cuando un usuario habilitado para UM usa la característica Reproducir en el teléfono

La llamada externa la usan dos tipos de usuarios: los autenticados y los no autenticados. Los usuarios sin autenticar llaman a un número de Outlook Voice Access configurado en un plan de marcado de UM, pero no inician sesión en su buzón. Estos usuarios también llaman a un número configurado en un operador automático de UM. Los usuarios autenticados llaman a un número de Outlook Voice Access e inician sesión en su buzón. Si un usuario llama a un número de Outlook Voice Access, al principio se le considera como no autenticado porque no ha dado ni su número de extensión ni su PIN, y tampoco ha iniciado sesión en su buzón. Los usuarios se autentican después de poner su número de extensión y PIN, y de iniciar sesión en su buzón.

Cuando un usuario no autenticado llama a un operador automático de UM y hace una llamada externa, se usa la configuración de llamada externa del plan de marcado y del operador automático de UM. Cuando un usuario sin autenticar llama a un número de Outlook Voice Access que está configurado en un plan de marcado, la única configuración que se usará será la establecida en el plan de marcado. Cuando un usuario ha iniciado sesión en su buzón, se aplica, al usuario autenticado, la configuración del plan de marcado y la directiva de buzón de UM asociada al usuario autenticado.

Para controlar las llamadas externas en la organización, hay que configurar varias opciones. Para controlar las llamadas externas, hay que configurar los planes de marcado de UM, los operadores automáticos y las directivas de buzón de UM en Mensajería unificada. Las siguientes configuraciones se pueden establecer en planes de marcado de UM, operadores automáticos y directivas de buzón de UM para controlar las llamadas externas:

  - Códigos de acceso internacional, nacional y a línea externa

  - Prefijos numéricos nacionales

  - Formatos de número nacional e internacional

  - Grupos de reglas de marcado nacional e internacional

  - Grupos de reglas de marcado nacional e internacional permitidos

  - Entradas de reglas de marcado

Los códigos de acceso, los prefijos numéricos y los formatos de número de un plan de marcado de UM se configuran en la página **Códigos de marcado** del Centro de administración de Exchange (EAC). Estas opciones también se pueden configurar mediante el cmdlet **Set-UMDialPlan** del Shell de administración de Exchange. Puede elegir todas, ninguna o solamente alguna de estas configuraciones. Cada configuración controla una parte específica del proceso de llamada externa.

Mensajería unificada usa códigos de acceso, prefijos numéricos y formatos de número para averiguar el número correcto al que debe llamar. Se pueden configurar para restringir las llamadas salientes de usuarios que llaman a un operador automático de UM asociado con un plan de marcado de UM o que llaman al número de Outlook Voice Access configurado en el plan de marcado.

Para más información sobre las llamadas externas de Mensajería unificada, vea [Códigos de marcado, prefijos numéricos y formatos de número](dial-codes-number-prefixes-and-number-formats-exchange-2013-help.md).

Introducción

## Código de acceso a línea externa

Se puede configurar un código de acceso a línea externa, también conocido como *código de acceso troncal*, en cada plan de marcado que se crea. Este es el número que se usa para acceder a una línea telefónica externa. Este número también está configurado en las centrales de conmutación (PBX) o IP PBX de la organización. En la mayoría de las redes telefónicas, los usuarios marcan el número 9 para acceder a una línea externa y realizar una llamada a un número de teléfono externo.

Hay que configurar un código de acceso a línea externa en cada plan de marcado que se crea. Este código de marcado se aplicará a todos los usuarios vinculados con una directiva de buzón de UM que, a su vez, esté vinculada al plan de marcado de UM. Cuando un llamador vinculado al plan de marcado hace una llamada y el plan de marcado marca la llamada saliente, Mensajería unificada agrega el código de acceso a línea externa (suele ser 9) al principio de la cadena del número marcado para que la PBX o IP PBX pueda marcar el número correctamente. Si no configura el código de acceso a línea externa, la PBX o IP PBX pueden no reconocer el número enviado. Por ejemplo, como hemos explicado, en muchas organizaciones el código de acceso que marcan los usuarios para acceder a una línea externa es el 9, y este código está configurado en una PBX o IP PBX. Mensajería unificada tiene que agregar el código de acceso a línea externa (9) antes de la cadena del número de teléfono para que la PBX o IP PBX marquen correctamente el número saliente. Si se configura el código de marcado de modo que Mensajería unificada agregue el código de acceso a línea externa, Mensajería unificada podrá usar este código para acceder a una línea externa antes de marcar la cadena del número de teléfono externo. El código de marcado que se configure se aplicará a todos los usuarios vinculados a una directiva de buzón de UM que, a su vez, esté vinculada al plan de marcado de UM.

## Prefijo de número nacional

El prefijo numérico nacional y el código de país o región también se pueden configurar en un plan de marcado de UM. Mensajería unificada usa el número escrito para marcar el prefijo numérico nacional o el código de país o región correctos cuando un usuario realiza una llamada saliente destinada al mismo país o región, o una llamada internacional. Por ejemplo, cuando un usuario de Norteamérica realiza una llamada saliente internacional a Europa, Mensajería unificada agregará el prefijo numérico nacional antes de la cadena del número que envía a la PBX o IP PBX para realizar la llamada saliente. El número 1 se usa como prefijo numérico nacional para Norteamérica.

## Código de acceso nacional o regional

En un plan de marcado de UM se puede configurar un código de país o región. El código de acceso de país o región consta de los dígitos que están asociados a un país o una región específicos. Mensajería unificada usa el código de acceso de país o región para marcar el número de teléfono correcto cuando se realiza una llamada a un número de teléfono desde el mismo país o región donde se realiza la llamada. Mensajería unificada agregará este número antes de la cadena de números que envía a la PBX o IP PBX cuando realiza la llamada saliente. Por ejemplo, Mensajería unificada agregará el número 1 a una llamada realizada desde los Estados Unidos y destinada a los Estados Unidos. Para el Reino Unido, el código de país o región es el 44.

## Código de acceso internacional

En un plan de marcado de UM se puede configurar un código de acceso internacional. El código de acceso internacional consta de los dígitos usados para acceder a números de teléfono internacionales. Mensajería unificada usa el código de acceso internacional para marcar el código de acceso internacional correcto cuando se realiza una llamada desde un número de teléfono de un país/región a un número de otro país/región. Mensajería unificada agregará este número antes de la cadena de números que envía a la PBX o IP PBX cuando realiza la llamada saliente. Mensajería unificada usará 011 como código de acceso internacional para los Estados Unidos, por ejemplo. Para Europa, el código de acceso internacional es el 00.

Introducción

## Formatos de número nacionales o regionales e internacionales

En un plan de marcado de UM se puede establecer la configuración de llamadas entrantes para formatos de número nacional e internacional. Una vez establecida esta configuración, Mensajería unificada podrá diferenciar las llamadas entrantes provenientes de un país o región y las llamadas internacionales de los planes de marcado de UM de una misma organización. También puede agregar formatos de número para las llamadas entrantes que se hacen dentro de un mismo plan de marcado. La configuración de estas opciones permite a la organización ahorrar dinero al evitar las llamadas salientes que los usuarios no están autorizados a hacer desde la organización, a la vez que ayuda a evitar el fraude tarifario. Mensajería unificada usará la información configurada para examinar el formato de número de la llamada entrante y comprobar que el patrón de número coincide antes de aceptar la llamada. Por ejemplo, es posible que tenga varios planes de marcado en una organización. Si tiene un plan de marcado para los Estados Unidos y otro para el Reino Unido, puede que quiera permitir a los usuarios del plan de marcado de los Estados Unidos hacer llamadas con Mensajería unificada a usuarios ubicados en el Reino Unido, pero, en cambio, no permitirles hacer llamadas a otros países o regiones ni llamadas internacionales directamente.

