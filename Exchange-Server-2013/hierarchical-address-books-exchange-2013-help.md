---
title: 'Libretas de direcciones jerárquicas: Exchange 2013 Help'
TOCTitle: Libretas de direcciones jerárquicas
ms:assetid: a1d277a0-5437-40af-aade-e4730a0d1308
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ff629379(v=EXCHG.150)
ms:contentKeyID: 49895806
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Libretas de direcciones jerárquicas

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-03-26_

La libreta jerárquica de direcciones (HAB) permite a los usuarios finales buscar destinatarios en su libreta de direcciones usando una jerarquía organizativa. Normalmente, los usuarios están limitados a la lista global de direcciones (GAL) y sus propiedades de destinatario, y la estructura de la GAL no suele reflejar de forma precisa las relaciones de administración y antigüedad de los destinatarios de la organización. Poder personalizar una HAB que asigne a la organización una estructura empresarial exclusiva dota a los usuarios de un método eficiente para buscar destinatarios internos.

## Uso de libretas jerárquicas de direcciones

En una libreta jerárquica de direcciones, la organización raíz (por ejemplo, Contoso, Ltd) se utiliza como nivel superior. Debajo de este nivel superior, puede agregar varios niveles subordinados para crear una HAB segmentada por división, departamento o cualquier otro nivel organizativo que especifique. La figura siguiente muestra una libreta jerárquica de direcciones de Contoso, Ltd con esta estructura:

  - El nivel superior representa la organización raíz, Contoso, Ltd.

  - Los segundos niveles inferiores representan las divisiones de negocios de Contoso, Ltd: Corporate Office, Product Support Organization y Sales & Marketing Organization.

  - Los terceros niveles inferiores representan los departamentos en la división Corporate Office: Human Resources, Accounting Group y Administration Group.

**HAB de ejemplo para Contoso, Ltd**

![Cuadro de diálogo de libreta de direcciones jerárquica](images/Ff607473.d8cc782f-61cd-44c4-9c74-432ebea0c3db(EXCHG.150).gif "Cuadro de diálogo de libreta de direcciones jerárquica")

El parámetro *SeniorityIndex* permite proporcionar un nivel adicional de estructura jerárquica. Al crear una libreta jerárquica de direcciones, utilice el parámetro *SeniorityIndex* para clasificar destinatarios individuales o grupos organizativos de forma jerárquica dentro de estos niveles organizativos. Esta clasificación determina el orden en que los destinatarios o los grupos aparecen en la libreta jerárquica de direcciones. Así, en el ejemplo anterior, el parámetro *SeniorityIndex* de los destinatarios de la división Corporate Office se establece de la manera siguiente:

  - `100` para David Hamilton

  - `50` para Rajesh M. Patel

  - `25` para Amy Alberts


> [!NOTE]
> Si el parámetro <EM>SeniorityIndex</EM> no está configurado o es igual para dos o más usuarios, la HAB usa el parámetro <EM>PhoneticDisplayName</EM> para clasificar los usuarios en orden alfabético ascendente. Si el parámetro <EM>PhoneticDisplayName</EM> no está configurado, la HAB usa el parámetro <EM>DisplayName</EM> para clasificar los usuarios en orden alfabético ascendente.



## Configuración de libretas jerárquica de direcciones

En [Habilitar o deshabilitar libretas jerárquicas de direcciones](enable-or-disable-hierarchical-address-books-exchange-2013-help.md) se proporcionan instrucciones precisas para crear libretas jerárquica de direcciones. Los pasos generales son los siguientes:

1.  Cree un grupo de distribución que se usará para la organización raíz (nivel superior). Si lo desea, use una unidad organizativa ya creada del bosque de Exchange para el grupo de distribución.

2.  Cree grupos de distribución para los niveles subordinados y desígnelos miembros de la HAB. Modifique el parámetro *SeniorityIndex* de estos grupos para que aparezcan en el orden jerárquico correcto dentro de la organización raíz.

3.  Agregue miembros de la organización. Modifique el parámetro *SeniorityIndex* de estos miembros para que aparezcan en el orden jerárquico correcto dentro de los niveles subordinados.

4.  Para obtener acceso, use el parámetro *PhoneticDisplayName*, que especifica la pronunciación del parámetro *DisplayName*.

