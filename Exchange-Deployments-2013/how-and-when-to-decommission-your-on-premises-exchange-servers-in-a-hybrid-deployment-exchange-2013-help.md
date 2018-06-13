---
title: 'Cómo y cuándo se deben retirar los servidores de Exchange locales en una implementación híbrida: Exchange 2013 Help'
TOCTitle: Cómo y cuándo se deben retirar los servidores de Exchange locales en una implementación híbrida
ms:assetid: 4f884b7a-3b8a-4207-8843-65d3141731dc
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn931280(v=EXCHG.150)
ms:contentKeyID: 64966458
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Cómo y cuándo se deben retirar los servidores de Exchange locales en una implementación híbrida

 

_**Se aplica a:**Exchange Online, Exchange Server, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2017-07-27_

Lea este artículo si está listo para pasar de una implementación híbrida de Exchange a una implementación completa de nube.

Una de las opciones más atractivas para conseguir una empresa Exchange Online es utilizar el enfoque de implementación híbrida descrito en [implementación híbrida de Exchange y migración de Office 365](https://msdn.microsoft.com/en-us/library/ff633682\(v=exchsrvcs.149\).aspx). Esta es la única opción que le permite fácilmente a bordo y off board buzones (todas las demás opciones nativos a bordo sólo están). Además de la capacidad de off-board, una configuración híbrida tiene las siguientes opciones de clave.

Este tema le ayudará a comprender las opciones para dar de baja el híbrido de Exchange y deben implementarse cuando cada una de las opciones. Hay muchas variaciones en cuándo y cómo dar de baja los servidores de Exchange híbrido. Es importante tomarse el tiempo para comprender las implicaciones y planificar adecuadamente el desmantelamiento total o parcial de los servidores locales.

  - **Disponibilidad entre locales**. Permite ver la información de disponibilidad de un usuario al programar una reunión, independientemente del local del buzón.

  - **Archivo entre locales**. Permite mover solo el buzón de archivo de un usuario a la nube. Este suele ser el primer paso para que los clientes prueben Office 365 y, más específicamente, Exchange Online.

  - **Búsquedas de detección entre locales**. Permite a un cliente realizar una búsqueda de exhibición de documentos electrónicos que rastreará los buzones y los archivos en ambos locales (requiere configurar la autenticación OAuth).

  - **Outlook Web App Redireccionamiento de URL**. Permite redireccionar los usuarios a los locales adecuados para el acceso a Outlook Web App.

  - **El perfil no se vuelve a crear después del traslado**. A diferencia de otras opciones de migración, el GUID del buzón no cambia. Esto significa que no tendrá que volver a crear el perfil y volver a descargar el archivo OST después de trasladar un buzón.

Dependiendo de las necesidades de su organización, una implementación híbrida es la mejor opción para proporcionar la experiencia de usuario y la coexistencia más fluida.

## Otros métodos para migrar a Exchange Online

Una implementación híbrida no es para todos los usuarios; de hecho, hay generalmente mejores opciones. Muchos de los inquilinos que han decidido implementar una configuración híbrida son menores de cincuenta asientos. Mientras que la lista de las ventajas de una implementación híbrida puede parecer atractiva, viene con un precio considerable con respecto a la complejidad. Algunos de los inquilinos más pequeños requieren las características de una implementación híbrida, pero para la mayoría de los inquilinos, es una experiencia mucho mejor utilizar ya sea un traslado, por etapas, o la opción de migración de IMAP. Hay un programa llamado FastTrack puede utilizar al decidir el proceso de migración a tomar. Información sobre FastTrack se describe en la [página de Office 365 FastTrack](https://go.microsoft.com/fwlink/?linkid=846696).

Utilice la tabla siguiente para decidir qué tipo de migración que funciona en la organización. (Para obtener más información, vea [formas de migrar varias cuentas de correo electrónico a Office 365](https://support.office.com/en-us/article/ways-to-migrate-multiple-email-accounts-to-office-365-0a4913fe-60fb-498f-9155-a86516418842?ui=en-us%26rs=en-sg%26ad=sg))


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Organización existente</th>
<th>Número de buzones que se van a migrar</th>
<th>¿Desea administrar cuentas de usuario en su organización local?</th>
<th>Tipo de migración</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2013, Exchange 2010, Exchange 2007 o Exchange 2003</p></td>
<td><p>Menos de 2.000 buzones</p></td>
<td><p>No</p></td>
<td><p>Migración de Exchange de traslado</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2007 o Exchange 2003</p></td>
<td><p>Menos de 2.000 buzones</p></td>
<td><p>No</p></td>
<td><p>Migración de Exchange preconfigurada</p></td>
</tr>
<tr class="odd">
<td><p>Exchange 2007 o Exchange 2003</p></td>
<td><p>Más de 2.000 buzones*</p></td>
<td><p>Sí</p></td>
<td><p>Migración preconfigurada de Exchange o migración de movimiento remoto en una implementación híbrida de Exchange</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013 o Exchange 2010</p></td>
<td><p>Más de 2.000 buzones*</p></td>
<td><p>Sí</p></td>
<td><p>Migración de movimiento remoto en una implementación híbrida de Exchange</p></td>
</tr>
<tr class="odd">
<td><p>Exchange 2000 Server o versiones anteriores</p></td>
<td><p>Sin máximo</p></td>
<td><p>Sí</p></td>
<td><p>Migración de IMAP</p></td>
</tr>
<tr class="even">
<td><p>Sistema de mensajería local distinto de Exchange</p></td>
<td><p>Sin máximo</p></td>
<td><p>Sí</p></td>
<td><p>Migración de IMAP</p></td>
</tr>
</tbody>
</table>


\* Algunas organizaciones con menos de 2.000 buzones pueden beneficiarse de características y funcionalidades que sólo están disponibles con una implementación híbrida. Es importante considerar detenidamente las ventajas de una implementación híbrida con la complejidad que presenta. Se recomienda encarecidamente que los clientes con menos de 2.000 buzones considerar traslados o almacenados provisionalmente la migración antes de continuar con una implementación híbrida.

## Por qué podría no querer retirar servidores de Exchange de local

Los clientes con una configuración híbrida suelen encontrar que, después de tiempo, todos sus buzones se movieron a Exchange Online. En este punto, pueden decidir quitar los servidores de Exchange de local. Sin embargo, descubren que ya no pueden administrar sus buzones de nube.

Cuando la sincronización de directorios está habilitada para un inquilino y un usuario se sincroniza desde local, la mayoría de los atributos no se pueden administrar desde Exchange Online y deben administrarse desde local. Esto no es debido a la configuración híbrida, se produce debido a la sincronización de directorios. Además, aunque tenga activada la sincronización de directorios sin ejecutar el Asistente para la configuración híbrida, sigue sin poder administrar la mayoría de las tareas de destinatarios desde la nube. Para obtener más información, consulte este [blog de TechNet](http://blogs.technet.com/b/exchange/archive/2012/12/05/decommissioning-your-exchange-2010-servers-in-a-hybrid-deployment.aspx).

## ¿Se pueden usar herramientas de administración de terceros?

Una pregunta frecuente es si se pueden usar herramientas de administración de terceros o ADSIEDIT. La respuesta es que se pueden usar, pero no están admitidas. La Consola de administración de Exchange, el Centro de administración de Exchange (EAC) y el Shell de administración de Exchange son las únicas herramientas admitidas que hay disponibles para administrar destinatarios y objetos de Exchange. Si decide usar las herramientas de administración de terceros, sería bajo su propio riesgo. Las herramientas de administración de terceros suelen funcionar bien, pero Microsoft no las valida.

## Escenarios comunes

No es fácil cambiar de una configuración híbrida a la nube. Nos llevó mucho tiempo definir el proceso correcto para establecer una configuración híbrida. Aunque haya problemas, creemos haber hecho un buen trabajo y conseguimos la misión casi imposible de pasar a híbrido con un proceso basado en asistente bastante sencillo.

Sin embargo, hemos trabajado poco en cómo pasar de una configuración híbrida a solo nube. Dependiendo de sus objetivos inmediatos, este proceso puede ser bastante sencillo con alguna orientación. Los siguientes son tres escenarios híbridos habituales y nuestra recomendación sobre cómo lograr adecuadamente el objetivo final del cliente.

Como la base de clientes híbridos es muy diversa, tratar de ajustarlos todos a escenarios "comunes" es difícil. Tratamos de proporcionar algunos escenarios genéricos para la retirada de servidores de Exchange Server locales. Cuando lea estos escenarios y elabore un plan de retirada, deberá determinar cuál se adapta a sus necesidades.

## Escenario uno

**Problema:** mi organización se ha estado ejecutando en una configuración híbrida y tengo todos mis buzones de Exchange Online. No es necesario administrar Mis usuarios de local y ya no tiene necesidad de sincronización de directorios o la sincronización de contraseña.

**Solución:** Como todos los usuarios se administrarán en Office 365 y no hay requisitos adicionales de sincronización de directorios, puede deshabilitar la sincronización de directorios de forma segura y quitar Exchange del entorno local.

![Quitar Exchange del entorno local](images/Dn931280.f9c2a2cb-4c16-4ca3-8244-b89c1cdf0744(EXCHG.150).jpg "Quitar Exchange del entorno local") Para deshabilitar la sincronización de directorios y desinstalar la implementación híbrida de Exchange

1.  Ejecute `Get-OrganizationConfig |fl PublicFoldersEnabled` y asegúrese de que no se establece en el control remoto. Si se establece en el control remoto y las carpetas públicas son algo que desea seguir teniendo acceso a, deberá migrarlos a Exchange Online. Para obtener más información, consulte [Usar la migración por lotes para migrar carpetas públicas heredadas a Office 365 y Exchange Online](https://technet.microsoft.com/es-es/library/dn874017\(v=exchg.150\)).

2.  Si ya movió todos los buzones a Exchange Online, puede apuntar los registros MX y DNS de detección automática a Exchange Online, en lugar de a local. Para obtener más información, consulte [Referencia: Registros externos del Sistema de nombres de dominio para Office 365](http://technet.microsoft.com/es-es/library/hh852557.aspx).
    

    > [!IMPORTANT]
    > Asegúrese de actualizar el DNS interno y externo o el comportamiento de la conectividad del cliente será incoherente.



3.  Después, debe quitar los valores de punto de conexión de servicio (SCP) en los servidores de Exchange. Esto garantiza que no se devolverá ningún SCP y que el cliente usará en su lugar el método DNS de detección automática. A continuación se muestra un ejemplo:
    
        Get-ClientAccessServer | Set-ClientAccessServer -AutoDiscoverServiceInternalUri $Null
    

    > [!NOTE]
    > Si tiene servidores de Exchange 2007 en el entorno, tendrá que ejecutar un comando similar en los servidores de Exchange 2007 para anular la configuración.



4.  Hay conectores de entrada y de salida creados por el Asistente para la configuración híbrida que querrá eliminar. Para ello, siga estos pasos:
    
    1.  Inicie sesión en el [portal de administración de Office 365](http://portal.office.com) e inicie sesión como administrador de inquilinos.
    
    2.  Seleccione la opción para administrar **Exchange**.
    
    3.  Vaya a **Flujo de correo** -\> **Conexión**.
    
    4.  Ahora, puede desactivar o eliminar los conectores de entrada y de salida. El HCW crea conectores con un espacio de nombres único **enlace interno desde \<identificador único\>** y **enlace externo desde \<identificador único\>** como se muestra en el gráfico siguiente.
        
        ![El Asistente para la configuración híbrida crea conectores con un espacio de nombres único](images/Dn931280.7b1b6f0b-43d6-4407-8cd7-7dd52e016697(EXCHG.150).jpg "El Asistente para la configuración híbrida crea conectores con un espacio de nombres único")  

5.  Quite la relación de organización creada por el Asistente para la configuración híbrida. Para ello, siga estos pasos:
    
    1.  Inicie sesión en el [portal de administración de Office 365](http://portal.office.com) e inicie sesión como administrador de inquilinos.
    
    2.  Seleccione la opción para administrar Exchange.
    
    3.  Vaya a **Organización**.
    
    4.  En **Uso compartido de la organización**, quite la organización llamada **O365 a local: \<identificador único\>** como se muestra en el gráfico siguiente.
        
        ![Quite la relación de organización creada por el Asistente para la configuración híbrida.](images/Dn931280.2f0c1077-8785-487a-87a5-a75f0a4f0fea(EXCHG.150).jpg "Quite la relación de organización creada por el Asistente para la configuración híbrida.")  

6.  Si OAuth está configurado para una implementación híbrida Exchange, querrá deshabilitar la configuración tanto de local como de Office 365. En la mayoría de los entornos, puede omitir estos pasos porque solo un pequeño conjunto de nuestros clientes tienen OAuth configurado.
    
    Para deshabilitar la configuración local:
    
    1.  Abra el Shell de administración de Exchange desde un servidor de Exchange 2013.
    
    2.  Ejecute el siguiente comando:
        
            Get-IntraorganizationConnector -Identity ExchangeHybridOnPremisesToOnline | Set-IntraOrganizationConnector -Enabled $False
    
    Para deshabilitar la configuración de Exchange Online:
    
    1.  Conecte Windows PowerShell con Exchange Online.
    
    2.  Ejecute el siguiente comando:
        
            Run Get-IntraorganizationConnector -Identity ExchangeHybridOnlineToOnPremises | Set-IntraOrganizationConnector -Enabled $False
        
        El parámetro *Identity* da por hecho que usó el Asistente para la configuración híbrida para configurar OAuth. Si no es así, deberá ajustar el valor especificado para la identidad de los conectores.

7.  Deshabilite la sincronización de directorios para los inquilinos. Cuando haya completado este paso, se realizarán todas las tareas de administración de usuarios desde las herramientas de administración de Office 365. Esto significa que ya no usará la Consola de administración de Exchange o el Centro de administración de Exchange (EAC). Para obtener más información acerca de cómo deshabilitar la sincronización de directorios, consulte [Desactivar la sincronización de directorios](https://technet.microsoft.com/es-es/library/dn144760.aspx).

8.  Ahora puede desinstalar Exchange de los servidores locales con seguridad.

## Escenario dos

**Problema:** Mi organización se estuvo ejecutando en una configuración híbrida durante casi un año y finalmente se movió el último buzón a la nube. Planeo mantener los Servicios de federación de Active Directory (AD FS) para la autenticación de usuarios de mis buzones de Exchange Online. (Este escenario sería aplicable a cualquier cliente que tenga planeado mantener la sincronización de directorios).

**Solución:** Como el cliente tiene planeado mantener AD FS, también tendrá que mantener la sincronización de directorios porque es un requisito previo. Por eso, no puede quitar completamente los servidores de Exchange del entorno local. Sin embargo, puede retirar la mayoría de los servidores de Exchange y dejar un par de servidores para la administración de usuarios. Tenga en cuenta que los servidores que se dejan en ejecución se pueden ejecutar en máquinas virtuales, ya que la carga de trabajo se traslada casi por completo a Exchange Online.

El siguiente gráfico describe el estado final deseado:

![Retirar servidores de Exchange manteniendo algunos](images/Dn931280.d7734579-6999-45b2-9a0f-a23f18353a49(EXCHG.150).jpg "Retirar servidores de Exchange manteniendo algunos")

El siguiente gráfico describe el estado final real:

![Estado antes de retirar servidores de Exchange](images/Dn931280.c692f0af-6536-4bc9-950d-58a1e486525f(EXCHG.150).jpg "Estado antes de retirar servidores de Exchange") Para mantener AD FS y la sincronización de directorios, y retirar la mayoría de los servidores de Exchange

1.  Ejecute `Get-OrganizationConfig |fl PublicFoldersEnabled` y asegúrese de que no está establecido en remoto. Si está establecido en remoto y quiere seguir accediendo a las carpetas públicas, necesitará migrarlas a Exchange Online. Para obtener información sobre cómo hacerlo, consulte [Usar la migración por lotes para migrar carpetas públicas heredadas a Office 365 y Exchange Online](https://technet.microsoft.com/es-es/library/dn874017\(v=exchg.150\)).
    

    > [!IMPORTANT]
    > Si la migración de carpetas públicas a Exchange Online no es una opción y aún las necesita para los usuarios, no debe seguir adelante.



2.  Después de mover todos los buzones a Exchange Online, lo primero que querrá hacer para retirar la mayor parte de los servidores Exchange es apuntar los registros MX y DNS de detección automática a Exchange Online en lugar de a local. Para obtener más información, consulte [Referencia: Registros externos del Sistema de nombres de dominio para Office 365](http://technet.microsoft.com/es-es/library/hh852557.aspx).
    

    > [!IMPORTANT]
    > Asegúrese de actualizar el DNS interno y externo o el comportamiento de la conectividad del cliente y del flujo de correo será incoherente.



3.  Después, debe quitar los valores de punto de conexión de servicio (SCP) en los servidores de Exchange. Esto garantiza que no se devolverá ningún SCP y que el cliente usará en su lugar el método DNS de detección automática. A continuación se muestra un ejemplo:
    
        Get-ClientAccessServer | Set-ClientAccessServer -AutoDiscoverServiceInternalUri $Null
    

    > [!NOTE]
    > Si tiene servidores de Exchange 2007 en el entorno, tendrá que ejecutar un comando similar en los servidores de Exchange 2007 para anular la configuración.



4.  Para evitar que se vuelvan a crear objetos de configuración híbrida en el futuro, debe quitar el objeto de configuración híbrida de Active Directory. Para ello, abra el Shell de administración de Exchange y ejecute lo siguiente:
    
        Remove-HybridConfiguration

5.  Quite todos los servidores de Exchange, excepto los servidores que conservará para la creación y administración de usuarios. Dos servidores deberían ser suficientes para la administración de usuarios, aunque posiblemente sea suficiente con uno. Además, no es necesario tener un grupo de disponibilidad de la base de datos ni otras opciones de alta disponibilidad.

6.  Si OAuth está configurado para una implementación híbrida Exchange, querrá deshabilitar la configuración tanto de local como de Office 365. En la mayoría de los entornos, puede omitir estos pasos porque solo un pequeño conjunto de nuestros clientes tienen OAuth configurado.
    
    Para deshabilitar la configuración local:
    
    1.  Abra el Shell de administración de Exchange desde un servidor de Exchange 2013.
    
    2.  Ejecute el siguiente comando:
        
            Get-IntraorganizationConnector -Identity ExchangeHybridOnPremisesToOnline | Set-IntraOrganizationConnector -Enabled $False
    
    Para deshabilitar la configuración de Exchange Online:
    
    1.  Conecte Windows PowerShell con Exchange Online.
    
    2.  Ejecute el siguiente comando:
        
            Run Get-IntraorganizationConnector -Identity ExchangeHybridOnlineToOnPremises | Set-IntraOrganizationConnector -Enabled $False
        
        El parámetro Identity da por hecho que usó el Asistente para la configuración híbrida para configurar OAuth. Si no es así, deberá ajustar el valor especificado para la identidad de los conectores.

7.  Hay conectores de entrada y de salida creados por el Asistente para la configuración híbrida que querrá eliminar. Para ello, siga estos pasos:
    
    1.  Inicie sesión en el [portal de administración de Office 365](http://portal.office.com) e inicie sesión como administrador de inquilinos.
    
    2.  Seleccione la opción para administrar **Exchange**.
    
    3.  Vaya a **Flujo de correo** -\> **Conectores**.
    
    4.  Ahora, puede desactivar o eliminar los conectores de entrada y de salida. El HCW crea conectores con un espacio de nombres único **enlace interno desde \<identificador único\>** y **enlace externo desde \<identificador único\>** como se muestra en el gráfico siguiente.
        
        ![El Asistente para la configuración híbrida crea conectores con un espacio de nombres único](images/Dn931280.7b1b6f0b-43d6-4407-8cd7-7dd52e016697(EXCHG.150).jpg "El Asistente para la configuración híbrida crea conectores con un espacio de nombres único")  

8.  Quite la relación de organización creada por el Asistente para la configuración híbrida. Para ello, siga estos pasos:
    
    1.  Inicie sesión en el [portal de administración de Office 365](http://portal.office.com) e inicie sesión como administrador de inquilinos.
    
    2.  Seleccione la opción para administrar **Exchange**.
    
    3.  Vaya a **Organización**.
    
    4.  En **Uso compartido de la organización**, quite la organización llamada **O365 a local: \<identificador único\>** como se muestra en el gráfico siguiente.
        
        ![Quite la relación de organización creada por el Asistente para la configuración híbrida.](images/Dn931280.2f0c1077-8785-487a-87a5-a75f0a4f0fea(EXCHG.150).jpg "Quite la relación de organización creada por el Asistente para la configuración híbrida.")  

## Escenario tres

**Problema:** Quiero quitar mis servidores locales de Exchange después de mover todos los buzones a Exchange Online. Sin embargo, descubrimos que usan Exchange para otros fines, por ejemplo, para una retransmisión del Protocolo simple de transferencia de correo (SMTP) para una aplicación o para acceder a carpetas públicas. Si necesita servidores locales de Exchange para satisfacer las necesidades actuales de su organización, puede que no sea conveniente quitar los servidores locales.

**Solución:** Recomendamos no eliminar Exchange ni la configuración híbrida en este momento. Si tuviera que comenzar el proceso apuntando los registros de detección automática a Exchange Online, rompería inmediatamente algunas características, como el acceso a las carpetas públicas híbridas. Podría cambiar el registro MX para que apunte a Exchange Online Protection, si aún no lo hizo, e incluso podría quitar algunos de los servidores locales de Exchange. Sin embargo, necesitaría mantener un número suficiente para controlar las funciones híbridas restantes. Normalmente, esto produciría una huella local muy pequeña.

