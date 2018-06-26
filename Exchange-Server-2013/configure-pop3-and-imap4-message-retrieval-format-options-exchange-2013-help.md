---
title: 'Configurar las opciones de formato de recepción de mensajes POP3 e IMAP4: Exchange 2013 Help'
TOCTitle: Configurar las opciones de formato de recepción de mensajes POP3 e IMAP4
ms:assetid: 481096e0-4492-46c2-8ca8-bdf84a84531e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997869(v=EXCHG.150)
ms:contentKeyID: 50556790
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar las opciones de formato de recepción de mensajes POP3 e IMAP4

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

Puede configurar el formato de recuperación de mensajes para usuarios que se conecten a su correo electrónico con POP3 e IMAP4. Las opciones de recuperación de mensajes pueden configurarse en el nivel del servidor con el Centro de Administración de Exchange o el Shell, y pueden configurarse en el nivel de usuario con el Shell.

Para obtener más información acerca de POP3 e IMAP4, vea [POP3 e IMAP4 en Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entradas “Configuración de POP3” y “Configuración de IMAP4” en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Configura el formato de recuperación de mensajes POP3 en el nivel de servidor

## Uso del Centro de Administración de Exchange para configurar el formato de recuperación de mensajes POP3 en el nivel de servidor

1.  En la consola EAC, desplácese hasta **Servidores** \> **Servidores**.

2.  En la lista de servidores, seleccione el servidor de acceso de cliente y, luego, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades del servidor, haga clic en **POP3**.

4.  En **Formato de mensaje MIME**, elija entre las siguientes opciones:
    
      - Text
    
      - HTML
    
      - HTML y texto alternativo
    
      - Texto enriquecido
    
      - Texto enriquecido y texto alternativo
    
      - Formato óptimo para el cuerpo
    
      - TNEF

5.  Haga clic en **Guardar**.

Una vez establecida la configuración de formato de recuperación de mensajes para POP3, debe reiniciar los servicios POP3 para que la configuración surta efecto. Para obtener más información acerca de cómo reiniciar los servicios POP3, consulte [Iniciar y detener los servicios POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

## Uso del Shell para configurar el formato de recuperación de mensajes POP3 en el nivel de servidor

En este ejemplo, se configuran la opción de formato de recuperación de mensajes para sólo texto para todos los usuarios de POP3 en el servidor CAS01.

    Set-PopSettings -Identity CAS01 -MessageRetrievalMimeFormat TextOnly

Se puede elegir entre la siguiente configuración. Puede especificar el valor del parámetro *MessageRetrievalMimeFormat* usando un valor numérico o una cadena de texto.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Formato del mensaje</strong></p></td>
<td><p><strong>Valor</strong></p></td>
</tr>
<tr class="even">
<td><p>Text</p></td>
<td><p><code>0</code> o <code>TextOnly</code></p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p><code>1</code> o <code>HtmlOnly</code></p></td>
</tr>
<tr class="even">
<td><p>HTML y texto alternativo</p></td>
<td><p><code>2</code> o <code>HtmlAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Texto enriquecido</p></td>
<td><p><code>3</code> o <code>TextEnriched</code></p></td>
</tr>
<tr class="even">
<td><p>Texto enriquecido y texto alternativo</p></td>
<td><p><code>4</code> o <code>TextEnrichedAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Formato óptimo para el cuerpo</p></td>
<td><p><code>5</code> o <code>BestBodyFormat</code></p></td>
</tr>
<tr class="even">
<td><p>TNEF</p></td>
<td><p><code>6</code> o <code>Tnef</code></p></td>
</tr>
</tbody>
</table>


Una vez establecida la configuración de formato de recuperación de mensajes para POP3, debe reiniciar los servicios POP3 para que la configuración surta efecto. Para obtener más información acerca de cómo reiniciar los servicios POP3, consulte [Iniciar y detener los servicios POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

Para obtener más información sobre sintaxis y parámetros, consulte [Set-POPSettings](https://technet.microsoft.com/es-es/library/aa997154\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Realice lo siguiente para comprobar que haya configurado correctamente los ajustes de recuperación de mensajes POP3 en un servidor.

1.  Ejecute el siguiente comando en el Shell.
    
        Get-PopSettings | format-list

2.  Compruebe que la configuración de *MessageRetrievalMimeFormat* sea correcta.

## Configura el formato de recuperación de mensajes IMAP4 en el nivel de servidor

## Uso del Centro de Administración de Exchange para configurar el formato de recuperación de mensajes IMAP4 en el nivel de servidor

1.  En la consola EAC, desplácese hasta **Servidores** \> **Servidores**.

2.  En la lista de servidores, seleccione el servidor de acceso de cliente y, luego, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades del servidor, haga clic en **IMAP4**.

4.  En **Formato de mensaje MIME**, elija entre las siguientes opciones:
    
      - Text
    
      - HTML
    
      - HTML y texto alternativo
    
      - Texto enriquecido
    
      - Texto enriquecido y texto alternativo
    
      - Formato óptimo para el cuerpo
    
      - TNEF

5.  Haga clic en **Guardar**.

Una vez establecida la configuración de formato de recuperación de mensajes para IMAP4, debe reiniciar los servicios IMAP4 para que la configuración surta efecto. Para obtener más información acerca de cómo reiniciar los servicios IMAP4, consulte [Iniciar y detener los servicios IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md).

## Uso del Shell para configurar el formato de recuperación de mensajes IMAP4 en el nivel de servidor

En este ejemplo, se configuran la opción de formato de recuperación de mensajes para sólo texto para todos los usuarios de IMAP4 en el servidor CAS01.

    Set-ImapSettings -Identity CAS01 -MessageRetrievalMimeFormat TextOnly

Se puede elegir entre la siguiente configuración. Puede especificar el valor del parámetro *MessageRetrievalMimeFormat* usando un valor numérico o una cadena de texto.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Formato del mensaje</strong></p></td>
<td><p><strong>Valor</strong></p></td>
</tr>
<tr class="even">
<td><p>Text</p></td>
<td><p><code>0</code> o <code>TextOnly</code></p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p><code>1</code> o <code>HtmlOnly</code></p></td>
</tr>
<tr class="even">
<td><p>HTML y texto alternativo</p></td>
<td><p><code>2</code> o <code>HtmlAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Texto enriquecido</p></td>
<td><p><code>3</code> o <code>TextEnriched</code></p></td>
</tr>
<tr class="even">
<td><p>Texto enriquecido y texto alternativo</p></td>
<td><p><code>4</code> o <code>TextEnrichedAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Formato óptimo para el cuerpo</p></td>
<td><p><code>5</code> o <code>BestBodyFormat</code></p></td>
</tr>
<tr class="even">
<td><p>TNEF</p></td>
<td><p><code>6</code> o <code>Tnef</code></p></td>
</tr>
</tbody>
</table>


Una vez establecida la configuración de formato de recuperación de mensajes para IMAP4, debe reiniciar los servicios IMAP4 para que la configuración surta efecto. Para obtener más información acerca de cómo reiniciar los servicios IMAP4, consulte [Iniciar y detener los servicios IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md).

Para obtener más información sobre sintaxis y parámetros, consulte [Set-ImapSettings](https://technet.microsoft.com/es-es/library/aa998252\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Realice lo siguiente para comprobar que haya configurado correctamente los ajustes de recuperación de mensajes IMAP4 en un servidor.

1.  Ejecute el siguiente comando en el Shell.
    
        Get-ImapSettings | format-list

2.  Compruebe que la configuración de *MessageRetrievalMimeFormat* sea correcta.

## Configura el formato de recuperación de mensajes POP3 para un usuario

## Uso del Shell para definir el formato de recuperación de mensajes POP3 para un usuario

En este ejemplo, se define el formato de recuperación de mensajes de sólo texto para el acceso de POP3 para `USER01`.

    Set-CASMailbox -Identity USER01 -PopMessagesRetrievalMimeFormat TextOnly

Se puede elegir entre la siguiente configuración. Puede especificar el valor del parámetro *PopMessagesRetrievalMimeFormat* usando un valor numérico o una cadena de texto.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Formato del mensaje</strong></p></td>
<td><p><strong>Valor</strong></p></td>
</tr>
<tr class="even">
<td><p>Text</p></td>
<td><p><code>0</code> o <code>TextOnly</code></p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p><code>1</code> o <code>HtmlOnly</code></p></td>
</tr>
<tr class="even">
<td><p>HTML y texto alternativo</p></td>
<td><p><code>2</code> o <code>HtmlAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Texto enriquecido</p></td>
<td><p><code>3</code> o <code>TextEnriched</code></p></td>
</tr>
<tr class="even">
<td><p>Texto enriquecido y texto alternativo</p></td>
<td><p><code>4</code> o <code>TextEnrichedAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Formato óptimo para el cuerpo</p></td>
<td><p><code>5</code> o <code>BestBodyFormat</code></p></td>
</tr>
<tr class="even">
<td><p>TNEF</p></td>
<td><p><code>6</code> o <code>Tnef</code></p></td>
</tr>
</tbody>
</table>


Una vez establecida la configuración de formato de recuperación de mensajes para POP3, debe reiniciar los servicios POP3 para que la configuración surta efecto. Para obtener más información acerca de cómo reiniciar los servicios POP3, consulte [Iniciar y detener los servicios POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

Para obtener más información sobre sintaxis y parámetros, consulte [Set-CASMailbox](https://technet.microsoft.com/es-es/library/bb125264\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Realice lo siguiente para comprobar que haya configurado correctamente los ajustes de recuperación de mensajes POP3 para un usuario.

1.  Ejecute el siguiente comando en el Shell.
    
        Get-CAS Mailbox <identity> | format-list

2.  Compruebe que el valor de *PopMessagesRetrievalMimeFormat* sea correcto.

## Configura el formato de recuperación de mensajes IMAP4 para un usuario

## Uso del Shell para definir el formato de recuperación de mensajes IMAP4 para un usuario

En este ejemplo, se define el formato de recuperación de mensajes de sólo texto para el acceso de IMAP4 para `USER01`.

    Set-CASMailbox -Identity USER01 -ImapMessagesRetrievalMimeFormat TextOnly

Puede especificar el valor del parámetro *ImapMessagesRetrievalMimeFormat* usando un valor numérico o una cadena de texto.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Formato del mensaje</strong></p></td>
<td><p><strong>Valor</strong></p></td>
</tr>
<tr class="even">
<td><p>Text</p></td>
<td><p><code>0</code> o <code>TextOnly</code></p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p><code>1</code> o <code>HtmlOnly</code></p></td>
</tr>
<tr class="even">
<td><p>HTML y texto alternativo</p></td>
<td><p><code>2</code> o <code>HtmlAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Texto enriquecido</p></td>
<td><p><code>3</code> o <code>TextEnriched</code></p></td>
</tr>
<tr class="even">
<td><p>Texto enriquecido y texto alternativo</p></td>
<td><p><code>4</code> o <code>TextEnrichedAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Formato óptimo para el cuerpo</p></td>
<td><p><code>5</code> o <code>BestBodyFormat</code></p></td>
</tr>
<tr class="even">
<td><p>TNEF</p></td>
<td><p><code>6</code> o <code>Tnef</code></p></td>
</tr>
</tbody>
</table>


Una vez establecida la configuración de formato de recuperación de mensajes para IMAP4, debe reiniciar los servicios IMAP4 para que la configuración surta efecto. Para obtener más información acerca de cómo reiniciar los servicios IMAP4, consulte [Iniciar y detener los servicios IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md).

Para obtener más información sobre sintaxis y parámetros, consulte [Set-CASMailbox](https://technet.microsoft.com/es-es/library/bb125264\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Realice lo siguiente para comprobar que haya configurado correctamente los ajustes de recuperación de mensajes IMAP4 para un usuario.

1.  Ejecute el siguiente comando en el Shell.
    
        Get-CAS Mailbox <identity> | format-list

2.  Compruebe que el valor de *ImapMessagesRetrievalMimeFormat* sea correcto.

## Más información

Después de definir el formato de recuperación de mensajes de usuarios IMAP4 y POP3, es posible que también desee realizar las siguientes tareas:

[Habilitar o deshabilitar el acceso POP3 para un usuario](enable-or-disable-pop3-access-for-a-user-exchange-2013-help.md)

[Habilitar o deshabilitar el acceso a IMAP4 para un usuario](enable-or-disable-imap4-access-for-a-user-exchange-2013-help.md)

[Configurar opciones de calendario para IMAP4](configure-calendar-options-for-imap4-exchange-2013-help.md)

[Configurar las opciones de calendario para POP3](configure-calendar-options-for-pop3-exchange-2013-help.md)

