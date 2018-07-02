---
title: 'Implementación de Exchange 2013 en una topología de bosques de recursos de Exchange: Exchange 2013 Help'
TOCTitle: Implementación de Exchange 2013 en una topología de bosques de recursos de Exchange
ms:assetid: 537a7b2b-d002-40a6-84ae-fd02635f9e23
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998031(v=EXCHG.150)
ms:contentKeyID: 51406515
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Implementación de Exchange 2013 en una topología de bosques de recursos de Exchange

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

En este tema, se explica cómo implementar Microsoft Exchange 2013 en una topología de bosques de recursos de Exchange. Un bosque de recursos de Exchange se llama también bosque dedicado de Exchange. En este tema, se supone que no tiene una topología existente de Exchange 2013.

En la figura siguiente se muestra una organización de Exchange con un bosque de recursos.

**Ejemplo de una organización de Exchange con un bosque de recursos de Exchange**

![Organización de Exchange compleja con bosque de recursos](images/Aa998031.706725cf-e520-4b89-a275-acd8fb58943a(EXCHG.150).gif "Organización de Exchange compleja con bosque de recursos")

## ¿Qué necesita saber antes de comenzar?

Para llevar a cabo el siguiente procedimiento en Exchange 2013, confirme los siguientes aspectos:

  - Dispone de los siguientes dos bosques de Active Directory:
    
      - Un bosque contiene las cuentas de usuario de la organización. En este procedimiento, este bosque recibe el nombre de *bosque de cuentas*.
    
      - Un bosque no contiene cuentas de usuario y aún no tiene instalado Exchange. En este procedimiento, este bosque recibe el nombre de *bosque de Exchange*. Usará el procedimiento para instalar Exchange 2013 en este bosque.

  - Ha configurado correctamente el Sistema de nombres de dominio (DNS) para la resolución de nombres en todos los bosques en la organización. Para comprobar que ha configurado DNS correctamente , haga ping en cada bosque desde otro bosque o bosques de la organización. Para obtener más información acerca de la configuración del DNS, consulte la [Guía de operaciones de servidores DNS](https://go.microsoft.com/fwlink/p/?linkid=282295).

## Implementación de Exchange 2013 en una topología de bosques de recursos de Exchange

1.  En un controlador de dominio en el bosque de Exchange, cree una relación de confianza externa unidireccional de modo que el bosque de Exchange confíe en el bosque de cuentas. Para ver pasos detallados, consulte [Crear una confianza de bosque unidireccional de salida para ambos lados de la confianza](https://go.microsoft.com/fwlink/p/?linkid=69130) .
    

    > [!NOTE]
    > Aunque se recomienda que cree una confianza de bosque, puede crear una confianza de bosque o una confianza externa. Si crea una confianza externa, al crear buzones de correo vinculados en el Paso&nbsp;3, en la página <STRONG>Cuenta maestra</STRONG> del Asistente para nuevo buzón de correo, debe especificar una cuenta de usuario que pueda tener acceso al controlador de dominio en el bosque de confianza. No puede usar las credenciales con las que inició la sesión actual. Si crea buzones de correo vinculados con el cmdlet <STRONG>New-Mailbox</STRONG>, debe especificar una cuenta de usuario que pueda tener acceso al controlador de dominio en el bosque de confianza con el parámetro <EM>LinkedCredential</EM>.



2.  En el bosque de Exchange, instale Exchange 2013. Instale Exchange del mismo modo que si se tratara de un escenario de bosque único. Para obtener instrucciones detalladas acerca de cómo instalar Exchange 2013, consulte uno de los siguientes temas:
    
      - [Implementar una nueva instalación de Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)
    
      - [Instalar Exchange 2013 utilizando el asistente de configuración](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)

3.  En el bosque de Exchange, cree un buzón de correo que esté asociado a una cuenta externa para cada usuario en el bosque de cuentas que tendrá un buzón de correo en el bosque de Exchange. Para conocer los pasos detallados, consulte [Administrar buzones vinculados](manage-linked-mailboxes-exchange-2013-help.md).

