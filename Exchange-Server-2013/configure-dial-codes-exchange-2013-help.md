---
title: 'Configurar códigos de marcado: Exchange 2013 Help'
TOCTitle: Configurar códigos de marcado
ms:assetid: e5b5efee-b734-4f70-8357-11be07b23bd0
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124992(v=EXCHG.150)
ms:contentKeyID: 51406566
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar códigos de marcado

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-22_

Puede configurar códigos de marcado, prefijos numéricos y formatos de número que la mensajería unificada usa para marcar llamadas entrantes y salientes de los usuarios con mensajería unificada habilitada. En la mayoría de los casos, se configurará un plan de marcado con los códigos de marcado, los prefijos y los formatos de número actualmente configurados en la red telefónica.

Los códigos de marcado y los prefijos de números se usan para determinar el número correcto para una llamada saliente efectuada por un usuario habilitado para mensajería unificada. *Llamada externa* es el término que se usa para describir el proceso mediante el cual un usuario inicia una llamada saliente en un plan de marcado de mensajería unificada. Los formatos de número se usan para las llamadas entrantes dentro de un país o región, para llamadas internacionales o llamadas ubicadas en un plan de marcado. Puede configurar un plan de marcado para que coincida con el formato de número de llamadas entrantes para los números nacionales/regionales e internacionales. Al configurar los formatos de números nacionales/regionales e internacionales, se pueden restringir las llamadas entrantes a los usuarios vinculados con un plan de marcado.

Para otras tareas de administración relacionadas con las llamadas externas, vea [Permitir a los usuarios realizar llamadas a procedimientos](allowing-users-to-make-calls-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Planes de marcado de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso del EAC para configurar códigos de marcado, prefijos y formatos de número

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**.

2.  Seleccione el plan de marcado de mensajería unificada que quiera administrar y luego haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Plan de marcado de mensajería unificada**, haga clic en **Configurar**.

4.  En la página **Plan de marcado de mensajería unificada** \> **Códigos de marcado**, configure las siguientes opciones:
    
      - **Código de acceso de línea exterior**
    
      - **Código de acceso internacional**
    
      - **Prefijo de número nacional**
    
      - **Código de país/región**

5.  En **Formatos numéricos para marcar entre planes de marcado**, configure lo siguiente:
    
      - **Formato de número nacional o regional**
    
      - **Formato de número internacional**
    
      - **Formatos numéricos para llamadas entrantes dentro del mismo plan de marcado**   Para agregar un formato de número, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

6.  Haga clic en **Guardar** para guardar los cambios.

## Uso del Shell para configurar códigos de marcado, prefijos y formatos de número

En este ejemplo se configura un plan de marcado de mensajería unificada denominado `MyUMDialPlan` con un formato de número nacional o regional y un formato de número internacional, y los siguientes códigos de marcado:

  - 9 para el código de acceso de línea exterior

  - 011 para el código de acceso internacional

  - 1 para el prefijo numérico nacional

  - 1 para el código de país o región

<!-- end list -->

    Set-UMDialPlan -Identity MyUMDialPlan -OutsideLineAccessCode 9 -InternationalAccessCode 011 -NationalNumberPrefix 1 CountryorRegionCode 1 -InCountryOrRegionNumberFormat 1425xxxxxxx -InternationalNumberFormat 441425xxxxxxx

