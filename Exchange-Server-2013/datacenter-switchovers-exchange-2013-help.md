---
title: 'Cambios en el centro de datos: Exchange 2013 Help'
TOCTitle: Cambios en el centro de datos
ms:assetid: ac208c12-04d0-4809-bacd-72478ff14983
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd351049(v=EXCHG.150)
ms:contentKeyID: 62523849
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Cambios en el centro de datos

 

_**Se aplica a:** Exchange Server 2013 SP1_

_**Última modificación del tema:** 2016-03-17_

En una configuración con resistencia de sitios se puede producir una recuperación automática en respuesta a un fallo en el nivel de sitio dentro de un DAG, lo que permitiría al sistema de mensajería permanecer operativo. Esta configuración requiere al menos tres ubicaciones ya que necesita la implementación de los miembros de DAG en dos ubicaciones y el servidor de testigo de DAG en una tercera.

Si no dispone de tres ubicaciones, o incluso si las tiene pero desea controlar las acciones de recuperación en el nivel del centro de datos, puede configurar el DAG para su recuperación manual en caso de que se produzca un fallo en el nivel de sitio. En ese caso, realizará un proceso denominado un *cambio de centro de datos*. Como sucede con muchas situaciones de recuperación ante desastres, la planificación y la preparación anticipadas de un cambio de centro de datos pueden simplificar el proceso de recuperación y reducir la duración de la interrupción.

Existen cuatro pasos básicos que es necesario completar para realizar un cambio de centro de datos, tras tomar la decisión inicial de activar el segundo centro de datos:

1.  **Finalizar un centro de datos en ejecución parcial**   Este paso implica la finalización de los servicios Exchange en el centro de datos principal, si aún hay servicios en ejecución. Esto revierte una importancia especial para el rol de servidor Buzón de correo, ya que usa un modelo de alta disponibilidad activo/pasivo. Si no se detienen los servicios de un centro de datos parcialmente dañado, es posible que los problemas de dicho centro de datos afecten de manera negativa los servicios durante un cambio al centro de datos principal.
    

    > [!IMPORTANT]
    > Si la confiabilidad de la infraestructura de Active Directory o la red está en riesgo a causa de un error en el centro de datos principal, recomendamos que todos los servicios de mensajería permanezcan desactivados hasta que estas dependencias se restauren a un estado de servicio normal.



2.  **Validar y confirmar los requisitos previos para el segundo centro de datos**   Este paso se puede realizar al mismo tiempo que el paso 1, ya que la validación del mantenimiento de las dependencias de la infraestructura del segundo centro de datos es, en gran medida, independiente de los servicios del centro de datos principal. Por lo general, cada organización requiere su propio método para llevar a cabo este paso. Por ejemplo, puede decidir que desea completar este paso analizando la información de mantenimiento recopilada y filtrada por una aplicación de supervisión de infraestructuras, o bien utilizando una herramienta específica para la infraestructura de su organización. Este paso es fundamental porque la activación del segundo centro de datos cuando su infraestructura es incorrecta e inestable suele generar resultados deficientes.

