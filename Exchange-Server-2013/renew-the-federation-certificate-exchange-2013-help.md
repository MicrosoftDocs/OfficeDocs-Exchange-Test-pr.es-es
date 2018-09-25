---
title: 'Renovar el certificado de federación: Exchange 2013 Help'
TOCTitle: Renovar el certificado de federación
ms:assetid: 0f390713-3058-44d0-9c07-3c982616e790
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Mt779252(v=EXCHG.150)
ms:contentKeyID: 74429221
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Renovar el certificado de federación

 

_**Última modificación del tema:** 2017-02-28_

En este tema, se explica cómo actualizar el certificado autofirmado de federación que se utiliza en una confianza de federación:

  - Si el certificado de la federación no ha expirado, siga los pasos de la sección Actualizar un certificado de federación operativo.

  - Si el certificado de la federación ya ha expirado, siga los pasos de la sección Reemplazar un certificado de federación expirado.

Para obtener más información acerca de las confianzas de federación y la federación, consulte [Federación](federation-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  10 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Federación y certificados" en el tema [Permisos de infraestructura de la Shell y de Exchange](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - En los procedimientos de este tema, se usa: Shell de administración de Exchange. Para obtener información sobre cómo abrir el Shell de administración de Exchange en su organización local Exchange, vea [Abrir el Shell](https://technet.microsoft.com/es-es/library/dd638134\(v=exchg.150\)).

  - Para ver si ha expirado el certificado de federación existente, ejecute el siguiente comando en el Shell de administración de Exchange:
    
    ```powershell
    Get-ExchangeCertificate -Thumbprint (Get-FederationTrust).OrgCertificate.Thumbprint | Format-Table -Auto Thumbprint,NotAfter
    ```

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!WARNING]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Actualizar un certificado de federación operativo

Si el certificado de federación no ha expirado, puede actualizar la confianza de federación existente con un nuevo certificado de federación.

## Paso 1: Crear un nuevo certificado de federación

Ejecute el comando siguiente en el Shell de administración de Exchange para crear un nuevo certificado de federación:

