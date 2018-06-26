---
title: 'Cambios y conmutaciones por error: Exchange 2013 Help'
TOCTitle: Cambios y conmutaciones por error
ms:assetid: 75388645-cae1-402e-bf02-c4949d3e2c31
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd298067(v=EXCHG.150)
ms:contentKeyID: 62523848
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Cambios y conmutaciones por error

 

_**Se aplica a:**Exchange Server 2013 SP1_

_**Última modificación del tema:**2015-12-02_

Los cambios y las conmutaciones por error son las dos formas de interrupciones en Microsoft Exchange Server 2013.

  - Un *cambio* es una interrupción programada de una base de datos o servidor que es iniciada explícitamente por un cmdlet o por el sistema de disponibilidad administrada en Exchange de 2013. Los cambios suelen llevarse a cabo como preparación para realizar una operación de mantenimiento. Los cambios implican que la copia activa de la base de datos de buzones de correo se mueve a otro servidor en el grupo de disponibilidad de base de datos (DAG). Si no se encuentra ningún destino correcto durante un cambio, los administradores recibirán un error y la base de datos de buzón permanecerá activa o montada.

  - Una *conmutación por error* es un evento inesperado que hace que los datos, los servicios o ambos no estén disponibles. Una conmutación por error implica que el sistema se recupere automáticamente de un error al activar una copia pasiva de la base de datos de buzones de correo para convertirla en la copia activa de la base de datos de buzones de correo. Si no se encuentra ningún destino correcto durante una conmutación por error, se desmontará la base de datos de buzones de correo.

Exchange 2013 está diseñado específicamente para tratar tanto los cambios como las conmutaciones por error.

¿Está buscando tareas de administración relacionadas con la alta disponibilidad y la resistencia del sitio? Vea [Administración de alta disponibilidad y resistencia de sitios](managing-high-availability-and-site-resilience-exchange-2013-help.md).

## Cambios

Existen tres tipos de cambios en Exchange 2013:

  - Cambios de base de datos

  - Cambios de servidor

  - Cambios de centro de datos

## Cambios de base de datos

Un *cambio de base de datos* es el proceso por el cual una base de datos activa individual se pasa a otra copia de la base de datos (una copia pasiva), y dicha copia de la base de datos se convierte en la nueva copia activa de la base de datos. Los cambios de base de datos pueden ocurrir tanto dentro de los centros de datos como entre ellos. Se puede realizar un cambio de base de datos mediante el Centro de administración de Exchange (EAC) o el Shell. Independientemente de la interfaz que se use, el proceso de cambio es el siguiente:

1.  El administrador inicia un cambio de base de datos para mover la copia actualmente activa de la base de datos de buzones de correo a otro servidor.

2.  El cliente usado para la tarea realiza una llamada RPC al servicio de replicación de Microsoft Exchange en un miembro del DAG.

3.  Si el miembro de DAG no cuenta con el rol de administrador activo principal (PAM), envía la tarea al servidor que contiene el rol de PAM.

4.  La tarea realiza una llamada RPC al servicio de replicación de Microsoft Exchange en el servidor que contiene el rol de PAM.

5.  El PAM lee y actualiza la información de la ubicación de la base de datos que está almacenada en la base de datos del clúster para el DAG.

6.  El PAM se pone en contacto con el servicio de replicación de Microsoft Exchange en el miembro del DAG cuya copia pasiva se está activando como la nueva copia activa de la base de datos de buzones de correo.

7.  El servicio de replicación de Microsoft Exchange en el servidor de destino solicita a los servicios de replicación de Microsoft Exchange en todos los demás miembros del DAG que determinen el mejor origen del registro para la copia de la base de datos.

8.  La base de datos se desmonta del servidor actual, y el servicio de replicación de Microsoft Exchange en el servidor de destino copia los registros restantes en el servidor de destino.

9.  El servicio de replicación de Microsoft Exchange en el servidor de destino solicita un montaje de base de datos.

10. El servicio de almacén de información de Microsoft Exchange en el servidor de destino reproduce los archivos de registro y monta la base de datos.

11. Los códigos de error se devuelven al servicio de replicación de Microsoft Exchange en el servidor de destino.

12. El PAM actualiza la información del estado de la copia de la base de datos en la base de datos del clúster para el DAG.

13. Los códigos de error son devueltos por el servicio de replicación de Microsoft Exchange en el servidor de destino al servicio de replicación de Microsoft Exchange en el PAM.

14. El servicio de replicación de Microsoft Exchange en el PAM devuelve los errores a la interfaz administrativa en la cual se llamó a la tarea.

15. PowerShell en remoto devuelve los resultados de la operación a la interfaz administrativa que realiza la llamada.

