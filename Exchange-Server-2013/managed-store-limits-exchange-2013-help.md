---
title: 'Límites del almacén administrado: Exchange 2013 Help'
TOCTitle: Límites del almacén administrado
ms:assetid: bea9ec15-bfb5-4716-b14e-010e389c9f9e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Mt741981(v=EXCHG.150)
ms:contentKeyID: 73226004
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Límites del almacén administrado

 

_**Última modificación del tema:** 2016-09-15_

**Resumen:**  Acerca de los límites de conexión de un almacén administrado y cómo configurarlos.

En MicrosoftExchange Server 2013, los límites de uso y conexión se han colocado en el almacén administrado de Exchange para evitar que una única aplicación o un único usuario use todas las conexiones disponibles para el almacén administrado. Si se permite que un único usuario o una única aplicación use todas las conexiones, los otros usuarios o las otras aplicaciones no podrán acceder al almacén administrado, lo que podría provocar tiempo de inactividad.


> [!NOTE]
> En el caso de las conexiones realizadas por cuentas con privilegios administrativos, se han aumentado los límites máximos de sesión a 64 000.



## Terminología

El conocimiento de los siguientes términos le ayudará a comprender los tipos de conexiones a los que se hace referencia en este tema.

  - Sesiones  
    Las sesiones representan las conexiones usadas por servicios y aplicaciones cliente, como Microsoft Outlook, para conectarse al almacén administrado. Los servicios y los clientes pueden tener varias sesiones en un momento determinado. Los términos *conexiones* y *sesiones* se pueden usar indistintamente.

<!-- end list -->

  - Subprocesos  
    Los subprocesos representan las solicitudes de ejecución de manera simultánea al almacén administrado. Por ejemplo, si un usuario abre una carpeta en Outlook, Outlook ejecuta una solicitud en el almacén administrado en nombre del usuario. Esa ejecución de la solicitud es un subproceso único.
    
    En Exchange Server 2013, ya no existen límites de subproceso basados en el tipo de cliente. En su lugar, para todos los clientes, el número máximo de subprocesos **por base de datos de buzones** es 50. La excepción es el Servicio de disponibilidad, que tiene un límite máximo de 16 por usuario.

Volver al principio

## Límites de sesión

En la siguiente tabla se enumeran los tipos de conexiones de clientes al almacén administrado y los límites basados en esas conexiones. Si quiere modificar los límites de sesión, vea "Configurar límites de sesión" inmediatamente a continuación de la tabla.

Las versiones anteriores de Exchange establecen límites en el número de conexiones al almacén administrado basándose en el número de conexiones por servidor. En Exchange 2013, los límites de sesión se basan en conexiones por base de datos de buzones.

Los tipos de límites de conexión en Exchange 2013 son los siguientes:

  - **Cantidad máxima de sesiones por proceso** Especifica la cantidad máxima de sesiones que un servicio de Exchange puede tener abierto al mismo tiempo en una base de datos de buzones.

  - **Cantidad máxima de sesiones de usuario por proceso** Especifica la cantidad máxima de sesiones de un protocolo en particular para un usuario único.

En la siguiente sección, "Configurar límites de sesión", se describe cómo modificar estos límites.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de cliente</th>
<th></th>
<th>Cantidad máxima de sesiones por base de datos de buzones</th>
<th>Número predeterminado de sesiones de usuario por base de datos de buzones</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Administrador</p></td>
<td></td>
<td><p>10,000</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="even">
<td><p>Servicio de disponibilidad</p></td>
<td></td>
<td><p>10,000</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>Indexación de contenido</p></td>
<td></td>
<td><p>10,000</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync</p></td>
<td></td>
<td><p>No aplicable</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>Servicios Web Exchange</p></td>
<td></td>
<td><p>No aplicable</p></td>
<td><p>16</p></td>
</tr>
<tr class="even">
<td><p>Administración</p></td>
<td></td>
<td><p>No aplicable</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>MAPI en el nivel intermedio (MoMT)</p></td>
<td></td>
<td><p>No aplicable</p></td>
<td><p>32</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeMailboxAssistants: Eventos</p></td>
<td></td>
<td><p>10,000</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeMailboxAssistants: Programado</p></td>
<td></td>
<td><p>10,000</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="even">
<td><p>Llamada de procedimiento remoto de MSExchange</p></td>
<td></td>
<td><p>No aplicable</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft OfficeOutlook Web App</p></td>
<td></td>
<td><p>No aplicable</p></td>
<td><p>16</p></td>
</tr>
<tr class="even">
<td><p>POP3 e IMAP4</p></td>
<td></td>
<td><p>No aplicable</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>Transporte</p></td>
<td></td>
<td><p>10,000</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="even">
<td><p>Mensajería unificada</p></td>
<td></td>
<td><p>No aplicable</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>Otros</p></td>
<td></td>
<td><p>No aplicable</p></td>
<td><p>16</p></td>
</tr>
</tbody>
</table>


