---
title: 'Iniciar o detener una búsqueda de exhibición de documentos electrónicos local: Exchange 2013 Help'
TOCTitle: Iniciar o detener una búsqueda de exhibición de documentos electrónicos local
ms:assetid: 0d546763-4bf5-4523-91f4-d181b7ee4ac2
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd335090(v=EXCHG.150)
ms:contentKeyID: 49895458
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Iniciar o detener una búsqueda de exhibición de documentos electrónicos local

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2014-07-14_

Puede parar o reiniciar una búsqueda de Exhibición de documentos electrónicos en contexto en cualquier momento. Por ejemplo, si desea modificar las propiedades de búsqueda como palabras clave o búsquedas realizadas en buzones, primero debe detener una búsqueda. Puede reiniciar la búsqueda después de realizar los cambios necesarios.


> [!WARNING]
> Si reinicia una búsqueda de Exhibición de documentos electrónicos en contexto, los resultados de la búsqueda copiados en el buzón de correo de exhibición especificado en la búsqueda se quitarán.



## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Exhibición de documentos electrónicos en contexto" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Use el EAC para iniciar o parar una búsqueda de Exhibición de documentos electrónicos en contexto

1.  Vaya a **Administración de cumplimiento** \> **Conservación local y exhibición de documentos electrónicos en contexto**.

2.  Para parar la búsqueda en marcha, seleccione la búsqueda y haga clic en **Detener la búsqueda**.

3.  Para iniciar una búsqueda que se detuvo, selecciónela y haga clic en **Reanudar búsqueda**.

## Usar el Shell para iniciar o parar una búsqueda de Exhibición de documentos electrónicos en contexto

Para ver un ejemplo sobre cómo iniciar una búsqueda de Exhibición de documentos electrónicos en contexto, consulte el "Ejemplo 1" de [Start-MailboxSearch](https://technet.microsoft.com/es-es/library/dd351245\(v=exchg.150\)).

Para ver un ejemplo sobre cómo parar una búsqueda de Exhibición de documentos electrónicos en contexto, consulte el "Ejemplo 1" de [Stop-MailboxSearch](https://technet.microsoft.com/es-es/library/dd351075\(v=exchg.150\)).

