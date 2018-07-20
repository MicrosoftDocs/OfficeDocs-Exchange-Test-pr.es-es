---
title: 'Importar mensajes personalizados de Exchange 2007 a Exchange 2013: Exchange 2013 Help'
TOCTitle: Importar mensajes personalizados de Exchange 2007 a Exchange 2013
ms:assetid: 70c0b0bc-c0de-4e3c-8144-1fe59f86ebf4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg309147(v=EXCHG.150)
ms:contentKeyID: 54652440
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Importar mensajes personalizados de Exchange 2007 a Exchange 2013

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2015-04-08_

Puede importar los archivos de audio que contienen saludos, anuncios, menús y mensajes personalizados de mensajería unificada (UM) de Exchange 2007 a mensajería unificada de Exchange 2013. Mediante un script del Shell, los mensajes se importan en un buzón del sistema de Exchange denominado {e0dc1c29-89c3-4034-b678-e6c29d823ed9}, que se crea cuando instala Microsoft Exchange 2013. Este buzón de sistema se usa en la mensajería unificada para almacenar saludos, anuncios, menús, mensajes e informes de mensajería unificada personalizados del operador automático y plan de marcado.

Los archivos de audio, en formato .wav o .wma, se usan de la siguiente manera:

  - En los planes de marcado de mensajería unificada, los archivos de audio se usan para saludos personalizados de bienvenida y anuncios informativos. Se reproducen cuando los usuarios de Outlook Voice Access llaman a un número de Outlook Voice Access.

  - En los operadores automáticos de mensajería unificada, los archivos de audio se utilizan para saludos utilizados para horarios comerciales y no comerciales, anuncios informativos, mensajes de menú y menús de navegación personalizados. Se reproducen cuando los usuarios llaman a un operador automático de mensajería unificada.

El script MigrateUMCustomPrompts.ps1 se usa para migrar una copia de todos los saludos, anuncios, menús y mensajes personalizados de mensajería unificada de Exchange Server 2007 a mensajería unificada de Exchange 2013 para todos los operadores automáticos de mensajería unificada y planes de marcado de mensajería unificada de Exchange 2007.

De manera predeterminada, el script MigrateUMCustomPrompts.ps1 se encuentra en la carpeta \<Archivos de programa\>\\Microsoft\\Exchange Server\\V15\\Scripts en un servidor de Exchange 2013.


> [!NOTE]
> El script MigrateUMCustomPrompts.ps1 se incluye con Exchange&nbsp;2013. Se debe ejecutar en un servidor de buzón de Exchange&nbsp;2013 en la misma organización con sus servidores de mensajería unificada de Exchange 2007.



Para otras tareas de administración relacionadas con los planes de marcado de mensajería unificada, consulte [Procedimientos de plan de marcado de mensajería unificada](um-dial-plan-procedures-exchange-2013-help.md).

Para conocer tareas de administración adicionales relacionadas con los operadores automáticos de mensajería unificada, consulte [Procedimientos operador automático de mensajería unificada](um-auto-attendant-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 3 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el entradas \&quot;Planes de marcado de mensajería unificada\&quot; y \&quot;Operadores automáticos de mensajería unificada\&quot; del tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de mensajería unificada. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un operador automático de mensajería unificada. Para conocer los pasos detallados, consulte [Crear un operador automático de mensajería unificada](create-a-um-auto-attendant-exchange-2013-help.md).

  - Solo puede usar el Shell para realizar este procedimiento. Para obtener información sobre cómo abrir el Shell de administración de Exchange en su organización local Exchange, vea [Abrir el Shell](https://technet.microsoft.com/es-es/library/dd638134\(v=exchg.150\)).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Use el script MigrateUMCustomPrompts.ps1 para migrar una copia de todos los mensajes personalizados para los planes de marcado y operadores automáticos de mensajería unificada.

1.  Haga clic en **Inicio** \> **Todos los programas** \> **Microsoft Exchange Server 2013** \> **Consola de administración de Exchange**.

2.  En la consola, en el símbolo del sistema, escriba la ruta de acceso al script. Por ejemplo, escriba **cd "D:\\Archivos de programa\\Microsoft\\Exchange Server\\V15\\Scripts"** y, a continuación, presione Entrar.

3.  En el símbolo del sistema del Shell, escriba **".\\MigrateUMCustomPrompt"** y, a continuación, presione Entrar.

