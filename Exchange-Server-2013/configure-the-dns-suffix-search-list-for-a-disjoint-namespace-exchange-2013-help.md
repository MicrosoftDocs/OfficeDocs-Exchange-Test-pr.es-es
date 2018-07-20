---
title: 'Configurar la lista de búsqueda de sufijos DNS para un espacio de nombres distintos: Exchange 2013 Help'
TOCTitle: Configurar la lista de búsqueda de sufijos DNS para un espacio de nombres distintos
ms:assetid: cfa715ac-7b69-47c3-b206-933ec2cf677b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb847901(v=EXCHG.150)
ms:contentKeyID: 49895924
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar la lista de búsqueda de sufijos DNS para un espacio de nombres distintos

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

En este tema se explica cómo usar la Consola de administración de directivas de grupos (GPMC) para configurar la lista de búsqueda de sufijos del Sistema de nombres de dominio (DNS). En algunos escenarios de Microsoft Exchange 2013, si tiene un espacio de nombres distinto, debe configurar la lista de búsqueda de sufijos DNS para incluir varios sufijos DNS.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 10 minutos

  - Para efectuar este procedimiento, la cuenta que use debe tener delegada la pertenencia al grupo Admins. del dominio.

  - Confirme que ha instalado .NET Framework 3.0 en el equipo en el que instalará la GPMC.
    

    > [!NOTE]
    > La versión actual de la GPMC que puede descargar del Centro de descargas de Microsoft funciona en versiones de 32 bits de los sistemas operativos Windows Server 2003&nbsp;y Windows&nbsp;XP, y puede administrar, de forma remota, objetos de directiva de grupo en controladores de dominio de 32 y 64 bits. Esta versión de la GPMC no incluye una versión de 64 bits, y la versión de 32 bits no se ejecuta en plataformas de 64 bits. La versión de 32 bits de Windows Server 2008&nbsp;y la versión de 32 bits de Windows Vista&nbsp;incluyen ambas una versión de 32 bits de la GPMC. La versión de 64 bits de Windows Server 2008&nbsp;y la versión de 64 bits de Windows Vista&nbsp;incluyen ambas una versión de 64 bits de la GPMC.



  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Usar la GPMC para configurar la lista de búsqueda de sufijos del DNS

1.  En un equipo de 32 bits de su dominio, instale GPMC con Service Pack 1 (SP1). Para obtener información sobre la descarga, consulte [Consola de administración de directivas de grupos con Service Pack 1](https://go.microsoft.com/fwlink/p/?linkid=100126).
    

    > [!NOTE]
    > Si en su dominio hay un equipo con Windows Server 2008&nbsp;o Windows Vista, puede omitir este paso.



2.  Haga clic en **Inicio** \> **Programas** \> **Herramientas administrativas** \> **Administración de directivas de grupos**.

3.  En **Administración de directivas de grupo**, expanda el bosque y el dominio al que aplicará la Directiva de grupo. Haga clic con el botón secundario en **Objetos de directiva de grupo** y haga clic en **Nuevo**.

4.  En **Nuevo GPO**, escriba el nombre de la directiva y haga clic en **Aceptar**.

5.  Haga clic con el botón secundario en la nueva directiva creada en el paso 4 y, a continuación, haga clic en **Modificar**.

6.  En el **Editor de administración de directivas de grupo**, expanda **Configuración del equipo**, expanda **Directivas**, expanda **Plantillas administrativas**, expanda **Red** y, a continuación, haga clic en **Cliente DNS**.

7.  Haga clic con el botón secundario en **Lista de búsqueda de sufijos DNS**, haga clic en **Todas las tareas** y, a continuación, haga clic en **Propiedades**.

8.  En la página **Propiedades de la lista de búsqueda de sufijos DNS**, seleccione **Habilitada**. En el cuadro **Sufijos DNS**, escriba el sufijo DNS primario del equipo distinto, el nombre del dominio DNS y otros espacios de nombres adicionales para los servidores con los que Exchange pudiera interoperar, por ejemplo, servidores de supervisión o servidores para aplicaciones de terceros. Haga clic en **Aceptar**.

9.  En **Administración de directivas de grupo**, expanda **Objetos de directiva de grupo** y, a continuación, seleccione la directiva creada en el paso 4. En la ficha **Ámbito**, seleccione para la directiva un ámbito que permita aplicarla sólo a los equipos distintos.

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la migración se completó correctamente, realice lo siguiente:

  - Una vez que haya instalado Exchange 2013, compruebe que puede enviar mensajes de correo electrónico dentro y fuera de su organización.

## Más información

[Directiva de grupo de Windows Server](https://go.microsoft.com/fwlink/p/?linkid=100128)

[Directiva de grupo](https://go.microsoft.com/fwlink/?linkid=268043)

[Escenarios de espacios de nombres distintos](disjoint-namespace-scenarios-exchange-2013-help.md)

