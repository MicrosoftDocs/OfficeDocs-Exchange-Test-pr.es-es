---
title: 'Habilitar la publicación del calendario de Internet: Exchange 2013 Help'
TOCTitle: Habilitar la publicación del calendario de Internet
ms:assetid: b4c71696-52bb-492c-8259-0e419acd0bbc
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ853046(v=EXCHG.150)
ms:contentKeyID: 50556868
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Habilitar la publicación del calendario de Internet

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2016-08-22_

**Resumen:**  Use estos procedimientos para permitir que los usuarios OWA en la organización de Exchange 2013 compartan información de disponibilidad de calendario con organizaciones externas.

Los usuarios de las organizaciones de Microsoft Exchange Server 2013 pueden compartir la información de disponibilidad (libre/ocupado) de calendario con usuarios de organizaciones que no son de Exchange y con otros usuarios con acceso a Internet. La publicación de calendarios en Internet ofrece una mayor flexibilidad y aumenta el número de usuarios que pueden compartir la información de disponibilidad de calendario.

Para habilitar la publicación de calendarios en Internet, hay que seguir tres pasos:

1.  Configure la dirección URL de proxy web para el servidor de correo electrónico (este paso solo es necesario si ya existe una dirección URL de proxy web en su organización. Si no es así, vaya al paso 2).

2.  Habilitar el directorio virtual de publicación para el servidor de acceso de cliente.

3.  Crear una directiva de uso compartido dedicada para la publicación de calendarios en Internet o actualizar la directiva de uso compartido predeterminada para que admita el dominio **Anonymous**. Ambos métodos permiten que los usuarios de la organización de Exchange inviten a otros usuarios con acceso a Internet a ver información limitada acerca de la disponibilidad de calendario mediante el acceso a una URL publicada.


> [!IMPORTANT]
> Después de completar el Paso 3, los usuarios tendrán que publicar sus calendarios desde Outlook. La publicación de calendarios crea direcciones URL que los usuarios pueden dar a usuarios externos a la organización. Una dirección URL permite que los destinatarios se suscriban a calendarios con Outlook o Outlook Web App y la otra permite que los destinatarios vean un calendario en un explorador web. Cada usuario puede controlar la cantidad de cosas que podrán ver los demás.



Para otras tareas de administración relacionadas con las directivas de uso compartido, consulte [Directivas de uso compartido](sharing-policies-exchange-2013-help.md)

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar esta tarea: 15 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada «Permisos de calendario y uso compartido" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Un servidor de acceso de clientes de Exchange 2013 existe en la organización de Exchange que comparte la información de calendario de los usuarios.

  - Los buzones de usuario están ubicados en los servidores de buzones de Exchange 2013 en la organización de Exchange que comparte la información de calendario de los usuarios.

  - Únicamente los usuarios de Outlook 2010 o superior y Outlook Web App pueden crear invitaciones de uso compartido.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Cómo realiza esto?

## Paso 1: Uso del Shell para configurar la dirección URL de proxy web


> [!NOTE]
> Este paso solo es necesario si ya existe una dirección URL de proxy web en su organización. Si no es así, vaya al Paso 2.<BR>No se puede utilizar el Centro de administración de Exchange (EAC) para configurar la dirección URL de proxy web.



En este ejemplo se configura una dirección URL de proxy web en el servidor de buzones MAIL01.