Para obtener instrucciones detalladas acerca de cómo realizar un cambio de base de datos, vea [Activación de una copia de base de datos de buzones](activate-a-mailbox-database-copy-exchange-2013-help.md).

## Cambios de servidor

Un cambio de servidor es el proceso por el cual todas las bases de datos activas en un miembro del DAG se activan en uno o más miembros del DAG. Al igual que los cambios de base de datos, se puede producir un cambio de servidor tanto dentro de un centro de datos como entre centros de datos, y puede ser iniciado mediante el uso del EAC y el Shell. Independientemente de la interfaz que se use, el proceso de cambio de servidor es el siguiente:

1.  El administrador inicia un cambio de servidor para mover todas las copias actualmente activas de la base de datos de buzones de correo a uno o más servidores.

2.  La tarea realiza los mismos pasos detallados anteriormente en este tema para los cambios de base de datos (pasos 2 a 4) de cada una de las bases de datos activas en el servidor actual.

3.  El PAM lee y actualiza la información de la ubicación de la base de datos que está almacenada en la base de datos del clúster para el DAG.

4.  El PAM se pone en contacto con el servicio de replicación de Microsoft Exchange en cada miembro del DAG en el cual se está activando una copia pasiva.

5.  El servicio de replicación de Microsoft Exchange en los servidores de destino solicita a los servicios de replicación de Microsoft Exchange en todos los demás miembros del DAG que determinen el mejor origen del registro para la copia de la base de datos.

6.  La base de datos se desmonta del servidor actual, y el servicio de replicación de Microsoft Exchange en cada servidor de destino copia los registros restantes.

7.  El servicio de replicación de Microsoft Exchange en cada servidor de destino solicita un montaje de base de datos.

8.  El servicio de almacén de información de Microsoft Exchange en cada servidor de destino reproduce los archivos de registro y monta la base de datos.

9.  Los códigos de error se devuelven al servicio de replicación de Microsoft Exchange en el servidor de destino.

10. El PAM actualiza la información del estado de la copia de la base de datos en la base de datos del clúster para el DAG.

11. Los códigos de error son devueltos por el servicio de replicación de Microsoft Exchange en el servidor de destino al servicio de replicación de Microsoft Exchange en el PAM.

12. El servicio de replicación de Microsoft Exchange en el PAM devuelve los errores a la interfaz administrativa en la cual se llamó a la tarea.

13. PowerShell en remoto devuelve los resultados de la operación a la interfaz administrativa que realiza la llamada.

Para obtener instrucciones detalladas acerca de cómo realizar un cambio de servidor, vea [Realizar un cambio de servidor](perform-a-server-switchover-exchange-2013-help.md).

## Cambios de centro de datos

En una configuración con resistencia de sitios se puede producir una recuperación automática en respuesta a un fallo en el nivel de sitio dentro de un DAG, lo que permitiría al sistema de mensajería permanecer operativo. Esta configuración requiere al menos tres ubicaciones ya que necesita la implementación de los miembros de DAG en dos ubicaciones y el servidor de testigo de DAG en una tercera.

Si no dispone de tres ubicaciones, o incluso si las tiene pero desea controlar la acciones de recuperación en el nivel del centro de datos, puede configurar el DAG para su recuperación manual en caso de que se produzca un fallo en el nivel de sitio. En ese caso, realizará un proceso denominado *cambio de centro de datos*. Como sucede con muchas situaciones de recuperación ante desastres, la planificación y la preparación anticipadas de un cambio de centro de datos pueden simplificar el proceso de recuperación y reducir la duración de la interrupción.

Debido a los numerosos cambios en la arquitectura de Exchange 2013, incluida la consolidación de los roles de servidor, la realización de un cambio de centro de datos en Exchange 2013 es considerablemente más fácil de lo que era en Exchange 2010. Para obtener el procedimiento detallado de cómo realizar un cambio de centro de datos, vea [Cambios en el centro de datos](datacenter-switchovers-exchange-2013-help.md).

## Conmutaciones por error

Una conmutación por error es un proceso de activación automática que tiene lugar en el nivel de la base de datos, el servidor o el centro de datos. Las conmutaciones por error ocurren en respuesta a un error que afecta a una base de datos individual (por ejemplo, una pérdida de almacenamiento aislada), a un servidor completo (por ejemplo, un error en la placa base o una pérdida de energía) o a un sitio completo (por ejemplo, la pérdida de todos los miembros de DAG de un sitio).

Los DAG y las copias de bases de datos de buzones de correo proporcionan una redundancia completa y una recuperación rápida tanto de los datos como de los servicios que permiten obtener acceso a los datos. En la siguiente tabla, se describen las acciones de recuperación previstas para diversos errores. Algunos errores requieren que el administrador inicie la recuperación, mientras que otros son administrados automáticamente por el sistema.


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
<thead>
<tr class="header">
<th>Descripción</th>
<th>Activación automática</th>
<th>Acción de reparación automática</th>
<th>Estado durante la reparación: Activo</th>
<th>Estado durante la reparación: Pasivo</th>
<th>Acciones de reparación</th>
<th>Comentarios</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Error en la base de datos de software del motor de almacenamiento extensible (ESE): Las unidades que almacenan la base de datos devuelven errores en algunas lecturas (por ejemplo, un error -1018).</p></td>
<td><p>Posible interrupción breve.</p>
<p>Posible conmutación por error automática.</p></td>
<td><p>Aplicación de revisión automática de página errónea.</p></td>
<td><p>Cambio manual, conmutación por error automática o reparación en línea.</p></td>
<td><p>Error</p></td>
<td><p>Reconstruir RAID, reparar copia de base de datos y base de datos, restaurar y ejecutar la recuperación, y luego aplicar la revisión de páginas, o aplicar la revisión de páginas de la copia.</p></td>
<td><p>Puede haber otros códigos de error de base de datos de software.</p>
<p>No se incluyen errores de bloqueo del sistema de archivos NTFS.</p>
<p>Si se realiza una conmutación por error o un cambio, se actualiza el servidor host.</p></td>
</tr>
<tr class="even">
<td><p>Error en la base de datos &quot;<em>semisoft</em>&quot; de ESE: Las unidades que almacenan la base de datos devuelven errores en algunas escrituras.</p></td>
<td><p>Interrupción breve durante la conmutación por error automática.</p></td>
<td><p>Reconstrucción automática de volumen o disco después de un posible reemplazo de unidad.</p></td>
<td><p>Desmontar si no se puede recuperar.</p></td>
<td><p>Error</p></td>
<td><p>La reconstrucción de RAID puede resolver el problema.</p>
<p>Copiar y reparar, restaurar y ejecutar una recuperación, o reconstruir el disco o volumen después de un posible reemplazo.</p></td>
<td><p>Un error de escritura semisoft de ESE significa que algunas escrituras son correctas.</p>
<p>No se incluye un error de bloqueo de NTFS.</p></td>
</tr>
<tr class="odd">
<td><p>Error en el registro &quot;semisoft&quot; de ESE: Las unidades que almacenan los datos del registro devuelven errores no recuperados en algunas lecturas o escrituras.</p></td>
<td><p>Interrupción breve durante la conmutación por error automática.</p></td>
<td><p>Reconstrucción automática de volumen o disco después de un posible reemplazo de unidad.</p></td>
<td><p>Desmontar si no se puede recuperar.</p></td>
<td><p>Error</p></td>
<td><p>La reconstrucción de RAID puede resolver el problema.</p>
<p>Copiar y reparar, restaurar y ejecutar una recuperación, o reconstruir el disco o volumen después de un posible reemplazo.</p></td>
<td><p>Un error de lectura o escritura semisoft de ESE significa que algunas lecturas o escrituras son correctas.</p>
<p>Si la base de datos falla, una recuperación automática ocurrirá antes de que comience el proceso de recuperación de datos del registro.</p></td>
</tr>
<tr class="even">
<td><p>Agotamiento de recursos o error de software de ESE: Un error en el cual ESE termina la instancia (por ejemplo, Id. de evento 1022, gran profundidad de punto de control).</p></td>
<td><p>Interrupción breve durante la conmutación por error automática.</p></td>
<td><p>Ninguno.</p></td>
<td><p>Desmontar si no se puede recuperar.</p></td>
<td><p>Error</p></td>
<td><p>Solucionar problema de recursos subyacente.</p></td>
<td><p>Este error podría ser el error expuesto de otros casos.</p></td>
</tr>
<tr class="odd">
<td><p>Errores de bloqueo de NTFS: Las unidades que almacenan la base de datos o los registros experimentan un error de escritura o lectura en una estructura de control de NTFS.</p></td>
<td><p>Interrupción breve durante la conmutación por error automática.</p></td>
<td><p>Volumen reconstruido completamente después de un posible reemplazo de unidad.</p></td>
<td><p>Desmontar si no se puede recuperar.</p></td>
<td><p>Error</p></td>
<td><p>La reconstrucción de RAID puede resolver el problema. Las utilidades de NTFS pueden resolver los problemas de NTFS. Es posible que se requiera la recuperación de Exchange.</p></td>
<td><p>Esto es más probable que ocurra cuando RAID no está en uso. Si esto afecta el volumen activo del registro, algunos archivos de registro recientes se perderán.</p>
<p>No se incluyen errores corregidos de manera automática por NTFS, su software subyacente ni su pila de hardware.</p></td>
</tr>
<tr class="even">
<td><p>Error en la unidad de base de datos o de registro: Una unidad que almacena la base de datos o los registros ha fallado completamente y no se puede obtener acceso a ella.</p></td>
<td><p>Interrupción breve durante la conmutación por error automática.</p></td>
<td><p>Unidad reformateada o reemplazada, seguida de una reconstrucción completa del volumen.</p></td>
<td><p>Desmontar si no se puede recuperar.</p></td>
<td><p>Error</p></td>
<td><p>Reemplazo de unidad, seguido de una posible reconstrucción de RAID.</p>
<p>Reemplazo de unidad, seguido de una reconstrucción completa del volumen.</p>
<p>Reconstrucción completa del volumen.</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="odd">
<td><p>Error en el volumen de base de datos o de registro: Se produce un error en el volumen debido a problemas de nivel más bajo de volumen o NTFS.</p></td>
<td><p>Interrupción breve durante la conmutación por error automática.</p></td>
<td><p>Unidad reformateada o reemplazada.</p></td>
<td><p>Desmontar si no se puede recuperar.</p></td>
<td><p>Error</p></td>
<td><p>Reemplazo de unidad, seguido de una posible reconstrucción de RAID.</p>
<p>Reemplazo de unidad, seguido de una reconstrucción completa del volumen.</p>
<p>Reconstrucción completa del volumen.</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="even">
<td><p>Volumen de base de datos o registro sin espacio: El sistema de archivos NTFS con los archivos de registro o base de datos no tiene espacio.</p></td>
<td><p>Conmutación por error automática si otra copia no está en un estado similar.</p></td>
<td><p>Ninguno.</p></td>
<td><p>Desmontado.</p></td>
<td><p>Error</p></td>
<td><p>Ejecutar copias de seguridad incrementales o completas; eliminar registros de forma manual; esperar; reanudar la copia de la base de datos; o reparar la copia de la base de datos que falló.</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="odd">
<td><p>El administrador desmonta la base de datos incorrecta.</p></td>
<td><p>Si la conmutación por error automática no es bloqueada por el administrador, ocurrirá una breve interrupción.</p>
<p>Si la conmutación por error automática es evitada, habrá una interrupción hasta que la base de datos se monte.</p></td>
<td><p>Ninguno.</p></td>
<td><p>Desmontado.</p></td>
<td><p>No aplicable</p></td>
<td><p>El administrador corrige el error.</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="even">
<td><p>El administrador suspende la copia de la base de datos incorrecta.</p></td>
<td><p>En función de la configuración y la copia afectada, puede evitarse la recuperación automática.</p></td>
<td><p>Ninguno.</p></td>
<td><p>No aplicable</p></td>
<td><p>Suspended</p></td>
<td><p>El administrador corrige el error.</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="odd">
<td><p>El administrador desmonta una base de datos para el mantenimiento de almacenamiento, NTFS o volumen.</p></td>
<td><p>Si la conmutación por error automática no es bloqueada por el administrador, ocurrirá una breve interrupción.</p>
<p>Si la conmutación por error automática es bloqueada, habrá una interrupción hasta que el administrador complete la tarea.</p></td>
<td><p>Ninguno.</p></td>
<td><p>Desmontado.</p></td>
<td><p>No aplicable</p></td>
<td><p>El administrador finaliza la tarea.</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="even">
<td><p>El administrador suspende una copia de la base de datos para el mantenimiento de almacenamiento, NTFS o volumen.</p></td>
<td><p>En función de la configuración y la copia afectada, puede evitarse la recuperación automática.</p></td>
<td><p>Ninguno.</p></td>
<td><p>No aplicable</p></td>
<td><p>Suspended</p></td>
<td><p>El administrador completa las acciones.</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="odd">
<td><p>El administrador desmonta una base de datos para el mantenimiento de la base de datos sin conexión.</p></td>
<td><p>Interrupción hasta que se haya reparado.</p></td>
<td><p>Ninguno.</p></td>
<td><p>Desmontado.</p></td>
<td><p>Suspended</p></td>
<td><p>El administrador completa las acciones.</p></td>
<td><p>Las copias activas y pasivas de la base de datos se separan.</p>
<p>El administrador debe suspender las copias.</p></td>
</tr>
<tr class="even">
<td><p>Error de red de área de almacenamiento (SAN), disco o controlador de almacenamiento.</p></td>
<td><p>Interrupción breve durante la conmutación por error automática.</p></td>
<td><p>Ninguno.</p></td>
<td><p>Desmontado.</p></td>
<td><p>Cualquiera</p></td>
<td><p>Reparar el hardware.</p></td>
<td><p>Una copia pasiva de la base de datos estará en el estado en que se encontraba en el momento en que falló el sistema.</p></td>
</tr>
<tr class="odd">
<td><p>Mantenimiento de hardware del servidor.</p></td>
<td><p>Interrupción breve durante la conmutación por error automática (a menos que sea bloqueada por un administrador).</p></td>
<td><p>Ninguno.</p></td>
<td><p>Desmontado.</p></td>
<td><p>Cualquiera</p></td>
<td><p>Completar las acciones.</p></td>
<td><p>Una copia pasiva de la base de datos estará en el estado en que se encontraba en el momento en que se apagó el sistema.</p></td>
</tr>
<tr class="even">
<td><p>Mantenimiento de software del servidor.</p></td>
<td><p>Interrupción breve durante la conmutación por error automática (a menos que sea bloqueada por un administrador).</p></td>
<td><p>Ninguno.</p></td>
<td><p>Desmontado.</p></td>
<td><p>Cualquiera</p></td>
<td><p>Completar las acciones.</p></td>
<td><p>Una copia pasiva de la base de datos estará en el estado en que se encontraba en el momento en que se apagó el sistema.</p></td>
</tr>
<tr class="odd">
<td><p>Un administrador ha interrumpido o detenido el servicio Almacén de información de Microsoft Exchange.</p></td>
<td><p>Interrupción breve durante la conmutación por error automática.</p></td>
<td><p>Ninguno.</p></td>
<td><p>Desmontado.</p></td>
<td><p>Cualquiera</p></td>
<td><p>Reiniciar el servicio de almacén de información de Microsoft Exchange.</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="even">
<td><p>Se produce un error en el servicio de almacén de información de Microsoft Exchange; el sistema operativo aún se está ejecutando.</p></td>
<td><p>Interrupción breve durante la conmutación por error automática.</p></td>
<td><p>El Administrador de control de servicios reinicia el servicio de almacén de información de Microsoft Exchange.</p></td>
<td><p>Desmontado.</p></td>
<td><p>Cualquiera</p></td>
<td><p>Reiniciar de forma manual o automática el servicio de almacén de información de Microsoft Exchange.</p></td>
<td><p>Una copia pasiva de la base de datos estará en el estado en que se encontraba cuando falló el servicio de almacén de información de Microsoft Exchange.</p></td>
</tr>
<tr class="odd">
<td><p>Error parcial en el servicio de almacén de información de Microsoft Exchange; cierta parte del almacén de Exchange deja de funcionar, pero no se identifica como un error completo.</p></td>
<td><p>Posible interrupción breve durante la conmutación por error automática.</p></td>
<td><p>Ninguno.</p></td>
<td><p>Montado y parcialmente funcional.</p></td>
<td><p>Cualquiera, pero puede estar sólo parcialmente funcional</p></td>
<td><p>Reiniciar el servidor, el sistema operativo o el servicio de almacén de información de Microsoft Exchange.</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="even">
<td><p>Error en el servidor: El servidor ha producido un error debido a una de las siguientes razones:</p>
<ul>
<li><p>Error total de alimentación</p></li>
<li><p>Error no recuperado del chip del procesador, la placa base o el backplane</p></li>
<li><p>Error de detención de sistema operativo</p></li>
<li><p>El sistema operativo deja de responder</p></li>
<li><p>Error total de comunicación</p></li>
</ul></td>
<td><p>Interrupción breve durante la conmutación por error automática.</p></td>
<td><p>Reiniciar el equipo.</p></td>
<td><p>Desmontado.</p></td>
<td><p>Cualquiera</p></td>
<td><p>Restaurar la energía; cambiar la configuración del sistema operativo; cambiar la configuración del hardware; reemplazar el hardware; reiniciar el sistema operativo; reparar el sistema operativo; reparar el hardware; o reparar los problemas de comunicación.</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="odd">
<td><p>El DAG tiene un error de quórum.</p></td>
<td><p>Interrupción hasta que se haya reparado.</p></td>
<td><p>Ninguno.</p></td>
<td><p>Desmontado.</p></td>
<td><p>Cualquiera</p></td>
<td><p>Reparar el quórum que falló; asignar un nuevo quórum; o restaurar la red que está provocando el error de quórum.</p></td>
<td><p>Una copia pasiva de la base de datos estará en el estado en que se encontraba en el momento en que falló el sistema.</p></td>
</tr>
<tr class="even">
<td><p>Error de comunicación de red MAPI: El servidor ya no está disponible en la red MAPI.</p></td>
<td><p>Interrupción breve durante la conmutación por error automática; no deben existir pérdidas.</p></td>
<td><p>Ninguno. La comunicación se sigue intentado.</p></td>
<td><p>Desmontado.</p></td>
<td><p>Cualquiera</p></td>
<td><p>Solucionar problema de comunicación corrigiendo problemas de hardware o software.</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="odd">
<td><p>Error de comunicación de red de replicación: El servidor no puede recibir latidos, copias de registro ni valores de inicialización por medio de la red de replicación que falló.</p></td>
<td><p>Posible interrupción breve de inicialización o copia mientras la carga de trabajo se cambia a otra red.</p></td>
<td><p>Ninguno. La comunicación se sigue intentado.</p></td>
<td><p>Ninguno.</p></td>
<td><p>Cualquiera</p></td>
<td><p>Solucionar problema de comunicación corrigiendo problemas de hardware o software.</p></td>
<td><p>Resistencia afectada por el error.</p></td>
</tr>
<tr class="even">
<td><p>Error múltiple de comunicación de red: El servidor no puede recibir latidos, copias de registro ni valores de inicialización por medio de varias redes.</p></td>
<td><p>Interrupción breve durante la conmutación por error automática; no deben existir pérdidas.</p></td>
<td><p>Ninguno. La comunicación se sigue intentado.</p></td>
<td><p>Desmontado.</p></td>
<td><p>Cualquiera</p></td>
<td><p>Solucionar problema de comunicación corrigiendo problemas de hardware o software.</p></td>
<td><p>Al menos una red todavía funciona.</p></td>
</tr>
<tr class="odd">
<td><p>Error parcial de una o varias redes: Las redes tienen tasas de error elevadas.</p></td>
<td><p>Error no detectado; sin acción.</p></td>
<td><p>Ninguno.</p></td>
<td><p>Montado; pero posibles problemas de rendimiento.</p></td>
<td><p>Cualquiera</p></td>
<td><p>Solucionar problema de comunicación corrigiendo problemas de hardware o software.</p></td>
<td><p>La red tiene tasas de error superiores a las normales.</p></td>
</tr>
<tr class="even">
<td><p>Bloqueo del sistema operativo no detectado: El sistema operativo deja de responder; pero no se detecta mediante supervisión ni agrupación en clústeres.</p></td>
<td><p>Ninguno.</p></td>
<td><p>Ninguno.</p></td>
<td><p>Cualquiera.</p></td>
<td><p>Cualquiera</p></td>
<td><p>Reiniciar o terminar los recursos que no responden.</p></td>
<td><p>No se detectó el bloqueo, por lo que no se toma ninguna acción.</p>
<p>Algunas funciones pueden estar operativas.</p></td>
</tr>
<tr class="odd">
<td><p>La unidad del sistema operativo tiene un error.</p></td>
<td><p>Interrupción breve durante la conmutación por error automática.</p></td>
<td><p>Ninguno.</p></td>
<td><p>Desmontado.</p></td>
<td><p>Cualquiera</p></td>
<td><p>Reemplazar la unidad y reconstruir el servidor, o reconstruir el volumen utilizando RAID.</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="even">
<td><p>La unidad del sistema operativo se ha quedado sin espacio.</p></td>
<td><p>Interrupción breve durante la conmutación por error automática.</p></td>
<td><p>Ninguno.</p></td>
<td><p>Desmontado.</p></td>
<td><p>Cualquiera</p></td>
<td><p>Liberar manualmente espacio en el volumen.</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="odd">
<td><p>La unidad que contiene archivos binarios de Exchange tiene un error en la unidad o en el volumen.</p></td>
<td><p>Interrupción breve durante la conmutación por error automática.</p></td>
<td><p>Ninguno.</p></td>
<td><p>Desmontado.</p></td>
<td><p>Cualquiera</p></td>
<td><p>Reemplazar la unidad y volver a instalar la aplicación, o reconstruir el volumen usando RAID.</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="even">
<td><p>La unidad que contiene los archivos binarios de Exchange se ha quedado sin espacio.</p></td>
<td><p>Interrupción breve durante la conmutación por error automática.</p></td>
<td><p>Ninguno.</p></td>
<td><p>Desmontado.</p></td>
<td><p>Cualquiera</p></td>
<td><p>Liberar manualmente espacio en el volumen.</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="odd">
<td><p>Nuevo registro no válido detectado: La secuencia de registro es interrumpida por un archivo existente.</p></td>
<td><p>Breve interrupción durante la conmutación por error automática; suponer que otras copias no tienen el mismo problema.</p></td>
<td><p>Ninguno.</p></td>
<td><p>Desmontado.</p></td>
<td><p>Error</p></td>
<td><p>Quitar registros perjudiciales después de determinar el origen.</p></td>
<td><p>No se deben replicar los registros perjudiciales.</p></td>
</tr>
<tr class="even">
<td><p>La replicación continua detecta registro no válido: La reproducción detecta un registro inadecuado durante la copia o reproducción.</p></td>
<td><p>No aplicable</p></td>
<td><p>Descartar registro.</p></td>
<td><p>No aplicable</p></td>
<td><p>Error</p></td>
<td><p>Descartar registro no válido; mover la secuencia de registro que afecta.</p></td>
<td><p>No aplicable</p></td>
</tr>
</tbody>
</table>


## Conmutaciones por error de base de datos

Una conmutación por error de base de datos sucede cuando una copia de la base de datos que estaba activa ya no puede permanecer activa. Como parte de una conmutación por error de base de datos, ocurre lo siguiente:

1.  El error de base de datos es detectado por el servicio de almacén de información de Microsoft Exchange.

2.  El servicio de almacén de información de Microsoft Exchange escribe eventos de error en el registro de eventos del canal crimson.

3.  El administrador activo en el servidor que contiene la base de datos con error detecta los eventos de error.

4.  El administrador activo solicita el estado de la copia de la base de datos de otros servidores que contienen una copia de la base de datos.

5.  Los demás servidores devuelven el estado de la copia de la base de datos solicitado al administrador activo que lo solicita.

6.  El PAM comienza a mover la base de datos activa a otro servidor en el DAG mediante un algoritmo de selección de la mejor copia.

7.  El PAM actualiza la ubicación de montaje de la base de datos en la base de datos del clúster para enviarla al servidor seleccionado.

8.  El PAM envía una solicitud al administrador activo en el servidor seleccionado para convertirse en el patrón de base de datos.

9.  El administrador activo en el servidor seleccionado solicita que el servicio de replicación de Microsoft Exchange intente copiar los últimos registros del servidor anterior y establezca la marca de montaje para la base de datos.