```powershell
$SKI = [System.Guid]::NewGuid().ToString("N"); New-ExchangeCertificate -DomainName 'Federation' -FriendlyName "Exchange Delegation Federation" -Services Federation -SubjectKeyIdentifier $SKI -PrivateKeyExportable $true
```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-ExchangeCertificate](https://technet.microsoft.com/es-es/library/aa998327\(v=exchg.150\)).

El resultado que proporciona el comando contiene el valor de huella digital del nuevo certificado. Necesitará este valor en los pasos restantes; puede copiarlo directamente desde la ventana del Shell de administración de Exchange:

1.  Haga clic con el botón derecho en cualquier parte de la ventana del Shell de administración de Exchange y seleccione **Marcar** en el cuadro que aparece.

2.  Seleccione el valor de huella digital y, a continuación, presione ENTRAR.

Para el resto de procedimientos de este tema, vamos a utilizar el valor de huella digital del certificado de federación: `6A99CED2E4F2B5BE96C5D17D662D217EF58B8F73`. El valor de huella digital de su certificado es diferente.

## Paso 2: Configurar el nuevo certificado como certificado de federación

Para usar el Shell de administración de Exchange para configurar el nuevo certificado como certificado de federación, utilice la siguiente sintaxis:

```powershell
Set-FederationTrust -Identity "Microsoft Federation Gateway" -Thumbprint <Thumbprint> -RefreshMetaData
```

En este ejemplo, se utiliza el valor de huella digital de certificado de `6A99CED2E4F2B5BE96C5D17D662D217EF58B8F73` del paso 1.

```powershell
Set-FederationTrust -Identity "Microsoft Federation Gateway" -Thumbprint 6A99CED2E4F2B5BE96C5D17D662D217EF58B8F73 -RefreshMetaData
```

Para obtener información detallada sobre la sintaxis y los parámetros, consulte [Set-FederationTrust](https://technet.microsoft.com/es-es/library/dd298034\(v=exchg.150\)).

**Nota:**  El resultado que proporciona el comando contiene una advertencia que le indica que debe actualizar el registro TXT de prueba de propiedad del dominio en DNS. Lo podrá hacer en el paso siguiente.

## Paso 3: Actualizar el registro TXT de prueba de propiedad del dominio de federación en un DNS externo

Ahora ya puede realizar este paso de manera segura, ya que el registro TXT de prueba de propiedad del dominio solo se comprueba durante la activación (paso 5). Sin embargo, después de actualizar el registro TXT y antes de continuar con el paso siguiente, debe dejar tiempo para que se propague el registro TXT actualizado (en función del período de vida o el valor TTL del registro DNS).

1.  Encontrará los valores necesarios para el registro TXT necesario ejecutando el siguiente comando en el Shell de administración de Exchange:
    
    ```powershell
    Get-FederatedDomainProof -DomainName <Domain> | Format-List Thumbprint,Proof
    ```
    
    Por ejemplo, si su dominio federado es contoso.com, ejecute el comando siguiente:
    
    ```powershell
    Get-FederatedDomainProof -DomainName contoso.com | Format-List Thumbprint,Proof
    ```
    
    El resultado del comando tiene este aspecto:
    
    ```powershell
    `Thumbprint : <new certificate thumbprint>` (por ejemplo, `6A99CED2E4F2B5BE96C5D17D662D217EF58B8F73`)

    `Proof      : <new hash text>` (por ejemplo, `znMfbkgSbOQSsWFdsW+gm3to0nZSdE3zbcPPHGVAqdgsLFGsCPuLHiyVbKoPmgyZKX90NH2g1PbCZH0YTQF6oA==`)

    `Thumbprint : <old certificate thumbprint>` (por ejemplo, `CC9BC204BB4DC60D06FC1F10F3C373DC785DA2A5`)

    `Proof      : <old hash text>` (por ejemplo, `m4gZX7OLr9iOWYJMVjEklQpoSkPb5hSbcFjD7Q3/vsqmdJ2Z+HcSt7j5pzBKFmEW2s27JYr3xsK2POzAI/8Ffw==`)
    ```
    
    Observe que el resultado del comando devuelve información para dos registros de pruebas de propiedad del dominio: uno para el nuevo certificado y otro para el certificado actual que va a reemplazar. Puede saber cuál es cuál por el valor de huella digital y por el valor de texto de hash que se ha configurado en el registro TXT de prueba de propiedad del dominio actual en su DNS externo (público).

2.  Actualice el registro TXT de prueba de propiedad del dominio de federación en su DNS externo. Las instrucciones variarán en función de su proveedor de DNS, pero puede editar el registro TXT actual para reemplazar el valor de texto de hash actual con el nuevo. Para obtener más información, consulte la sección de Exchange Online [Registros externos del Sistema de nombres de dominio para Office 365](https://go.microsoft.com/fwlink/p/?linkid=26552).

## Paso 4: Comprobar la distribución del nuevo certificado de federación a todos los servidores de Exchange

Exchange distribuye automáticamente el nuevo certificado de federación a todos los servidores, pero tenemos que comprobar la distribución antes de continuar.

Para utilizar el Shell de administración de Exchange para comprobar la distribución del nuevo certificado de federación, ejecute el siguiente comando:

```powershell
$Servers = Get-ExchangeServer; $Servers | foreach {Get-ExchangeCertificate -Server $_ | Where {$_.Services -match 'Federation'}} | Format-List Identity,Thumbprint,Services,Subject
```

**Nota:**  En Exchange 2010, el resultado del cmdlet de **Test-FederationCertificate** contiene nombres de servidor. El resultado del cmdlet en Exchange 2013 o posterior no incluye nombres de servidor.

## Paso 5: Activar el nuevo certificado de federación

Para utilizar el Shell de administración de Exchange para activar el nuevo certificado de federación, ejecute el siguiente comando:

```powershell
Set-FederationTrust -Identity "Microsoft Federation Gateway" -PublishFederationCertificate
```

Para obtener información detallada sobre la sintaxis y los parámetros, consulte [Set-FederationTrust](https://technet.microsoft.com/es-es/library/dd298034\(v=exchg.150\)).

**Nota:**  El resultado que proporciona el comando contiene una advertencia que le indica que debe actualizar el registro TXT de prueba de propiedad del dominio en DNS (lo que ya hizo en el paso 3).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que ha actualizado correctamente la confianza de federación existente con un nuevo certificado de federación, siga estos pasos:

  - En el Shell de administración de Exchange, ejecute el siguiente comando para comprobar que se está utilizando el nuevo certificado:
    
    ```powershell
    Get-FederationTrust | Format-List *priv*
    ```
    
      - La propiedad **OrgPrivCertificate** debe contener la huella digital del nuevo certificado de federación.
    
      - La propiedad **OrgPrevPrivCertificate** debe contener la huella digital del (reemplazado) certificado de federación antiguo.

  - En el Shell de administración de Exchange, reemplace *\<user's email address\>* con la dirección de correo electrónico de un usuario de su organización y ejecute el siguiente comando para comprobar que funciona la confianza de federación:
    
        Test-FederationTrust -UserIdentity <user's email address>

## Reemplazar un certificado de federación expirado

Si el certificado de federación ya ha expirado, debe quitar todos los dominios federados de la confianza de federación y, a continuación, quitar y volver a crear la confianza de federación.

1.  Si tiene varios dominios federados, deberá identificar el dominio compartido del dominio principal para quitarlo en último lugar. Para utilizar el Shell de administración de Exchange para identificar el dominio compartido principal y todos los dominios federados, ejecute el siguiente comando:
    
    ```powershell
    Get-FederatedOrganizationIdentifier | Format-List AccountNamespace,Domains
    ```
    
    El valor de la propiedad **AccountNamespace** contiene el dominio compartido principal con el formato `FYDIBOHF25SPDLT<primary shared domain>`. Por ejemplo, en el valor `FYDIBOHF25SPDLT.contoso.com`, contoso.com es el dominio compartido principal.

2.  Quite todos los dominios federados que no sean el dominio compartido principal ejecutando el siguiente comando en el Shell de administración de Exchange:
    
    ```powershell
    Remove-FederatedDomain -DomainName <domain> -Force
    ```

3.  Una vez que haya quitado el resto de dominios federados, quite el dominio compartido principal ejecutando el siguiente comando en el Shell de administración de Exchange:
    
    ```powershell
    Remove-FederatedDomain -DomainName <domain> -Force
    ```

4.  Quite la confianza de federación ejecutando el siguiente comando en el Shell de administración de Exchange:
    
    ```powershell
    Remove-FederationTrust "Microsoft Federation Gateway"
    ```

5.  Vuelva a crear la confianza de federación. Para obtener instrucciones, consulte [Crear una confianza de federación](https://technet.microsoft.com/es-es/library/dd335198\(v=exchg.150\)).

