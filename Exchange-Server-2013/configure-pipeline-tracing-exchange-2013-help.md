---
title: 'Configuración del seguimiento de canalización: Exchange 2013 Help'
TOCTitle: Configuración del seguimiento de canalización
ms:assetid: 10293c83-2157-474e-840d-942e064a4672
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ916678(v=EXCHG.150)
ms:contentKeyID: 52062004
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configuración del seguimiento de canalización

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-04-08_

El seguimiento de canalizaciones captura copias de los mensajes de correo cuando se mueven por la canalización de transporte en el servicio de transporte o en el de transporte de buzones del servidor de buzones y de los servidores de transporte perimetral.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar este procedimiento: 15 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entradas "Servicio de transporte" y "Servicio de transporte de buzones" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Solo puede usar el Shell para realizar este procedimiento.

  - El seguimiento de canalización copia todo el contenido de los mensajes de correo que se envían desde la dirección de correo del remitente. Para evitar la exposición no deseada de información confidencial, debe establecer permisos de seguridad apropiados en la ubicación de la carpeta de seguimiento de canalizaciones.

  - No habilite el seguimiento de canalización durante largos períodos de tiempo. El seguimiento de canalizaciones crea varios archivos de capturas de mensajes que se acumulan en poco tiempo. Compruebe siempre el espacio disponible en disco cuando esté habilitado el seguimiento de canalización.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Habilitar y configurar el seguimiento de canalizaciones

## Paso 1: Utilice el Shell para configurar la dirección del remitente de seguimiento de canalización

Use la siguiente sintaxis para configurar la dirección del remitente de seguimiento de canalización.

```powershell
<Set-TransportService | Set-MailboxTransportService> <ServerIdentity> -PipelineTracingSenderAddress <SMTPAddress | "<>">
```

En este ejemplo se configura el seguimiento de canalización para hacer capturas de pantalla de todos los mensajes enviados por el remitente chris@contoso.com en el servicio de transporte del servidor de buzones Mailbox01.

```powershell
Set-TransportService Mailbox01 -PipelineTracingSenderAddress chris@contoso.com
```

En este ejemplo se configura el seguimiento de canalización para hacer capturas de pantalla de todos los mensajes generados por el sistema que ha recibido el servicio de transporte del servidor de buzones Mailbox02.

```powershell
Set-TransportService Mailbox02 -PipelineTracingSenderAddress "<>"
```


> [!WARNING]
> Configurar el seguimiento de canalización para capturar todos los mensajes generados por el servidor en un servicio de transporte puede generar una carga importante en el servidor y consumir rápidamente el espacio de disco disponible. Compruebe siempre el espacio disponible en disco cuando esté habilitado el seguimiento de canalización.



## Paso 2: (Opcional) Usar el Shell para especificar una carpeta de seguimiento de canalización personalizada

La carpeta predeterminada de seguimiento de canalizaciones no existe hasta que se habilita el seguimiento. Los mensajes que cumplen con los criterios que especifique con el parámetro *PipelineTracingSenderAddress* fluyen a través del servicio de transporte del servidor. Para el servicio de transporte de un servidor de buzones, la ubicación predeterminada es `%ExchangeInstallPath%TransportRoles\Logs\Hub\PipelineTracing`. Para el servicio de transporte de buzones de un servidor de buzones, la ubicación predeterminada es `%ExchangeInstallPath%TransportRoles\Logs\Mailbox\PipelineTracing`. Si especifica una ruta personalizada, esta debe estar en el servidor local de Exchange.

Use la siguiente sintaxis para configurar la carpeta de seguimiento de canalización.

```powershell
<Set-TransportService | Set-MailboxTransportService> <ServerIdentity> -PipelineTracingPath <LocalFilePath>
```

En este ejemplo se especifica la carpeta de seguimiento de canalización para el servicio de transporte del servidor de buzones Mailbox01 en D:\\Hub\\Pipeline Tracing.

```powershell
Set-TransportService Mailbox01 -PipelineTracingPath "D:\Hub\Pipeline Tracing"
```

## Paso 3: Utilice el Shell para habilitar el seguimiento de canalización

De forma predeterminada, el seguimiento de canalización está deshabilitado en todos los servidores de Exchange. Al habilitar el seguimiento de canalización, permite el seguimiento en el servicio de transporte especificado únicamente en el servidor de Exchange especificado. Antes de habilitar el seguimiento de canalización, debe especificar la dirección del remitente tal como aparece en el Paso 1.

Utilice la siguiente sintaxis para habilitar el seguimiento de canalización.

```powershell
<Set-TransportService | Set-MailboxTransportService> <ServerIdentity> -PipelineTracingEnabled $true
```

En este ejemplo se permite el seguimiento de canalización del servicio de transporte en el servidor de buzones Mailbox01.

```powershell
Set-TransportService Mailbox01 -PipelineTracingEnabled $true
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si configuró correctamente el seguimiento de canalización, siga estos pasos:

1.  Ejecute el siguiente comando:
    
    ```powershell
    <Get-TransportService | Get-MailboxTransportService> <ServerIdentity> | Format-List PipelineTracing*
    ```

2.  Verifique que los valores mostrados son los valores que ha configurado.

3.  Compruebe la carpeta de seguimiento de canalización del servicio de transporte o el servicio de transporte de buzones, y asegúrese de que se están creando los archivos de captura de mensajes en esta carpeta.

## Deshabilitar el seguimiento de canalización

Debido a los problemas de espacio del disco y seguridad asociados al seguimiento de canalizaciones, el seguimiento es una acción temporal para diagnosticar y solucionar problemas. Siempre que habilite el seguimiento de canalización, recuerde deshabilitarlo al acabar.

Use la siguiente sintaxis para deshabilitar el seguimiento de canalización.

```powershell
<Set-TransportService | Set-MailboxTransportService> <ServerIdentity> -PipelineTracingEnabled $false
```

En este ejemplo se deshabilita el seguimiento de canalización del servicio de transporte en el servidor de buzones Mailbox01.

```powershell
Set-TransportService Mailbox01 -PipelineTracingEnabled $false
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si deshabilitó correctamente el seguimiento de canalización, siga estos pasos:

1.  Ejecute el siguiente comando:
    
    ```powershell
    <Get-TransportService | Get-MailboxTransportService> <ServerIdentity> | Format-List PipelineTracingEnabled
    ```
    
2.  Compruebe si el valor del parámetro *PipelineTracingEnabled* es $false.

3.  Compruebe la carpeta de seguimiento de canalización y asegúrese de que ya no se creen archivos de captura de mensajes en esta carpeta.