10. El servicio de replicación de Microsoft Exchange copia los registros del servidor que tenía previamente la copia activa de la base de datos.

11. El administrador activo lee el número de generación de registro máximo de la base de datos del clúster.

12. El servicio de almacén de información de Microsoft Exchange monta la nueva copia activa de la base de datos.

## Conmutaciones por error de servidor

Una conmutación por error de servidor sucede cuando el miembro del DAG ya no puede reparar la red MAPI, o cuando el Servicio de clúster en un miembro del DAG ya no puede ponerse en contacto con los miembros del DAG restantes. Como parte de una conmutación por error de servidor, ocurre lo siguiente:

1.  El Servicio de clúster en el PAM envía una notificación al PAM por una de las dos razones:
    
    1.  **Nodo inactivo**   El servidor es accesible, pero no puede participar en las operaciones del DAG.
    
    2.  **Red MAPI inactiva**   No se puede poner en contacto con el servidor mediante la red MAPI; por lo tanto, el servidor no puede participar en las operaciones del DAG.

2.  Si el servidor es accesible, el PAM contacta al administrador activo en el servidor afectado y solicita que se desmonten todas las bases de datos inmediatamente.

3.  Para cada copia de base de datos afectada:
    
    1.  El PAM solicita el estado de la copia de la base de datos de todos los servidores en el DAG.
    
    2.  El PAM recibe una respuesta de todos los miembros del DAG accesibles y activos.
    
    3.  El PAM intenta determinar el mejor origen del registro entre todos los servidores que responden al consultar el número de generación de registro más reciente de cada uno de los respondedores.
    
    4.  Cada uno de los servidores responde con el número de generación de registro.