## Configurar límites de sesión

Puede modificar los límites de sesión predeterminados.


> [!NOTE]
> Si quiere modificar los límites de sesión, necesitará modificarlos en todos los servidores de buzón dentro de cualquier grupo de disponibilidad de base de datos (DAG). Si no realiza los mismos cambios en todos los servidores, los resultados serán incoherentes. Para aumentar el límite de sesión en el servidor de acceso de cliente, el valor <CODE>RCAMaxConcurrency</CODE> debe incrementarse en la directiva de limitación. Para obtener más información, vea <A href="https://technet.microsoft.com/es-es/library/dd298094(v=exchg.150)">Set-ThrottlingPolicy</A>.




> [!WARNING]
> La edición incorrecta del Registro puede dar lugar a graves problemas que pueden suponer la reinstalación del sistema operativo. Es posible que los problemas derivados de la edición incorrecta del Registro no puedan resolverse. Antes de editar el Registro, realice una copia de seguridad de los datos más importantes.



1.  Inicie el Editor del Registro (regedit).

2.  Vaya a la siguiente subclave del Registro:
    
    **\\\\HKEY\_LOCAL\_MACHINE \\SYSTEM\\CurrentControlSet\\Services\\MSExchangeIS\\ParametersSystem**.

3.  Haga clic con el botón derecho en **ParametersSystem**, seleccione **Nuevo** y, después, haga clic en **Valor de DWORD (32 bits)**.
    
    Se crea el nuevo valor en el panel de resultados.

4.  Cambie el nombre de la clave por uno de los siguientes valores y, después, presione Entrar:
    
      - **Sesiones máximas permitidas por usuario** Este límite especifica la cantidad máxima de sesiones permitidas por usuario.
    
      - **Sesiones de servicio máximas permitidas por usuario** Este límite especifica la cantidad máxima de sesiones de servicio permitidas por usuario.
    
      - **Sesiones de Exchange máximas permitidas por servicio** Este límite especifica la cantidad máxima permitida de sesiones de Exchange por servicio. El valor predeterminado es 10 000.

5.  Haga clic con el botón derecho en la clave que se ha creado recientemente y, después, haga clic en **Modificar**.

6.  En el cuadro de **datosde valor**, escriba el número de objetos al que quiera limitar esta entrada y, después, haga clic en **Aceptar**. Use la tabla anterior para ver la configuración predeterminada.

Volver al principio

## Límites de elementos abiertos

Los límites de elementos abiertos son límites impuestos sobre la cantidad de elementos que pueden ser abiertos por un único buzón de correo en una única sesión. En cambio, los usuarios pueden tener varias sesiones abiertas simultáneamente. Por ejemplo, si el usuario tiene dos sesiones abiertas, este podría abrir 1000 carpetas.

