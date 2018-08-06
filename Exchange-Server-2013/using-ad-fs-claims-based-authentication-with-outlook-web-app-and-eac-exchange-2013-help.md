---
title: 'Uso autenticación basada en notificaciones de AD FS con Outlook Web App y EAC | Microsoft Docs'
TOCTitle: Usar la autenticación basada en notificaciones de AD FS con Outlook Web App y EAC
ms:assetid: 919a9bfb-c6df-490a-b2c4-51796b0f0596
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn635116(v=EXCHG.150)
ms:contentKeyID: 61204110
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Usar la autenticación basada en notificaciones de AD FS con Outlook Web App y EAC

 

_**Se aplica a:** Exchange Server 2013 SP1_

_**Última modificación del tema:** 2017-04-14_

**Resumen:** 

En el caso de las implementaciones locales de Exchange 2013 Service Pack 1 (SP1), si instala y configura Servicios de federación de Active Directory (AD FS), podrá usar la autenticación basada en notificaciones de AD FS para conectarse a Outlook Web App y EAC. Puede integrar AD FS y la autenticación basada en notificaciones con Exchange 2013 SP1, y su uso reemplaza los métodos de autenticación convencionales, incluidos los siguientes:

  - Autenticación de Windows

  - Autenticación de formularios

  - Autenticación implícita

  - Autenticación básica

  - Autenticación de certificados de cliente de Active Directory

La autenticación es el proceso de confirmación de la identidad de un usuario. La autenticación valida que el usuario sea quien dice ser. La identidad basada en notificaciones es otro enfoque para la autenticación. La autenticación basada en notificaciones quita de la aplicación la administración de la autenticación, en este caso Outlook Web App y EAC, para facilitar la administración de cuentas mediante una autenticación centralizada. Outlook Web App y EAC no son responsables de autenticar usuarios, de almacenar las cuentas de usuario y las contraseñas, de buscar información sobre la identidad del usuario ni de integrarse con otros sistemas de identidad. La autenticación centralizada permite actualizarse fácilmente a otros métodos de autenticación en el futuro.


> [!NOTE]
> OWA para dispositivos no admite la autenticación basada en notificaciones de AD FS.



En la tabla siguiente se resumen las diversas versiones de AD FS que se pueden usar.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Versión de Windows Server</th>
<th>Instalación</th>
<th>Versión de AD FS</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Server 2008 R2</p></td>
<td><p><strong>Descargar e instalar</strong> AD FS 2.0, que es un complemento de Windows.</p></td>
<td><p>AD FS 2.0</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2012</p></td>
<td><p>Instale el rol de servidor de AD FS <strong>integrado</strong>.</p></td>
<td><p>AD FS 2.1</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2012 R2</p></td>
<td><p>Instale el rol de servidor de AD FS <strong>integrado</strong>.</p></td>
<td><p>AD FS 3.0</p></td>
</tr>
</tbody>
</table>


Las tareas que realizará aquí se basan en Windows Server 2012 R2, que incluye el servicio de rol AD FS.

**Introducción a los pasos necesarios**

Step 1 - Review the certificate requirements for AD FS

Step 2 - Install and configure Active Directory Federation Services (AD FS)

Paso 3: Crear una relación de confianza para usuario autenticado y reglas personalizadas para las notificaciones para Outlook Web App y EAC

Paso 4: Instalar el servicio de rol Proxy de aplicación web (opcional)

Paso 5: Configurar el servicio de rol Proxy de aplicación web (opcional)

Paso 6: Publicar Outlook Web App y EAC con Proxy de aplicación web (opcional)

Paso 7: Configurar Exchange 2013 para usar la autenticación de AD FS

Paso 8: Habilitar la autenticación de AD FS en los directorios virtuales de OWA y ECP

Paso 9: Reiniciar o reciclar Internet Information Services (IIS)

Paso 10: Probar las notificaciones de AD FS para Outlook Web App y EAC

Additional information you might want to know

