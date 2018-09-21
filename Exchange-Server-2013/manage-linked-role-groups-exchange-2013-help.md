---
title: 'Administrar grupos de funciones vinculadas: Exchange 2013 Help'
TOCTitle: Administrar grupos de funciones vinculadas
ms:assetid: e2a07395-90c2-4d62-b15d-ac3ff28fe786
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ657502(v=EXCHG.150)
ms:contentKeyID: 49895977
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Administrar grupos de funciones vinculadas

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-09_

Puede usar un grupo de roles de administración vinculado para permitirles a los miembros de un grupo de seguridad universal (USG) en un bosque Active Directory externo administrar una organización de Exchange Server 2013 de Microsoft en un bosque Active Directory de recursos. Al asociar un USG en un bosque externo con un grupo de funciones vinculado, las funciones de administración asignadas al grupo de funciones vinculado conceden permisos a los miembros de ese USG. Para obtener más información acerca de los grupos de funciones vinculados, consulte [Descripción de los grupos de roles de administración](understanding-management-role-groups-exchange-2013-help.md).

Para crear y configurar grupos de roles vinculados, debe usar los cmdlets **New-RoleGroup** y **Set-RoleGroup**. Para obtener información detallada acerca de la sintaxis y los parámetros, consulte los siguientes temas:

  - [New-RoleGroup](https://technet.microsoft.com/es-es/library/dd638181\(v=exchg.150\))

  - [Set-RoleGroup](https://technet.microsoft.com/es-es/library/dd638182\(v=exchg.150\))

Para otras tareas de administración relacionadas con los grupos de roles, consulte [Permisos](permissions-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: de 5 a 10 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Grupos de roles" en el tema [Permisos de administración de roles](role-management-permissions-exchange-2013-help.md).

  - No puede usar el centro de administración de Exchange (EAC) para crear o configurar grupos de roles vinculados. Se debe usar el Shell de administración de Exchange.

  - La configuración de un grupo de roles vinculado requiere, como mínimo, confianza unidireccional entre el bosque de recursos Active Directory en el que residirá el grupo de roles vinculado, y el bosque externo Active Directory en donde residen los usuarios o miembros del USG. El bosque de recursos debe confiar en el bosque externo.

  - Debe tener la siguiente información sobre el bosque externo Active Directory:
    
      - **Credenciales**   Debe tener un nombre de usuario y una contraseña con los que se pueda tener acceso al bosque externo Active Directory. Esta información se usa con el parámetro *LinkedCredential* en los cmdlets **New-RoleGroup** y **Set-RoleGroup**.
    
      - **Controlador de dominio**   Debe tener el nombre de dominio completo (FQDN) de un controlador de dominio de Active Directory en el bosque externo Active Directory. Esta información se usa con el parámetro *LinkedDomainController* en los cmdlets **New-RoleGroup** y **Set-RoleGroup**.
    
      - **USG externo**   Debe tener el nombre completo de USG en el bosque externo Active Directory que contenga a los miembros que desee asociar con el grupo de funciones vinculado. Esta información se usa con el parámetro *LinkedForeignGroup* en los cmdlets **New-RoleGroup** y **Set-RoleGroup**.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Crear un grupo de roles vinculado

## Usar Shell para crear un grupo de funciones vinculado sin ámbito

Para crear un grupo de funciones vinculado y asignarle funciones de administración, realice las siguientes acciones:

1.  Almacene las credenciales del bosque externo Active Directory en una variable.
    
    ```powershell
$ForeignCredential = Get-Credential
```

2.  Cree el grupo de funciones vinculadas con la siguiente sintaxis.
    
        New-RoleGroup <role group name> -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential -Roles <role1, role2, role3...>

3.  Agregue o quite miembros del grupo de seguridad universal externo mediante usuarios y equipos Active Directory en un equipo en el bosque externo Active Directory.

En este ejemplo se realiza lo siguiente:

  - Se recuperan las credenciales para el bosque externo Active Directory de users.contoso.com. Las credenciales se usan para establecer conexión con el controlador de dominio DC01.users.contoso.com en el bosque externo.

  - Se crea un grupo de funciones vinculado denominado Compliance Role Group en el bosque de recursos donde se instala Exchange 2013.

  - El nuevo grupo de funciones está vinculado Compliance Administrators USG en el bosque externo Active Directory usuarios.contoso.com.

  - Se asignan las Reglas de transporte y las funciones de administración de registro en diario al nuevo grupo de funciones vinculado.

<!-- end list -->

```powershell
$ForeignCredential = Get-Credential
```
    New-RoleGroup "Compliance Role Group" -LinkedForeignGroup "Compliance Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -Roles "Transport Rules", "Journaling"

## Usar Shell para crear un grupo de funciones vinculado con un ámbito de administración personalizado

Es posible crear grupos de funciones vinculados con ámbitos de administración de destinatarios personalizados, ámbitos de administración de configuración personalizados, o ambos. Para crear un grupo de funciones vinculado y asignarle funciones de administración con ámbitos personalizados, realice las siguientes acciones:

1.  Almacene las credenciales del bosque externo Active Directory en una variable.
    
    ```powershell
$ForeignCredential = Get-Credential
```

2.  Cree el grupo de funciones vinculadas con la siguiente sintaxis.
    
        New-RoleGroup <role group name> -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -CustomConfigWriteScope <name of configuration scope> -CustomRecipientWriteScope <name of recipient scope> -LinkedCredential $ForeignCredential -Roles <role1, role2, role3...>

3.  Agregue o quite miembros del grupo de seguridad universal externo mediante usuarios y equipos Active Directory en un equipo en el bosque externo Active Directory.

En este ejemplo se realiza lo siguiente:

  - Se recuperan las credenciales para el bosque externo Active Directory de users.contoso.com. Las credenciales se usan para establecer conexión con el controlador de dominio DC01.users.contoso.com en el bosque externo.

  - Se crea un grupo de funciones vinculado denominado Seattle Compliance Role Group en el bosque de recursos donde se instala Exchange 2013.

  - El nuevo grupo de funciones está vinculado al Seattle Compliance Administrators USG en el bosque externo Active Directory usuarios.contoso.com.

  - Se asignan las Reglas de transporte y funciones de administración en diario al nuevo grupo de funciones vinculado al ámbito de destinatarios personalizado de Seattle Recipients.

<!-- end list -->

```powershell
$ForeignCredential = Get-Credential
```
    New-RoleGroup "Seattle Compliance Role Group" -LinkedForeignGroup "Seattle Compliance Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -CustomRecipientWriteScope "Seattle Recipients" -Roles "Transport Rules", "Journaling"

Para obtener más información acerca de los ámbitos de administración, consulte [Descripción de los ámbitos de roles de administración](understanding-management-role-scopes-exchange-2013-help.md).

## Usar Shell para crear un grupo de funciones vinculado con un ámbito de UO

Puede crear grupos de funciones vinculados que utilizan un ámbito de destinatario de UO. Para crear un grupo de funciones vinculado y asignarle funciones de administración con un ámbito de UO, realice las siguientes acciones:

1.  Almacene las credenciales del bosque externo Active Directory en una variable.
    
    ```powershell
$ForeignCredential = Get-Credential
```

2.  Cree el grupo de funciones vinculadas con la siguiente sintaxis.
    
        New-RoleGroup <role group name> -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential -RecipientOrganizationalUnitScope <OU name> -Roles <role1, role2, role3...>

3.  Agregue o quite miembros del grupo de seguridad universal externo mediante usuarios y equipos Active Directory en un equipo en el bosque externo Active Directory.

En este ejemplo se realiza lo siguiente:

  - Se recuperan las credenciales para el bosque externo Active Directory de users.contoso.com. Las credenciales se usan para establecer conexión con el controlador de dominio DC01.users.contoso.com en el bosque externo.

  - Se crea un grupo de funciones vinculado denominado Executives Compliance Role Group en el bosque de recursos donde se instala Exchange 2013.

  - El nuevo grupo de funciones está vinculado a Executives Compliance Role Group en el bosque externo Active Directory usuarios.contoso.com.

  - Se asignan las Reglas de transporte y funciones de administración en diario al nuevo grupo de funciones vinculado con UO de Ejecutivos de ámbito de destinatario de UO.

<!-- end list -->

```powershell
$ForeignCredential = Get-Credential
```
    New-RoleGroup "Executives Compliance Role Group" -LinkedForeignGroup "Executives Compliance Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -RecipientOrganizationalUnitScope "Executives OU" -Roles "Transport Rules", "Journaling"

Para obtener más información acerca de los ámbitos de administración, consulte [Descripción de los ámbitos de roles de administración](understanding-management-role-scopes-exchange-2013-help.md).

## Cambiar el USG externo en un grupo de roles vinculado

## Uso del Shell para cambiar el grupo de seguridad universal externo en un grupo de funciones vinculado

Para cambiar el grupo de seguridad universal externo asociado con un grupo de funciones vinculado, efectúe lo siguiente:

1.  Almacene las credenciales del bosque externo Active Directory en una variable.
    
    ```powershell
$ForeignCredential = Get-Credential
```

2.  Use la siguiente sintaxis para cambiar el USG externo en el grupo de roles vinculado existente.
    
        Set-RoleGroup <role group name> -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential 

En este ejemplo se realiza lo siguiente:

  - Se recuperan las credenciales para el bosque externo Active Directory de users.contoso.com. Las credenciales se usan para establecer conexión con el controlador de dominio DC01.users.contoso.com en el bosque externo.

  - Cambia el grupo de seguridad universal externo en el grupo de funciones Compliance Role Group a Regulatory Compliance Officers.

<!-- end list -->

```powershell
$ForeignCredential = Get-Credential
```
    Set-RoleGroup "Compliance Role Group" -LinkedForeignGroup "Regulatory Compliance Officers" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential

