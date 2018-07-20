---
title: 'Configuración de la cuenta en Outlook para iOS y Android mediante la autenticación básica: Exchange 2013 Help'
TOCTitle: Configuración de la cuenta en Outlook para iOS y Android mediante la autenticación básica
ms:assetid: 013dbe8c-30de-4c9c-baa9-75081b9229e8
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Mt829322(v=EXCHG.150)
ms:contentKeyID: 74518384
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configuración de la cuenta en Outlook para iOS y Android mediante la autenticación básica

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2018-04-30_

**Resumen:**  ¿cómo los usuarios de la organización de Exchange de 2013 pueden configurar rápidamente su Outlook para iOS y Android cuentas mediante autenticación básica.

Outlook para iOS y Android ofrece a los administradores de Exchange la capacidad de "empuje" configuraciones de cuenta a sus usuarios locales que utilicen la autenticación básica a través del protocolo de ActiveSync. Esta función funciona con cualquier proveedor de Mobile Device Management (MDM) que utiliza el canal de [Configuración de la aplicación administrada](https://developer.apple.com/library/content/samplecode/sc2279/introduction/intro.html) para el canal [Android en la empresa](https://developer.android.com/samples/apprestrictions/index.html) o de iOS para Android.

Para los usuarios locales está inscrito en Microsoft Intune, puede implementar la configuración de cuenta mediante Intune en el Portal de Azure.

Una vez que se ha creado una configuración de cuenta y el usuario inscribe su dispositivo, Outlook para iOS y Android detectará una cuenta se "encuentra" y le pedirá al usuario que agregue la cuenta. La única información que el usuario debe introducir para completar el proceso de instalación es su contraseña. A continuación, se cargará el contenido del buzón del usuario y el usuario puede empezar a utilizar la aplicación.

Las siguientes imágenes muestran un ejemplo del proceso de instalación para el usuario final después de configurar Outlook para iOS y Android en Intune en el Portal de Azure.

![Configuración local de la cuenta de Outlook para iOS y Android](images/Mt829322.04bd56f2-5c45-4268-8762-436994acd656(EXCHG.150).png "Configuración local de la cuenta de Outlook para iOS y Android")

## Crear una directiva de configuración de la aplicación para Outlook para iOS y Android mediante Microsoft Intune

Si está utilizando Microsoft Intune como proveedor de administración de dispositivos móviles, los pasos siguientes permiten implementar opciones de configuración de cuenta para los buzones locales que aprovechan la autenticación básica con el protocolo ActiveSync. Una vez creada la configuración, puede asignar a los valores a grupos de usuarios, como se detalla en la siguiente sección, asignar a valores de configuración.


> [!NOTE]
> Si los usuarios de su organización utilizan iOS y Android para dispositivos de trabajo, debe crear una directiva de configuración de aplicación independiente para cada plataforma.



1.  Iniciar sesión en el portal de Azure.

2.  Seleccione **más servicios \> supervisión + Administración \> Intune**.

3.  En el módulo de **aplicaciones móviles** de la lista Administrar, seleccione **directivas de configuración de la aplicación**.

4.  En el módulo de **directivas de configuración de la aplicación** , elija **Agregar**.

5.  En la hoja de **configuración de la aplicación de agregar** , escriba un **nombre**y una **Descripción** opcional para la configuración de la aplicación.

6.  Tipo de **inscripción del dispositivo** , seleccione **los dispositivos administrados**.

7.  Para la **plataforma**, elija **iOS** o **Android para el trabajo**.

8.  Elegir **las aplicaciones de asociados**y, a continuación, en el módulo de **aplicaciones de destino** , elija **Microsoft Outlook para iOS** o **Microsoft Outlook para Android**.

9.  Haga clic en **Aceptar** para volver a la hoja de **configuración de la aplicación de complemento** .

10. Elegir **Opciones de configuración**. En la hoja de **configuración** , definir los pares de valores clave que proporcionan configuraciones de Outlook para iOS y Android. Los pares de valores clave que escriba se definen más adelante en este artículo, en la sección de pares de valor clave.
    

    > [!NOTE]
    > Para introducir los pares de valores clave, tiene la opción entre mediante el Diseñador de configuración o especificar una lista de propiedades XML.



11. Cuando haya terminado, seleccione **Aceptar**.

12. En la hoja de **configuración de la aplicación de agregar** , elija **crear**.

La directiva de configuración recién creado se mostrará en el módulo de **directivas de configuración de la aplicación** .

## Asignar a valores de configuración

Asignar a la configuración que creó en la sección anterior para grupos de usuarios de Active Directory de Azure. Cuando un usuario tiene de la aplicación Microsoft Outlook instalada, la aplicación se administrarán por la configuración que ha especificado. Para hacer esto:

1.  En el módulo de **aplicaciones móviles** de la consola de administración de aplicaciones móviles Intune, elija **directivas de configuración de la aplicación**.

2.  Desde la lista de directivas de configuración de la aplicación, seleccione la que desea asignar y, a continuación, elija **las asignaciones**.

3.  En la hoja de **tareas** , elija **Seleccionar grupos**.

4.  En la hoja **Seleccionar grupos** , seleccione el grupo de AD Azure al que desea asignar la directiva de configuración de la aplicación, a continuación, elija **Seleccionar**y, a continuación, **Guardar**.

## Pares de valores clave

Cuando se crea una directiva de configuración de la aplicación en el Portal de Azure o a través de su proveedor MDM, necesitará los siguientes pares de valores clave:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tecla</th>
<th>Valores</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>com.microsoft.outlook.EmailProfile.EmailAccountName</p></td>
<td><p>Este valor especifica la cuenta de correo electrónico Mostrar nombre tal y como aparecerá para los usuarios en sus dispositivos.</p>
<p><strong>Valores aceptados</strong>: cadena</p>
<p><strong>El valor predeterminado si no se especifica</strong>: &lt; en blanco &gt;</p>
<p><strong>Ejemplo</strong>: user@companyname.com</p>
<p><strong>Símbolo (token) * Intune</strong>: {{username}}</p></td>
</tr>
<tr class="even">
<td><p>com.microsoft.outlook.EmailProfile.EmailAddress</p></td>
<td><p>Este valor especifica la dirección de correo electrónico que se utilizará para enviar y recibir correo.</p>
<p><strong>Valores aceptados</strong>: cadena</p>
<p><strong>El valor predeterminado si no se especifica</strong>: &lt; en blanco &gt;</p>
<p><strong>Ejemplo</strong>: user@companyname.com</p>
<p><strong>Símbolo (token) * Intune</strong>: {{correo}}</p></td>
</tr>
<tr class="odd">
<td><p>com.microsoft.outlook.EmailProfile.EmailUPN</p></td>
<td><p>Este valor especifica el nombre Principal de usuario para el perfil de correo electrónico que se utilizará para autenticar la cuenta.</p>
<p><strong>Valores aceptados</strong>: cadena</p>
<p><strong>El valor predeterminado si no se especifica</strong>: &lt; en blanco &gt;</p>
<p><strong>Ejemplo</strong>: userupn@companyname.com</p>
<p><strong>Símbolo (token) * Intune</strong>: {{userprincipalname}}</p></td>
</tr>
<tr class="even">
<td><p>com.microsoft.outlook.EmailProfile.ServerAuthentication</p></td>
<td><p>Este valor especifica el método de autenticación del usuario.</p>
<p><strong>Valores aceptados</strong>: 'Nombre de usuario y contraseña'; «Certificados»</p>
<p><strong>El valor predeterminado si no se especifica</strong>: 'Nombre de usuario y contraseña'</p>
<p><strong>Ejemplo</strong>: 'Nombre de usuario y contraseña'</p></td>
</tr>
<tr class="odd">
<td><p>com.microsoft.outlook.EmailProfile.ServerHostName</p></td>
<td><p>Este valor especifica el nombre de host del servidor de Exchange.</p>
<p><strong>Valores aceptados</strong>: cadena</p>
<p><strong>El valor predeterminado si no se especifica</strong>: &lt; en blanco &gt;</p></td>
</tr>
</tbody>
</table>


**\*** Los usuarios de Microsoft Intune pueden utilizar tokens que se expandirán en el valor correcto según el usuario inscrito de MDM. Para obtener más información, vea [Agregar directivas de configuración de la aplicación para dispositivos iOS administrados](https://docs.microsoft.com/en-us/intune/app-configuration-policies-use-ios) .

