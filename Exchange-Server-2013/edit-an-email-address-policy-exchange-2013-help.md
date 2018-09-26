---
title: 'Editar una directiva de dirección de correo electrónico: Exchange 2013 Help'
TOCTitle: Editar una directiva de dirección de correo electrónico
ms:assetid: cc8b36a0-95f4-43e9-bc64-87646d2e14e4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124580(v=EXCHG.150)
ms:contentKeyID: 49895920
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.EditEmailAddressPolicyWizardForm.EmailAddressPolicyIntroductionPage
ms.translationtype: HT
---

# Editar una directiva de dirección de correo electrónico

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-12-10_

Las directivas de direcciones de correo electrónico generan la dirección principal y la secundaria de los destinatarios (usuarios, contactos y grupos) para que puedan recibir y enviar correo electrónico.

Para ver otras tareas de administración relacionadas con las directivas de direcciones de correo electrónico, consulte [Procedimientos de directivas de direcciones de correo electrónico](email-address-policy-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - No puede usar el Centro de Administración de Exchange (EAC) para editar una directiva de direcciones de correo electrónico si esta se creó mediante el Shell.

  - Si la directiva de direcciones de correo electrónico se creó mediante un filtrado de remitentes, debe usar el Shell para editarla. Para obtener más información, consulte [Crear una directiva de la dirección de correo electrónico mediante filtros de destinatario](create-an-email-address-policy-by-using-recipient-filters-exchange-2013-help.md).

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Directivas de direcciones de correo electrónico" en el tema [Direcciones de correo electrónico y libretas de direcciones](email-addresses-and-address-books-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!WARNING]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Utilice el EAC para cambiar los destinatarios a los que se aplica la directiva

1.  Navegue hasta **Flujo de correo** \> **Directivas de direcciones de correo electrónico**.

2.  En la vista de lista, seleccione la directiva de direcciones de correo electrónico que quiere cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En **Directiva de direcciones de correo electrónico**, haga clic en **Aplicar a** y modifique la configuración.

## Utilice el EAC para cambiar la prioridad de directiva de direcciones de correo electrónico

Un usuario puede tener varias direcciones de correo electrónico del proxy para la misma cuenta de correo electrónico (por ejemplo, ayla@exchange.mail.contoso.com o ayla@contoso.com). De este modo, estas direcciones de correo electrónico pueden aplicarse por prioridad. Por ejemplo, considere la siguiente situación: tiene dos directivas de direcciones de correo electrónico y les asigna las prioridades 1 y 2. Si crea otra directiva, se le asignará automáticamente la prioridad 3. Sin embargo, supongamos que tiene dos directivas y especifica que una tenga la prioridad 1, pero que a la otra se le asigne la prioridad 2 predeterminada cuando se cree. En ese caso, la próxima directiva que cree se convertirá, de manera predeterminada, en una directiva de prioridad 2. A la directiva de prioridad 2 previa se le asignará una prioridad de 3.

1.  Navegue hasta **Flujo de correo** \> **Directivas de direcciones de correo electrónico**.

2.  Seleccione la directiva de direcciones de correo electrónico para la que desea cambiar la prioridad y luego haga clic en **Aumentar prioridad**![Icono flecha arriba](images/JJ150576.1732c727-328b-4a1a-b84d-6d7252c7dcab(EXCHG.150).gif "Icono flecha arriba") o **Reducir prioridad**![Icono flecha abajo](images/JJ150576.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif "Icono flecha abajo").

## Use el Shell para editar una directiva de direcciones de correo electrónico

En este ejemplo se edita la directiva de direcciones de correo electrónico de South East Offices que actualmente incluye los destinatarios de Georgia, Alabama y Louisiana para que incluya también los destinatarios de Texas.

```powershell
Set-EmailAddressPolicy -Identity "South East Offices" -ConditionalStateorProvince "Georgia","Alabama","Louisiana","Texas"
```


> [!NOTE]
> Aunque la directiva de direcciones de correo electrónico ya se aplica a los destinatarios de Georgia, Alabama y Louisiana, debe incluirlos en el parámetro debido a que el parámetro sobrescribe los valores; no anexa valores a los ya existentes.



Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-EmailAddressPolicy](https://technet.microsoft.com/es-es/library/bb124517\(v=exchg.150\)).

