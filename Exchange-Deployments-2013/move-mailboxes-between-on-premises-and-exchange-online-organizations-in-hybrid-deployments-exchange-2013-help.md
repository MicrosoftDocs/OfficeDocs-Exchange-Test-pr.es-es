---
title: 'Mover buzones de correo entre organizaciones locales y de Exchange Online en implementaciones híbridas: Exchange 2013 Help'
TOCTitle: Mover buzones de correo entre organizaciones locales y de Exchange Online en implementaciones híbridas
ms:assetid: d6289f7b-f67e-48db-9570-9fd3c9547548
ms:mtpsurl: https://technet.microsoft.com/es-es/library/o365e_hrcmoverequest_fl312271(v=EXCHG.150)
ms:contentKeyID: 51406227
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Mover buzones de correo entre organizaciones locales y de Exchange Online en implementaciones híbridas

 

_<strong>Se aplica a:</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>Última modificación del tema:</strong>2017-10-02_

Con una implementación híbrida basada en Exchange, puede elegir si desea mover los buzones de correo de Exchange locales a la organización de Exchange Online o mover los buzones de correo de Exchange Online a la organización de Exchange. Cuando mueve los buzones de correo entre las organizaciones locales y de Exchange Online, usa lotes de migración para realizar la solicitud de movimiento remoto de buzones de correo. Este enfoque le permite mover los buzones de correo existentes en lugar de crear nuevos buzones de usuario e importar la información de los usuarios. Este enfoque es distinto a la migración de buzones de usuario desde una organización de Exchange local a Exchange Online como parte de una migración completa de Exchange a la nube. Los movimientos de buzones de correo se describen en este tema como parte de la administración de Exchange en una relación de coexistencia a largo plazo entre una organización de Exchange local y una organización de Exchange Online.

