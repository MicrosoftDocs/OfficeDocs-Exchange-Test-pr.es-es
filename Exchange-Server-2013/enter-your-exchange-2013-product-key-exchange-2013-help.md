---
title: 'Introducir la clave de producto de Exchange 2013: Exchange 2013 Help'
TOCTitle: Introducir la clave de producto de Exchange 2013
ms:assetid: ccb14685-4bdc-42a4-a985-35cd2a1a415c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124582(v=EXCHG.150)
ms:contentKeyID: 51406549
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.EnterProductKeyWizardForm.EnterProductKeyWizardPage
ms.translationtype: HT
---

# Introducir la clave de producto de Exchange 2013

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Una clave de producto indica a Exchange Server 2013 que ha comprado una licencia Standard o Enterprise Edition. Si la clave de producto que adquirió es para una licencia Enterprise Edition, puede montar más de cinco bases de datos por servidor además de todas las características disponibles con una licencia Standard Edition. Para más información sobre las licencias de Exchange, vea [Exchange 2013: ediciones y versiones](exchange-2013-editions-and-versions-exchange-2013-help.md).

Si no especifica una clave de producto, el servidor obtiene automáticamente una licencia de edición de prueba. La edición de prueba funciona exactamente igual que un servidor estándar de Exchange y resulta útil para probar Exchange antes de comprobarlo o ejecutar pruebas en un laboratorio. La única diferencia es que solo puede usar un servidor de Exchange con licencia de prueba durante un máximo de 180 días. Si quiere continuar usando el servidor pasados los 180 días, deberá especificar una clave de producto. De lo contrario, el Centro de administración de Exchange (EAC) comenzará a mostrarle recordatorios de que debe especificar una clave de producto para obtener la licencia para el servidor.


> [!TIP]
> Hemos observado que algunos visitantes de esta página buscan información sobre cómo instalar o activar Office. Si ese es su caso, consulte estas páginas: 
> <UL>
> <LI>
> <P><A href="http://go.microsoft.com/fwlink/p/?linkid=403360">Instalar Office</A></P>
> <LI>
> <P><A href="http://go.microsoft.com/fwlink/p/?linkid=403361">¿Necesita ayuda con la clave de producto de Office?</A></P></LI></UL>Si desea introducir una clave de producto en un servidor de Exchange 2010, vaya a <A href="http://go.microsoft.com/fwlink/p/?linkid=403370">Introducir una clave de producto de Exchange 2010</A>.<BR>Si desea introducir una clave de producto en un servidor de Exchange&nbsp;2013, ¡está en el sitio adecuado! Siga leyendo.



## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar este procedimiento: menos de 5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Clave de producto" en el tema [Permisos de infraestructura de la Shell y de Exchange](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Si activa la licencia de un servidor de Exchange en el que se ejecuta el rol de servidor Buzón de correo, necesitará reiniciar el servicio Almacén de información de Microsoft Exchange en el servidor después de introducir la clave de producto.

  - Si desea actualizar un servidor de Exchange desde una edición estándar a una empresarial, siga los pasos que se indican en este tema.

  - Si desea degradar un servidor de Exchange de una licencia de edición empresarial a una edición estándar, deberá reinstalar Exchange.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Usar el EAC para especificar la clave del producto

1.  Abra el EAC navegando hasta https://\<*Nombre de servidor de acceso de cliente*\>/ecp.

2.  Escriba su nombre de usuario y contraseña en **Dominio\\nombre de usuario** y **Contraseña** y, a continuación, haga clic en **Iniciar sesión**.

3.  Vaya a **Servidores** \> **Servidores**. Seleccione el servidor para el que desee obtener una licencia y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

4.  (Opcional) Si desea actualizar un servidor de una licencia Standard Edition a una licencia Enterprise Edition, en la página **General**, seleccione **Cambiar la clave del producto**. Solo verá esta opción si el servidor ya dispone de licencia.

5.  En la página **General**, especifique su clave de producto en los cuadros de texto **Escriba una clave de producto válida**.

6.  Haga clic en **Guardar**.

7.  Si activo una licencia para un servidor de Exchange en el que se ejecuta el rol de servidor de Buzón de correo, realice el siguiente procedimiento para reiniciar el servicio Almacén de Información de Microsoft Exchange:
    
    1.  Abra **Panel de control**, vaya a **Herramientas administrativas** y, a continuación, abra **Servicios**.
    
    2.  Haga clic con el botón secundario en **Almacén de información de Microsoft Exchange** y, a continuación, haga clic en **Reiniciar**.

## Uso del Shell para especificar la clave del producto

En este ejemplo se usa el cmdlet **set-ExchangeServer** para especificar la clave del producto.


> [!NOTE]
> Puede volver a ejecutar este comando en el mismo servidor para actualizarlo de una licencia Standard&nbsp;Edition a una licencia Enterprise&nbsp;Edition.



    Set-ExchangeServer ExServer01 -ProductKey aaaaa-aaaaa-aaaaa-aaaaa-aaaaa

Para obtener información detallada acerca de las sintaxis y los parámetros, consulte [Set-ExchangeServer](https://technet.microsoft.com/es-es/library/bb123716\(v=exchg.150\)).

Si activo una licencia para un servidor de Exchange en el que se ejecuta el rol de servidor de Buzón de correo, realice el siguiente procedimiento para reiniciar el servicio Almacén de Información de Microsoft Exchange:

1.  Abra **Panel de control**, vaya a **Herramientas administrativas** y, a continuación, abra **Servicios**.

2.  Haga clic con el botón derecho en **Almacén de información de Microsoft Exchange** y luego haga clic en **Reiniciar**.

## ¿Cómo saber si el proceso se ha completado correctamente?

Haga lo siguiente para usar el EAC con objeto de confirmar que se ha obtenido una licencia correctamente en el servidor como Standard Edition o Enterprise Edition:

1.  Escriba su nombre de usuario y contraseña en **Dominio\\nombre de usuario** y **Contraseña** y, a continuación, haga clic en **Iniciar sesión**.

2.  Vaya a **Servidores** \> **Servidores**.

3.  Seleccione el servidor que desee ver y, a continuación, consulte el panel de detalles del servidor. Si la clave de producto se ha aceptado, **Con licencia** aparecerá junto a la edición de Exchange 2013.

Haga lo siguiente para usar el Shell con objeto de confirmar que se ha obtenido una licencia correctamente en el servidor como Standard Edition o Enterprise Edition:

1.  Abra el Shell.

2.  Ejecute el siguiente comando para consultar el estado de la licencia de un servidor de Exchange concreto.
    
        Get-ExchangeServer ExServer01 | Format-Table Edition,*Trial*

3.  (Opcional) Ejecute el siguiente comando para ver el estado de la licencia de todos los servidores Exchange de su organización.
    
        Get-ExchangeServer | Format-Table Name, Edition, *Trial* -Auto

