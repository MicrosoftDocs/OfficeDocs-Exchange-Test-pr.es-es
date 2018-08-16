---
title: 'Exportar tipo información confidencial DLP de Exchange 2013 Exchange 2013 Help'
TOCTitle: Exportar tipos de información confidencial de DLP desde Exchange
ms:assetid: 8f02fbc2-dd1c-4276-be1a-517a43fe39b2
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn479225(v=EXCHG.150)
ms:contentKeyID: 59637135
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exportar tipos de información confidencial de DLP desde Exchange 2013

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2016-05-04_

Puede ver o cambiar los detalles de las directivas DLP sin utilizar el Centro de administración de Exchange (CEF) o cmdlets Shell de administración de Exchange exportar las directivas, guardarlos como un archivo XML y modificando el archivo XML. Normalmente, a continuación, podría importar el archivo XML en Exchange. De esta forma, las directivas pueden editarse independiente de Exchange. Sin embargo, deben cumplir los requisitos de formato específico, que también se conoce como un esquema XML para funcionar correctamente.

Para otras tareas de administración relacionadas con DLP, consulte [Administrar directivas de DLP](manage-dlp-policies-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 15 minutos

  - entrada Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el "Prevención de pérdida de datos (DLP)" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué quiere hacer?

El EAC no ofrece una manera de exportar directivas o plantillas DLP a un archivo externo. Use el Shell de administración de Exchange para realizar esta tarea.

## Utilice la Shell de administración de Exchange para exportar los tipos de información confidencial de DLP

En este ejemplo se exportan todos los tipos de información confidencial de DLP, junto con sus atributos, a un archivo XML en la ruta C:\\Mis documentos\\exportedInformationTypes.xml. Le recomendamos hacer una copia de seguridad de su colección de tipos de información confidencial de DLP actual. Una manera de hacerlo es exportar un archivo XML e inmediatamente copiarlo y cambiar el nombre del mismo.

1.  Abra el Shell de administración de Exchange.

2.  Escriba **Get-ClassificationRuleCollection** y los tipos de información confidencial de su organización se mostrarán en pantalla. Si no ha creado sus propios tipos de información confidencial, solo verá la colección de tipos de información integrados predeterminados, con la etiqueta "Paquete de reglas de Microsoft".

3.  Almacene los tipos de información confidencial en una variable; para ello, escriba **$ruleCollections = Get-ClassificationRuleCollection**.

4.  Ahora, escriba **Set-Content -path "C:\\My Documents\\exportedRules.xml" -Encoding Byte -Value $ruleCollections.SerializedClassificationRuleCollection** para crear un archivo XML con formato con todos esos datos.

Ya puede editar el archivo XML para ajustar las directivas según sea necesario. Para obtener información sobre cómo personalizar los tipos de información confidencial integrados, consulte [Personalizar los tipos de información confidencial de DLP integrados](customize-the-built-in-dlp-sensitive-information-types-exchange-2013-help.md). Para obtener información sobre cómo importar de nuevo las directivas a Exchange, consulte [Importar una plantilla de directiva DLP personalizada desde un archivo](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md).

## Más información

[Qué buscan los tipos de información confidencial de Exchange](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

[Personalizar los tipos de información confidencial de DLP integrados](customize-the-built-in-dlp-sensitive-information-types-exchange-2013-help.md)

[Importar una plantilla de directiva DLP personalizada desde un archivo](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

