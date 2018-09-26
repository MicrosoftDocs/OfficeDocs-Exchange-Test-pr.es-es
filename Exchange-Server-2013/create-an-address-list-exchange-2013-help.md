---
title: 'Crear una lista de direcciones: Exchange 2013 Help'
TOCTitle: Crear una lista de direcciones
ms:assetid: e86ba1b7-c41c-4050-bc29-13996cf53c59
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb125036(v=EXCHG.150)
ms:contentKeyID: 49895987
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.NewAddressListWizardForm.AddressListIntroductionPage
ms.translationtype: MT
---

# Crear una lista de direcciones

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-12_

Las listas de direcciones son un conjunto de objetos de destinatario y otros objetos de Active Directory. Cada lista de direcciones puede contener uno o varios tipos de objetos (por ejemplo, usuarios, contactos, grupos, carpetas públicas, conferencias y otros recursos). Las listas de direcciones además proporcionan un mecanismo para crear particiones de objetos habilitados para correo de Active Directory a fin de ayudar a grupos de usuarios específicos.

Para conocer otras tareas de administración relacionadas con las listas de direcciones, consulte [Procedimientos de la lista de direcciones](address-list-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Listas de direcciones" en el tema [Permisos de libreta de direcciones y dirección de correo electrónico](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Usar el EAC para crear una lista de direcciones

1.  Vaya a **Organización** \> **Listas de direcciones** y, a continuación, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

2.  En **Lista de direcciones**, escriba un nombre y especifique los tipos de destinatarios que desea incluir en la lista.

3.  De manera predeterminada, Exchange crea listas de direcciones que contienen todos los miembros de su organización. Para crear una lista de direcciones personalizada única, haga clic en **Agregar una regla**.
    

    > [!IMPORTANT]
    > Si no agrega una regla, creará una lista de direcciones redundante con una de las listas de direcciones predeterminadas.



4.  En la lista, seleccione una opción de filtrado (por ejemplo, **Atributo personalizado 1**).

5.  En **Especificar palabras o frases**, escriba las palabras o frases que desea usar para el filtro, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") y, a continuación, haga clic en **Aceptar**.
    
    Para seguir agregando varias frases o palabras, repita el paso 4. El filtro es una declaración **OR** booleana. Por ejemplo, puede crear un filtro que aplicará la lista de direcciones a usuarios cuyo Atributo personalizado 1 sea igual a **Oregon**, **Idaho** o **Washington**.

6.  (Opcional) Haga clic en **Agregar una regla** nuevamente para agregar filtros adicionales. Los filtros adicionales crean una declaración **And** booleana. Cuantos más filtros agregue, menor será la cantidad de usuarios a quienes se aplicará la lista de direcciones.

7.  Haga clic en **Vista previa de destinatarios incluidos en la lista de direcciones** para ver los destinatarios a quienes se aplicará esta lista de direcciones.

8.  Haga clic en **Guardar**.

9.  Se mostrará una advertencia que indicará que la lista de direcciones no se aplicará hasta que la actualice. Según el tamaño de su organización y de los filtros que agregó a la lista de direcciones, algunas listas de direcciones pueden contener miles o decenas de miles de destinatarios. La actualización de las listas de direcciones puede afectar los recursos; por lo tanto, posiblemente desee actualizar la dirección durante horas de poca actividad.
    
    Para obtener detalles sobre cómo actualizar una lista de direcciones, consulte [Actualizar una lista de direcciones](update-an-address-list-exchange-2013-help.md).

## Uso del Shell para crear una lista de direcciones

En este ejemplo, se crea la lista de direcciones MyAddressList usando el parámetro *RecipientFilter*; la lista incluye destinatarios que son usuarios de buzones de correo y tienen `StateOrProvince` establecido en `Washington` u `Oregon`.
```powershell
    New-AddressList -Name MyAddressList -RecipientFilter {((RecipientType -eq 'UserMailbox') -and ((StateOrProvince -eq 'Washington') -or (StateOrProvince -eq 'Oregon')))}
```

En este ejemplo se crea la lista de direcciones secundaria denominada "Building 34 Meeting Rooms" en el contenedor principal "All Rooms" usando condiciones integradas.
```powershell
    New-AddressList -Name "Building 34 Meeting Rooms" -Container "\All Rooms" -IncludedRecipients Resources -ConditionalCustomAttribute1 "Building 34"
```
Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-AddressList](https://technet.microsoft.com/es-es/library/aa996912\(v=exchg.150\)).

