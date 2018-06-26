---
title: 'Agregar el buzón de la federación para el grupo de usuarios de AD RMS Super: Exchange 2013 Help'
TOCTitle: Agregar el buzón de la federación para el grupo de usuarios de AD RMS Super
ms:assetid: 44618df9-54f0-4474-a450-dcba48a02901
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee424431(v=EXCHG.150)
ms:contentKeyID: 49895598
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Agregar el buzón de la federación para el grupo de usuarios de AD RMS Super

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

En las siguientes características de Microsoft Exchange Server 2013 Information Rights Management (IRM) que se habilitarán, debe agregar un buzón de correo de la federación (un buzón de correo del sistema creado por la configuración de Exchange 2013) para el grupo de superusuarios en el clúster [Información general sobre Active Directory Rights Management Services](https://technet.microsoft.com/es-es/library/hh831364.aspx):

  - IRM en Microsoft Office Outlook Web App

  - IRM en Exchange ActiveSync

  - Descifrado de informe de diarios

  - Descifrado de transporte

Puede configurar un grupo de distribución habilitado para correo como un grupo de superusuarios de AD RMS. Los miembros del grupo de distribución obtienen una licencia de uso de propietario cuando solicitan una licencia al clúster de AD RMS. Esto les permite descifrar todos los contenidos protegidos por RMS que fueron publicados por ese clúster. Si usa un grupo de distribución existente o crea un grupo de distribución y lo configura como grupo de superusuarios en AD RMS, se recomienda que destine el grupo de distribución a este fin y configure las opciones necesarias para aprobar, auditar y supervisar los cambios de pertenencia.


> [!WARNING]
> La configuración de un grupo de superusuarios en AD RMS permite a los miembros del grupo descifrar el contenido protegido de IRM. Le recomendamos que tome las medidas adecuadas para controlar y supervisar la pertenencia a un grupo y habilitar la auditoría para hacer un seguimiento de los cambios de pertenencia. También puede limitar los cambios no deseados a la pertenencia a un grupo configurando el grupo como grupo restringido usando directivas de grupo. Para obtener información, consulte <A href="https://technet.microsoft.com/es-es/library/cc756802(v=ws.10).aspx">Configuración de la directiva de grupos restringidos</A> .



Para otras tareas de administración relacionadas con IRM, consulte [Procedimientos de Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  15 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Grupos de distribución" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Un clúster de AD RMS se debe implementar en el bosque Active Directory.

  - Si ya existe un grupo de superusuarios configurado en un clúster de AD RMS, cualquier modificación de la pertenencia al grupo de distribución puede demorar hasta 24 horas para que el clúster de AD RMS la actualice. Esto es consecuencia del almacenamiento en caché de la pertenencia al grupo en el clúster.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Cómo realiza esto?

## Paso 1: Use el comando Shell para agregar el buzón de la federación a un grupo de distribución

Si se ha creado un grupo de distribución y se configura como un grupo de superusuarios en el clúster AD RMS, puede agregar el buzón de correo de la federación de Exchange 2013 como integrante de ese grupo. Si no se ha configurado un grupo de superusuarios, debe crear un grupo de distribución y agregar el buzón de correo de la federación como miembro.

1.  Cree un grupo de distribución destinado a ser usado como un grupo de superusuarios de AD RMS. Para obtener información detallada, consulte [Crear y administrar grupos de distribución](create-and-manage-distribution-groups-exchange-2013-help.md).

2.  Agregue el usuario **FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042** al grupo de distribución nuevo. El buzón de correo de la federación es un buzón de correo del sistema y, por lo tanto, no está visible en el EAC. Para agregarlo a un grupo de distribución, debe usar el cmdlet [Add-DistributionGroupMember](https://technet.microsoft.com/es-es/library/bb124340\(v=exchg.150\)) del Shell.
    
    Este ejemplo agrega el buzón de federación al grupo de distribución de ADRMSSuperUsers.
    
        Add-DistributionGroupMember ADRMSSuperUsers -Member FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Add-DistributionGroupMember](https://technet.microsoft.com/es-es/library/bb124340\(v=exchg.150\)).

## Paso 2: Usar AD RMS para configurar un grupo de superusuarios

Lleve a cabo el siguiente procedimiento en un clúster de AD RMS. La cuenta usada para llevar a cabo este procedimiento debe ser miembro del grupo local Administradores de empresa de AD RSM en el servidor de AD RMS.

1.  Abra la consola de Active Directory Rights Management Services y expanda el clúster de AD RMS.

2.  En el árbol de consola, expanda **Directivas de seguridad** y haga clic en **Superusuarios**.

3.  En el panel de acciones, haga clic en **Habilitar superusuarios**.

4.  En el panel de resultados, haga clic en **Cambiar grupo de superusuarios** para abrir la hoja de propiedades **Superusuarios**.

5.  En el cuadro **Grupo de superusuarios**, escriba la dirección de correo electrónico del grupo de distribución creado en el procedimiento anterior o haga clic en **Examinar** para seleccionar un grupo de distribución.

## ¿Cómo saber si el proceso se ha completado correctamente?

Después de haber añadido un buzón de correo de la federación a un grupo de distribución nuevo o existente, use el cmdlet [Get-DistributionGroupMember](https://technet.microsoft.com/es-es/library/aa996367\(v=exchg.150\)) para comprobar la pertenencia al grupo.

Para ver un ejemplo sobre cómo comprobar la pertenencia a un grupo de distribución, consulte [Examples](https://technet.microsoft.com/es-es/aa996367\(exchg.150\)#examples) en **Get-DistributionGroupMember**.

Después de haber usado AD RMS para configurar un grupo de superusuarios, puede usar los siguientes métodos para comprobar que el grupo de superusuarios se haya configurado correctamente. Además, puede usar el cmdlet [Test-IRMConfiguration](https://technet.microsoft.com/es-es/library/dd979798\(v=exchg.150\)) para comprobar la funcionalidad de IRM.

  - Use la consola AD RMS para comprobar que se haya configurado el grupo correcto como grupo de superusuarios.

  - Ejecute el siguiente comando de PowerShell en un servidor de AD RMS para recuperar el grupo de superusuarios.
    

    > [!IMPORTANT]
    > El módulo ADRMSAdmin PowerShell está disponible en Windows Server 2008 R2 y posterior.

    
        Import-Module ADRMSAdmin
        New-PSDrive -Name MyRmsAdmin -PsProvider AdRmsAdmin -Root https://localhost 
        Get-ItemProperty -Path MyRmsAdmin:\SecurityPolicy\SuperUser

