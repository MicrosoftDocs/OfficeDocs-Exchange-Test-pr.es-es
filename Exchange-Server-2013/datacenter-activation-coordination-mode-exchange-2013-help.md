---
title: 'Modo de coordinación de activación de centro de datos: Exchange 2013 Help'
TOCTitle: Modo de coordinación de activación de centro de datos
ms:assetid: 57e4bf22-eeae-42a5-beb3-d68d06489592
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd979790(v=EXCHG.150)
ms:contentKeyID: 48268146
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modo de coordinación de activación de centro de datos

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2014-07-14_

El modo de coordinación de activación de centro de datos (DAC) es una propiedad del grupo de disponibilidad de base de datos (DAG). El modo DAC está deshabilitado de forma predeterminada pero se debe habilitar para todos los DAG con dos o más miembros y que usan replicación continua. El modo DAC no se debe habilitar para los DAG que usan el modo de replicación de terceros, excepto que el proveedor externo lo especifique.

El modo DAC se usa para controlar el montaje de la base de datos en el comportamiento de inicio de un DAG. Este control está diseñado para impedir que se produzca un cerebro dividido en el nivel de la base de datos durante una recuperación del centro de datos. El cerebro dividido, también conocido como síndrome de cerebro dividido, es una condición que se produce en una copia de base de datos que se monta como copia activa en dos miembros del mismo DAG que no se pueden comunicar. El cerebro dividido se puede evitar mediante el modo DAC porque el modo DAC necesita miembros del DAG para obtener permiso para montar bases de datos antes de que puedan montarse.

Por ejemplo, consideremos un escenario donde el centro de datos primario contiene dos miembros de DAG y el servidor testigo, y un centro de datos secundario contiene otros dos miembros de DAG. En este escenario, el DAG no está en modo DAC. El centro de datos primario pierde alimentación, por lo que activa el DAG en el centro de datos secundario. Finalmente se restaura la alimentación del centro de datos primario y los miembros del DAG en el centro de datos primario, que tenían quórum antes del error de alimentación, iniciarán y montarán sus bases de datos. Como el centro de datos primario se restauró sin conectividad de red en el centro de datos secundario, y como el DAG no estaba en modo DAC, las bases de datos activas dentro del DAG entraron en un estado de cerebro dividido.

## Funcionamiento del modo DAC

El modo DAC está diseñado para evitar que ocurra el síndrome de cerebro dividido, mediante la introducción de un protocolo denominado Protocolo de coordinación de activación de centro de datos (DACP). Cuando el modo DAC está habilitado, los miembros del DAG no montarán las bases de datos automáticamente aun cuando tengan quórum. En lugar de ello, el DACP determinará el estado actual del DAG, para saber si corresponde que Active Manager intente montar las bases de datos.

Es posible considerar al modo DAC como un quórum en el nivel de aplicación, para el montaje de bases de datos. Para comprender el propósito del DACP y su funcionamiento, es importante conocer el escenario principal que puede para afrontar. Consideremos el escenario de dos centros de datos. Supongamos que existe un corte total de energía en el centro de datos principal. En este evento, todos los servidores y la WAN están inactivos, por lo que la organización toma la decisión de activar el centro de datos en espera. En casi todos los escenarios de recuperación de este tipo, cuando se restaura la energía al centro de datos principal, la conectividad WAN por lo general no se restaura de inmediato. Esto significa que los miembros del DAG del centro de datos principal se activarán, pero no podrán comunicarse con los miembros del DAG del centro de datos en espera activado. El centro de datos principal siempre debe contener la mayoría de los votantes de quórum de DAG. Esto significa que cuando se restaure la energía, aunque no haya conectividad de WAN con los miembros del centro de datos en espera, los miembros del DAG del centro de datos principal serán la mayoría y por lo tanto tendrán quórum. Esto es problemático porque, teniendo quórum, estos servidores pueden tener la capacidad de montar sus propias bases de datos, lo que causa una divergencia de las bases de datos realmente activas que ahora se encuentran montadas en el centro de datos en espera activado.

DACP se creó para solucionar este problema. Active Manager almacena un bit en memoria (ya sea un 0 ó 1) que le indica al DAG si tiene permitido montar bases de datos locales que asignadas como activas en el servidor. Cuando un DAG se está ejecutando en modo DAC, cada vez que se inicia Active Manager el bit se establece en 0, lo cual significa que no está permitido montar bases de datos. Dado que está en modo DAC, el servidor debe tratar de comunicarse con los otros miembros del DAG que conoce, para que alguno de ellos le responda si puede montar bases de datos locales que estén asignadas como activas. La respuesta será en forma de opción de bit para los otros Active Managers del DAG. Si otro servidor responde que su bit está establecido en 1, significa que los servidores tienen permitido montar bases de datos, por lo que el inicio del servidor establecerá su bit 1 y montará bases de datos.

