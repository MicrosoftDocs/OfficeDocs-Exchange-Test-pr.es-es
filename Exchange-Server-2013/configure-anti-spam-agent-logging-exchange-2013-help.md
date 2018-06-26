---
title: 'Configurar el registro de agentes contra correo electrónico no deseado: Exchange 2013 Help'
TOCTitle: Configurar el registro de agentes contra correo electrónico no deseado
ms:assetid: df157ca3-ad8e-4302-acbc-5fbb8570c21d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb691337(v=EXCHG.150)
ms:contentKeyID: 49895964
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar el registro de agentes contra correo electrónico no deseado

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-04-08_

El registro de agentes graba las acciones realizadas por agentes específicos contra correo electrónico no deseado de Exchange. La información escrita en el registro de agentes depende del agente, del evento SMTP y de la acción realizada en el mensaje.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 15 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el entradas "Servicio de transporte" y "Servidor de transporte perimetral" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - De manera predeterminada, las características contra correo no deseado no están habilitadas en el Servicio de transporte en un servidor de buzones. Por lo general, solo se habilitan las características contra correo no deseado si la organización de Exchange no realiza un filtrado previo contra correo no deseado antes de aceptar mensajes entrantes. Para obtener más información, consulte [Habilitar la funcionalidad contra correo electrónico no deseado en un servidor Buzón de correo](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - Solo puede usar el Shell para realizar este procedimiento.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Uso del Shell para configurar el registro de agentes contra correo no deseado

Ejecute el siguiente comando:

    Set-TransportService <ServerIdentity> -AgentLogEnabled <$true | $false> -AgentLogMaxAge <dd.hh:mm:ss> -AgentLogMaxDirectorySize <Size> -AgentLogMaxFileSize <Size> -AgentLogPath <LocalFilePath>

En este ejemplo, se establece la siguiente configuración de registro de agente en el servidor de buzones de correo denominado Mailbox01:

  -  
    Establece la ubicación de los archivos de registro de agente en D:\\Anti-Spam Agent Log. Tenga en cuenta que si la carpeta no existe, se creará para usted.

  -  
    Establece el tamaño máximo de un archivo de registro de agente en 20 MB.

  -  
    Establece el tamaño máximo del directorio de registro de agente en 400 MB.

  -  
    Establece la antigüedad máxima de un archivo de registro de agente en 14 días.

<!-- end list -->

    Set-TransportService Mailbox01 -AgentLogPath "D:\Anti-Spam Agent Log" -AgentLogMaxFileSize 20MB -AgentLogMaxDirectorySize 400MB -AgentLogMaxAge 14.00:00:00


> [!NOTE]
> <UL>
> <LI>
> <P>Si establece el parámetro <EM>AgentLogPath</EM> en el valor <CODE>$null</CODE>, se deshabilita el registro de agente. Sin embargo, si establece <EM>AgentLogPath</EM> en <CODE>$null</CODE> cuando el valor del parámetro <EM>AgentLogEnabled</EM> es <CODE>$true</CODE>, se generan errores de registro. El método preferido para deshabilitar el registro de eventos es establecer <EM>AgentLogEnabled</EM> en <CODE>$false</CODE>.</P>
> <LI>
> <P>Establecer el valor del parámetro <EM>AgentLogMaxAge</EM> en el valor <CODE>00:00:00</CODE> evita la eliminación automática de los archivos de registro de agente debido a la antigüedad.</P></LI></UL>



Para obtener información detallada acerca de la sintaxis y los parámetros, consulte los parámetros *AgentLog* en [Set-TransportService](https://technet.microsoft.com/es-es/library/jj215682\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que el registro de agente contra correo electrónico no deseado se configuró correctamente, realice lo siguiente:

1.  En el Shell, ejecute el siguiente comando:
    
        Get-TransportService <ServerIdentity> | Format-List AgentLog*

2.  Verifique que los valores mostrados son los valores que ha configurado.