Para obtener más información acerca de cómo migrar organizaciones de Exchange locales a Exchange Online, consulte [Formas de migrar varias cuentas de correo electrónico a Office 365](https://support.office.com/es-es/article/formas-de-migrar-varias-cuentas-de-correo-electr%c3%b3nico-a-office-365-0a4913fe-60fb-498f-9155-a86516418842?ui=es-es%26rs=es-es%26ad=es).


> [!IMPORTANT]
> Debe tener configurada una implementación híbrida entre sus organizaciones locales y las organizaciones de Exchange Online para poder completar los procedimientos sobre movimientos de buzones de correo que se describen en este tema. Para obtener más información acerca de implementaciones híbridas, consulte <A href="exchange-server-hybrid-deployments-exchange-2013-help.md">Implementaciones híbridas de Exchange Server</A>.<BR><BR>Antes de mover a Exchange Online los buzones habilitados para mensajería unificada (UM), debe asegurarse de que Skype Empresarial 2015, Skype Empresarial Online y Exchange Online locales cumplen los requisitos especificados en <A href="hybrid-deployment-prerequisites-exchange-2013-help.md">Requisitos previos de implementación híbrida</A>. Para obtener información sobre cómo asignar sus directivas de buzón de mensajería unificada locales a las directivas de Exchange Online, consulte <A href="https://technet.microsoft.com/es-es/library/bb124903(v=exchg.150)">Set-UMMailboxPolicy</A>.



## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 10 minutos para configurar el lote de migración, aunque el tiempo total para completar la migración depende del número de buzones de correo que contiene cada lote de migración.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Sección "Permisos de movimiento y migración de buzones" en el tema [Permisos de destinatarios](https://technet.microsoft.com/es-es/library/dd638132\(v=exchg.150\)).

  - La implementación híbrida está configurada entre su organización local y la organización de Exchange Online.

  - Si ejecuta Exchange 2013, asegúrese de que el servicio de proxy de replicación de buzones (MRSProxy) está habilitado en sus servidores locales de acceso de cliente de Exchange 2013.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](https://technet.microsoft.com/es-es/library/jj150484\(v=exchg.150\)).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Paso 1: Crear un extremo de migración

Antes de realizar migraciones de movimientos remotos de carga y descarga en una implementación híbrida de Exchange, recomendamos crear extremos de migración remota de Exchange. El extremo de migración contiene la configuración de conexión de un servidor local de Exchange que se ejecuta en el servicio de proxy MRS, que es necesario para realizar las migraciones de movimientos remotos desde Exchange Online y hacia esta aplicación.

Para conocer los procedimientos paso a paso, vea Crear extremos de migración.

## Paso 2: Habilitar el servicio de MRSProxy

Si el servicio de MRSProxy todavía no está habilitado en sus servidores locales de acceso de cliente de Exchange 2013, siga estos pasos en el Centro de administración de Exchange (EAC):

1.  Abra el EAC y vaya a **Servidores** \> **Directorios virtuales**.

2.  Seleccione el servidor de acceso de cliente y luego seleccione el directorio virtual **EWS** y haga clic en **Editar**![Icono Editar](images/JJ906432.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  Active la casilla **MRS Proxy habilitado** y luego haga clic en **Guardar**.

## Paso 3: Usar el EAC para mover buzones de correo

Puede usar el asistente de migración de movimientos remotos en la pestaña **Office 365** del EAC en un servidor de Exchange para mover los buzones de usuario existentes en la organización local a la organización de Exchange Online, o bien mover los buzones de correo de Exchange Online a la organización local. Realice uno de los procedimientos siguientes:

## Mover buzones de correo locales a Exchange Online

Puede usar el asistente de migración de movimientos remotos en la pestaña **Office 365** del EAC en un servidor de Exchange para mover los buzones de usuario existentes en la organización local a la organización de Exchange Online. Siga estos pasos:

1.  Abra el EAC y vaya a **Office 365** \> **Destinatarios** \> **Migración**.

2.  Haga clic en **Agregar** ![Agregar icono](images/JJ906432.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") y seleccione **Migrar a Exchange Online**.

3.  En la página **Seleccionar tipo de migración**, seleccione **Migración de movimiento remoto** y luego haga clic en **Siguiente**.

4.  En la página **Seleccionar usuarios**, haga clic en **Agregar**![Agregar icono](images/JJ906432.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") y seleccione los usuarios locales que quiere mover a Office 365. A continuación, haga clic en **Agregar** y luego en **Aceptar**. Haga clic en **Siguiente**.

5.  En la página **Introducir credenciales de cuenta de usuario de Windows**, escriba el nombre de cuenta del administrador local en el campo de texto **Nombre de administrador local** y escriba la contraseña asociada a esta cuenta en el campo de texto **Contraseña de administrador local**. Por ejemplo, “corp\\administrator” y una contraseña. Haga clic en **Siguiente**.
    

    > [!NOTE]
    > Si ya ha creado un extremo de migración, recibirá un mensaje de confirmación del extremo en este paso. Si ha creado dos o más extremos de migración, deberá seleccionar uno de ellos en el menú desplegable de extremos de migración.



6.  En la página **Confirmar el extremo de migración**, compruebe que el FDQN de su servidor local de Exchange aparece cuando el asistente confirma el extremo de migración. Por ejemplo, "mail.contoso.com". Haga clic en **Siguiente**.
    

    > [!NOTE]
    > El servicio de MRSProxy de los servidores de Exchange limita automáticamente las solicitudes de movimiento de buzones de correo al seleccionar varios buzones para moverlos a Exchange Online. El tiempo total para completar el movimiento de buzones depende del número total de buzones de correo seleccionados, el tamaño de los buzones y la configuración de MRSProxy. Para más información sobre la personalización de MRSProxy, vea <A href="https://technet.microsoft.com/es-es/library/bb232205(v=exchg.150)">Limitación de mensajes</A>.



7.  En la página **Mover configuración**, escriba un nombre para el lote de migración en el campo de texto **Nombre del nuevo lote de migración**. Use la flecha abajo ![Icono flecha abajo](images/JJ906432.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif "Icono flecha abajo") para seleccionar el **dominio de entrega de destino para los buzones de correo que se están migrando a Office 365**. En la mayoría de las implementaciones híbridas, este es el dominio SMTP principal que se usa para los buzones de correo de organizaciones de Exchange Online. Por ejemplo, contoso.mail.onmicrosoft.com. Compruebe que la opción **Mover el buzón principal junto con el buzón de archivo** está seleccionada y luego haga clic en **Siguiente**.

8.  En la página **Iniciar el lote**, seleccione como mínimo un destinatario para que reciba el informe completo del lote. Compruebe que la opción **Iniciar automáticamente el lote** esté seleccionada y luego active la casilla **Completar automáticamente el lote de migración**. Haga clic en **Nueva**.

## Mover buzones de correo de Exchange Online a la organización local

Puede usar el asistente de migración de movimientos remotos en la pestaña **Office 365** del EAC en un servidor de Exchange para mover los buzones de usuario existentes en la organización local a la organización de Exchange Online:

1.  Abra el EAC y vaya a **Office 365** \> **Destinatarios** \> **Migración**.

2.  Haga clic en **Agregar** ![Agregar icono](images/JJ906432.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") y seleccione **Migrar desde Exchange Online**.

3.  En la página **Seleccionar usuarios**, seleccione **Seleccionar usuarios que desea desplazar** y haga clic en **Siguiente**.

4.  En la página **Seleccionar usuarios**, haga clic en **Agregar**![Agregar icono](images/JJ906432.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") y seleccione los usuarios de Exchange Online que desea desplazar a la organización local. A continuación, haga clic en **Agregar** y luego en **Aceptar**. Haga clic en **Siguiente**.

5.  En la página **Confirmar el extremo de migración**, compruebe que el FDQN de su servidor local de Exchange aparece cuando el asistente confirma el extremo de migración. Por ejemplo, "mail.contoso.com". Haga clic en **Siguiente**.
    

    > [!NOTE]
    > El servicio de MRSProxy de los servidores de Exchange limita automáticamente las solicitudes de movimiento de buzones de correo al seleccionar varios buzones para moverlos a Exchange Online. La duración total para completar el movimiento de buzones depende del número de buzones seleccionados, su tamaño y las propiedades de MRSProxy. Para más información sobre la personalización de MRSProxy, vea <A href="https://technet.microsoft.com/es-es/library/bb232205(v=exchg.150)">Limitación de mensajes</A>.



6.  En la página **Configuración de la transferencia**, escriba un nombre para el lote de migración en el campo de texto **Nombre del nuevo lote de migración**. Después, escriba el dominio de entrega de destino en el campo **Dominio de entrega de destino para los buzones de correo que se están migrando a Office 365**. En la mayoría de las implementaciones híbridas, este es el dominio SMTP principal que se usa tanto para los buzones de correo de organizaciones locales como para buzones de organizaciones de Exchange Online. Por ejemplo, contoso.com.

7.  Seleccione si también quiere mover los buzones de archivo para los usuarios seleccionados y escriba el nombre de la base de datos donde quiere mover este buzón en el campo de texto **Base de datos de destino**. Por ejemplo, Base de datos de buzones 123456789. Haga clic en **Siguiente**.

8.  En la página **Iniciar el lote**, seleccione como mínimo un destinatario para que reciba el informe completo del lote. Compruebe que la opción **Iniciar automáticamente el lote** esté seleccionada y luego active la casilla **Completar automáticamente el lote de migración**. Haga clic en **Nueva**.

## Paso 4: Quitar los lotes de migración completados

Tras haber completado el movimiento de buzones de correo, recomendamos quitar los lotes de migración completados para minimizar las posibilidades de error en caso de volver a mover a los mismos usuarios.

Para quitar un lote de migración completado:

1.  Abra el EAC y vaya a **Office 365** \> **Destinatarios** \> **Migraciones**.

2.  Haga clic en un lote de migración completado y luego haga clic en **Eliminar** ![Eliminar icono](images/JJ906432.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Eliminar icono").

3.  En el diálogo de confirmación de advertencia de eliminación, haga clic en **Sí**.

## Paso 5: Rehabilitar el acceso sin conexión para Outlook en la web

El acceso sin conexión en Outlook en la web (antes conocido como Outlook Web App) permite a los usuarios obtener acceso a sus buzones de correo cuando no están conectados a una red. Si migra los buzones de correo de Exchange a Exchange Online, los usuarios deberán restablecer la configuración de acceso sin conexión en sus exploradores para poder usar Outlook en la web sin conexión. Para obtener más información acerca del acceso sin conexión en Outlook en la web, de los exploradores que lo admiten y de cómo activarlo, consulte [Using Outlook Web App offline (Usar Outlook Web App sin conexión)](https://go.microsoft.com/fwlink/p/?linkid=286942).

## ¿Cómo saber si el proceso se ha completado correctamente?

Cuando mueva buzones de usuario existentes entre organizaciones locales y de Exchange Online, la finalización con éxito del asistente de movimiento remoto será la primera indicación de que el movimiento de buzones se completará tal como se esperaba.

Dado que el proceso de movimiento de buzones tarda unos minutos en completarse, también puede comprobar que el movimiento se está realizando correctamente si abre el EAC y selecciona **Office 365** \> **Destinatarios** \> **Migración** para ver el estado del movimiento de los buzones seleccionados en el asistente. El valor de **Estado** es **Sincronizando** durante el movimiento de buzones, mientras que aparecerá **Finalizado** cuando se hayan movido correctamente tanto a la organización local como a la organización de Exchange Online.

Cuando el proceso de movimiento de buzones haya finalizado, compruebe las propiedades del buzón para asegurarse de que el buzón remoto ubicado en la organización local o de Exchange Online se ha movido correctamente. Para ello, vaya a **Destinatarios** \> **Buzones** en el EAC de la organización local o de la organización de Exchange Online. El buzón de usuario deberá mostrar un **Tipo de buzón** de **Office 365** para buzones de Exchange Online y **Usuario** para los buzones locales.

También puede ejecutar el siguiente cmdlet en el Shell de administración de Exchange para comprobar el estado del lote de migración.

    Get-MigrationBatch -Identity <batch name>

¿Problemas? Solicite ayuda en los foros de Office 365. Para obtener acceso a los foros, deberá iniciar sesión con una cuenta que tenga acceso de administrador al servicio basado en la nube. Visite los foros en: [Foros de Office 365](https://go.microsoft.com/fwlink/p/?linkid=201915)

## ¿Es la primera vez que usa Office 365?


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/Dn249373.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="Icono reducido de LinkedIn Learning" alt="Icono reducido de LinkedIn Learning" /> <strong>¿Es la primera vez que usa Office 365?</strong><br />
LinkedIn Learning pone a su disposición vídeos gratuitos de cursos de <a href="https://support.office.com/es-es/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a>.</p></td>
</tr>
</tbody>
</table>

