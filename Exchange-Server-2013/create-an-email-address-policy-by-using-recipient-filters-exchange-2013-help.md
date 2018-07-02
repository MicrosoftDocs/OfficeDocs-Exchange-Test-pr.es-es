---
title: 'Crear una directiva de la dirección de correo electrónico mediante filtros de destinatario: Exchange 2013 Help'
TOCTitle: Crear una directiva de la dirección de correo electrónico mediante filtros de destinatario
ms:assetid: e3f446bd-1511-479c-8d87-2dfce5547c90
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb232194(v=EXCHG.150)
ms:contentKeyID: 49895980
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Crear una directiva de la dirección de correo electrónico mediante filtros de destinatario

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-16_

Puede usar el Shell para crear una directiva de dirección de correo electrónico mediante filtros de destinatario. Para obtener más información acerca de las directivas de dirección de correo electrónico, consulte [Directivas de dirección de correo electrónico](email-address-policies-exchange-2013-help.md).

Para otras tareas de administración relacionadas con las directivas de dirección de correo electrónico, consulte [Procedimientos de directivas de direcciones de correo electrónico](email-address-policy-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Para usar el parámetro *RecipientFilter* para crear un filtro personalizado, debe especificar una cadena para el filtro. El Shell usa OPath para la sintaxis de filtrado. OPath es un lenguaje de consultas diseñado para consultar orígenes de datos de objetos.
    

    > [!IMPORTANT]
    > Si usa un filtro de destinatarios para crear o editar una directiva de dirección de correo electrónico, no puede usar el centro de administración de Exchange (EAC) para editar la directiva de dirección de correo electrónico. Debe usar el Shell. Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte <A href="https://technet.microsoft.com/es-es/library/bb124517(v=exchg.150)">Set-EmailAddressPolicy</A>.



  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Directivas de direcciones de correo electrónico" en el tema [Direcciones de correo electrónico y libretas de direcciones](email-addresses-and-address-books-exchange-2013-help.md).

  - Tenga en cuenta que para poder usar el dominio de direcciones SMTP en una directiva de direcciones de correo electrónico, debe configurar un dominio aceptado. Para obtener más información, consulte [Dominios aceptados](accepted-domains-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!WARNING]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Usar el Shell para crear una directiva de direcciones de correo electrónico mediante el uso de filtros de destinatarios

Para crear una directiva de dirección de correo electrónico mediante filtros de destinatario, use la siguiente sintaxis.

    New-EmailAddressPolicy -Name <String> -RecipientFilter <String>

En este ejemplo, se crea una directiva de dirección de correo electrónico que se aplica a todos los ejecutivos, para los cuales la parte local de la dirección de correo electrónico consta de las dos primeras letras del nombre y el apellido completo.

    New-EmailAddressPolicy -Name 'Execs' -EnabledEmailAddressTemplates 'SMTP:%2g%s@contoso.com' -RecipientFilter {((RecipientType -eq 'UserMailbox') -and (Title -like 'executive'))}

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [New-EmailAddressPolicy](https://technet.microsoft.com/es-es/library/aa996800\(v=exchg.150\)).