4.  El PAM recupera el estado actual del catálogo del índice de búsqueda de la base de datos del clúster.

5.  Según el número de generación de registro y el estado del catálogo de la copia de cada base de datos, el PAM selecciona las mejores copias para activar.

6.  El PAM actualiza la ubicación montada de la base de datos en la base de datos del clúster.

7.  El PAM inicia la conmutación por error de base de datos comunicándose con el administrador activo en uno o más servidores.

8.  El administrador activo en los servidores seleccionados solicita que el servicio de replicación de Microsoft Exchange intente copiar los últimos registros del servidor anterior y establezca la marca de montaje.

9.  Cuando la base de datos se puede montar, el administrador activo en los servidores monta la base de datos.

Para obtener más información acerca del mejor proceso de selección de copia del administrador activo, vea [Active Manager](active-manager-exchange-2013-help.md).

## Conmutaciones por error del centro de datos

Se han realizado cambios significativos en Exchange 2013 que abordan los retos de llevar a cabo una configuración con resistencia de sitios en Exchange 2010. Mediante la simplificación del espacio de nombres, la consolidación de los roles de servidor, la separación del servidor de acceso de cliente y la recuperación DAG (en Exchange 2013, no es necesario mover el espacio de nombres con el DAG), así como los cambios en el equilibrio de carga, Exchange 2013 proporciona nuevas opciones de resistencia como, por ejemplo, poder usar un único espacio de nombres global. Además, si tiene más de dos ubicaciones en las que implementar los componentes del servicio de mensajería, Exchange 2013 también proporciona la capacidad de configurar el servicio de mensajería para una conmutación por error automática como respuesta a fallos que en Exchange 2010 requerían una intervención manual.

