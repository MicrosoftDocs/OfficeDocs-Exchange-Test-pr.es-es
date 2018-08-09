---
title: 'Preconfiguración de objeto nombre clúster para grupo disponibilidad base datos'
TOCTitle: Preconfiguración del objeto de nombre de clúster para un grupo de disponibilidad de base de datos
ms:assetid: 51ebf2f6-8a02-44ef-a489-ca361cb0f63a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ff367878(v=EXCHG.150)
ms:contentKeyID: 48268123
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Preconfiguración del objeto de nombre de clúster para un grupo de disponibilidad de base de datos

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-08-14_

En entornos donde la creación de cuentas de equipo se encuentra restringida o donde las cuentas se crean en un contenedor que no es el predeterminado, debe preconfigurar el objeto de nombre de clúster (CNO) y, a continuación, aprovisionarlo asignándole permisos. También es necesario preconfigurar el CNO para los miembros de DAG de Windows Server 2012 y Windows Server 2012 R2, debido a cambios en los permisos en Windows para los objetos de equipo. Cuando implemente un grupo de disponibilidad de base de datos (DAG) con servidores de buzones que ejecuten Windows Server 2012 o Windows Server 2012 R2, debe preconfigurar y aprovisionar el CNO, a menos que esté implementando un DAG sin punto de acceso administrativo del clúster. Los DAG sin punto de acceso administrativo del clúster no usan CNO; por lo tanto no se requiere preconfiguración para esos DAG.

Se crea una cuenta de equipo para el CNO, se deshabilita y, a continuación, hay dos alternativas:

  - Asignar el control total de la cuenta de equipo a la cuenta de equipo del primer servidor del buzón de correo que se agrega al DAG.

  - Asignar el control total de la cuenta de equipo al grupo de seguridad universal (USG) del subsistema de confianza de Exchange.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 1 minuto

  - Debe usar una cuenta que tenga permisos para crear objetos de equipo en Active Directory.

  - Después de completar los pasos siguientes, espere a que se produzca la replicación de Active Directory. Una vez que el objeto esté replicado, podrá agregar el primer miembro al DAG.


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Ensayo de CNO

1.  Abra Usuarios y equipos de Active Directory.

2.  Expanda el nodo del bosque.

3.  Haga clic con el botón secundario en la unidad organizativa (UO) en la que desea crear la nueva cuenta, seleccione **Crear** y, a continuación, seleccione **Equipo**.

4.  En el panel **Nuevo Objeto: equipo**, escriba el nombre de la cuenta de equipo para el CNO, en la casilla **Nombre de equipo**. Éste es el nombre que usará para el DAG. Haga clic en **Aceptar** para crear la cuenta.

5.  Haga clic con el botón secundario en la nueva cuenta de equipo y, a continuación, haga clic en **Deshabilitar cuenta**. Haga clic en **Sí** para confirmar la acción de deshabilitar y, a continuación, haga clic en **Aceptar**.

## Asignar permisos al CNO

1.  Abra Usuarios y equipos de Active Directory.

2.  Si las características avanzadas no están habilitadas, actívelas haciendo clic en **Ver** y, a continuación, en **Características avanzadas**.

3.  Haga clic con el botón secundario en la nueva cuenta de equipo y, a continuación, haga clic en **Propiedades**.

4.  En **Propiedades de \<nombre de equipo\>**, en la ficha **Seguridad**, haga clic en **Agregar** para agregar la cuenta de equipo para el primer nodo que se agregará al DAG o para agregar el USG del subsistema de confianza de Exchange:
    
      - Para agregar el subsistema de confianza de Exchange escriba **Exchange Trusted Subsystem** en el campo **Escriba los nombres de objeto que desea seleccionar**. Haga clic en **Aceptar** para agregar el USG. Seleccione el USG del subsistema de confianza de Exchange y, en el campo **Permisos para el subsistema de confianza de Exchange**, seleccione la opción **Control total** en la columna **Permitir**. Haga clic en **Aceptar** para guardar la configuración de permisos.
    
      - Para agregar la cuenta de equipo para el primer nodo que se agregará al DAG, haga clic en **Tipos de objetos**. En el cuadro de diálogo **Tipos de objetos** desactive las casillas **Principios de seguridad integrados**, **Grupos** y **Usuarios**. Seleccione la casilla **TCP** y, a continuación, haga clic en **Aceptar**. En el campo **Escriba los nombres de objeto que desea seleccionar** escriba el nombre del primer servidor de buzones de correo que se agregará al DAG y, a continuación, haga clic en **Aceptar**. Seleccione la cuenta de equipo del primer nodo y, en el campo **Permisos para \<NodeName\>**, seleccione **Control total** en la columna **Permitir**. Haga clic en **Aceptar** para guardar la configuración de permisos.

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que el CNO se creó correctamente, siga estos pasos:

1.  Abra Usuarios y equipos de Active Directory.

2.  Expanda el nodo del bosque.

3.  Abra la OU en la que creó la cuenta y compruebe que la cuenta aparece en la lista.

