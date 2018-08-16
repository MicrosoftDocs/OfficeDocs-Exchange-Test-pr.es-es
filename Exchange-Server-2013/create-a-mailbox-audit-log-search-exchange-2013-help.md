---
title: 'Crear una búsqueda en los registros de auditoría de buzones Exchange 2013 Help'
TOCTitle: Crear una búsqueda en los registros de auditoría de buzones
ms:assetid: 48ba22cf-b1f2-4dbc-98fc-fed22d97db14
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ff461929(v=EXCHG.150)
ms:contentKeyID: 49895607
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Crear una búsqueda en los registros de auditoría de buzones

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-11_

Puede crear una búsqueda de registros de auditoría de buzón de correo para buscar de forma asincrónica uno o más buzones de correo y hacer que los resultados de búsqueda se envíen por correo electrónico como archivo XML a las direcciones especificadas.

Para buscar los registros de auditoría de buzones de correo para un buzón de correo único y para que los resultados se muestren en la ventana del Shell, consulte [Buscar el registro de auditoría de un buzón](search-the-mailbox-audit-log-for-a-mailbox-exchange-2013-help.md).

Para otras tareas de administración relacionadas con los registros de auditorías de buzones de correo, consulte [Procedimientos de registro de auditoría de buzones](mailbox-audit-logging-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  2 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Registro de auditoría de buzones" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - De manera predeterminada, el registro de auditoría de buzón de correo está deshabilitado para todos los buzones de correo. Para cada buzón que desee auditar, debe habilitar los registros de auditoría y especificar las acciones del propietario, delegado o administrador del buzón que desea auditar. Para obtener más información, consulte [Habilitar o deshabilitar el registro de auditoría de buzones para un buzón](enable-or-disable-mailbox-audit-logging-for-a-mailbox-exchange-2013-help.md).

  - No puede usar el EAC para buscar registros de auditoría de buzones de correo para el acceso de los propietarios. La sección de auditoría en el EAC incluye informes para el acceso a buzones de correo no propietarios y también le permite buscar y exportar eventos de accesos no propietarios.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Utilice el EAC para crear una búsqueda de registro de auditoría de buzón

1.  Vaya a **Administración de cumplimiento** \> **Auditoría**.

2.  En la vista de lista, seleccione **Exportar registros de auditoría de buzones de correo**.

3.  En **Exportar registros de auditoría de buzones de correo**, complete los siguientes campos y, a continuación, haga clic en **Exportar**:
    
      - **Fecha de inicio**
    
      - **Fecha de finalización**
    
      - **Busque estos buzones de correo o déjelo en blanco para encontrar todos los buzones de correo a los cuales han accedido no propietarios**
        

        > [!WARNING]
        > En función del número de buzones de correo de su organización y de la cantidad de datos de registro de auditoría de buzones de correo en cada buzón de correo, la búsqueda en buzones de correo puede tardar un tiempo.

    
      - **Búsqueda de acceso por**
        
        Seleccione entre los siguientes tipos de eventos de acceso que desea buscar:
        
          - **Todos los no propietarios**
        
          - **Usuarios externos**
        
          - **Los administradores y usuarios delegados**
        
          - **Administradores**
    
      - **Enviar el informe de auditoría a**

## Utilice el comando Shell para crear una búsqueda de registro de auditoría de buzón

Para ver un ejemplo acerca del uso del Shell para crear una búsqueda de registro de auditoría de buzones de correo, consulte [Example 1](https://technet.microsoft.com/es-es/95365cab-bbb2-4a64-8e8f-1c89fa9e0352\(exchg.150\)#example1) en **New-MailboxAuditLogSearch**.