En Exchange 2013 se ha simplificado el funcionamiento de la resistencia de sitios. Exchange aprovecha la tolerancia a errores incorporada en el espacio de nombres mediante múltiples direcciones IP, el equilibrio de cargas (y, en caso necesario, la capacidad de activar y desactivar los servidores). Otro de los cambios más importantes de Exchange 2013 es aprovechar la capacidad de los clientes de copiar en caché múltiples direcciones IP devueltas desde el servidor DNS en respuesta a una solicitud de resolución de nombre. Si suponemos que el cliente tiene la capacidad de copiar en caché múltiples direcciones IP (lo que hacen la mayoría de clientes HTTP y dado que la mayoría de los protocolos de acceso de cliente de Exchange 2013 se basan en HTTP (Outlook, Outlook en cualquier lugar, EAS, EWS, OWA, EAC, RPS, etc.), todos los clientes HTTP compatibles tienen la capacidad de usar múltiples direcciones IP), lo que proporciona la conmutación por error del lado cliente. Puede configurar DNS para entregar varias direcciones IP a un cliente durante la resolución de nombres. El cliente solicita mail.contoso.com y obtiene, por ejemplo, dos o cuatro direcciones IP. Sin embargo, el cliente usará muchas de las direcciones IP que obtiene de forma confiable. Esto mejora mucho la situación del cliente porque si se produce un error en una de las direcciones IP, tiene muchas más a las que intentar conectarse. Si el cliente prueba una y genera un error, espera unos 20 segundos y, a continuación, prueba la siguiente de la lista. Así, si pierde conectividad en la matriz CAS principal pero dispone de una segunda dirección IP pública para una segunda matriz CAS, la recuperación de los clientes es automática y se produce en unos 21 segundos.

