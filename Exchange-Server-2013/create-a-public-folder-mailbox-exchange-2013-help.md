---
title: 'Crear un buzón de carpetas públicas: Exchange 2013 Help'
TOCTitle: Crear un buzón de carpetas públicas
ms:assetid: 64437ffd-231b-4c10-84df-232ccbe9538f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ552410(v=EXCHG.150)
ms:contentKeyID: 49116262
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Crear un buzón de carpetas públicas

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2014-10-23_

Para poder crear una carpeta pública primero debe crear un buzón de carpetas públicas. Los buzones de carpetas públicas contienen la información de jerarquía además del contenido de las carpetas públicas. El primer buzón de carpetas públicas que cree será el buzón de jerarquía principal, que contiene la copia de solo escritura de la jerarquía. El resto de los buzones de carpetas públicas que cree serán buzones secundarios, que contienen una copia de sólo lectura de la jerarquía.


> [!NOTE]
> For more information about the storage quotas and limits for public folders, see the following topics: 
> <UL>
> <LI>
> <P>Para carpetas públicas de Office 365, vea <A href="https://go.microsoft.com/fwlink/?linkid=391188">Límites de Exchange Online</A>.</P>
> <LI>
> <P>For public folders in on-premises Exchange Server 2013, see <A href="limits-for-public-folders-exchange-2013-help.md">Límites de las carpetas públicas</A>.</P></LI></UL>



Para otras tareas de administración relacionadas con las carpetas públicas de Exchange 2013, consulte [Procedimientos de carpetas públicas](public-folder-procedures-exchange-2013-help.md).

Para otras tareas de administración relacionadas con carpetas públicas en Exchange Online, consulte [Procedimientos de carpetas públicas en Office 365 y Exchange Online](https://technet.microsoft.com/es-es/library/jj966272\(v=exchg.150\)).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: menos de 5 minutos.

  - No puede haber carpetas públicas de Exchange 2013 y carpetas públicas en servidores de Exchange heredados en la misma organización. Si intenta crear un buzón de carpetas públicas cuando aún tiene carpetas públicas heredadas, recibirá el error **Se detectó una implementación de carpetas públicas existente. Para migrar los datos de carpetas públicas, cree un buzón de carpetas públicas nuevo mediante el modificador -HoldForMigration.**
    
    Para poder crear carpetas públicas en Exchange 2013, deberá migrar sus carpetas públicas heredadas a Exchange 2013. Para ello, siga los pasos de [Usar la migración en serie para migrar carpetas públicas a Exchange 2013 desde versiones anteriores](https://technet.microsoft.com/es-es/library/jj150486\(v=exchg.150\)). Estos pasos le muestran cómo crear un buzón de carpetas públicas que se pueden usar para almacenar las carpetas públicas migradas.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Carpetas públicas" en el tema [Permisos de uso compartido y colaboración](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## ¿Qué desea hacer?

## Uso del Centro de Administración de Exchange para crear un buzón de carpetas públicas

1.  Vaya a **Carpetas públicas** \> **Buzones de carpetas públicas** y haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

2.  En **Buzón de carpetas públicas**, especifique un nombre para el buzón de carpetas públicas.

3.  Haga clic en **Guardar**.

## Uso del Shell para crear un buzón de carpetas públicas

En este ejemplo, se crea el buzón de carpetas públicas principal.

    New-Mailbox -PublicFolder -Name MasterHierarchy

En este ejemplo, se crea un buzón de carpetas públicas secundario. La única diferencia entre crear un buzón de jerarquía principal y uno secundario es que el principal es el primero que se crea en la organización. Puede agregar buzones de carpetas públicas adicionales para equilibrar la carga.

    New-Mailbox -PublicFolder -Name Istanbul 

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-Mailbox](https://technet.microsoft.com/es-es/library/aa997663\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que el buzón de carpetas públicas principal se haya creado correctamente, ejecute el siguiente comando del Shell:

    Get-OrganizationConfig | Format-List RootPublicFolderMailbox

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-OrganizationConfig](https://technet.microsoft.com/es-es/library/aa997571\(v=exchg.150\)).

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