3.  **Activar los servidores de buzones de correo**   Este paso inicia el proceso de activación del segundo centro de datos. Este paso se puede efectuar al mismo tiempo que el paso 4 porque los servicios de Microsoft Exchange pueden controlar las interrupciones de las bases de datos y llevar a cabo la recuperación. La activación de los servidores de buzones de correo conlleva un proceso que consiste en marcar los servidores dañados del centro de datos principal como no disponibles, seguido por la activación de los servidores en el segundo centro de datos. El proceso de activación de los servidores de buzones de correo depende de si el DAG está en modo DAC (coordinación de activación de base de datos). Para obtener más información acerca del modo de coordinación de activación de bases de datos, consulte [Modo de coordinación de activación de centro de datos](datacenter-activation-coordination-mode-exchange-2013-help.md).
    
    Si el DAG está en modo DAC, se pueden utilizar los cmdlets de resistencia de sitio de Exchange para finalizar un centro de datos dañado parcialmente (si fuera necesario), y activar los servidores de buzones de correo. Por ejemplo, en el modo DAC, este paso se realiza a través del cmdlet [Stop-DatabaseAvailabilityGroup](https://technet.microsoft.com/es-es/library/dd335133\(v=exchg.150\)). En algunos casos, es necesario marcar los servidores como no disponibles dos veces (una vez en cada centro de datos). A continuación, se ejecuta el cmdlet [Restore-DatabaseAvailabilityGroup](https://technet.microsoft.com/es-es/library/dd351169\(v=exchg.150\)) para restaurar los miembros restantes del grupo de disponibilidad de base de datos (DAG) en el segundo centro de datos. Para ello, se reducen los miembros del DAG a aquellos que aún están en funcionamiento y, de esta manera, se restablece el quórum. Si el DAG no está en modo DAC, es necesario utilizar las herramientas del clúster de conmutación por error de Windows para activar los servidores de buzones de correo. Después de completar uno de los procesos, las copias de la base de datos que anteriormente fueron pasivas en el segundo centro de datos pueden pasar a ser activas y estar montadas. En este momento, la recuperación de servidores de buzones de correo se ha completado.

4.  **Activar los servidores de acceso de cliente**   Esto implica usar la información de asignación de direcciones URL y la metodología de cambios del Sistema de nombres de dominio (DNS) para efectuar todas las actualizaciones de DNS requeridas. La información de asignación describe qué cambios de DNS se deben realizar. El tiempo que se requiere para completar la actualización depende de la metodología usada y la configuración del período de vida (TTL) en el registro DNS (y de si la infraestructura de la implementación cumple el TTL).

Los usuarios deberían comenzar a tener acceso a los servicios de mensajería después de completar los pasos 3 y 4. Los pasos 3 y 4 se describen en detalle más adelante en este tema.

**Contenido**

Finalización de un centro de datos parcialmente dañado

Activación de los servidores de buzones de correo

Activación de los servidores de acceso de cliente

Restauración del servicio en el centro de datos principal

Restablecimiento de la resistencia de sitios

## Finalización de un centro de datos parcialmente dañado

Si aún hay miembros DAG en ejecución en el centro de datos dañado, se deben finalizar.

Cuando el DAG esté en modo DAC, las acciones específicas para finalizar cualquier miembro DAG todavía activo en el centro de datos principal son las siguientes:

1.  Los miembros del DAG del centro de datos principal deben marcarse como detenidos en el centro de datos principal. *Detenido* es un estado de Active Manager que impide el montaje de las bases de datos. Active Manager pasa a este estado en cada servidor del centro de datos dañado mediante el cmdlet [Stop-DatabaseAvailabilityGroup](https://technet.microsoft.com/es-es/library/dd335133\(v=exchg.150\)). El parámetro *ActiveDirectorySite* de este cmdlet se puede usar para marcar como detenidos todos los servidores del centro de datos principal con un solo comando. Según el error, es posible que este paso no se pueda realizar. Este paso se debe llevar a cabo si el estado del centro de datos lo permite. El cmdlet **Stop-DatabaseAvailabilityGroup** se debe ejecutar en todos los servidores del centro de datos principal. Si el servidor de buzones de correo no está disponible, pero Active Directory funciona en el centro de datos principal, se debe ejecutar el comando **Stop-DatabaseAvailabilityGroup** con el parámetro *ConfigurationOnly* en todos los servidores con este estado del centro de datos principal, o bien se debe apagar el servidor de buzones de correo. Si no se pueden apagar los servidores de buzones de correo en el centro de datos dañado o no se puede ejecutar correctamente el comando **Stop-DatabaseAvailabilityGroup** en los servidores, es posible que se genere el síndrome de cerebro dividido entre los dos centros de datos. Para cumplir este requisito, es posible que deba apagar cada equipo por medio de dispositivos de administración de energía.

2.  Ahora se debe actualizar el segundo centro de datos para reflejar los servidores detenidos del centro de datos principal. Para realizar esta tarea, se debe ejecutar el comando **Stop-DatabaseAvailabilityGroup** con el parámetro *ConfigurationOnly*. Para ello, se debe usar el mismo parámetro *ActiveDirectorySite* y especificar el nombre del sitio de Active Directory en el centro de datos principal dañado. La finalidad de este paso es informar a los servidores del segundo centro de datos sobre los servidores de buzones de correo que se pueden usar al restaurar el servicio.

Cuando el DAG no esté en modo DAC, las acciones específicas para finalizar cualquier miembro DAG todavía activo en el centro de datos principal son las siguientes:

1.  Los miembros DAG del centro de datos principal tienen que desalojarse obligatoriamente del clúster subyacente del DAG mediante la ejecución de los siguientes comandos en cada uno de los miembros:
    
    ```powershell
net stop clussvc
```
        cluster <DAGName> node <DAGMemberName> /forcecleanup

2.  Ahora es necesario reiniciar los miembros DAG del segundo centro de datos y, posteriormente, utilizarlos para completar el proceso de desalojo del segundo centro de datos. Detenga el servicio de clúster de cada miembro DAG en el segundo centro de datos; para ello, ejecute el siguiente comando en cada miembro:
    
    ```powershell
net stop clussvc
```

3.  En un miembro DAG del segundo centro de datos, fuerce un inicio de quórum del servicio de clúster mediante la ejecución del siguiente comando:
    
    ```powershell
net start clussvc /forcequorum
```

4.  Abra la herramienta Administración del clúster de conmutación por error y conéctela al clúster subyacente del DAG. Expanda el clúster y a continuación expanda **Nodos**. Haga clic con el botón secundario en cada nodo del centro de datos primario, seleccione **Más acciones** y, a continuación, **Expulsar**. Cuando haya terminado de expulsar a los miembros de DAG del centro de datos principal, cierre la herramienta de administración de clústeres de conmutación por error.

Volver al principio

## Activación de los servidores de buzones de correo

Los pasos necesarios para activar los servidores de buzones de correo durante un cambio de centro de datos también dependen de si el DAG está o no en modo DAC. Antes de activar los miembros DAG en el segundo centro de datos, recomendamos validar que los servicios de infraestructura del segundo centro de datos están listos para la activación del servicio de mensajería.

Cuando el DAG está en modo DAC, los pasos para completar la activación de los servidores de buzones de correo en el segundo centro de datos son los siguientes:

1.  Se debe detener el Servicio de clúster en cada miembro del DAG del segundo centro de datos. Puede usar el cmdlet **Stop-Service** para detener el servicio (por ejemplo, `Stop-Service ClusSvc`) o puede usar `net stop clussvc` desde un símbolo del sistema con privilegios elevados.

2.  Los servidores de buzones de correo del centro de datos en espera se activan luego mediante el cmdlet [Restore-DatabaseAvailabilityGroup](https://technet.microsoft.com/es-es/library/dd351169\(v=exchg.150\)). El sitio de Active Directory del centro de datos en espera se transfiere al cmdlet **Restore-DatabaseAvailabilityGroup** para identificar los servidores que se deben usar para restaurar el servicio y para configurar el DAG que se usará como servidor testigo alternativo. Si el servidor testigo alternativo no se ha configurado anteriormente, puede configurarlo con los parámetros *AlternateWitnessServer* y *AlternateWitnessDirectory* del cmdlet [Restore-DatabaseAvailabilityGroup](https://technet.microsoft.com/es-es/library/dd351169\(v=exchg.150\)). Si este comando se ejecuta correctamente, los criterios de quórum se reducen a los servidores del centro de datos en espera. Si el número de servidores de ese centro de datos es par, el DAG pasará a usar el servidor testigo alternativo, según se identificó en la configuración del objeto DAG.

3.  Ahora se pueden activar las bases de datos. De acuerdo con la configuración específica usada por la organización, es posible que este proceso no sea automático. Si los servidores del centro de datos en espera tienen configurado un bloqueo de activación, el sistema no efectuará una conmutación por error automática del centro de datos principal al centro de datos en espera de ninguna base de datos. Si no existen restricciones respecto de la conmutación por error para ninguna de las copias de bases de datos en el centro de datos en espera, el sistema activará las copias en el segundo centro de datos, ya que dará por sentado que son correctas. Si hay bases de datos configuradas con un bloqueo de activación que requiere una acción manual explícita, existen dos posibilidades:
    
    1.  Desactivar la configuración que bloquea la activación. De esta manera, el sistema retomará su comportamiento predeterminado, es decir, activará cualquier copia disponible.
    
    2.  No modificar la configuración y usar el cmdlet [Move-ActiveMailboxDatabase](https://technet.microsoft.com/es-es/library/dd298068\(v=exchg.150\)) para completar la activación de bases de datos en el segundo centro de datos. Para completar este paso mediante el cmdlet **Move-ActiveMailboxDatabase** cuando esté configurado el bloqueo de activación, debe identificar de manera explícita el destino del traslado.

4.  El último paso consiste en revisar todos los mensajes de error y de advertencia de las tareas. Se debe realizar un seguimiento y una corrección de todas las advertencias indicadas. El modelo de diseño de las tareas establece que los comandos sólo fallan si no pueden cumplir el objetivo esencial de su diseño. Por ejemplo, el cmdlet **Restore-DatabaseAvailabilityGroup** generará un error si no puede reducir el quórum del DAG para permitir que un servidor del segundo centro de datos se reinicie sin provocar una interrupción del quórum. No obstante, los resultados de cada tarea también se emplean para identificar los problemas que requieren un seguimiento por parte del administrador. Recomendamos guardar todos los resultados de las tareas y revisarlos para realizar las acciones de seguimiento.

Cuando el DAG no está en modo DAC, los pasos para completar la activación de los servidores de buzones de correo en el segundo centro de datos son los siguientes:

1.  Es necesario modificar el quórum, basándose en el número de miembros DAG del segundo centro de datos.
    
    1.  Si hay un número impar de miembros DAG, cambie el modelo de quórum de DAG, de quórum Mayoría de recurso compartido de archivos y nodos, a quórum Mayoría de nodo, mediante la ejecución del siguiente comando:
        
        ```powershell
cluster <DAGName> /quorum /nodemajority
```
    
    2.  Si hay un número par de miembros DAG, vuelva a configurar el servidor testigo y el directorio; para ello, ejecute el siguiente comando en el Shell de administración de Exchange:
        
        ```powershell
Set-DatabaseAvailabilityGroup <DAGName> -WitnessServer <ServerName>
```

2.  Inicie el Servicio de clúster en cualquier miembro DAG restante del segundo centro de datos, mediante el siguiente comando:
    
    ```powershell
net start clussvc
```

3.  Realice los cambios de servidor, con el fin de activar las bases de datos de buzones de correo del DAG, mediante el siguiente comando para cada miembro DAG:
    
        Move-ActiveMailboxDatabase -Server <DAGMemberinPrimarySite> -ActivateOnServer <DAGMemberinSecondSite>

4.  Monte las bases de datos de buzones de correo de cada miembro DAG en el segundo sitio; para ello, ejecute el siguiente comando:
    
    ```powershell
Get-MailboxDatabase <DAGMemberinSecondSite> | Mount-Database
```

Volver al principio

## Activación de los servidores de acceso de cliente

Los clientes se conectan a extremos de servicio (por ejemplo, Outlook Web App, Detección automática, Exchange ActiveSync, Outlook Anywhere, POP3, IMAP4 y la matriz de acceso de clientes RPC) para tener acceso a servicios y datos de Exchange. Por lo tanto, para activar los servidores de acceso de clientes hay que cambiar la asignación de registros DNS de los extremos de servicio desde las direcciones IP del centro de datos primario a las direcciones IP del centro de datos secundario configuradas como nuevos extremos de servicio. En función de la configuración DNS, los registros DNS que hay que modificar pueden o no estar en la misma zona DNS.

## Activación de los servidores de acceso de cliente

Luego, los clientes se podrán conectar automáticamente a los nuevos extremos de servicio de dos maneras:

  - Los clientes seguirán intentando establecer la conexión y deberían conectarse automáticamente una vez que hayan expirado el TTL para la entrada DNS original y la entrada de la memoria caché DNS del cliente. Los usuarios también pueden ejecutar el comando `ipconfig /flushdns` desde un símbolo del sistema para borrar manualmente la memoria caché DNS.

  - Los clientes que se inicien o reinicien realizarán una búsqueda DNS en el inicio y obtendrán la nueva dirección IP para el extremo de servicio, que será una matriz o un servidor de acceso de cliente en el segundo centro de datos.

Suponiendo que se han completado todos los cambios adecuados en la configuración para definir y configurar los servicios en el segundo centro de datos a fin de que funcionen como en el centro de datos principal, y suponiendo que la configuración DNS establecida es correcta, no será necesario efectuar cambios adicionales para activar los servidores de acceso de cliente.

## Activación de los servicios de transporte

Los clientes y otros servidores que envían mensajes al servidor suelen identificar esos servidores mediante DNS. Activar los servicios de transporte en el segundo centro de datos implica modificar los registros DNS para que apunten a las direcciones IP de los servidores de buzones del segundo centro de datos. Luego, los clientes y los servidores de envío se conectarán automáticamente a los servidores del segundo centro de datos de dos maneras:

  - Los clientes seguirán intentando establecer la conexión y deberían conectarse automáticamente una vez que hayan expirado el TTL para la entrada DNS original y la entrada de la memoria caché DNS del cliente. Los usuarios también pueden ejecutar el comando `ipconfig /flushdns` desde un símbolo del sistema para borrar manualmente la memoria caché DNS.

  - Los clientes que se inicien o reinicien realizarán una búsqueda DNS en el inicio y obtendrán la nueva dirección IP para el extremo SMTP, que será un servidor de buzones en el segundo centro de datos.

Suponiendo que se han completado todos los cambios adecuados en la configuración para definir y configurar los servicios en el segundo centro de datos a fin de que funcionen como en el centro de datos principal, y suponiendo que la configuración DNS establecida es correcta, no será necesario efectuar cambios adicionales para activar los servicios de transporte.

## Activación de los servicios de mensajería unificada

Los servicios de mensajería unificada (MU) se conectan con el sistema PBX y las líneas telefónicas de una organización. La conexión lógica entre el sistema PBX y el servicio de mensajería unificada se proporciona mediante una puerta de enlace IP. Las puertas de enlace IP incluyen funcionalidades de alta disponibilidad y pueden alternar entre varios servicios de mensajería unificada cuando se detecta un error.

Si existen servicios de mensajería unificada en el segundo centro de datos que estaban deshabilitados porque se dedican a la solución de resistencia de sitios, es posible habilitarlos mediante el cmdlet [Enable-UMService](https://technet.microsoft.com/es-es/library/jj552411\(v=exchg.150\)) (por ejemplo, `Enable-UMService EX4`).

Suponiendo que las puertas de enlace IP se asocian a los servicios de mensajería unificada por medio de servidores DNS, activar los servicios de mensajería unificada implica modificar los registros DNS para que apunten a las nuevas direcciones IP que se configurarán para el servicio de mensajería unificada en el segundo centro de datos. Suponiendo que se hayan efectuado todos los cambios adecuados en la configuración para definir y configurar los servicios en el segundo centro de datos a fin de que funcionen como en el centro de datos principal, y suponiendo que la configuración DNS establecida sea correcta, no será necesario efectuar cambios adicionales para activar los servicios de mensajería unificada.

Si la puerta de enlace IP en uso no admite la utilización de nombres DNS para resolver los servicios de mensajería unificada, será necesario efectuar pasos de configuración adicionales para que la puerta de enlace IP apunte a las direcciones IP de los servicios de mensajería unificada en el segundo centro de datos.

## Activación de los servidores Transporte perimetral

Los pasos para activar el rol de servidor Transporte perimetral pueden variar en función de cada configuración. Los servidores Transporte perimetral de dos centros de datos se pueden definir con una configuración activo/pasivo o activo/activo. En una configuración activo/pasivo, el servidor Transporte perimetral del segundo centro de datos estará inactivo hasta que se active el segundo centro de datos. En una configuración activo/activo, los servidores Transporte perimetral de ambos centros de datos podrán entregar correos en todo momento.

En una configuración activo/activo, no es necesario realizar pasos para activar los servidores Transporte perimetral del segundo centro de datos porque ya están en ejecución. En una configuración activo/pasivo, se debe actualizar el registro de recursos MX de DNS para cada dominio SMTP como parte del cambio del centro de datos primario al centro de datos en espera. Si bien la configuración activo/activo ofrece una solución sencilla para el cambio de un centro de datos, también presenta una desventaja, ya que se debe supervisar cuidadosamente la carga para garantizar que, tras el cambio del centro de datos, los servidores Transporte perimetral del segundo centro de datos pueden proporcionar la capacidad suficiente para respaldar el aumento de la carga que ahora fluye a través de él. Este aumento se debe a que los servidores Transporte perimetral del centro de datos principal no están disponibles.

Incluso en una configuración activo/activo, puede resultar útil actualizar los registros de recursos MX para los servidores Transporte perimetral durante el cambio de un centro de datos. Si se permite que el registro de recursos MX del centro de datos dañado siga apuntando al centro de datos dañado, cuando éste comience a recuperarse, podría intentar establecer una conexión con sus servidores Transporte perimetral. Esto podría ocurrir mientras los servicios de transporte perimetral están inestables (por ejemplo, porque se están restaurando los servicios dependientes del centro de datos).

Si se asume que los registros DNS están bajo el control de la organización, activar los servidores Transporte perimetral implicará actualizar el registro de recursos MX para cada dominio SMTP hospedado por el servidor.


> [!NOTE]
> Si el registro de recursos MX usado por la organización no está hospedado por un servidor DNS bajo el control de la organización, se recomienda hacer referencia a un registro CNAME en el registro de recursos MX y usar un registro CNAME bajo el control de la organización que luego se pueda actualizar.



Las actualizaciones de DNS habilitan el tráfico entrante, mientras que el tráfico saliente se controla mediante la activación de las bases de datos de buzones de correo en un sitio con servidores Transporte perimetral en funcionamiento:

  - Cuando se inician conexiones SMTP entrantes mediante la información actualizada de resolución de nombres, los clientes SMTP se conectarán con los servidores Transporte perimetral del segundo centro de datos. El servidor Transporte perimetral enrutará el tráfico de manera adecuada, y no se requerirán cambios adicionales.

  - Cuando se inician conexiones SMTP salientes, se intentará usar el servidor Transporte perimetral disponible de manera local, y esos mensajes se pondrán en la cola o se enviarán de inmediato, según el estado del servidor de recepción.

Volver al principio

## Restauración del servicio en el centro de datos principal

Generalmente, los errores en los centros de datos son temporales o permanentes. En el caso de un error permanente, como un evento que provocó la destrucción permanente de un centro de datos principal, no hay expectativas de que el centro de datos principal se active. Sin embargo, en el caso de un error temporal (por ejemplo, una pérdida de energía prolongada o un daño importante pero reparable), existen expectativas de que el centro de datos principal se restaure eventualmente a un estado de servicio completo.

El proceso que consiste en restaurar el servicio en un centro de datos dañado se denomina *recuperación*. Los pasos ejecutados para realizar una recuperación de un centro de datos son similares a los que se usan para realizar el cambio de un centro de datos. Una diferencia importante es que la recuperación de un centro de datos se programa y la duración de la interrupción suele ser mucho más breve.

Es importante que la recuperación no se efectúe hasta que las dependencias de la infraestructura de Exchange se hayan reactivado y validado, y estén estables y en funcionamiento. Si estas dependencias no están disponibles o no son correctas, es probable que el proceso de recuperación provoque una interrupción más prolongada de lo necesario o que el proceso falle por completo.

## Recuperación del rol del servidor de buzones de correo

El rol de servidor de buzones de correo debe ser el primer rol en el que se efectúe la recuperación al centro de datos principal. Los siguientes pasos detallan el proceso de recuperación del rol de servidor de buzones de correo:

1.  Como parte del proceso de cambio de un centro de datos, se detuvieron los servidores de buzones de correo del centro de datos principal. Cuando el entorno (como el centro de datos principal, las dependencias de Exchange y la conectividad de la red de área extensa o WAN) está preparado, el primer paso consiste en iniciar los servidores de buzones de correo del centro de datos restaurado e incorporarlos en el DAG. La forma en que esto se hace depende de si el DAG está o no en modo DAC.
    
    1.  Si el DAG está en modo DAC, puede volver a incorporar los miembros DAG en el sitio principal mediante el cmdlet [Start-DatabaseAvailabilityGroup](https://technet.microsoft.com/es-es/library/dd335076\(v=exchg.150\)). Para asegurarse de que el DAG está usando el modelo de quórum correcto, ejecute el cmdlet [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/es-es/library/dd297934\(v=exchg.150\)) en el DAG sin especificar ningún parámetro.
    
    2.  Si el DAG no está en modo DAC, puede volver a incorporar los miembros DAG mediante el cmdlet [Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/es-es/library/dd298049\(v=exchg.150\)).

2.  Una vez que se incorporaron los servidores de buzones de correo del centro de datos principal en el DAG, necesitarán tiempo para sincronizar las copias de bases de datos. Según la naturaleza del error, la duración de la interrupción y las acciones realizadas por un administrador durante la interrupción, es posible que se deban repropagar las copias de bases de datos. Por ejemplo, si durante la interrupción, quita las copias de bases de datos del centro de datos principal dañado para permitir el truncamiento del archivo de registro en las copias aún activas del segundo centro de datos, la repropagación será necesaria. Las bases de datos pueden continuar individualmente a partir de este punto. Una vez que una copia de base de datos replicada del centro de datos principal tiene un estado normal, puede continuar con el siguiente paso.
    

    > [!NOTE]
    > Este proceso no requiere que todas las bases de datos se muevan al mismo tiempo. Se recomienda mover la mayoría de las bases de datos de la organización al mismo tiempo, pero es posible que algunas bases de datos se retrasen en el segundo centro de datos si existen problemas asociados a las copias de bases de datos en el centro de datos principal.



3.  Cuando la mayoría de las bases de datos tengan un estado normal en el centro de datos principal, se puede programar la interrupción de la recuperación. Cuando llega el momento programado, se deben llevar a cabo los siguientes pasos:
    
    1.  Durante el proceso de cambio del centro de datos, se configuró el DAG para que use un servidor testigo alternativo. Se debe reconfigurar el DAG para que use un servidor testigo en el centro de datos principal. Si utiliza el mismo servidor testigo y directorio testigo que se usó antes de la interrupción del centro de datos principal, puede ejecutar el comando `Set-DatabaseAvailabilityGroup -Identity DAGName`. Si planea utilizar un servidor o un directorio testigo diferente del servidor y del directorio testigo originales, debe usar el comando [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/es-es/library/dd297934\(v=exchg.150\)) para configurar los parámetros de servidor testigo y directorio testigo con los valores apropiados.
    
    2.  Las bases de datos que se reactivarán en el centro de datos principal deben desmontarse en el segundo centro de datos. Puede usar el cmdlet [Dismount-Database](https://technet.microsoft.com/es-es/library/bb124936\(v=exchg.150\)) para desmontar las bases de datos.
    
    3.  Una vez desmontadas las bases de datos, las direcciones URL del servidor de acceso de cliente se deben mover del segundo centro de datos al centro de datos principal. Para lograr esto, se debe modificar el registro DNS para que las direcciones URL apunten a la matriz o al servidor de acceso de cliente del centro de datos principal. Como consecuencia, el sistema funcionará como si se hubiera producido una conmutación por error en cada base de datos que se mueva.
        

        > [!IMPORTANT]
        > No continúe con el siguiente paso hasta que se hayan movido las direcciones URL del servidor de acceso de cliente y hayan expirado el TTL y las entradas de la memoria caché DNS. Si se activan las bases de datos en el centro de datos principal antes de mover las direcciones URL del servidor de acceso de cliente al centro de datos principal, se generará una configuración no válida (por ejemplo, una base de datos montada que no tiene servidores de acceso de cliente en su sitio de Active Directory).

    
    4.  Como todas las bases de datos del centro de datos principal tienen un estado normal, es posible activarlas en el centro de datos principal por medio de cambios de bases de datos. Para ello, se debe usar el cmdlet [Move-ActiveMailboxDatabase](https://technet.microsoft.com/es-es/library/dd298068\(v=exchg.150\)) para cada base de datos que se activará.
    
    5.  Una vez que se han movido todas las bases de datos al centro de datos principal, es posible montarlas mediante el cmdlet [Mount-Database](https://technet.microsoft.com/es-es/library/aa998871\(v=exchg.150\)).

Después de activar y montar una o varias bases de datos en el centro de datos principal, se pueden realizar procedimientos de recuperación para los otros roles de servidor.

## Recuperación del servidor de acceso de cliente

Como parte del proceso de cambio, se modificaron los registros DNS internos y externos usados por los clientes, otros servidores y las puertas de enlace IP para resolver los extremos de servicio de los servidores de acceso de cliente, servicios de transporte y de mensajería unificada y servidores de transporte perimetral para que apunten a los extremos correspondientes en el segundo centro de datos. El proceso de recuperación para los otros roles de servidor implica la modificación de esos registros para que apunten a los extremos de servicio restaurados en el centro de datos principal.

Como sucede con las modificaciones de DNS realizadas durante el cambio al segundo centro de datos, los clientes, los servidores y las puertas de enlace IP seguirán intentando establecer la conexión y deberían conectarse automáticamente una vez que hayan expirado el TTL para la entrada DNS original y la entrada de la memoria caché DNS.

Volver al principio

## Restablecimiento de la resistencia de sitios

Una vez que la recuperación se haya completado correctamente en el centro de datos principal, puede restablecer la resistencia de sitios para el centro de datos principal mediante la comprobación del estado de mantenimiento de cada copia de base de datos de buzones de correo en el segundo centro de datos. Asimismo, si alguna de las copias de bases de datos del segundo centro de datos se bloqueó originalmente para la activación, puede reconfigurar los valores en este momento.

Volver al principio

