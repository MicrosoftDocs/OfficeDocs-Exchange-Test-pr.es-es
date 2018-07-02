---
title: 'Habilitar o deshabilitar libretas jerárquicas de direcciones: Exchange 2013 Help'
TOCTitle: Habilitar o deshabilitar libretas jerárquicas de direcciones
ms:assetid: b4c3a175-ce5e-4bfb-a4a0-92d25f3644b3
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ff607473(v=EXCHG.150)
ms:contentKeyID: 49895853
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Habilitar o deshabilitar libretas jerárquicas de direcciones

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Puede configurar una libreta jerárquica de direcciones (HAB), que es una característica disponible para usuarios finales de Microsoft Outlook 2010 o posterior. Con una HAB, los usuarios pueden buscar destinatarios en su organización de Exchange usando una jerarquía organizativa basada en la estructura de antigüedad o administración. Para obtener más información sobre las HAB, vea [Libretas de direcciones jerárquicas](hierarchical-address-books-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 1 hora.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Grupos de distribución" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - No puede usar el Centro de Administración de Exchange (EAC) para realizar este procedimiento. Debe usar el Shell.

  - Antes de comenzar, lea el tema [Libretas de direcciones jerárquicas](hierarchical-address-books-exchange-2013-help.md). Debe comprender si una HAB es apropiada para la organización de Exchange.

  - Comprenda cómo se configuran las unidades organizativas (OU), los grupos, los usuarios y los contactos en la organización de Exchange.

  - Comprenda los cmdlets y parámetros asociados de la siguiente tabla, necesarios para configurar una HAB.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Cmdlet</th>
    <th>Parámetro</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><a href="https://technet.microsoft.com/es-es/library/aa997443(v=exchg.150)">Set-OrganizationConfig</a></p></td>
    <td><p><em>HierarchicalAddressBookRoot</em></p></td>
    </tr>
    <tr class="even">
    <td><p><a href="https://technet.microsoft.com/es-es/library/bb123770(v=exchg.150)">Set-Group</a></p></td>
    <td><p><em>IsHierarchicalGroup</em></p>
    <p><em>SeniorityIndex</em></p>
    <p><em>PhoneticDisplayName</em></p></td>
    </tr>
    <tr class="odd">
    <td><p><a href="https://technet.microsoft.com/es-es/library/aa998221(v=exchg.150)">Set-User</a></p></td>
    <td><p><em>SeniorityIndex</em></p>
    <p><em>PhoneticDisplayName</em></p></td>
    </tr>
    <tr class="even">
    <td><p><a href="https://technet.microsoft.com/es-es/library/bb124535(v=exchg.150)">Set-Contact</a></p></td>
    <td><p><em>SeniorityIndex</em></p>
    <p><em>PhoneticDisplayName</em></p></td>
    </tr>
    </tbody>
    </table>


  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Usar el Shell para habilitar una HAB


> [!NOTE]
> A pesar de que no puede usar la EAC para habilitar una HAB, después de que esté habilitado puede usar la EAC para administrar la pertenencia de los grupos en la jerarquía organizacional.



En este ejemplo se creará una OU llamada HAB para la HAB. El nombre del dominio de la organización es Contoso-dom y el nombre de la organización de nivel superior de la jerarquía será Contoso, Ltd (la *organización raíz*). Se crearán grupos subordinados llamados Corporate Office, Product Support Organization y Sales & Marketing Organization como organizaciones subordinadas a Contoso,Ltd. Además, se crearán los grupos Human Resources, Accounting Group y Administration Group como organizaciones subordinadas a Corporate Office.

Para obtener información detallada acerca de la creación de grupos de distribución, vea [Crear y administrar grupos de distribución](create-and-manage-distribution-groups-exchange-2013-help.md).

1.  Cree una unidad organizativa denominada HAB en la organización Contoso. Puede usar Usuarios y equipos de Active Directory o escribir lo siguiente en una ventana de símbolo del sistema.
    

    > [!NOTE]
    > Como alternativa, puede utilizar una unidad organizativa existente en su bosque de Exchange.

    
        dsadd ou "OU=HAB,DC=Contoso-dom,DC=Contoso,DC=com"
    

    > [!NOTE]
    > Para obtener más detalles, vea <A href="https://go.microsoft.com/fwlink/p/?linkid=198986">Crear una nueva unidad organizativa</A>.



2.  Cree el grupo de distribución raíz Contoso,Ltd para la HAB.
    

    > [!NOTE]
    > Para este tema se ofrece el ejemplo del Shell. Sin embargo, también puede usar la EAC para crear un grupo de distribución. Para obtener información más detallada, vea <A href="create-and-manage-distribution-groups-exchange-2013-help.md">Crear y administrar grupos de distribución</A>.

    
        New-DistributionGroup -Name "Contoso,Ltd" -DisplayName "Contoso,Ltd" -Alias "ContosoRoot" -OrganizationalUnit "Contoso-dom.Contoso.com/HAB" -SamAccountName "ContosoRoot" -Type "Distribution"

3.  Designe Contoso,Ltd como organización raíz de la HAB.
    
        Set-OrganizationConfig -HierarchicalAddressBookRoot "Contoso,Ltd"

4.  Cree grupos de distribución para los demás niveles de la HAB. En este ejemplo, crearía los siguientes grupos: Corporate Office, Product Support Organization, Sales & Marketing Organization, Human Resources, Accounting Group y Administration Group. En este ejemplo se crea el grupo de distribución Corporate Office.
    

    > [!NOTE]
    > Para este tema se ofrece el ejemplo del Shell. Sin embargo, también puede usar la EAC para crear grupos de distribución. Para obtener información más detallada, vea <A href="create-and-manage-distribution-groups-exchange-2013-help.md">Crear y administrar grupos de distribución</A>.

    
        New-DistributionGroup -Name "Corporate Office" -DisplayName "Corporate Office" -Alias "CorporateOffice" -OrganizationalUnit "Contoso-dom.Contoso.com/HAB" -SamAccountName "CorporateOffice" -Type "Distribution"

5.  Designe cada uno de los grupos como miembros de la HAB. En este ejemplo, designaría los siguientes grupos como grupos jerárquicos: Contoso,Ltd, Corporate Office, Product Support Organization, Sales & Marketing Organization, Human Resources, Accounting Group y Administration Group. En este ejemplo se designa el grupo de distribución Contoso,Ltd como miembro de la HAB.
    
        Set-Group -Identity "Contoso,Ltd" -IsHierarchicalGroup $true

6.  Agregue cada uno de los grupos subordinados como miembros de la organización raíz. En este ejemplo, los grupos de distribución Corporate Office, Product Support Organization y Sales & Marketing Organization se agregan como miembros de la organización raíz Contoso,Ltd en la HAB. En este ejemplo se agrega el grupo de distribución Corporate Office como miembro del grupo de distribución raíz Contoso,Ltd.
    

    > [!NOTE]
    > En este ejemplo se utilizan los alias de los grupos de distribución.

    
        Add-DistributionGroupMember -Identity "ContosoRoot" -Member "CorporateOffice"

7.  Agregue cada uno de los grupos subordinados al grupo de distribución Corporate Office como miembros del grupo. En este ejemplo, los grupos de distribución Human Resources, Accounting Group y Administration Group se agregan como miembros del grupo de distribución Corporate Office. En este ejemplo se agrega el grupo de distribución Human Resources como miembro del grupo de distribución Corporate Office.
    

    > [!NOTE]
    > En este ejemplo se usan los alias de los grupos de distribución y se supone que el alias del grupo de distribución Human Resources es HumanResources.

    
        Add-DistributionGroupMember -Identity "CorporateOffice" -Member "HumanResources"

8.  Agregue usuarios a los grupos de la HAB. En este ejemplo, David Hamilton (dirección SMTP DHamilton@contoso.com) es un usuario existente de la OU Contoso-dom.Contoso.com/Users y se agregará al grupo Corporate Office. Repita este paso para agregar otros usuarios a grupos de la HAB.
    
        Add-DistributionGroupMember -Identity "CorporateOffice" -Member "DHamilton"

9.  Establezca el parámetro *SeniorityIndex* para los grupos de la HAB. En este ejemplo, el grupo Corporate Office contiene tres grupos subordinados: Human Resources, Accounting Group y Administration Group. En lugar de ordenar la lista de grupos por orden alfabético ascendente, que es el formato predeterminado, la clasificación preferida será Human Resources (*SeniorityIndex* = 100), Accounting Group (*SeniorityIndex* = 50) y, por último, Administration Group (*SeniorityIndex* = 25). En este ejemplo se establece el parámetro *SeniorityIndex* del grupo Human Resources en 100.
    
        Set-Group -Identity "Human Resources" -SeniorityIndex 100
    

    > [!NOTE]
    > El parámetro <EM>SeniorityIndex</EM> es un valor numérico usado para clasificar grupos o usuarios en orden numérico descendente en una HAB. Si el parámetro <EM>SeniorityIndex</EM> no está configurado o es igual para dos o más usuarios, la HAB usa el parámetro <EM>PhoneticDisplayName</EM> para clasificar los usuarios en orden alfabético ascendente. Si el parámetro <EM>PhoneticDisplayName</EM> no está configurado, la HAB usa el parámetro <EM>DisplayName</EM> para clasificar los usuarios en orden alfabético ascendente.



10. Establezca el parámetro *SeniorityIndex* para los usuarios de los grupos HAB. En este ejemplo, el grupo Corporate Office contiene tres usuarios: Amy Alberts, David Hamilton y Rajesh M. Patel. En vez de ordenar los usuarios por orden alfabético ascendente, la clasificación preferida será David Hamilton (*SeniorityIndex* = 100), Rajesh M. Patel (*SeniorityIndex* = 50) y, por último, Amy Alberts (*SeniorityIndex* = 25). En este ejemplo se establece el parámetro *SeniorityIndex* del usuario David Hamilton en 100.
    
        Set-User -Identity "DHamilton@contoso.com" -SeniorityIndex 100

Después de completar los pasos anteriores, la HAB podrá verse en Outlook. Para ver la HAB, abra Outlook y haga clic en **Libreta de direcciones**. La HAB se muestra en la ficha **Organización**, como en la imagen siguiente.

**HAB de ejemplo para Contoso,Ltd**

![Cuadro de diálogo de libreta de direcciones jerárquica](images/Ff607473.d8cc782f-61cd-44c4-9c74-432ebea0c3db(EXCHG.150).gif "Cuadro de diálogo de libreta de direcciones jerárquica")

Después de crear la HAB, puede usar la EAC para administrar la pertenencia a los grupos de la jerarquía organizativa. Sin embargo, debe usar el Shell para modificar el parámetro *SeniorityIndex* de los grupos o usuarios nuevos.

Para obtener información detallada acerca de la sintaxis y los parámetros, vea estos temas:

  - [New-DistributionGroup](https://technet.microsoft.com/es-es/library/aa998856\(v=exchg.150\))

  - [Set-OrganizationConfig](https://technet.microsoft.com/es-es/library/aa997443\(v=exchg.150\))

  - [Set-Group](https://technet.microsoft.com/es-es/library/bb123770\(v=exchg.150\))

  - [Add-DistributionGroupMember](https://technet.microsoft.com/es-es/library/bb124340\(v=exchg.150\))

  - [Set-User](https://technet.microsoft.com/es-es/library/aa998221\(v=exchg.150\))

## Uso del Shell para deshabilitar una libreta de direcciones jerárquica

En este ejemplo se deshabilita la organización raíz utilizada para la HAB.

    Set-OrganizationConfig -HierarchicalAddressBookRoot $null


> [!NOTE]
> Este comando no borra la organización raíz ni los grupos subordinados usados en la estructura de la HAB y tampoco restaura los valores de <EM>SeniorityIndex</EM> de grupos o usuarios. Solo impide que la HAB se muestre en Outlook. Para volver a habilitar la HAB con la misma configuración, solo tiene que volver a habilitar la organización raíz.



Para obtener información más detallada acerca de la sintaxis y los parámetros, vea [Set-OrganizationConfig](https://technet.microsoft.com/es-es/library/aa997443\(v=exchg.150\)).