Los clientes HTTP modernos (sistemas operativos y exploradores web de 10 años o menos) simplemente utilizan esta redundancia de manera automática. La pila HTTP puede aceptar múltiples direcciones IP para un FQDN, y si se produce un error grave en la primera IP que intenta (por ejemplo, no se puede conectar), intentará en la siguiente IP de la lista. En los errores temporales (la conexión se pierde después de que se establece la sesión, quizás debido a un error intermitente en el servicio en el que, por ejemplo, un dispositivo deja paquetes y debe colocarse fuera de servicio), es posible que el usuario deba actualizar el explorador.

Con la configuración correcta, la conmutación por error se produce en el nivel del cliente y los clientes se redireccionan automáticamente a un segundo centro de datos que tiene servidores de acceso de cliente operativos. Dichos servidores envían la comunicación mediante proxy de vuelta al servidor de buzones de correo del usuario, al que no le afectará la interrupción (porque no se realiza ningún cambio). En lugar de centrarse en recuperar el servicio, éste se recupera de forma automática y usted podrá dedicarse a solucionar el problema principal (p. ej., reemplazar el equilibrador de carga erróneo).

Dado que puede realizar la conmutación por error del espacio de nombre entre centros de datos, lo único que se necesita para lograr una conmutación por error del centro de datos es un mecanismo para la conmutación por error del rol del servidor de buzones de correo en centros de datos. Para obtener una conmutación por error automática para el DAG, simplemente cree una solución donde el DAG se divida en partes iguales entre dos centros de datos y, luego, coloque el servidor testigo en una tercera ubicación para que los miembros de DAG puedan arbitrarla en cualquier centro de datos, independientemente del estado de la red entre los centros de datos que contienen los miembros de DAG. La clave es que la tercera ubicación está al margen de los fallos que afectan a las ubicaciones que contienen a los miembros de DAG.

Si solo tiene dos centros de datos y querría configurar la conmutación por error automática, puede utilizar Microsoft Azure como tercera ubicación. Tendrá que crear una red virtual de Azure y conectarla a los dos centros de datos mediante una VPN multipunto. Después podrá colocar el servidor testigo en una máquina virtual de Microsoft Azure. Para obtener más información, vea [Usar una máquina virtual de Microsoft Azure como un servidor testigo del DAG](using-a-microsoft-azure-vm-as-a-dag-witness-server-exchange-2013-help.md).