Pero al recuperarse de un corte de energía en el centro de datos principal, donde los servidores se recuperaron pero aún no se restauró la conectividad WAN, todos los miembros del DAG de dicho centro de datos tendrán un valor de bit DACP igual a 0. Por lo tanto, ninguno de los servidores que se inicien en el centro de datos principal montará bases de datos, porque ninguno podrá comunicarse con un miembro del DAG que tenga un valor de bit DACP igual a 1.

## Modo DAC para DAG que tienen dos miembros

Los DAG que tienen dos miembros tienen limitaciones inherentes que evitan que el bit DACP solo se proteja completamente contra el síndrome de cerebro dividido al nivel de la aplicación. En el caso de los DAG que tienen solo dos miembros, el modo DAC también usa el tiempo de arranque del servidor testigo del DAG para determinar si puede montar bases de datos al inicio. El tiempo de arranque del servidor testigo se compara con el tiempo en que el bit DACP se estableció en 1.

  - Si el tiempo en que el bit DACP se estableció es anterior al tiempo de arranque del servidor testigo, el sistema asume que el miembro del DAG y el servidor testigo se reiniciaron al mismo tiempo (quizás debido a una pérdida de alimentación eléctrica en el centro de datos primario), y no se le permite al miembro del DAG montar bases de datos.

  - Si el tiempo en que el bit DACP se estableció es más reciente que el tiempo de arranque del servidor testigo, el sistema asume que el miembro del DAG se reinició por algún otro motivo (quizás debido a una pausa programada en la que se realizaron tareas de mantenimiento o quizás debido a un bloqueo del sistema o una pérdida de alimentación eléctrica aislada que le ocurrió al miembro del DAG), y se le permite al miembro DAG montar bases de datos.


> [!IMPORTANT]
> Dado que el tiempo de arranque del servidor testigo se usa para determinar si el miembro del DAG puede montar sus bases de datos activas al inicio, usted nunca debe reiniciar el servidor testigo y el único miembro del DAG al mismo tiempo. Si lo hace, podría dejar al miembro del DAG en un estado en el que no puede montar bases de datos al inicio. Si esto sucede, debe ejecutar el cmdlet de <A href="https://technet.microsoft.com/es-es/library/dd351169(v=exchg.150)">Restore-DatabaseAvailabilityGroup</A> en el DAG. Esto restablece el bit DACP y permite que el miembro del DAG monte las bases de datos.



## Otras ventajas del modo DAC

Además de prevenir el síndrome de cerebro dividido al nivel de la aplicación, el modo DAC también permite el uso de los cmdlets de resistencia de sitio integrados usados para llevar a cabo cambios del centro de datos. Por ejemplo, los siguientes:

  - [Stop-DatabaseAvailabilityGroup](https://technet.microsoft.com/es-es/library/dd335133\(v=exchg.150\))

  - [Restore-DatabaseAvailabilityGroup](https://technet.microsoft.com/es-es/library/dd351169\(v=exchg.150\))

  - [Start-DatabaseAvailabilityGroup](https://technet.microsoft.com/es-es/library/dd335076\(v=exchg.150\))

Realizar un cambio del centro de datos para DAG que no están en el modo DAC implica usar una combinación de herramientas de Exchange y herramientas de administración de clústeres. Para más información, vea [Cambios en el centro de datos](datacenter-switchovers-exchange-2013-help.md).

## Habilitar el modo DAC

El modo DAC solo se puede habilitar mediante el Shell de administración de Exchange. En especial, puede usar el cmdlet [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/es-es/library/dd297934\(v=exchg.150\)) para habilitar el modo DAC, tal como lo ilustra el ejemplo siguiente.

    Set-DatabaseAvailabilityGroup -Identity DAG2 -DatacenterActivationMode DagOnly

En el ejemplo anterior, DAG2 se habilita en el modo DAC.

Para obtener más información acerca de la habilitación del modo DAC, consulte [Configurar las propiedades del grupo de disponibilidad de base de datos](configure-database-availability-group-properties-exchange-2013-help.md) y [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/es-es/library/dd297934\(v=exchg.150\)).