```powershell
Set-ExchangeServer -Identity "MAIL01" -InternetWebProxy "<Webproxy URL>"
```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-ExchangeServer](https://technet.microsoft.com/es-es/library/bb123716\(v=exchg.150\)).

## ¿Cómo sabe si este paso se ha completado correctamente?

Para comprobar que configuró correctamente la dirección URL de proxy web, ejecute el siguiente comando del Shell y compruebe la información del parámetro *InternetWebProxy*.

```powershell
Get-ExchangeServer | format-list
```

## Paso 2: Uso del Shell para habilitar el directorio virtual de publicación


> [!NOTE]
> No puede usar el EAC para habilitar un directorio virtual de publicación.



En este ejemplo se habilita el directorio virtual de publicación en el servidor de acceso de cliente CAS01.
```powershell
    Set-OwaVirtualDirectory -Identity "CAS01\owa (Default Web Site)" -ExternalUrl "<URL for CAS01>" -CalendarEnabled $true
```

La identidad `CAS01\owa (Default Web Site)` es tanto el nombre del servidor como el directorio virtual de Outlook Web App.

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-OwaVirtualDirectory](https://technet.microsoft.com/es-es/library/bb123515\(v=exchg.150\)).

## ¿Cómo sabe si este paso se ha completado correctamente?

Para comprobar que habilitó correctamente el directorio virtual de publicación, ejecute el siguiente comando del Shell y compruebe la información del parámetro *ExternalURL*.

```powershell
Get-OwaVirtualDirectory | format-list
```

## Paso 3: Crear o configurar una directiva de uso compartido específicamente para la publicación de calendarios de Internet


> [!NOTE]
> Las siguientes opciones del Paso 3 solo se aplican a los entornos de Exchange Online.



Tiene la posibilidad de crear una directiva de uso compartido para la publicación de calendarios de Internet (opción 1) o configurar la directiva de uso compartido para la publicación de calendarios de Internet predeterminada (opción 2). Con ambas opciones puede elegir usar el EAC o el Shell.

## Opción 1: Crear una directiva de uso compartido específicamente para la publicación de calendarios de Internet

Si desea crear una directiva de uso compartido específicamente para la publicación de calendarios en Internet, siga estos pasos.

## Uso de EAC

1.  Vaya a **Organización** \> **Uso compartido**.

2.  En la vista de lista, en **Uso compartido individual**, haga clic en **Nuevo**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

3.  En **Directiva de uso compartido**, escriba un nombre descriptivo en el campo **Nombre de la directiva** (por ejemplo, **Internet**).

4.  Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para definir las reglas de uso compartido para la política de uso compartido.

5.  En **Regla de uso compartido**, haga clic en **Compartir con un dominio específico** y, a continuación, escriba **Anonymous** en el cuadro correspondiente.

6.  Para especificar los niveles de uso compartido del calendario que desea establecer para la directiva de uso compartido, marque la casilla **Compartir la carpeta de calendario** y, a continuación, seleccione una de las siguientes opciones:
    
      - **Información de disponibilidad de calendario solo con hora**
    
      - **Información de disponibilidad de calendario con hora, asunto y ubicación**
    
      - **Toda la información de citas de calendarios, incluidas la hora, el asunto, la ubicación y el título**

7.  Haga clic en **Guardar** para configurar las reglas de la directiva de uso compartido.

8.  En **Directiva de uso compartido**, haga clic en **Guardar** para crear la directiva.

## Usar el Shell

En este ejemplo se crea una directiva de uso compartido de publicación de calendarios en Internet llamada Internet y se configura la directiva para compartir únicamente la información de disponibilidad. La directiva está habilitada.

```powershell
    New-SharingPolicy -Name "Internet" -Domains 'Anonymous: CalendarSharingFreeBusySimple' -Enabled $true
```

En este ejemplo se agrega la directiva compartida a un buzón de usuario.

```powershell
Set-Mailbox -Identity <user name> -SharingPolicy "Internet"
```

En este ejemplo se agrega la directiva de uso compartido a una unidad organizativa (OU).

```powershell
Set-Mailbox -OrganizationalUnit <OU name> -SharingPolicy "Internet"
```

Para obtener más información acerca de la sintaxis y los parámetros, consulte [New-SharingPolicy](https://technet.microsoft.com/es-es/library/dd298186\(v=exchg.150\)) y [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)).

## ¿Cómo sabe si este paso se ha completado correctamente?

Para comprobar que la directiva de uso compartido se creó correctamente, ejecute el siguiente comando del Shell para comprobar la información de directiva de uso compartido.

```powershell
Get-SharingPolicy <policy name> | format-list
```

## Opción 2: Configurar la directiva de uso compartido predeterminada para la publicación de calendarios de Internet

Si desea configurar la directiva de uso compartido predeterminada para la publicación de calendarios en Internet, siga estos pasos.

## Uso de EAC

1.  Vaya a **Organización** \> **Uso compartido**.

2.  En la vista de lista, en **Uso compartido individual**, seleccione la directiva predeterminada de uso compartido y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En **Directiva de uso compartido**, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para agregar una regla de uso compartido a la directiva.

4.  En **Regla de uso compartido**, haga clic en **Compartir con un dominio específico** y, a continuación, escriba **Anonymous** en el cuadro correspondiente.

5.  Para especificar los niveles de uso compartido del calendario que desea establecer para la directiva de uso compartido, marque la casilla **Compartir la carpeta de calendario** y, a continuación, seleccione una de las siguientes opciones:
    
      - **Información de disponibilidad de calendario solo con hora**
    
      - **Información de disponibilidad de calendario con hora, asunto y ubicación**
    
      - **Toda la información de citas de calendarios, incluidas la hora, el asunto, la ubicación y el título**

6.  Haga clic en **Guardar** para configurar las reglas de la directiva de uso compartido.

7.  En **Directiva de uso compartido**, haga clic en **Guardar** para guardar los cambios.

## Usar el Shell

En este ejemplo se actualiza la directiva de uso compartido predeterminada y se configura la directiva para compartir solo la información de disponibilidad. La directiva está habilitada.

```powershell
    Set-SharingPolicy -Name "Default Sharing Policy" -Domains 'Anonymous: CalendarSharingFreeBusySimple' -Enabled $true
```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)).

## ¿Cómo sabe si este paso se ha completado correctamente?

Para comprobar que la directiva de uso compartido predeterminada se actualizó correctamente, ejecute el siguiente comando del Shell para comprobar la información de directiva de uso compartido.

```powershell
Get-SharingPolicy <policy name> | format-list
```

