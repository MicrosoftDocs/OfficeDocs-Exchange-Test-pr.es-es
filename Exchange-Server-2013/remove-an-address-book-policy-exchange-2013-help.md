---
title: 'Quitar una política de libreta de direcciones: Exchange 2013 Help'
TOCTitle: Quitar una política de libreta de direcciones
ms:assetid: c20c6f82-2f75-4116-9be1-c5af10113f71
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Hh529946(v=EXCHG.150)
ms:contentKeyID: 49895892
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Quitar una política de libreta de direcciones

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2014-03-25_

Utilice este procedimiento para quitar una directiva de libreta de direcciones (ABP).

Para otras tareas de administración relacionadas con las directivas de libretas de direcciones (ABP), consulte [Procedimientos de directivas de la libreta de direcciones](address-book-policy-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Directivas de libreta de direcciones" en el tema [Permisos de libreta de direcciones y dirección de correo electrónico](email-address-and-address-book-permissions-exchange-2013-help.md).

  - No puede eliminar la ABP si aún está asignada al buzón de un usuario o a un buzón eliminado temporalmente. Para determinar si una ABP está asignada a un usuario, ejecute el siguiente comando en el Shell:
    
    `Get-Mailbox | Where $._AddressBookPolicy -eq <AddressBookPolicyName>`
    
    Para determinar si una ABP está asignada a un buzón eliminado temporalmente, ejecute el siguiente comando:
    
    `Get-Mailbox -SoftDeletedMailbox | Where $._AddressBookPolicy -eq <AddressBookPolicyName>`

  - Para quitar la ABP del buzón de un usuario, use la ficha **Características de buzón de correo** de la página de propiedades del buzón o el cmdlet **Set-Mailbox**.

  - No puede usar el Centro de Administración de Exchange (EAC) para eliminar un ABP. Debe usar el Shell.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Uso del Shell para quitar una ABP

En este ejemplo se quita la ABP llamada ABP\_TailspinToys.

    Remove-AddressBookPolicy -Identity "ABP_TailspinToys"

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Remove-AddressBookPolicy](https://technet.microsoft.com/es-es/library/hh529929\(v=exchg.150\)).