## ¿Qué necesito saber antes de comenzar?

  - Como mínimo, debe instalar varios servidores de Windows Server 2012 R2 diferentes: uno como controlador de dominio que usa Servicios de dominio de Active Directory (AD DS), un servidor de Exchange 2013, un servidor de Proxy de aplicación web y un servidor de Servicios de federación de Active Directory (AD FS) . Compruebe que están instaladas todas las actualizaciones.

  - Instale AD DS en el número de servidores de Windows Server 2012 R2 apropiado para su organización. También puede usar **Notificaciones** en **Administrador del servidor**\>**Panel** para **Promover este servidor a controlador de dominio**.

  - Instale el número de servidores de acceso de cliente y servidores de buzones de correo apropiado para su organización. Compruebe que están instaladas todas las actualizaciones, incluido SP1, en todos los servidores de Exchange 2013 de su organización. Para descargar SP1, vea [Actualizaciones para Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md).

  - Para implementar Proxy de aplicación web en un servidor se necesitan permisos de administrador local. Debe implementar AD FS en un servidor que ejecute Windows Server 2012 R2 en su organización antes de poder implementar Proxy de aplicación web.

  - Instale y configure el rol AD FS y cree las relaciones de confianza para usuarios autenticados y las reglas de notificaciones en Windows Server 2012 R2. Para ello, debe iniciar sesión con una cuenta de usuario que sea miembro del grupo Admins. del dominio, del grupo Administradores de empresa o del grupo Administradores local.

  - Determine los permisos necesarios para Exchange 2013; para ello, vea [Permisos de características](feature-permissions-exchange-2013-help.md).

  - Necesita que le asignen permisos para administrar Outlook Web App. Para ver los permisos que necesita, vea la entrada "Permisos de Outlook Web App" en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Necesita que le asignen permisos para administrar EAC. Para ver qué permisos necesita, vea la entrada "Conectividad del Centro de administración de Exchange" en el tema [Permisos de infraestructura de la Shell y de Exchange](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Quizás solo pueda usar el Shell para realizar algunos procedimientos. Para obtener información sobre cómo abrir el Shell en su organización de Exchange local, vea [Abrir el Shell](https://technet.microsoft.com/es-es/library/dd638134\(v=exchg.150\)).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Paso 1: Revisar los requisitos de certificado para AD FS

Los certificados juegan un papel fundamental en la protección de las comunicaciones entre los servidores de Exchange 2013 SP1, los clientes web como Outlook Web App y EAC, los servidores de Windows Server 2012 R2, incluidos los servidores de Servicios de federación de Active Directory (AD FS), y los servidores de Proxy de aplicación web. Los requisitos de certificados varían según esté configurando un servidor de AD FS, un servidor proxy de AD FS o un servidor de Proxy de aplicación web. Los certificados que se usan para los servicios de AD FS, incluidos los certificados de SSL y de firma de tokens, deben importarse al almacén de entidades de certificación raíz de confianza en todos los servidores de Exchange, AD FS y Proxy de aplicación web. La huella digital del certificado que se importe también se usa en los servidores de Exchange 2013 SP1 cuando se usa el cmdlet [Set-OrganizationConfig](https://technet.microsoft.com/es-es/library/aa997443\(v=exchg.150\)).

En los diseños de AD FS, se deben usar varios certificados para proteger la comunicación entre los usuarios de Internet y los servidores de AD FS. Cada servidor de federación debe tener un certificado de comunicaciones de servicio o un certificado de Capa de sockets seguros (SSL) y un certificado de firma de tokens para que los servidores de AD FS, los controladores de dominio de Active Directory y los servidores de Exchange 2013 puedan comunicarse y autenticarse. En función de sus requisitos de seguridad y presupuesto, considere detenidamente cuál de sus certificados se obtendrá mediante una entidad de certificación pública o una entidad de certificación empresarial. Si quiere instalar y configurar una entidad de certificación raíz de la empresa o una entidad de certificación subordinada, puede usar los Servicios de certificados de Active Directory (AD CS). Si quiere obtener más información sobre AD CS, vea [Información general de Servicios de certificados de Active Directory](https://go.microsoft.com/fwlink/?linkid=392697).

Aunque AD FS no necesita que los certificados sean emitidos por una entidad de certificación, el certificado SSL (que también se usa como certificado de comunicaciones de servicio de forma predeterminada) debe ser de confianza para los clientes de AD FS. Le recomendamos que no use certificados autofirmados. Los servicios de federación usan un certificado SSL para proteger el tráfico de los servicios web para la comunicación SSL con los clientes web y con los servidores proxy del servidor de federación. Como el certificado SSL debe ser de confianza para los equipos cliente, le recomendamos que use un certificado firmado por una entidad de certificación de confianza. Todos los certificados que seleccione deben tener su clave privada correspondiente. Después de recibir un certificado de una entidad de certificación (empresarial o pública), asegúrese de que todos los certificados se importan al almacén de entidades de certificación raíz de confianza en todos los servidores. Puedes importar certificados al almacén con el complemento **Certificados** de MMC o distribuirlos mediante los Servicios de certificados de Active Directory. Si el certificado que importas expira, es importante que importes manualmente otro certificado válido.


> [!IMPORTANT]
> Si usas el certificado de firma de tokens autofirmado de AD FS, debes importar este certificado en el almacén de entidades de certificación raíz de confianza en todos los servidores de Exchange&nbsp;2013. Si no se usa el certificado de firma de tokens autofirmado y se implementa Proxy de aplicación web, debe actualizar la clave pública en la configuración de Proxy de aplicación web y todas las relaciones de confianza para usuarios autenticados de AD FS.



Al instalar Exchange 2013 SP1, AD FS y Proxy de aplicación web, siga estas recomendaciones de certificados:

  - **Servidores de buzones de correo**   Los certificados que se usan en los servidores de buzones de correo son certificados autofirmados que se crean al instalar Exchange 2013. Como todos los clientes se conectan a un servidor de buzones de correo de Exchange 2013 mediante un servidor de acceso de cliente de Exchange 2013, los únicos certificados que necesita administrar son los de los servidores de acceso de cliente.

  - **Servidores de acceso de cliente**   Se necesita un certificado SSL para las comunicaciones de servicio. Si su certificado SSL existente ya incluye el nombre completo que está usando para instalar el extremo de la relación de confianza para usuario autenticado, no se necesitan certificados adicionales.

  - **AD FS**   AD FS necesita dos tipos de certificados:
    
      - Certificado SSL usado en las comunicaciones de servicio
        
          - Nombre de sujeto: **adfs.contoso.com** (nombre de la implementación de AD FS)
        
          - Nombre alternativo del firmante (SAN): Ninguno
    
      - Certificado de firma de tokens
        
          - Nombre de sujeto: **tokensigning.contoso.com**
        
          - Nombre alternativo del firmante (SAN): Ninguno
        

        > [!NOTE]
        > Cuando se reemplace el certificado de firma de tokens en AD FS, deben actualizarse las actuales relaciones de confianza para usuarios autenticados para que usen el nuevo certificado de firma de tokens.



  - **Proxy de aplicación web**
    
      - Certificado SSL usado en las comunicaciones de servicio
        
          - Nombre de sujeto: **owa.contoso.com**
        
          - Nombre alternativo del firmante (SAN): Ninguno
        

        > [!NOTE]
        > Si la dirección URL externa de Proxy de aplicación web es la misma que su dirección URL interna, puede reutilizar aquí el certificado SSL de Exchange.

    
      - Certificado SSL de Proxy de AD FS
        
          - Nombre de sujeto: **adfs.contoso.com** (nombre de la implementación de AD FS)
        
          - Nombre alternativo del firmante (SAN): Ninguno
    
      - Certificado de firma de tokens: se copiará desde AD FS automáticamente como parte de los siguientes pasos. Si se usa este certificado, debe ser de confianza para los servidores de Exchange 2013 de su organización.

Vea la sección sobre requisitos de certificados en el tema de [revisión de los requisitos para implementar AD FS](https://go.microsoft.com/fwlink/?linkid=392699) para obtener más información sobre los certificados.


> [!NOTE]
> Aunque tenga un certificado SSL para AD FS, sigue necesitando un certificado de cifrado SSL para Outlook Web App y EAC. El certificado SSL se usa en los directorios virtuales OWA y ECP.



## Paso 2: Instalar y configurar los Servicios de federación de Active Directory (AD FS)

En Windows Server 2012 R2, AD FS proporciona funcionalidades de federación de identidad simplificada y protegida, así como de inicio de sesión único (SSO) web. AD FS incluye un servicio de federación que permite una autenticación basada en notificaciones, multifactor, SSO web y basada en explorador. AD FS simplifica el acceso a sistemas y aplicaciones usando una autenticación basada en notificaciones y un mecanismo de autorización de acceso para mantener la seguridad de las aplicaciones.

Para instalar AD FS en Windows Server 2012 R2:

1.  Abra **Administrador del servidor** en la pantalla **Inicio** o **Administrador del servidor** en la barra de tareas del escritorio. Haga clic en **Agregar roles y características** en el menú **Administrar**.

2.  En la página **Antes de empezar**, haga clic en **Siguiente**.

3.  En la página **Seleccionar tipo de instalación**, haga clic en **Instalación basada en características o en roles** y, a continuación, en **Siguiente**.

4.  En la página **Seleccionar servidor de destino**, haga clic en **Seleccionar un servidor del grupo de servidores**, compruebe que está seleccionado el equipo local y después, haga clic en **Siguiente**.

5.  En la página **Seleccionar roles de servidor**, haga clic en **Servicios de federación de Active Directory** y después, haga clic en **Siguiente**.
    
    En la página **Seleccionar características**, haga clic en **Siguiente**. Los requisitos previos o características necesarios ya están seleccionados automáticamente. No es necesario que seleccione otras características.

6.  En la página **Servicios de federación de Active Directory (AD FS)**, haga clic en **Siguiente**.

7.  En la página **Confirmar selecciones de instalación**, seleccione **Reiniciar automáticamente el servidor de destino en caso necesario** y haga clic en **Instalar**.
    

    > [!NOTE]
    > No cierre el asistente durante el proceso de instalación.



Después de instalar los servidores de AD FS necesarios y de generar los certificados necesarios, debe configurar AD FS y después, probar que AD FS funciona correctamente. También puede usar esta la lista de comprobación como ayuda para instalar y configurar AD FS: [Lista de comprobación: configurar un servidor de federación](https://go.microsoft.com/fwlink/?linkid=392700).

Para configurar los Servicios de federación de Active Directory:

1.  En la página **Progreso de la instalación**, en la ventana debajo de **Servicios de federación de Active Directory**, haga clic en **Configure el servicio de federación en este servidor**. Se abre el Asistente para la configuración de los Servicios de federación de Active Directory.

2.  En la página **principal**, haga clic en **Crear el primer servidor de federación de una granja de servidores de federación** y después, haga clic en **Siguiente**.

3.  En la página **Conectarse a AD DS**, especifique una cuenta con derechos de administrador del dominio para el dominio de Active Directory correcto al que está unido este equipo y después, haga clic en **Siguiente**. Si necesita seleccionar un usuario diferente, haga clic en **Cambiar**.

4.  En la página **Especificar propiedades del servicio**, haga lo siguiente y después, haga clic en **Siguiente**:
    
      - Importe el certificado SSL que obtuvo anteriormente de AD CS o de una entidad de certificación pública. Este es el certificado de autenticación del servicio necesario. Vaya a la ubicación de su certificado SSL. Para obtener más información sobre cómo crear e importar certificados SSL, vea [Certificados de servidor](https://go.microsoft.com/fwlink/?linkid=392703).
    
      - Especifique un nombre para su servicio de federación, por ejemplo, escriba **adfs.contoso.com**.
    
      - Para proporcionar al servicio de federación un nombre para mostrar, escriba el nombre de su organización, por ejemplo, **Contoso, Ltd.**.

5.  En la página **Especificar cuenta de servicio**, seleccione **Usar una cuenta de usuario de dominio o una cuenta de servicio administrada de grupo existente** y después, especifique la cuenta GMSA (FsGmsa) que creó al crear el controlador de dominio. Incluya la contraseña de la cuenta y después, haga clic en **Siguiente**.
    

    > [!NOTE]
    > La cuenta de servicio globalmente administrada (GMSA) es una cuenta que se debe crear cuando se configura un controlador de dominio. La cuenta GMSA se necesita durante la instalación y configuración de AD FS. Si aún no ha creado esta cuenta, ejecute el siguiente comando de Windows PowerShell. Crea la cuenta para el dominio contoso.com y el servidor de AD FS:



6.  Ejecute el comando siguiente.
    
        Add-KdsRootKey -EffectiveTime (Get-Date).AddHours(-10)

7.  En este ejemplo se crea una nueva cuenta GMSA denominada FsGmsa para el servicio de federación denominado adfs.contoso.com. El nombre de servicio de federación es el valor que sea visible para los clientes.
    
        New-ADServiceAccount FsGmsa -DNSHostName adfs.contoso.com -ServicePrincipalNames http/adfs.contoso.com

8.  En la página **Especificar base de datos de configuración**, seleccione **Crear una base de datos en este servidor que usa Windows Internal Database** y haga clic en **Siguiente**.

9.  En la página **Revisar opciones**, compruebe las opciones de configuración seleccionadas. También puede usar el botón **Ver script** para automatizar otras instalaciones de AD FS. Haga clic en **Siguiente**.

10. En la página **Comprobaciones de requisitos previos**, compruebe que se han completado todas las comprobaciones de los requisitos previos y, después, haga clic en **Configurar**.

11. En la página **Progreso de la instalación**, compruebe que todo se instala correctamente y haga clic en **Cerrar**.

12. En la página **Resultados**, revise los resultados, compruebe si la configuración se realizó correctamente y después, haga clic en **Hay que realizar los siguientes pasos para completar la implementación del servicio de federación**.

Los siguientes comandos de PowerShell Windows hacen lo mismo que los pasos anteriores.
```
    Import-Module ADFS
```
```
    Install-AdfsFarm -CertificateThumbprint 0E0C205D252002D535F6D32026B6AB074FB840E7 -FederationServiceDisplayName "Contoso Corporation" -FederationServiceName adfs.contoso.com -GroupServiceAccountIdentifier "contoso\FSgmsa`$"
```

Para obtener detalles y la sintaxis, vea [Install-AdfsFarm](https://go.microsoft.com/fwlink/?linkid=392704).

Para comprobar la instalación: en el servidor de AD FS, abra el explorador web y vaya a la dirección URL de los metadatos de federación. Por ejemplo, **https://adfs.contoso.com/federationmetadata/2007-06/federationmetadata.xml**.

## Paso 3: Crear una relación de confianza para usuario autenticado y reglas personalizadas para las notificaciones para Outlook Web App y EAC

Debe configurar una relación de confianza para usuario autenticado en el servidor de AD FS para las aplicaciones y los servicios que quiera publicar mediante Proxy de aplicación web. En el caso de las implementaciones con varios sitios de Active Directory que usen espacios de nombres diferentes, es necesario agregar una relación de confianza para usuario autenticado para Outlook Web App y EAC por cada espacio de nombres.

EAC usa el directorio virtual ECP. Puede ver o configurar las opciones de EAC usando los cmdlets [Get-EcpVirtualDirectory](https://technet.microsoft.com/es-es/library/dd351058\(v=exchg.150\)) y [Set-EcpVirtualDirectory](https://technet.microsoft.com/es-es/library/dd297991\(v=exchg.150\)). Para acceder a EAC, debe usar un explorador web e ir a **http://server1.contoso.com/ecp**.


> [!NOTE]
> El uso de la barra diagonal <STRONG>/</STRONG> en las URL de ejemplo que figuran a continuación es intencionado. Es importante asegurarse de que las relaciones de confianza para usuario autenticado de AD&nbsp;FS y los URI de audiencia de Exchange <STRONG>sean idénticos</STRONG>. Esto significa que las relaciones de confianza para usuario autenticado de AD&nbsp;FS y los URI de audiencia de Exchange deben <STRONG>tener</STRONG> o <STRONG>emitir</STRONG> las barras diagonales finales de sus URL. Los ejemplos de esta sección contienen las barras diagonales (<STRONG>/</STRONG>) finales después de todas las URL que terminan en "owa" (/owa/) o "ecp" (/ecp/).



Para Outlook Web App, para crear relaciones de confianza para usuarios autenticados mediante el complemento Administración de AD FS en Windows Server 2012 R2:

1.  En **Administrador del servidor**, haga clic en **Herramientas** y seleccione **Administración de AD FS**.

2.  En el **complemento AD FS**, en **AD FS\\Relaciones de confianza**, haga clic con el botón secundario en **Relaciones de confianza para usuarios autenticados** y después, haga clic en **Agregar relación de confianza para usuario autenticado** para abrir el asistente **Agregar relación de confianza para usuario autenticado**.

3.  En la página **principal**, haga clic en **Iniciar**.

4.  En la página **Seleccionar origen de datos**, haga clic en **Escribir manualmente los datos del usuario de confianza** y después, haga clic en **Siguiente**.

5.  En la página **Especificar nombre para mostrar**, en el cuadro **Nombre para mostrar**, escriba **Outlook Web App** y, en **Notas**, escriba una descripción de esta relación de confianza para usuario autenticado (como **This is a trust for https://mail.contoso.com/owa**); después, haga clic en **Siguiente**.

6.  En la página **Elegir perfil**, haga clic en **Perfil de AD FS** y en **Siguiente**.

7.  En la página **Configurar certificado**, haga clic en **Siguiente**.

8.  En la página **Configurar URL**, haga clic en **Habilitar compatibilidad para el protocolo WS-Federation Passive** y, en **Dirección URL del protocolo WS-Federation Passive del usuario de confianza**, **type https://mail.contoso.com/owa** y haga clic en **Siguiente**.

9.  En la página **Configurar identificadores**, especifique uno o varios identificadores para este usuario de confianza, haga clic en **Agregar** para agregarlos a la lista y después, haga clic en **Siguiente**.

10. En la página **¿Configurar ahora la autenticación multifactor?**, seleccione **Configurar las opciones de autenticación multifactor para esta relación de confianza para usuario autenticado**.

11. En la página **Configurar autenticación multifactor**, compruebe que **No quiero configurar ahora las opciones de autenticación multifactor para esta relación de confianza para usuario autenticado** está seleccionada y haga clic en **Siguiente**.

12. En la página **Elegir reglas de autorización de emisión**, seleccione **Permitir a todos los usuarios acceder a este usuario de confianza** y haga clic en **Siguiente**.

13. En la página **Listo para agregar relación de confianza**, revise la configuración y después, haga clic en **Siguiente** para guardar la información de la relación de confianza para usuario autenticado.

14. En la página **Finalizar**, compruebe que **Abrir el cuadro de diálogo Editar reglas de notificación para esta relación de confianza para usuario autenticado cuando se cierre el asistente** no está seleccionada y haga clic en **Cerrar**.

Para crear una relación de confianza para usuario autenticado para EAC, debe seguir estos pasos y crear una segunda relación de confianza para usuario autenticado pero, en lugar de poner **Outlook Web App** como nombre para mostrar, escriba **EAC**. Como descripción, escriba **This is a trust for the Exchange Admin Center** y la **Dirección URL del protocolo WS-Federation Passive del usuario de confianza** es **https://mail.contoso.com/ecp**.

En un modelo de identidad basada en notificaciones, la función de los Servicios de federación de Active Directory (AD FS) como servicio de federación es emitir un token que contiene un conjunto de notificaciones. Las reglas de notificaciones rigen las decisiones relativas a las notificaciones que AD FS emite. Las reglas de notificaciones y todos los datos de configuración de los servidores se almacenan en la base de datos de configuración de AD FS.

Es necesario crear dos reglas de notificaciones:

  - SID de usuario de Active Directory

  - UPN de Active Directory

Para agregar las reglas de notificaciones necesarias:

1.  En **Administrador del servidor**, haga clic en **Herramientas** y seleccione **Administración de AD FS**.

2.  En el árbol de consola, en **AD FS\\Relaciones de confianza**, haga clic en **Relaciones de confianza para proveedores de notificaciones** o **Relaciones de confianza para usuarios autenticados** y haga clic en la relación de confianza para usuario autenticado para Outlook Web App.

3.  En la ventana **Relaciones de confianza para usuarios autenticados**, haga clic con el botón secundario en la relación de confianza de Outlook Web App y después, haga clic en **Editar reglas de notificación**.

4.  En la pestaña **Reglas de transformación de emisión** de la ventana **Editar reglas de notificación**, haga clic en **Agregar regla** para abrir el asistente para agregar regla de notificación de transformación.

5.  En la página **Seleccionar plantilla de regla**, en **Plantilla de regla de notificación**, elija **Enviar reclamaciones mediante una regla personalizada** en la lista y, luego, haga clic en **Siguiente**.

6.  En el paso **Elegir tipo de regla** de la página **Configurar regla**, en **Nombre de regla de notificación**, escriba el nombre de la regla de notificación. Use un nombre descriptivo para la regla de notificación (por ejemplo, **ActiveDirectoryUserSID**). En **Regla personalizada**, escriba la siguiente sintaxis de lenguaje de regla de notificación para esta regla:
    
        c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"] => issue(store = "Active Directory", types = ("http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid"), query = ";objectSID;{0}", param = c.Value);

7.  En la página **Configurar regla**, haga clic en **Finalizar**.

8.  En la pestaña **Reglas de transformación de emisión** de la ventana **Editar reglas de notificación**, haga clic en **Agregar regla** para abrir el asistente para agregar regla de notificación de transformación.

9.  En la página **Seleccionar plantilla de regla**, en **Plantilla de regla de notificación**, elija **Enviar reclamaciones mediante una regla personalizada** en la lista y, luego, haga clic en **Siguiente**.

10. En el paso **Elegir tipo de regla** de la página **Configurar regla**, en **Nombre de regla de notificación**, escriba el nombre de la regla de notificación. Use un nombre descriptivo para la regla de notificación (por ejemplo, **ActiveDirectoryUPN**). En **Regla personalizada**, escriba la siguiente sintaxis de lenguaje de regla de notificación para esta regla:
    
        c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"] => issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn"), query = ";userPrincipalName;{0}", param = c.Value);

11. Haga clic en **Finalizar**.

12. En la ventana **Editar reglas de notificación**, haga clic en **Aplicar** y después, en **Aceptar**.

13. Repita los pasos del 3 al 12 de este procedimiento para la relación de confianza para usuario autenticado de EAC.

Otra opción es crear relaciones de confianza para usuario autenticado y reglas de notificaciones con PowerShell Windows:

1.  Cree los dos archivos .txt IssuanceAuthorizationRules.txt e IssuanceTransformRules.txt.

2.  Importe su contenido en dos variables.

3.  Ejecute los siguientes dos cmdlets para crear las relaciones de confianza para usuarios autenticados. En este ejemplo, esto también configurará las reglas de notificaciones.

**IssuanceAuthorizationRules.txt contiene:** 

    @RuleTemplate = "AllowAllAuthzRule" => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

**IssuanceTransformRules.txt contiene:** 

    @RuleName = "ActiveDirectoryUserSID" c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"] => issue(store = "Active Directory", types = ("http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid"), query = ";objectSID;{0}", param = c.Value); 
    
    @RuleName = "ActiveDirectoryUPN" c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"] => issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn"), query = ";userPrincipalName;{0}", param = c.Value);

**Ejecute los comandos siguientes:** 

    [string]$IssuanceAuthorizationRules=Get-Content -Path C:\IssuanceAuthorizationRules.txt
    
    [string]$IssuanceTransformRules=Get-Content -Path c:\IssuanceTransformRules.txt
    
    Add-ADFSRelyingPartyTrust -Name "Outlook Web App" -Enabled $true -Notes "This is a trust for https://mail.contoso.com/owa/" -WSFedEndpoint https://mail.contoso.com/owa/ -Identifier https://mail.contoso.com/owa/ -IssuanceTransformRules $IssuanceTransformRules -IssuanceAuthorizationRules $IssuanceAuthorizationRules
    
    Add-ADFSRelyingPartyTrust -Name "Exchange Admin Center (EAC)" -Enabled $true -Notes "This is a trust for https://mail.contoso.com/ecp/" -WSFedEndpoint https://mail.contoso.com/ecp/ -Identifier https://mail.contoso.com/ecp/ -IssuanceTransformRules $IssuanceTransformRules -IssuanceAuthorizationRules $IssuanceAuthorizationRules

## Paso 4: Instalar el servicio de rol Proxy de aplicación web (opcional)


> [!NOTE]
> Los pasos 4, 5 y 6 están pensados para los usuarios que quieran publicar Exchange OWA y ECP con Proxy de aplicación web y usar este último para llevar a cabo la autenticación de AD FS. Sin embargo, la publicación de Exchange con Proxy de aplicación web no es necesaria, de modo que puede omitir el paso 7 si no utiliza Proxy de aplicación web y desea que Exchange lleve a cabo la autenticación de AD FS.



Proxy de aplicación web es un nuevo servicio de rol de Acceso remoto de Windows Server 2012 R2. Proxy de aplicación web proporciona funcionalidad de proxy inversa para aplicaciones web dentro de su red corporativa para que los usuarios de numerosos dispositivos puedan acceder a ellas desde el exterior de la red corporativa. Proxy de aplicación web preautentica el acceso a las aplicaciones web usando los Servicios de federación de Active Directory (AD FS) y también funciona como proxy de AD FS. Aunque no se necesita Proxy de aplicación web, se recomienda cuando AD FS es accesible para los clientes externos. Sin embargo, no se admite el acceso sin conexión en Outlook Web App cuando se usa la autenticación de AD FS a través de Proxy de aplicación web. Encontrará más información sobre la integración con Proxy de aplicación web en el tema sobre cómo [instalar y configurar Proxy de aplicación web para publicar aplicaciones internas](https://go.microsoft.com/fwlink/?linkid=392705).


> [!WARNING]
> No puede instalar Proxy de aplicación web en el mismo servidor donde está instalado AD FS.



Para implementar Proxy de aplicación web, debe instalar el rol de servidor de Acceso remoto con el servicio de rol Proxy de aplicación web en un servidor que actúe como servidor de Proxy de aplicación web. Para instalar el servicio de rol Proxy de aplicación web:

1.  En el servidor de Proxy de aplicación web, en **Administrador del servidor**, haga clic en **Administrar** y después, haga clic en **Agregar roles y características**.

2.  En el Asistente para agregar roles y características, haga clic en **Siguiente** tres veces para llegar a la página **Roles de servidor**.

3.  En la página **Roles de servidor**, seleccione **Acceso remoto** en la lista y después, haga clic en **Siguiente**.

4.  En la página **Características**, haga clic en **Siguiente**.

5.  En la página **Acceso remoto**, lea la información y haga clic en **Siguiente**.

6.  En la página **Servicios de rol**, seleccione **Proxy de aplicación web**. Después, en la ventana **Asistente para agregar roles y características**, haga clic en **Agregar características** y haga clic en **Siguiente**.

7.  En la ventana **Confirmación**, haga clic en **Instalar**. También puede seleccionar **Reiniciar automáticamente el servidor de destino en caso necesario**.

8.  En el cuadro de diálogo **Progreso de la instalación**, compruebe que la instalación fue correcta y haga clic en **Cerrar**.

El siguiente cmdlet de PowerShell Windows no hace lo mismo que los pasos anteriores.

    Install-WindowsFeature Web-Application-Proxy -IncludeManagementTools

## Paso 5: Configurar el servicio de rol Proxy de aplicación web (opcional)

Debe configurar Proxy de aplicación web para conectarse al servidor de AD FS. Repita este procedimiento para todos los servidores que quiera implementar como servidores de aplicación web.

Para configurar el servicio de rol Proxy de aplicación web:

1.  En el servidor de Proxy de aplicación web, en **Administrador del servidor**, haga clic en **Herramientas** y después, haga clic en **Administración de acceso remoto**.

2.  En el panel **Configuración**, haga clic en **Proxy de aplicación web**.

3.  En la consola **Administración de acceso remoto**, en el panel central, haga clic en **Ejecutar el asistente de configuración de Proxy de aplicación web**.

4.  En el Asistente para configuración de Proxy de aplicación web, en la página **principal**, haga clic en **Siguiente**.

5.  En la página **Servidor de federación**, lleve a cabo estos pasos y después, haga clic en **Siguiente**:
    
      - En el cuadro **Nombre del servicio de federación**, escriba el nombre completo del servidor de AD FS; por ejemplo, **adfs.contoso.com**.
    
      - En los cuadros **Nombre de usuario** y **Contraseña**, escriba las credenciales de una cuenta de administrador local en los servidores de AD FS.

6.  En el cuadro de diálogo **Certificado de proxy de AD FS**, en la lista de certificados actualmente instalados en el servidor de Proxy de aplicación web, seleccione el certificado que usará Proxy de aplicación web para la funcionalidad de proxy de AD FS y después, haga clic en **Siguiente**. El certificado que elija aquí debe ser uno cuyo sujeto sea el nombre del servicio de federación; por ejemplo, **adfs.contoso.com**.

7.  En el cuadro de diálogo **Confirmación**, revise la configuración. Si es necesario, puede copiar el cmdlet de Windows PowerShell para automatizar otras instalaciones. Haga clic en **Configurar**.

8.  En el cuadro de diálogo **Resultados**, compruebe que la instalación fue correcta y haga clic en **Cerrar**.

El siguiente cmdlet de PowerShell Windows no hace lo mismo que los pasos anteriores.

    Install-WebApplicationProxy -CertificateThumprint 1a2b3c4d5e6f1a2b3c4d5e6f1a2b3c4d5e6f1a2b -FederationServiceName adfs.contoso.com

## Paso 6: Publicar Outlook Web App y EAC mediante Proxy de aplicación web (opcional)

En el paso 3, creó notificaciones y relaciones de confianza para usuario autenticado para Outlook Web App y EAC, y ahora necesita publicar ambas aplicaciones. Sin embargo, primero compruebe que se creó una relación de confianza para usuario autenticado para ellas y que en el servidor de Proxy de aplicación web haya un certificado apto para Outlook Web App y EAC. En el caso de los extremos de AD FS que necesite publicar con Proxy de aplicación web, establézcalos como **Habilitado para proxy** en la consola de administración de AD FS.

Siga los pasos para publicar Outlook Web App mediante Proxy de aplicación web. Para EAC, repita estos pasos. Cuando publique EAC, necesita cambiar el nombre, la dirección URL externa, el certificado externo y la dirección URL del servidor back-end.

Para publicar Outlook Web App y EAC mediante Proxy de aplicación web:

1.  En el servidor de Proxy de aplicación web, en el panel **Navegación** de la consola **Administración de acceso remoto**, haga clic en **Proxy de aplicación web** y, en el panel **Tareas**, haga clic en **Publicar**.

2.  En el Asistente para publicar nueva aplicación, en la página **principal**, haga clic en **Siguiente**.

3.  En la página **Preautenticación**, haga clic en **Servicios de federación de Active Directory (AD FS)** y después, haga clic en **Siguiente**.

4.  En la página **Usuario de confianza**, en la lista de usuarios de confianza, seleccione el usuario de confianza para la aplicación que quiere publicar y después, haga clic en **Siguiente**.

5.  En la página **Configuración de la publicación**, lleve a cabo estos pasos y después, haga clic en **Siguiente**:
    
    1.  En el cuadro **Nombre**, escriba un nombre descriptivo para la aplicación. Este nombre solo se usa en la lista de aplicaciones publicadas en la consola de **Administración de acceso remoto**. Puede usar **OWA** y **EAC** como nombres.
    
    2.  En el cuadro **URL externa**, escriba la dirección URL externa para esta aplicación; por ejemplo, **https://external.contoso.com/owa** para Outlook Web App y **https://external.contoso.com/ecp** para EAC.
    
    3.  En la lista **Certificado externo**, seleccione un certificado cuyo nombre de sujeto coincida con el nombre de host de la dirección URL externa.
    
    4.  En el cuadro **URL de servidor back-end**, escriba la dirección URL del servidor back-end. Tenga en cuenta que este valor se rellena automáticamente cuando se especifica la dirección URL externa, y solo debe cambiarlo si la dirección URL del servidor back-end es diferente; por ejemplo, **https://mail.contoso.com/owa** para Outlook Web App y **https://mail.contoso.com/ecp** para EAC.
    

    > [!NOTE]
    > Proxy de aplicación web puede traducir nombres de host en direcciones URL pero no puede traducir rutas de acceso. Por consiguiente, puede especificar nombres de host diferentes pero debe especificar la misma ruta de acceso. Por ejemplo, puede especificar una dirección URL externa <EM>https://external.contoso.com/app1/</EM> y una dirección URL de servidor back-end <EM>https://mail.contoso.com/app1/</EM>. Sin embargo, no puede especificar una dirección URL externa <EM>https://external.contoso.com/app1/</EM> y una dirección URL de servidor back-end <EM>https://mail.contoso.com/internal-app1/</EM>.



6.  En la página **Confirmación**, revise la configuración y haga clic en **Publicar**. Puede copiar el comando de Windows PowerShell para configurar otras aplicaciones publicadas.

7.  En la página **Resultados**, asegúrese de que la aplicación se publicó correctamente y haga clic en **Cerrar**.

El siguiente cmdlet de Windows PowerShell realiza las mismas tareas que el procedimiento anterior para Outlook Web App.

    Add-WebApplicationProxyApplication -BackendServerUrl 'https://mail.contoso.com/owa/' -ExternalCertificateThumbprint 'E9D5F6CDEA243E6E62090B96EC6DE873AF821983' -ExternalUrl 'https://external.contoso.com/owa/' -Name 'OWA' -ExternalPreAuthentication ADFS -ADFSRelyingPartyName 'Outlook Web App'

El siguiente cmdlet de Windows PowerShell realiza las mismas tareas que el procedimiento anterior para EAC.

    Add-WebApplicationProxyApplication -BackendServerUrl 'https://mail.contoso.com/ecp/' -ExternalCertificateThumbprint 'E9D5F6CDEA243E6E62090B96EC6DE873AF821983' -ExternalUrl 'https://external.contoso.com/ecp/' -Name 'EAC' -ExternalPreAuthentication ADFS -ADFSRelyingPartyName 'Exchange Admin Center'

Cuando haya completado estos pasos, Proxy de aplicación web llevará a cabo la autenticación de AD FS para los clientes de Outlook Web App y EAC, y habilitará para proxy las conexiones a Exchange en su nombre. No es necesario configurar Exchange para la autenticación de AD FS, de modo que puede avanzar al paso 10 para probar la configuración.

## Paso 7: Configurar Exchange 2013 para usar autenticación de AD FS

Cuando se configura AD FS para usarlo para autenticación basada en notificaciones con Outlook Web App y EAC en Exchange 2013, debe habilitar AD FS para su organización Exchange. Debe usar el cmdlet [Set-OrganizationConfig](https://technet.microsoft.com/es-es/library/aa997443\(v=exchg.150\)) para configurar las opciones de AD FS para su organización:

  - Establezca el emisor de AD FS en **https://adfs.contoso.com/adfs/ls**.

  - Establezca los URI de AD FS en **https://mail.contoso.com/owa** y **https://mail.contoso.com/ecp**.

  - Busque el símbolo (token) de AD FS huella digital de certificado de firma mediante Windows PowerShell en el servidor de AD FS y entrar en `Get-ADFSCertificate -CertificateType "Token-signing"`. A continuación, asignar la firma de tokens huella digital de certificado que encuentra. Si ha caducado el certificado de firma de tokens de AD FS, la huella digital del certificado de firma de tokens AD FS nuevo debe actualizarse mediante el cmdlet [Set-OrganizationConfig](https://technet.microsoft.com/es-es/library/aa997443\(v=exchg.150\)) .

Ejecute los comandos siguientes en el Shell de administración de Exchange.

    $uris = @(" https://mail.contoso.com/owa/","https://mail.contoso.com/ecp/")
    Set-OrganizationConfig -AdfsIssuer "https://adfs.contoso.com/adfs/ls/" -AdfsAudienceUris $uris -AdfsSignCertificateThumbprint "88970C64278A15D642934DC2961D9CCA5E28DA6B"


> [!NOTE]
> El parámetro <EM>-AdfsEncryptCertificateThumbprint</EM> no es compatible para estos escenarios.



Para obtener detalles y la sintaxis, vea [Set-OrganizationConfig](https://technet.microsoft.com/es-es/library/aa997443\(v=exchg.150\)) y [Get-ADFSCertificate](https://go.microsoft.com/fwlink/?linkid=392706).

## Paso 8: Habilitar la autenticación de AD FS en los directorios virtuales de OWA y ECP

Para los directorios virtuales de OWA y ECP, habilite la autenticación de AD FS como único método de autenticación y deshabilite otras formas de autenticación.


> [!WARNING]
> Debe configurar el directorio virtual de ECP antes de configurar el directorio virtual de OWA.



Configurar el directorio virtual ECP mediante el Shell de administración de Exchange. En la ventana del Shell, ejecute el siguiente comando.

    Get-EcpVirtualDirectory | Set-EcpVirtualDirectory -AdfsAuthentication $true -BasicAuthentication $false -DigestAuthentication $false -FormsAuthentication $false -WindowsAuthentication $false

Configurar el directorio virtual de OWA mediante el Shell de administración de Exchange. En la ventana del Shell, ejecute el siguiente comando.

    Get-OwaVirtualDirectory | Set-OwaVirtualDirectory -AdfsAuthentication $true -BasicAuthentication $false -DigestAuthentication $false -FormsAuthentication $false -WindowsAuthentication $false -OAuthAuthentication $false


> [!NOTE]
> Los comandos de Shell de administración de Exchange anteriores configuración los directorios virtuales OWA y ECP en cada servidor de acceso de cliente de la organización. Si no desea aplicar esta configuración a todos los servidores acceso de cliente, utilice el parámetro <EM>-Identity</EM> y especifique el servidor acceso de cliente. Es probable que desee aplicar esta configuración sólo a los servidores de acceso de cliente de la organización que están en Internet que enfrentan.



Para obtener detalles y la sintaxis, vea [Get-OwaVirtualDirectory](https://technet.microsoft.com/es-es/library/aa998588\(v=exchg.150\)) y [Set-OwaVirtualDirectory](https://technet.microsoft.com/es-es/library/bb123515\(v=exchg.150\)) o [Get-EcpVirtualDirectory](https://technet.microsoft.com/es-es/library/dd351058\(v=exchg.150\)) y [Set-EcpVirtualDirectory](https://technet.microsoft.com/es-es/library/dd297991\(v=exchg.150\)).

## Paso 9: Reiniciar o reciclar Internet Information Services (IIS)

Una vez completados todos los pasos necesarios, incluidos los cambios en los directorios virtuales de Exchange, debe reiniciar Internet Information Services. Para ello, puede usar uno de los siguientes métodos:

  - Mediante Windows PowerShell:
    
        Restart-Service W3SVC,WAS -noforce

  - Mediante una línea de comandos: Haga clic en **Inicio**, **Ejecutar**, escriba `IISReset /noforce` y, a continuación, haga clic en **Aceptar**.

  - Mediante el Administrador de Internet Information Services (IIS): En **Administrador del servidor**\>**IIS**, haga clic en **Herramientas** y, después, haga clic en **Administrador de Internet Information Services (IIS)**. En la ventana **Administrador de Internet Information Services (IIS)**, en el panel de acciones de **Administrar servidor**, haga clic en **Reiniciar**.

## Paso 10: Probar las notificaciones de AD FS para Outlook Web App y EAC

Para probar las notificaciones de AD FS para Outlook Web App:

  - En su explorador web, inicie sesión en Outlook Web App, por ejemplo, **https://mail.contoso.com/owa**.

  - Si obtiene un error de certificado en la ventana del explorador, simplemente continúe al sitio web de Outlook Web App. Se le redirigirá a la página de inicio de sesión de AD FS o se le solicitarán las credenciales.

  - Escriba su nombre de usuario (dominio\\usuario) y contraseña y haga clic en **Iniciar sesión**.

Outlook Web App se cargará en la ventana.

Para probar las notificaciones de AD FS para EAC:

1.  En su explorador web, vaya a **https://mail.contoso.com/ecp**.

2.  Si obtiene un error de certificado en la ventana del explorador, simplemente continúe al sitio web de ECP. Se le redirigirá a la página de inicio de sesión de AD FS o se le solicitarán las credenciales.

3.  Escriba su nombre de usuario (dominio\\usuario) y contraseña y haga clic en **Iniciar sesión**.

4.  EAC debería cargarse en la ventana.

## Información adicional que quizás quiera conocer

**Autenticación multifactor**

Para las implementaciones locales de Exchange 2013 SP1, implementar y configurar los Servicios de federación de Active Directory (AD FS) 2.0 usando notificaciones significa que Outlook Web App y EAC en Exchange 2013 SP1 pueden admitir métodos de autenticación multifactor, como la autenticación basada en certificados, tokens de autenticación o seguridad y autenticación con huella digital. La autenticación de dos factores suele confundirse con otras formas de autenticación. La autenticación multifactor requiere el uso de dos de tres factores de autenticación. Estos factores son:

  - Algo que solo el usuario conoce (por ejemplo, contraseña, PIN o patrón).

  - Algo que solo el usuario tiene (por ejemplo, tarjeta de cajero automático, token de seguridad, tarjeta inteligente o teléfono móvil).

  - Algo que solo el usuario es (por ejemplo, una característica biométrica como una huella digital)

Para obtener más información sobre la autenticación multifactor en Windows Server 2012 R2, vea [Información general: administración de riesgos con autenticación multifactor adicional para aplicaciones confidenciales](https://go.microsoft.com/fwlink/?linkid=392707) y [Guía de tutorial: administración de riesgos con autenticación multifactor adicional para aplicaciones confidenciales](https://go.microsoft.com/fwlink/?linkid=392708).

En el servicio de rol AD FS de Windows Server 2012 R2, el servicio de federación funciona como servicio de token de seguridad, proporciona los tokens de seguridad que se usan con las notificaciones, y le da la capacidad de admitir autenticación multifactor. El servicio de federación emite tokens basados en las credenciales que se presentan. Después de que el almacén de cuentas verifique las credenciales del usuario, se generan las notificaciones para el usuario de acuerdo con las reglas de la directiva de confianza y después, se agregan a un token de seguridad que se emite al cliente. Para obtener más información sobre las notificaciones, vea [Descripción de las notificaciones](https://go.microsoft.com/fwlink/?linkid=392709).

**Coexistencia con otras versiones de Exchange**

En los casos en los que hay más de una versión de Exchange implementada en la organización, es posible usar la autenticación de AD FS para Outlook Web App y EAC. Este escenario solo es compatible con las implementaciones de Exchange 2010 y Exchange 2013 y únicamente a condición de que todos los clientes se conecten mediante servidores de Exchange 2013 **y** de que dichos servidores de Exchange 2013 se hayan configurado para la autenticación de AD FS.

Los usuarios que tengan un buzón de correo en un servidor de Exchange 2010 pueden acceder a ellos a través de un servidor de Exchange de 2013 configurado para la autenticación de AD FS. Para la conexión inicial del cliente al servidor de Exchange de 2013 se usara la autenticación de AD FS. Sin embargo, la conexión proxy al servidor de Exchange 2010 usará Kerberos. No hay ningún modo compatible que permita configurar Exchange Server 2010 para la autenticación directa de AD FS.

