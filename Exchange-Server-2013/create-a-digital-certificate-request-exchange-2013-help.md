---
title: 'Crear una solicitud de certificado digital: Exchange 2013 Help'
TOCTitle: Crear una solicitud de certificado digital
ms:assetid: efb00de7-070b-46bf-a2fc-00d07ae085c1
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb125165(v=EXCHG.150)
ms:contentKeyID: 52062075
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Crear una solicitud de certificado digital

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2013-02-21_

En Exchange Server 2013, puede administrar certificados con el EAC o el Shell. El EAC incluye una nueva interfaz de usuario de administración de certificados. A través de esta nueva interfaz de usuario, puede crear un certificado nuevo, editar un certificado existente o quitar un certificado.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 10 minutos más el tiempo de respuesta de la entidad de certificación.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Seguridad del servidor de acceso de clientes" en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para crear una nueva solicitud de certificado

1.  En el EAC, vaya a **Servidores** \> **Certificados**.

2.  En la lista **Seleccione el servidor**, seleccione el servidor para el cual desee crear un certificado y, a continuación, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

3.  En el Asistente para **nuevo certificado de Exchange**, seleccione **Crear una solicitud para un certificado desde una entidad de certificación** o **Crear un certificado autofirmado** y, a continuación, seleccione **Siguiente**.

4.  Escriba un nombre descriptivo para el certificado y seleccione **Siguiente**.

5.  Si no seleccionó un certificado autofirmado y desea un certificado comodín, active la casilla **Solicitar un certificado comodín**, escriba el dominio raíz, por ejemplo, \*.contoso.com, y, a continuación, seleccione **Siguiente**. Si ha elegido un certificado autofirmado, omita este paso.

6.  Seleccione los servidores a los cuales desee aplicar este certificado y seleccione **Siguiente**.

7.  Especifique los dominios que desee incluir en el certificado y, a continuación, seleccione **Siguiente**.

8.  Compruebe que los dominios incluidos sean correctos. Si ha elegido un certificado autofirmado, seleccione **Finalizar**. De lo contrario, seleccione **Siguiente**.

9.  Escriba el nombre de la organización, el nombre del departamento, la ciudad o localidad, el estado o provincia, el país o región y, a continuación, seleccione **Siguiente**.

10. Especifique una ubicación para guardar la solicitud de certificado y seleccione **Finalizar**.

Si no seleccionó un certificado autofirmado, deberá enviar el archivo de solicitud de certificado a la entidad de certificación para su procesamiento.

## Usar el Shell para crear una nueva solicitud de certificado

Ejecute los siguientes comandos.

    $reqfile = New-ExchangeCertificate -GenerateRequest -SubjectName "C=US,o=Contoso,cn=contosotocert" -DomainName "contoso.com" -PrivateKeyExportable $true

    $reqfile | out-file c:\certreq.txt

## ¿Cómo saber si el proceso se ha completado correctamente?

Si creó un certificado autofirmado, el certificado creado recientemente aparecerá en la interfaz de usuario de administración de certificados. Si creó una solicitud de certificado a partir de una entidad de certificación, el archivo de solicitud de certificado estará en la ubicación especificada. Envíe este archivo a la entidad de certificación.

