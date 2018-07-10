---
title: 'Configurar la forma secundaria para los usuarios de Outlook Voice Access buscar: Exchange 2013 Help'
TOCTitle: Configurar la forma secundaria para los usuarios de Outlook Voice Access buscar
ms:assetid: 5cd4e0a0-d023-45a1-aa3c-b8dea6ec6d72
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998311(v=EXCHG.150)
ms:contentKeyID: 52061833
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar la forma secundaria para los usuarios de Outlook Voice Access buscar

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-22_

Al crear un plan de marcado, puede configurar los *métodos de marcado por nombre* o formas de que los autores de llamada puedan buscar nombres. Los autores de llamada usan estos métodos de marcado por nombre para buscar nombres cuando desean encontrar usuarios y comunicarse con ellos al llamar a un número de Outlook Voice Access o al llamar a un operador automático de mensajería unificada que está asociado al plan de marcado. Los autores de llamada pueden usar la marcación por tonos para localizar un usuario activo en la mensajería unificada.


> [!NOTE]
> Si se selecciona <STRONG>Ninguno</STRONG> como modo secundario para que los llamantes busquen nombres, sólo estará disponible el modo principal de búsqueda de nombres para los autores de llamada que quieran localizar usuarios. Si configura la forma principal y la secundaria mediante las cuales los autores de llamada pueden buscar por nombres, se les indicarán ambas formas.



Para otras tareas de administración relacionadas con los planes de marcado de mensajería unificada, consulte [Procedimientos de plan de marcado de mensajería unificada](um-dial-plan-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Planes de marcado de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para cambiar el método secundario de marcado por nombre

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**.

2.  En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Plan de marcado de mensajería unificada**, haga clic en **Configurar**.

4.  En **Configuración**, en **Forma secundaria de buscar nombres**, use la lista desplegable para seleccionar la opción que desee:
    
      - **Último primero** (predeterminado)
    
      - **Primero último**
    
      - **Dirección SMTP**
    
      - **Ninguno**

5.  Haga clic en **Guardar**.

## Usar el Shell para cambiar el método secundario de marcado por nombre

En este ejemplo, se establece el método secundario de marcado por nombre en `FirstLast`. Esto permite que las personas que llaman al número de Outlook Voice Access o a un operador automático de MU asociado con el plan de marcado busquen un usuario habilitado para MU primero por el nombre y, luego, por el apellido.

    Set-UMDialPlan -Identity MyUMDialPlan -DialByNameSecondary FirstLast

En este ejemplo, se establece el método secundario de marcado por nombre en `LastFirst`. Esto permite que las personas que llaman al número de Outlook Voice Access o a un operador automático de MU asociado con el plan de marcado busquen un usuario habilitado para MU primero por el apellido y, luego, por el nombre.

    Set-UMDialPlan -Identity MyUMDialPlan -DialByNameSecondary LastFirst 

En este ejemplo, se establece el método secundario de marcado por nombre en `SMTP address`. Esto permite que las personas que llaman al número de Outlook Voice Access o a un operador automático de MU asociado con el plan de marcado busquen un usuario habilitado para MU por la dirección SMTP.

    Set-UMDialPlan -Identity MyUMDialPlan -DialByNameSecondary SMTPAddress 

En este ejemplo se establece el método secundario de marcado por nombre en `None` y el método primario de marcado por nombre en `SMTP address`. Esto permite que las personas que llaman al número de Outlook Voice Access o a un operador automático de MU asociado con el plan de marcado busquen a un usuario habilitado para MU solo por la dirección SMTP.

    Set-UMDialPlan -Identity MyUMDialPlan -DialByNamePrimary SMTPAddress -DialByNameSecondary None

