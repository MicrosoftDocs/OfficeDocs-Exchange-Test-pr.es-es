---
title: 'Crear una directiva de dirección de correo electrónico: Exchange 2013 Help'
TOCTitle: Crear una directiva de dirección de correo electrónico
ms:assetid: eb2bf42e-2058-4e17-85d5-97546433b40a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb125137(v=EXCHG.150)
ms:contentKeyID: 49895992
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.NewEmailAddressPolicyWizardForm.EmailAddressPolicyIntroductionPage
ms.translationtype: MT
---

# Crear una directiva de dirección de correo electrónico

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2012-12-10_

Para que un destinatario reciba o envíe mensajes de correo electrónico, debe disponer de una dirección de correo electrónico. Las directivas de direcciones de correo electrónico generan la dirección principal y la secundaria de los destinatarios (usuarios, contactos y grupos) para que puedan recibir y enviar correo electrónico.

Al crear una política de direcciones de correo electrónico, puede usar los siguientes tipos de direcciones:

  - **Dirección de correo electrónico SMTP predefinida**. Las direcciones de correo electrónico SMTP *predefinida* son los tipos de direcciones de correo electrónico usadas habitualmente y que se le proporcionan.

  - **Dirección de correo electrónico SMTP personalizada**. Si no desea usar una de las direcciones de correo electrónico SMTP predefinidas, puede especificar una dirección de correo electrónico SMTP personalizada.
    
    Al crear una dirección de correo electrónico SMTP personalizada, puede usar las variables de la tabla que aparecen a continuación para especificar valores alternativos para la parte local de la dirección de correo electrónico.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Variable</th>
    <th>Valor</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>%g</p></td>
    <td><p>Nombre (nombre de pila)</p></td>
    </tr>
    <tr class="even">
    <td><p>%i</p></td>
    <td><p>Inicial del segundo nombre</p></td>
    </tr>
    <tr class="odd">
    <td><p>%s</p></td>
    <td><p>Apellido</p></td>
    </tr>
    <tr class="even">
    <td><p>%d</p></td>
    <td><p>Nombre para mostrar</p></td>
    </tr>
    <tr class="odd">
    <td><p>%m</p></td>
    <td><p>Alias de Exchange</p></td>
    </tr>
    <tr class="even">
    <td><p>%<em>x</em>s</p></td>
    <td><p>Utiliza las primeras <em>x</em> letras del apellido. Por ejemplo, si <em>x</em>=2, se utilizan las dos primeras letras del apellido.</p></td>
    </tr>
    <tr class="odd">
    <td><p>%<em>x</em>g</p></td>
    <td><p>Utiliza las primeras <em>x</em> letras del nombre de pila. Por ejemplo, si <em>x</em>=2, se utilizan las dos primeras letras del nombre.</p></td>
    </tr>
    </tbody>
    </table>


  - **Dirección de correo electrónico no SMTP**. Pueden utilizarse los siguientes tipos de direcciones de correo electrónico no SMTP:
    
      - EX (Parámetro DisplayName del prefijo de la dirección proxy de DN heredado)
    
      - X.500
    
      - X.400
    
      - MSMail
    
      - CcMail
    
      - Lotus Notes
    
      - Novell GroupWise
    
      - Dirección proxy de mensajería unificada de Exchange (dirección proxy EUM)
    

    > [!IMPORTANT]
    > En Exchange, todas las direcciones de correo electrónico no SMTP se consideran direcciones personalizadas. Exchange no proporciona cuadros de diálogo exclusivos ni páginas de propiedades para los tipos de direcciones de correo electrónico de X.400, GroupWise o Lotus Notes. Si agrega una dirección de correo electrónico personalizada no SMTP, debe tener los archivos de biblioteca de vínculos dinámicos (DLL) adecuados. Si no proporciona los archivos DLL apropiados, no podrá crear una directiva de direcciones de correo electrónico personalizadas. Se registrará el siguiente error en el Visor de eventos: "Falta el objeto de descripción de direcciones de correo electrónico del directorio de Microsoft Exchange para el tipo de dirección 'SADF' en equipos 'i386'."



Para obtener instrucciones detalladas para crear políticas de direcciones de correo electrónico, consulte los siguientes temas:

[Crear una directiva de dirección de correo electrónico](create-an-email-address-policy-exchange-2013-help.md)

[Crear una directiva de la dirección de correo electrónico mediante filtros de destinatario](create-an-email-address-policy-by-using-recipient-filters-exchange-2013-help.md)

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Directivas de direcciones de correo electrónico" en el tema [Direcciones de correo electrónico y libretas de direcciones](email-addresses-and-address-books-exchange-2013-help.md).

  - Tenga en cuenta que para poder usar el dominio de direcciones SMTP en una directiva de direcciones de correo electrónico, debe configurar un dominio aceptado. Para obtener más información, consulte [Dominios aceptados](accepted-domains-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!WARNING]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Usar el EAC para crear una directiva de direcciones de correo electrónico

1.  Vaya a **Flujo de correo** \> **Directivas de direcciones de correo** y, a continuación, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

2.  En **Directiva de dirección de correo**, complete los campos siguientes:
    
      - **Nombre de la directiva**
    
      - **Formato de dirección de correo**
    
      - **Especificar los tipos de destinatarios a los que se aplicará esta dirección de correo electrónico**

3.  
    
    Haga clic en **Agregar una regla** para restringir aún más los destinatarios a quienes se aplicará esta directiva. Esto crea una declaración **And** booleana.
    

    > [!WARNING]
    > Si aplica demasiadas reglas, es posible restringir la directiva de direcciones de correo electrónico hasta que no contenga ningún usuario.



4.  Haga clic en **Vista previa de destinatarios a los que se aplica la directiva** para ver los destinatarios a quienes se aplicará esta directiva.

5.  
    
    Haga clic en **Guardar** para guardar los cambios y crear la directiva.

6.  Se mostrará una advertencia que indicará que la directiva de direcciones de correo electrónico no se aplicará hasta que la actualice. Una vez creada, selecciónela y, a continuación, haga clic en **Aplicar** en el panel de detalles.

## Usar el Shell para crear una directiva de direcciones de correo electrónico

En este ejemplo, se crea una directiva de direcciones de correo electrónico que incluye usuarios de buzones de correo de las oficinas del sudeste, cuyas direcciones de correo electrónico contienen el apellido combinado con las primeras dos letras del nombre.

    New-EmailAddressPolicy -Name "southeast offices" -IncludedRecipients MailboxUsers -ConditionalStateorProvince "Georgia","Alabama","Louisiana" -EnabledEmailAddressTemplates "SMTP:%s%2g@southeast.contoso.com"

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-EmailAddressPolicy](https://technet.microsoft.com/es-es/library/aa996800\(v=exchg.150\)).

