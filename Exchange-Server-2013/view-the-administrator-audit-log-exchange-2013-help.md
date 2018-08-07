---
title: 'Ver el registro de auditoría del administrador: Exchange 2013 Help'
TOCTitle: Ver el registro de auditoría del administrador
ms:assetid: 5c62072a-556d-4fea-9973-d668c6b9fd57
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn342832(v=EXCHG.150)
ms:contentKeyID: 56271475
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ver el registro de auditoría del administrador

 

_**Se aplica a:** Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**Última modificación del tema:** 2016-05-03_

En Microsoft Exchange Online Protection (EOP), Microsoft Exchange Online y Microsoft Exchange 2013, puede usar el Centro de administración de Exchange (EAC) para buscar y ver entradas en el *registro de auditoría del administrador*. El registro de auditoría del administrador registra acciones específicas, según el cmdlet del Shell de administración de Exchange, realizadas por administradores y usuarios que tienen asignados privilegios de administrador. Las entradas en el registro de auditoría del administrador proporcionan información sobre el cmdlet que se ejecutó, los parámetros que se usaron, el usuario que ejecutó el cmdlet y los objetos que se vieron afectados.


> [!NOTE]
> <UL>
> <LI>
> <P>El registro de auditoría de administrador está habilitado de forma predeterminada.</P>
> <LI>
> <P>El registro de auditoría del administrador no registra ninguna acción basada en un cmdlet del Shell de administración de Exchange que empiece con las palabras <STRONG>Get</STRONG>, <STRONG>Search</STRONG> o <STRONG>Test</STRONG>.</P>
> <LI>
> <P>Las entradas de los registros de auditoría se conservan durante 90&nbsp;días. Cuando una entrada tiene una antigüedad mayor que 90&nbsp;días, se elimina.</P></LI></UL>



## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Ver informes" en el tema sobre [Feature permissions in EOP](https://technet.microsoft.com/es-es/library/jj723125\(v=exchg.150\)).

  - Como se mencionó anteriormente, el registro de auditoría de administrador está habilitado de forma predeterminada. Para comprobar que está habilitado, puede ejecutar el siguiente comando.
    
        Get-AdminAuditLogConfig | FL AdminAuditLogEnabled
    
    En Exchange 2013, puede habilitar el registro de auditoría de administrador, si está deshabilitado, ejecutando el siguiente comando.
    
        Set-AdminAuditLogConfig -AdminAuditLogEnabled $True
    
    En Exchange Online Protection y Exchange Online, el registro de auditoría de administrador siempre está habilitado. No se puede deshabilitar.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Uso del EAC para ver el registro de auditoría del administrador

1.  En el EAC, vaya a **Administración de cumplimiento** \> **Auditoría** y elija **Ejecutar el registro de auditoría del administrador**.

2.  Elija una **Fecha de inicio** y una **Fecha de finalización** y, a continuación, elija **Buscar**. Todos los cambios de configuración realizados durante el período de tiempo especificado se muestran y se pueden ordenar, mediante la siguiente información:
    
      - **Fecha:**  la fecha y hora en que se realizó el cambio de configuración. La fecha y la hora se almacenan en formato de hora universal coordinada (UTC).
    
      - **Cmdlet:**  el nombre del cmdlet que se usó para realizar el cambio de configuración.
    
      - **Usuario:**  el nombre de la cuenta de usuario del usuario que realizó el cambio de configuración.
    
    Se mostrarán hasta 5000 entradas en varias páginas. Especifique un intervalo de fechas menor si necesita limitar los resultados. Si selecciona un resultado de la búsqueda individual, se mostrará la siguiente información adicional en el panel de detalles:
    
      - **Objeto modificado:**  el objeto modificado por el cmdlet.
    
      - **Parámetros (Parámetro:Valor):**  los parámetros del cmdlet que se utilizaron, así como cualquier valor especificado con el parámetro.

3.  Si desea imprimir una entrada específica del registro de auditoría, elija el botón **Imprimir** en el panel de detalles.

## ¿Cómo puede saber si funcionó?

Si ejecutó correctamente un informe del registro de auditoría del administrador, los cambios de configuración realizados dentro del intervalo de fechas especificado aparecerán en el panel de resultados de la búsqueda. Si no hay resultados, cambie el intervalo de fechas y vuelva a ejecutar el informe.


> [!NOTE]
> Cuando se realiza un cambio en la organización, pueden transcurrir hasta 15 minutos para que aparezca en los resultados de la búsqueda del registro de auditoría. Si un cambio no aparece en el registro de auditoría del administrador, espere unos minutos y vuelva a ejecutar la búsqueda.


