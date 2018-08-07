---
title: 'Proteger datos formulario con huellas digitales documentos: Exchange 2013 Help'
TOCTitle: Proteger los datos de formulario con huellas digitales de documentos
ms:assetid: 110c839b-7693-42f6-aa5d-58ce64f4c357
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn635175(v=EXCHG.150)
ms:contentKeyID: 61204103
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Proteger los datos de formulario con huellas digitales de documentos

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2014-09-11_

Si su organización usa formularios para recopilar información confidencial, los usuarios podrían tratar de enviar esos formularios por correo electrónico a contactos externos, lo que supone un riesgo para la seguridad. La prevención de pérdida de datos (DLP) de Exchange le ayuda a proteger esa información mediante la detección con [Creación de huella digital de documento](overview-of-document-fingerprinting-in-exchange.md). Para usar huellas digitales de documentos, simplemente cargue un formulario en blanco, por ejemplo, un documento de propiedad intelectual, un formulario oficial u otro formulario estándar que se use en su organización. Después, agregue la huella digital de documento resultante a una regla de transporte o directiva de DLP. Aquí se muestra cómo hacerlo.

> [!VIDEO https://www.microsoft.com/es-es/videoplayer/embed/68138246-0546-46f9-8c99-cd2f0fc9b400]

## Usar el EAC para crear una huella digital de documento

![Ruta de acceso a Creación de huella digital de documento en EAC resaltada](images/Dn635175.e8562ea7-40ba-4feb-adde-2e81f029fcda(EXCHG.150).png "Ruta de acceso a Creación de huella digital de documento en EAC resaltada")

1.  En el Centro de administración de Exchange (EAC), vaya a **Administración de cumplimiento** \> **prevención de pérdida de datos**.

2.  Haga clic en **Administrar huellas digitales de documentos**.

3.  En la página de huellas digitales de documentos, haga clic en **Nuevo**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para crear una nueva huella digital de documento.

4.  Asigne a la huella digital de documento un **Nombre** y una **Descripción**. (El nombre que elija aparecerá en la lista de tipos de información confidencial).

5.  Para cargar un formulario, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

6.  Elija un formulario y haga clic en **Abrir**. (Asegúrese de que el archivo que cargue contiene texto, no esté protegido por contraseña y sea uno de los tipos admitidos en las reglas de transporte. Para obtener una lista de los tipos admitidos, consulte [Use mail flow rules to inspect message attachments in Office 365](https://technet.microsoft.com/es-es/library/jj919236\(v=exchg.150\)). De lo contrario, obtendrá un error al intentar crear la huella digital). Repita el procedimiento para otros archivos que quiera agregar a la lista de documentos para esta huella digital de documento. Si quiere, también puede agregar o quitar archivos de esta huella digital de documento más adelante.

7.  Haga clic en **Guardar**.

Ahora, la huella digital de documento forma parte de sus tipos de información confidencial y puede agregarla a una directiva de DLP o a una regla de transporte mediante la condición **Si el mensaje contiene información confidencial...**.

![Condición "Aplicar esta regla si" resaltada](images/Dn635175.9355a513-a790-48eb-a61b-575ba2ecdfa6(EXCHG.150).png "Condición \"Aplicar esta regla si\" resaltada")

Para obtener más información sobre cómo agregar reglas a una directiva de DLP, consulte la sección “Cambiar una directiva de DLP” de [Administrar directivas de DLP](manage-dlp-policies-exchange-2013-help.md), y para obtener más información sobre cómo modificar reglas de transporte, consulte [Integración de las reglas de información confidencial con las reglas de transporte](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md). Si quiere crear una nueva directiva, consulte [Crear una directiva DLP a partir de una plantilla](how-to-new-dlp-data-loss-prevention-policy-template.md).

## Usar el Shell para crear un paquete de reglas de clasificación basadas en huellas digitales de documentos


> [!TIP]
> Aunque puede crear y modificar paquetes de reglas de clasificación en el Shell, quizás le resulte más fácil crear huellas digitales de documentos en el EAC. Le recomendamos que lo intente allí antes de probar este procedimiento en el Shell.



DLP usa paquetes de reglas de clasificación para detectar contexto confidencial en los mensajes. Para crear un paquete de reglas de clasificación basadas en una huella digital de documento, use los cmdlets **New-Fingerprint** y **New-DataClassification**. Dado que los resultados de **New-Fingerprint** no se almacenan fuera de la regla de clasificación de datos, ejecute siempre **New-Fingerprint** y **New-DataClassification** o **Set-DataClassification** en la misma sesión de PowerShell. En el ejemplo siguiente se crea una huella digital de documento nueva a partir del archivo C:\\My Documents\\Contoso Employee Template.docx. La nueva huella digital se almacena como una variable, por lo que se puede utilizar con el cmdlet **New-DataClassification** en la misma sesión de PowerShell.

    $Employee_Template = Get-Content "C:\My Documents\Contoso Employee Template.docx" -Encoding byte
    $Employee_Fingerprint = New-Fingerprint -FileData $Employee_Template -Description "Contoso Employee Template"

Ahora, crearemos una nueva regla de clasificación de datos llamada "Contoso Employee Confidential" que usa la huella digital de documento del archivo C:\\My Documents\\Contoso Customer Information Form.docx.

    $Employee_Template = Get-Content "C:\My Documents\Contoso Customer Information Form.docx" -Encoding byte
    $Customer_Fingerprint = New-Fingerprint -FileData $Customer_Form -Description "Contoso Customer Information Form"
    New-DataClassification -Name "Contoso Customer Confidential" -Fingerprints $Customer_Fingerprint -Description "Message contains Contoso customer information." 

Ahora puede usar el cmdlet **Get-DataClassification** para buscar todos los paquetes de reglas de clasificación de datos de DLP y, en este ejemplo, “Contoso Customer Confidential” forma parte de la lista de paquetes de reglas de clasificación de datos.

Por último, agregue el paquete de reglas de clasificación de datos “Contoso Customer Confidential” a una directiva de DLP.

    New-TransportRule -Name "Notify :External Recipient Contoso confidential" -NotifySender NotifyOnly -Mode Enforce -SentToScope NotInOrganization -MessageContainsDataClassification @{Name=" Contoso Customer Confidential"}

El agente de DLP ahora detecta los documentos que coinciden con la huella digital de documento Contoso Customer Form.docx.

Para obtener información acerca de la sintaxis y los parámetros, consulte [New-Fingerprint](https://technet.microsoft.com/es-es/library/dn584142\(v=exchg.150\)), [New-DataClassification](https://technet.microsoft.com/es-es/library/dn584139\(v=exchg.150\)), [Set-DataClassification](https://technet.microsoft.com/es-es/library/dn584141\(v=exchg.150\)) y [Get-DataClassification](https://technet.microsoft.com/es-es/library/jj215720\(v=exchg.150\)).

## Más información

[Creación de huella digital de documento](overview-of-document-fingerprinting-in-exchange.md)

[Administrar directivas de DLP](manage-dlp-policies-exchange-2013-help.md)

[Integración de las reglas de información confidencial con las reglas de transporte](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)

