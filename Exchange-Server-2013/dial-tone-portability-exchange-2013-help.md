---
title: 'Portabilidad del tono de marcado: Exchange 2013 Help'
TOCTitle: Portabilidad del tono de marcado
ms:assetid: ea62fae0-5e0a-460c-beb6-52532c8c8dbc
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd876950(v=EXCHG.150)
ms:contentKeyID: 51406568
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Portabilidad del tono de marcado

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2013-01-28_

La portabilidad del tono de marcado es una función de Microsoft Exchange Server 2013 que proporciona una solución de continuidad empresarial limitada para los errores que afectan a una base de datos de buzones, un servidor o un sitio completo. La portabilidad del tono de marcado permite a los usuarios tener un buzón temporal para enviar y recibir mensajes de correo electrónico mientras su buzón original se restaura o repara. El buzón temporal puede estar en el mismo servidor de buzones de Exchange 2013 o en cualquier otro servidor de buzones de Exchange 2013 de su organización que tenga bases de datos con la misma versión de esquema de la base de datos. Esto permite que un servidor alternativo hospede los buzones de los usuarios que estaban previamente en un servidor que ya no estará disponible. Los clientes que son compatibles con la Detección automática se redirigen automáticamente al nuevo servidor sin necesidad de actualizar manualmente el perfil de escritorio del usuario. Una vez restaurados los datos del buzón original del usuario, un administrador puede combinar un buzón recuperado del usuario con el buzón de tono de marcado del usuario y crear un solo buzón actualizado.

El proceso para usar la portabilidad del tono de marcado se denomina *recuperación del tono de marcado*. Una recuperación del tono de marcado implica la creación de una base de datos vacía en un servidor de buzones para sustituir la base de datos en la que se produjeron los errores. Esta base de datos vacía, conocida como una *base de datos de tonos de marcado*, permite a los usuarios enviar y recibir mensajes de correo electrónico mientras se recupera la base de datos con error.

Existen tres opciones para realizar una recuperación del tono de marcado:

  - **Recuperación del tono de marcado en el servidor con la base de datos con errores**   Si el servidor que hospeda la base de datos con errores sigue operativo, se recomienda llevar a cabo una recuperación del tono de marcado en dicho servidor. Esto significa menos tiempo de inactividad, ya que no es necesario mover los archivos de la base de datos entre servidores. Además, no tendrá que volver a configurar los perfiles de mensajería de los clientes que no sean compatibles con la detección automática.

  - **Recuperación del tono de marcado mediante un servidor alternativo para la base de datos de tonos de marcado**   Si se producen errores en un servidor y es necesario reconstruirlo, la forma más eficaz de proporcionar a los usuarios una funcionalidad de correo básica consiste en crear una base de datos de tonos de marcado en otro servidor y utilizar la portabilidad de la base de datos para mover la configuración del buzón de usuario al nuevo servidor. Dado que este proceso implica devolver la base de datos de tonos de marcado al servidor original (recuperado), esta opción supone más tiempo para el proceso de recuperación global. Además, este proceso es más complejo que realizar una recuperación de tono de marcado en el servidor original. Cuando realice este proceso, el servidor que hospeda la base de datos de tonos de marcado debe tener los recursos suficientes para admitir la carga agregada de los usuarios adicionales. Además, si el cliente de los usuarios no admite la Detección automática, el perfil de mensajería deberá volver a configurarse para que apunte al servidor de tono de marcado.

  - **Recuperación del tono de marcado usando un servidor alternativo para la base de datos de tonos de marcado**   Es similar a la opción anterior, excepto en que no se necesita volver al servidor original. Esta opción se recomienda para situaciones en las que no es posible o viable recuperar el servidor con error. En este caso, los usuarios normalmente se quedan en un servidor alternativo una vez completada la operación de recuperación. Cuando realice este proceso, el servidor que hospeda la base de datos de tonos de marcado debe tener los recursos suficientes para admitir la carga agregada de los usuarios adicionales. Además, si el cliente de los usuarios no admite la Detección automática, el perfil de mensajería deberá volver a configurarse para que apunte al servidor de tono de marcado.

Las tres opciones siguen los mismos pasos básicos:

1.  **Crear una base de datos de tonos de marcado vacía para reemplazar la base de datos con error.**
    
    Esta nueva base de datos permitirá a los usuarios que tenían buzones en la base de datos con errores enviar y recibir nuevos mensajes. La portabilidad de tonos de marcado permite hacer que un usuario señale a una base de datos diferente sin tener que mover el buzón. Si creó la base de datos de tono de marcado en un servidor diferente al servidor en el que estaba la base de datos con errores, necesitará mover la configuración del buzón a ese nuevo servidor.

2.  **Restaurar la base de datos antigua.**
    
    Use el software de copia de seguridad y recuperación que suela usar para restaurar la base de datos con errores. Si no hay una copia de seguridad de la base de datos con errores, recupere dicha base de datos por otros medios, si es posible. Si usa el mismo servidor para la recuperación de tonos de marcado, necesitará restaurar la base de datos a una base de datos de recuperación.

3.  **Intercambiar la base de datos de tonos de marcado con la base de datos restaurada.**
    
    Después de restaurar la base de datos con errores, cámbiela por la base de datos de tonos de marcado. Esto permite a los usuarios enviar y recibir correo electrónico y tener acceso a todos los datos de la base de datos restaurada. Si los usuarios se trasladan a una base de datos de tonos de marcado en otro servidor, será necesario devolver la configuración del buzón al servidor original.

4.  **Combinar las bases de datos.**
    
    Para desplazar la base de datos de tonos de marcado a la base de datos restaurada, combine los datos usando el cmdlet [New-MailboxRestoreRequest](https://technet.microsoft.com/es-es/library/ff829875\(v=exchg.150\)).

Para ver los pasos detallados para realizar una recuperación del tono de marcado, consulte [Realizar una recuperación del tono de marcado](perform-a-dial-tone-recovery-exchange-2013-help.md).

