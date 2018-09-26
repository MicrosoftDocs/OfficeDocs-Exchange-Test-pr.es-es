---
title: 'Quitar un paquete de idioma de mensajería unificada: Exchange 2013 Help'
TOCTitle: Quitar un paquete de idioma de mensajería unificada
ms:assetid: a2bc2753-2c25-4ea0-a9d5-e3d42a699c6c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124004(v=EXCHG.150)
ms:contentKeyID: 49895807
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Quitar un paquete de idioma de mensajería unificada

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-14_

Puede usar el EAC o el Shell para administrar idiomas de mensajería unificada (UM) en servidores de buzón de correo que ejecutan el servicio de mensajería unificada de Exchange. Sin embargo, para quitar un idioma de la lista en un plan de marcado de mensajería unificada, debe quitar el correspondiente paquete de idioma de mensajería unificada usando el comando **Setup.exe /RemoveUmLanguagePack**. Después de quitar el paquete de idioma de mensajería unificada del servidor de buzón de correo, el lenguaje ya no estará disponible al configurar un plan de marcado de mensajería unificada o un operador automático de mensajería unificada. Si desea ver los paquetes de idiomas de mensajería unificada que están instalados, examine las propiedades del servidor de buzón de correo o use el cmdlet **Get-UMService**.

Para obtener tareas adicionales relacionadas con los idiomas de mensajería unificada, consulte [Procedimientos de lenguajes, mensajes y saludos de mensajería unificada](um-languages-prompts-and-greetings-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Servidor de buzones de correo (servicio de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Compruebe que está instalado un paquete de idioma de mensajería unificada que no sea en-US.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Usar Setup.exe para quitar un paquete de idioma de mensajería unificada

En el símbolo del sistema, ejecute el comando siguiente.

```powershell
Setup.exe /RemoveUmLanguagePack:<UmLanguagePackName>
```

En el comando anterior, *\<UmLanguagePackName\>* es el nombre del paquete de idioma de mensajería unificada, por ejemplo fr-FR.


> [!WARNING]
> No se puede usar el archivo Setup.exe ubicado en la carpeta \Bin para quitar un paquete de idioma de mensajería unificada después de haber instalado actualizaciones. Se debe usar el archivo Setup.exe del DVD de&nbsp;Exchange&nbsp;2013 o de los archivos de origen descargados. Si no lo hace, aparecerá el siguiente error: Las versiones de la aplicación en uso y la aplicación instalada no coinciden.