Si quiere modificar estos límites, vea "Configurar límites de elementos abiertos" inmediatamente a continuación de la tabla.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de elemento</th>
<th>Tipo de objeto de Registro</th>
<th>Cantidad máxima abierta por sesión</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Vista ACL</p></td>
<td><p>objtACLView</p></td>
<td><p>500</p></td>
</tr>
<tr class="even">
<td><p>Datos adjuntos</p></td>
<td><p>objtAttachment</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>Vista de datos adjuntos</p></td>
<td><p>objtAttachmentView</p></td>
<td><p>500</p></td>
</tr>
<tr class="even">
<td><p>CStream</p></td>
<td><p>objtCStream</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="odd">
<td><p>Carpeta</p></td>
<td><p>objtFolder</p></td>
<td><p>500</p></td>
</tr>
<tr class="even">
<td><p>Vista de carpeta</p></td>
<td><p>objtFolderView</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>Secuencia de destino FX</p></td>
<td><p>objtFXDstStrm</p></td>
<td><p>500</p></td>
</tr>
<tr class="even">
<td><p>Secuencia de origen FX</p></td>
<td><p>objtFXSrcStrm</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>Mensaje</p></td>
<td><p>objtMessage</p></td>
<td><p>250</p></td>
</tr>
<tr class="even">
<td><p>Vista de mensajes</p></td>
<td><p>objtMessageView</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>Notificación</p></td>
<td><p>objtNotify</p></td>
<td><p>500,000</p></td>
</tr>
<tr class="even">
<td><p>Vista de regla</p></td>
<td><p>objtRulesView</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="odd">
<td><p>Secuencia</p></td>
<td><p>objtStream</p></td>
<td><p>250</p></td>
</tr>
</tbody>
</table>


## Configurar límites de elementos abiertos

Puede limitar la cantidad máxima de recursos que un cliente MAPI puede usar simultáneamente.


> [!NOTE]
> Si quiere modificar los límites de elementos abiertos, necesitará modificarlos en todos los servidores de buzón dentro de cualquier DAG y matriz de acceso de clientes. Si no realiza los mismos cambios en todos los servidores, los resultados serán incoherentes.




> [!WARNING]
> La edición incorrecta del Registro puede dar lugar a graves problemas que pueden suponer la reinstalación del sistema operativo. Es posible que los problemas derivados de la edición incorrecta del Registro no puedan resolverse. Antes de editar el Registro, realice una copia de seguridad de los datos más importantes.



1.  Inicie el Editor del Registro (regedit).

2.  Vaya a la siguiente subclave del Registro:
    
    **\\\\HKEY\_LOCAL\_MACHINE \\SYSTEM\\CurrentControlSet\\Services\\MSExchangeIS\\ParametersSystem**

3.  Haga clic con el botón secundario en **ParametersSystem**, resalte **Nuevo** y luego haga clic en **Clave**.
    
    En el árbol de consola, se crea una nueva clave.

4.  Cambie el nombre de la clave **MaxObjsPerMapiSession** y, después, presione Entrar.

5.  Haga clic con el botón derecho en **MaxObjsPerMapiSession**, seleccione **Nuevo** y, después, haga clic en **Valor de DWORD (32 bits)**.
    
    Se crea el nuevo valor en el panel de resultados.

6.  Cambie el nombre de la clave a *\<Object\_type\>*, donde *\<Object\_type\>* es el nombre del tipo de objeto de Registro que está modificando. Por ejemplo, para modificar la cantidad de mensajes que se pueden abrir, use *objtMessage*. Presione Entrar.

7.  Haga clic con el botón derecho en la clave que se ha creado recientemente y, después, haga clic en **Modificar**.

8.  En el cuadro **Datos del valor**, escriba el número de objetos al que quiera limitar esta entrada y, después, haga clic en **Aceptar**. Por ejemplo, escriba **350** para aumentar el valor del objeto.

9.  Reinicie el servicio Almacén de información de Microsoft Exchange.

Volver al principio

## Límites de tamaño de elementos

Los límites de tamaño de elementos son los límites impuestos en los elementos del buzón de correo del usuario. Se configuran al usar los parámetros *MaxSendSize* y *MaxReceiveSize* en el cmdlet [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de elemento</th>
<th>Límite</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mensaje (guardado)</p></td>
<td><p>Tamaño máximo de SendLimit, ReceiveLimit</p></td>
</tr>
<tr class="even">
<td><p>Mensaje (enviado)</p></td>
<td><p>Tamaño máximo de SendLimit</p></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
</tr>
</tbody>
</table>


Volver al principio

