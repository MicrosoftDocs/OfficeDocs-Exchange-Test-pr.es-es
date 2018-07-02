---
title: 'Eliminar una directiva de la dirección de correo electrónico: Exchange 2013 Help'
TOCTitle: Eliminar una directiva de la dirección de correo electrónico
ms:assetid: f1d05223-7d41-406d-8fae-f4227be1c1c2
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb125181(v=EXCHG.150)
ms:contentKeyID: 49896008
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Eliminar una directiva de la dirección de correo electrónico

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-13_

De manera predeterminada, Exchange incluye una directiva de direcciones de correo electrónico que especifica el alias del destinatario como la parte local de la dirección de correo electrónico y usa el dominio predeterminado aceptado. La parte local de una dirección de correo electrónico es el nombre que aparece antes del símbolo de arroba (@). Esta directiva de direcciones de correo electrónico se aplica a todos los usuarios de la organización. No puede quitar esta directiva de direcciones de correo electrónico.

Para conocer tareas de administración adicionales relacionadas las directivas de direcciones de correo electrónico, consulte [Procedimientos de directivas de direcciones de correo electrónico](email-address-policy-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Si quita una directiva de direcciones de correo electrónico usada por destinatarios como la directiva principal y no hay ninguna otra directiva configurada para los destinatarios, se usará la directiva predeterminada.

  - No puede eliminar la directiva predeterminada. Si desea eliminar la directiva predeterminada, primero debe asignar una directiva diferente como directiva predeterminada.

  - Si la directiva de direcciones de correo electrónico que se elimina contiene más de 3.000 destinatarios, debe usar el Shell para realizar este procedimiento.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Directivas de direcciones de correo electrónico" en el tema [Direcciones de correo electrónico y libretas de direcciones](email-addresses-and-address-books-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!WARNING]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Usar el EAC para eliminar una directiva de direcciones de correo electrónico

1.  Vaya a **Flujo de correo** \> **Directivas de direcciones de correo**.

2.  En la vista de lista, seleccione la directiva de direcciones de correo electrónico que desea eliminar y, a continuación, haga clic en **Eliminar**![Eliminar icono](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Eliminar icono").

3.  En la advertencia, haga clic en **Si** para eliminar la directiva.

## Usar el Shell para eliminar una directiva de direcciones de correo electrónico

En este ejemplo se quita la directiva de direcciones de correo electrónico denominada South East Offices (Oficinas del Sudeste).

    Remove-EmailAddressPolicy -Identity "South East Offices"

Escriba **Y** para confirmar que desea quitar la directiva y, a continuación, presione INTRO.

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Remove-EmailAddressPolicy](https://technet.microsoft.com/es-es/library/bb124504\(v=exchg.150\)).

