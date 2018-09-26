---
title: 'Importar o exportar certificados para mensajería unificada: Exchange 2013 Help'
TOCTitle: Importar o exportar certificados para mensajería unificada
ms:assetid: ee688c33-2e08-47e7-95fc-04ba10238341
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn205143(v=EXCHG.150)
ms:contentKeyID: 54652460
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Importar o exportar certificados para mensajería unificada

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-12-18_

Puede usar el EAC o el Shell para importar o exportar certificados comerciales autofirmados, de infraestructura de clave pública (PKI) internos o de terceros. Para la mensajería unificada (UM), puede utilizar uno de estos certificados para el servicio de mensajería unificada de Microsoft Exchange y el servicio de enrutamiento de llamadas de mensajería unificada de Microsoft Exchange. Puede utilizar el mismo certificado para ambos servicios, o bien un certificado distinto para cada uno.

Importar certificados para Exchange puede ser útil cuando desee:

  - Importar un certificado que se exportó a un archivo.

  - Importar un archivo de certificado PKI que se generó mediante una entidad de certificación interna.

  - Importar un certificado comercial de terceros.

Exportar un certificado existente del almacén de certificados del servidor Exchange local puede ser útil cuando desee:

  - Exportarlo de modo que se pueda importar en otro servidor Exchange.

  - Exportarlo de modo que se pueda importar en una puerta de enlace VoIP, IP PBX o PBX con SIP habilitado.

  - Exportarlo de modo que se pueda hacer una copia de seguridad del certificado y de su clave privada.

Para otras tareas de administración relacionadas con la administración de certificados para la mensajería unificada, consulte [Implementación de certificados para los procedimientos de mensajería unificada](deploying-certificates-for-um-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Administración de certificados" en el tema [Permisos de infraestructura de la Shell y de Exchange](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md) y entrada "Servicio de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md). También debe iniciar sesión con una cuenta que pertenezca al grupo de administradores locales del equipo.

  - Antes de exportar un certificado, use el cmdlet **Get-ExchangeCertificate** para comprobar que el atributo *PrivateKeyExportable* del certificado está definido en `$true`.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para exportar un certificado

1.  En el EAC, haga clic en **Servidores** \> **Certificados** \> **Más opciones**![Icono Más opciones](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icono Más opciones") y, a continuación, haga clic en **Exportar certificado de Exchange**.

2.  En la página **Exportar certificado de Exchange**, en el cuadro **Archivo para exportar a**, escriba el nombre del archivo de certificado.

3.  En el cuadro **Contraseña**, escriba la contraseña que quiera utilizar para proteger la clave privada y, a continuación, haga clic en **Aceptar**.

## Usar el Shell para exportar un certificado

Este ejemplo exporta el certificado con la huella digital A36DE2B9B62980A717EBD0C3052F5F0B08FBFFCC a un archivo después de pedirle un nombre de usuario y una contraseña.

  ```powershell
  $file = Export-ExchangeCertificate -Thumbprint A36DE2B9B62980A717EBD0C3052F5F0B08FBFFCC -BinaryEncoded:$true -Password (Get-Credential).password
  ```

En este ejemplo se realiza lo siguiente:

1.  Se utiliza el cmdlet **Get-ExchangeCertificate** para encontrar el certificado que desea exportar.

2.  Se utiliza el cmdlet **Export-ExchangeCertificate** para establecer la contraseña para el certificado.

3.  Transforma el certificado en un archivo una vez especificados el nombre de usuario y la contraseña.

<!-- end list -->
  
  ```powershell
  $file = Get-ExchangeCertificate -DomainName umcorp.northwindtraders.com | Export-ExchangeCertificate -BinaryEncoded:$true -Password (Get-Credential).password
  ```

  ```powershell
    Set-Content -Path "d:\umcerts\selfsigned.pfx" -Value $file.FileData =Encoding Byte
  ```
  
## Usar el EAC para importar un certificado

1.  En el EAC, haga clic en **Servidores** \> **Certificados** \> **Más opciones**![Icono Más opciones](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icono Más opciones") y, a continuación, haga clic en **Importar certificado de Exchange**.

2.  En la página **Importar certificado de Exchange**, en el cuadro **Archivo para importar a**, escriba la ruta de carpeta compartida y el nombre del archivo de certificado. Si el certificado está protegido con una contraseña, escríbala en el cuadro **Contraseña** y, a continuación, haga clic en **Siguiente**.

3.  Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para seleccionar los servidores a los cuales desea aplicar el certificado y, a continuación, haga clic en **Aceptar**. Si desea eliminar un servidor de la vista de lista, haga clic en **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar") y, a continuación, en **Finalizar**.

## Usar el Shell para importar un certificado

Este ejemplo importa un certificado del archivo de certificado d:\\certificates\\exchange\\SelfSignedUMCert.pfx una vez especificados el nombre de usuario y la contraseña.

  ```powershell
  Import-ExchangeCertificate -FileData ([Byte[]]$(Get-Content -Path d:\certificates\exchange\SelfSignedUMCert.pfx -Encoding Byte -ReadCount 0)) -Password:(Get-Credential).password
  ```

