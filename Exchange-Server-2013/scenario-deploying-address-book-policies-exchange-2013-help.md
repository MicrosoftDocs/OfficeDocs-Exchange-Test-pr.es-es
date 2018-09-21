---
title: 'Caso: implementación directivas de libretas de direcciones: Exchange 2013 Help'
TOCTitle: 'Caso: implementación de directivas de libretas de direcciones'
ms:assetid: 6ac3c87d-161f-447b-afb2-149ae7e3f1dc
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ657455(v=EXCHG.150)
ms:contentKeyID: 49895688
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Caso: implementación de directivas de libretas de direcciones

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

## Escenarios de implementación

Los tres escenarios siguientes describen posibles soluciones de implementación para tres tipos de organización. Aunque existen muchos otros, los escenarios más conocidos se incluyen aquí. Las listas de direcciones y las listas globales de direcciones (LGD) de estos escenarios se crearon en base a filtros tales como Atributos personalizados que agrupan objetos de forma lógica.

## Escenario 1: Dos compañías independientes: una organización de Exchange

Este escenario es aplicable a las autoridades gubernamentales, divisiones o departamentos que compartan una infraestructura, pero que no tengan ninguna cadena de notificación ni empleados en común. Además, las divisiones no tienen ninguna preocupación especial relativa a la seguridad o a la privacidad. En este escenario se crean dos directivas de libretas de direcciones (ABP) en las que los empleados solo pueden ver a los miembros de la misma organización cuando visualizan la lista global de direcciones (GAL) o consultar la pertenencia de otros grupos de distribución. Además, ningún usuario es miembro de los grupos de distribución que abarcan toda la organización.

![Directivas de libreta de direcciones con dos empresas diferentes](images/JJ657455.b4fc82da-a659-4ade-ba33-d55d90dcf204(EXCHG.150).gif "Directivas de libreta de direcciones con dos empresas diferentes")

Las directivas de libretas de direcciones (ABP) Contoso y Humungous se crearon con las siguientes listas de direcciones, listas globales de direcciones, listas de salas y libretas de direcciones sin conexión (OAB), que a su vez se crearon mediante un filtro de destinatarios que agrupa los objetos con un filtro como, por ejemplo, Atributo personalizado. Debido a que las dos empresas son independientes y no existe ninguna interacción entre ambas, no hay ninguna lista de direcciones en común.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>Contoso</p></td>
<td><p>Humongous Insurance</p></td>
</tr>
<tr class="even">
<td><p>Listas de direcciones</p></td>
<td><p>LD_CON_Grupos</p>
<p>AL_CON_Users</p>
<p>LD_CON_Contactos</p></td>
<td><p>LD_HI_Grupos</p>
<p>AL_HI_Users</p>
<p>LD_HI_Contactos</p></td>
</tr>
<tr class="odd">
<td><p>Lista global de direcciones</p></td>
<td><p>LGD_CON</p></td>
<td><p>LGD_HI</p></td>
</tr>
<tr class="even">
<td><p>Lista de direcciones de salas</p></td>
<td><p>LD_CON_Salas</p></td>
<td><p>LD_HI_Salas</p></td>
</tr>
<tr class="odd">
<td><p>Libreta de direcciones sin conexión (OAB)</p></td>
<td><p>OAB_CON</p></td>
<td><p>OAB_HI</p></td>
</tr>
</tbody>
</table>


## Escenario 2: Dos empresas comparten un director general

En este escenario, Fabrikam y Tailspin Toys comparten la misma organización de Exchange y el mismo director general. El director general es la única persona en común entre las dos compañías. Este escenario requiere tres ABP, que tienen las siguientes características:

  - Los usuarios de Tailspin Toys solo pueden ver a los usuarios de Tailspin Toys cuando examinan la lista global de direcciones (GAL).

  - Los usuarios de Fabrikam solo pueden ver a los usuarios de Fabrikam cuando examinan la lista global de direcciones (GAL).

  - En cada empresa hay un grupo de distribución SeniorLeaders, que incluye a los altos ejecutivos de dicha empresa y al director general común.

  - Los usuarios que consulten la pertenencia del grupo del director general solo verán aquellos grupos que pertenezcan a su propia compañía, pero no a los que estén fuera de ella.

  - Se crean tres ABP: **Fab**, **Tail** y **CEO**.

![Dos empresas, un director general](images/JJ657455.c87a5654-d456-4688-acb2-0be15ba1cda6(EXCHG.150).gif "Dos empresas, un director general")


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>Fabrikam</p></td>
<td><p>Tailspin Toys</p></td>
<td><p>Presidente ejecutivo</p></td>
</tr>
<tr class="even">
<td><p>Listas de direcciones</p></td>
<td><p>LD_FAB_Usuarios_DG</p>
<p>LD_FAB_Contactos</p></td>
<td><p>LD_TAIL_Usuarios_DG</p>
<p>LD_TAIL_Contactos</p></td>
<td><p>LD_FAB_Usuarios_DG</p>
<p>LD_FAB_Contactos</p>
<p>LD_TAIL_Usuarios_DG</p>
<p>LD_TAIL_Contactos</p></td>
</tr>
<tr class="odd">
<td><p>Lista global de direcciones</p></td>
<td><p>LGD_FAB</p></td>
<td><p>LGD_TAIL</p></td>
<td><p>LGD predeterminada</p></td>
</tr>
<tr class="even">
<td><p>Lista de direcciones de salas</p></td>
<td><p>LD_FAB_Salas</p></td>
<td><p>LD_TAIL_Salas</p></td>
<td><p>Todas las salas predeterminadas</p></td>
</tr>
<tr class="odd">
<td><p>Libreta de direcciones sin conexión (OAB)</p></td>
<td><p>OAB_FAB</p></td>
<td><p>OAB_TAIL</p></td>
<td><p>OAB predeterminada</p></td>
</tr>
</tbody>
</table>


Cuando el director general se agrega a los grupos de distribución de cada organización y forma parte del ámbito de aplicación de la ABP de la compañía, el director general estará visible para todas las compañías. El director general puede crear grupos de distribución que abarquen ambas compañías y estén visibles en la GAL de cada compañía. No obstante, los miembros del grupo de distribución solo podrán ver a los miembros del grupo que estén dentro de su propia organización.

## Escenario 3: Educación

Este escenario se aplica a escuelas y universidades, en las que se necesita una división de aulas para asegurar la privacidad de los estudiantes. El escenario Educación tiene las siguientes características:

  - Los alumnos de cada aula solo pueden ver a los alumnos de su propia aula, a su profesor y al director.

  - Los profesores solo pueden ver a los alumnos de su propia aula.

  - Los profesores pueden ver al resto de profesores y al director.

  - Se crean grupos de distribución para los elementos principales de cada aula y para los profesores.

![Escenario de educación de directivas de libreta de direcciones](images/JJ657455.435f3b1a-9752-4c61-ab8a-80115c643d12(EXCHG.150).gif "Escenario de educación de directivas de libreta de direcciones")


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>Estudiantes_AulaA</p></td>
<td><p>Profesores_AulaA</p></td>
<td><p>Director</p></td>
</tr>
<tr class="even">
<td><p>Listas de direcciones</p></td>
<td><p>AL_ClassAAL_Principal</p></td>
<td><p>AL_ClassAAL_AllTeachersAL_AllGroupsAL_Principal</p></td>
<td><p>LD_AulaA</p>
<p>LD_AulaB</p>
<p>LD_TodosProfesores</p>
<p>LD_TodosEstudiantes</p>
<p>LD_TodosGrupos</p></td>
</tr>
<tr class="odd">
<td><p>Lista global de direcciones</p></td>
<td><p>LGD_EstudiantesAulaA</p></td>
<td><p>LGD_ProfesoresAulaA</p></td>
<td><p>LGD_Todos</p></td>
</tr>
<tr class="even">
<td><p>Lista de direcciones de salas</p></td>
<td><p>LD_SalaVacía</p></td>
<td><p>LD_SalaVacía</p></td>
<td><p>Todas las salas predeterminadas</p></td>
</tr>
<tr class="odd">
<td><p>Libreta de direcciones sin conexión (OAB)</p></td>
<td><p>OAB_EstudiantesAulaA</p></td>
<td><p>OAB_ProfesoresAulaA</p></td>
<td><p>OAB predeterminada</p></td>
</tr>
</tbody>
</table>


## Consideraciones y procedimientos recomendados

Cuando utilice las ABP en su organización, considere lo siguiente:

  - Para que las ABP funcionen correctamente, el buzón de usuario en el que aplica la ABP debe estar en un servidor Exchange 2010 SP3 o Exchange 2013.

  - No ejecute el rol de servidor de acceso de cliente de Exchange 2010 en el servidor de catálogo global. Si realiza esto, se usa Active Directory para la interfaz del proveedor de servicio de nombres (NSPI), en lugar del servicio de libreta de direcciones de Microsoft Exchange. Puede ejecutar los roles de servidor de Exchange 2013 en un servidor de catálogo global y lograr que las ABP funcionen correctamente; sin embargo, no se recomienda instalar Exchange en un controlador de dominio.

  - No se puede usar la libreta jerárquica de direcciones (LJD) y las ABP de manera simultánea. Para obtener más información, consulte [Libretas de direcciones jerárquicas](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/allow-users-to-see-a-voice-mail-transcript).

  - Los usuarios con ABP asignadas deben existir en su propia LGD.

  - Si permite que aplicaciones de clientes tengan acceso a Active Directory directamente a través de LDAP, omitirán la lógica integrada en las ABP. Outlook para Mac 2011 y Entourage 2008 usan consultas LDAP directas para tener acceso a Active Directory. Por este motivo, dichas aplicaciones de cliente no funcionarán adecuadamente con las ABP si el servicio de Detección automática les ha especificado o proporcionado un controlador de dominio o un servidor de catálogo global. Outlook para Mac 2011 puede usar EWS o una OAB local para tener acceso a la información del directorio. No obstante, si Outlook para Mac 2011 tiene acceso directamente a un servicio LDAP, intentará el acceso de este modo.

  - La LGD que se usa en una ABP debe contener, como mínimo, todas las listas de direcciones, incluida la lista de direcciones de salas definida y especificada en una ABP. No cree una LGD que contenga menos objetos que cualquiera de las listas de direcciones en la misma ABP.

  - Se recomienda crear grupos de distribución que no crucen los límites de la organización virtual. La creación de grupos de distribución que contengan miembros de varias organizaciones virtuales origina los siguientes problemas:
    
      - Si los miembros de los grupos solicitan confirmaciones de envío o de lectura cuando envían un correo al grupo de distribución, podrán ver las direcciones de correo electrónico de los miembros del grupo en otras organizaciones virtuales
    
      - Si se envía un mensaje cifrado al grupo de distribución y algunos miembros del grupo no poseen un identificador digital válido, el remitente recibirá un mensaje de advertencia que incluye el número total de miembros que no poseen un identificador válido y una lista de sus direcciones de correo electrónico. No obstante, si algunos de los miembros sin identificador digital válido están en una organización distinta a la del remitente, el mensaje de advertencia incluirá la cuenta correcta pero no incluirá las direcciones de correo electrónico de los miembros de la otra organización. Como resultado, el recuento total no coincidirá con la lista de direcciones de miembros.
        
        Por ejemplo, digamos que un grupo de distribución contiene en total cinco miembros de dos organizaciones, Agencia A y Agencia B. Tres miembros del grupo pertenecen a la Agencia A y uno de estos miembros tiene un identificador digital no válido. Los otros dos miembros pertenecen a la Agencia B y ambos tienen un identificador digital no válido. Si un miembro de la Agencia A envía un mensaje cifrado al grupo de distribución, dicho miembro recibirá un mensaje de advertencia de que hay un total de tres destinatarios sin identificador digital válido. No obstante, solo la dirección de correo electrónico para el destinatario de la Agencia A estará incluido en el mensaje de advertencia.
    
      - Las ABP no se aplican a los cmdlets **Get-Group**. Por lo tanto, cualquier usuario o proceso disponible para ejecutar **Get-Group** verá todos los miembros de cualquier grupo al que tenga acceso.
        
        Se recomienda modificar la configuración de la administración de grupos de las opciones OWA, de modo que los usuarios no puedan usar la Outlook Web App para administrar grupos. Para evitar que los usuarios usen las opciones OWA para administrar grupos, exclúyalos del rol RBAC MyDistributionGroupMembership. Para obtener información detallada, consulte [Rol MyDistributionGroupMembership](mydistributiongroupmembership-role-exchange-2013-help.md).
    
      - Si permite a los usuarios que usen Outlook o Outlook Web App para administrar grupos, los propietarios de los grupos deben tener completa visibilidad sobre los miembros del grupo.

  - Todas las ABP deben contener una lista de direcciones de salas. Sin embargo, si en su organización no se usan listas de direcciones de salas, puede crear una lista de direcciones de salas vacía predeterminada.

  - La implementación de las ABP no impide que los usuarios de una organización virtual envíen correos electrónicos a los usuarios de otra organización virtual. Si desea impedir que los usuarios envíen correos electrónicos de una organización a otra, se recomienda crear una regla de transporte. Por ejemplo, para crear una regla de transporte que impida que los usuarios de Contoso reciban mensajes de los usuarios de Fabrikam, pero que siga permitiendo al equipo de directivos de Fabrikam enviar mensajes a los usuarios de Contoso, ejecute el siguiente comando de Shell:
    
        New-TransportRule -Name "StopFabrikamtoContosoMail" -FromMemberOf "AllFabrikamEmployees" -SentToMemberOf "AllContosoEmployees" -DeleteMessage -ExceptIfFrom seniorleadership@fabrikam.com

  - Si quiere aplicar una característica similar a la ABP en el cliente Lync, puede establecer el atributo `msRTCSIP-GroupingID` en objetos específicos del usuario. Para obtener más detalles, vea el tema [PartitionByOU sustituida por msRTCSIP-GroupingID](https://go.microsoft.com/fwlink/p/?linkid=232306).

## Pasos generales de implementación

## Migración de la segmentación de listas de direcciones a ABP

Si en la organización se configuró una solución de segregación de listas de direcciones de Exchange 2007 mediante las instrucciones que figuran en las notas del producto [Configurar organizaciones virtuales y segregación de listas de direcciones en Exchange 2007](https://go.microsoft.com/fwlink/p/?linkid=109601) , primero debe migrar a Exchange Server 2010 siguiendo los pasos que se detallan en [Migrar a Exchange 2010 directivas de libretas de direcciones de una segregación de listas de direcciones de Exchange 2007](https://go.microsoft.com/fwlink/p/?linkid=235967). Este proceso requiere tiempo de inactividad para la organización y, por lo tanto, deberá programarlo de la manera conveniente.

## Nueva implementación de ABP

Si la organización va a implementar ABP de Exchange 2013 y no ha usado la segregación de listas de direcciones de Exchange 2007, utilice estas instrucciones para implementar las ABP en la organización.

Los pasos de esta sección lo guiarán a través del escenario 2: Escenario 2: Dos empresas comparten un director general. En este escenario, dos empresas (Fabrikam y Tailspin Toys) son independientes pero comparten el presidente ejecutivo y el equipo de directivos.

## Paso 1: Instalar y configurar al agente de enrutamiento de directivas de libretas de direcciones

Si usa ABP y no desea que los usuarios de diferentes organizaciones virtuales vean la información potencialmente confidencial del otro, puede activar el agente de enrutamiento de directivas de libretas de direcciones. El agente de enrutamiento de directivas de libretas de direcciones es un agente de transporte que se ejecuta en el servidor de buzones y controla cómo se resuelven los destinatarios en la organización. Cuando el agente de enrutamiento de directivas de libretas de direcciones está instalado y configurado, los usuarios a los que se les han asignado GAL diferentes aparecen como destinatarios externos, los cuales no pueden ver las tarjetas de contacto de otros destinatarios externos.

Para obtener instrucciones detalladas, consulte [Instalar y configurar al agente de enrutamiento de directivas de libretas de direcciones](install-and-configure-the-address-book-policy-routing-agent-exchange-2013-help.md).

## Paso 2: Dividir las organizaciones virtuales

Tendrá que desarrollar un modo para dividir las organizaciones. Se recomienda utilizar la propiedad CustomAttribute1-15 en los buzones, contactos y grupos, en lugar de los atributos condicionales predefinidos como Company, Department o StateOrProvince para dividir las organizaciones virtuales por los siguientes motivos:

  - No todos los tipos de destinatario de objetos tienen atributos condicionales predefinidos en Active Directory. Por ejemplo, Grupo de distribución y Grupo de distribución dinámico no admiten los atributos de compañía, departamento o estado.

  - No todos los atributos condicionales predefinidos están expuestos en cmdlets para algunos destinatarios. Por ejemplo, los parámetros *Company*, *department* y *StateOrProvince* no están disponibles en los cmdlets para usuarios, contactos, grupos de distribución y carpetas públicas habilitadas para correo.

  - Se requieren varios cmdlets para segregar destinatarios cuando se usa un atributo condicional predefinido. Por ejemplo, deberá ejecutar Set-User para etiquetar *Company*, *Department*, *StateOrProvince* para un UserMailbox después de ejecutar los cmdlets **New-Mailbox** o **Set-Mailbox**.

  - Los parámetros *CustomAttributeX* están expuestos en el cmdlet Set-\* de todos los tipos de destinatario, por lo que se puede completar la segregación de ese tipo a través de un solo cmdlet Set-

  - Los atributos CustomAttributeX se reservan explícitamente para la personalización de una organización y están bajo el control total de los administradores de la organización.

Otro procedimiento recomendado que puede implementar al segregar la organización es usar identificadores de compañía en los nombres de los grupos de distribución y los grupos de distribución dinámicos. Exchange incluye una característica de directiva de nomenclatura de grupo que agrega automáticamente un prefijo o un sufijo al nombre del grupo de distribución en función de varios atributos del usuario que crea el grupo de distribución, incluido el creador de los valores para Company, StateorProvince, Title y del CustomAttribute1 al CustomAttribute15 del grupo de distribución. Esta directiva de nomenclatura de grupo resulta especialmente importante si permite a los usuarios crear sus propios grupos de distribución. Para obtener más información, consulte [Crear una directiva de nomenclatura de grupos de distribución](https://docs.microsoft.com/es-es/exchange/recipients-in-exchange-online/manage-distribution-groups/create-group-naming-policy).

Las directivas de nomenclatura de grupo no se aplican a los grupos de distribución dinámicos, por lo que deberá segregarlos y aplicarles una directiva de nomenclatura manualmente.

## Paso 3: Crear las listas de direcciones, las LGD y las OAB

Al crear las listas de direcciones y las listas globales de direcciones, no use los parámetros "IncludedRecipient" ni "ConditionalX", como ConditionalCompany o ConditionalCustomAttribute5. En su lugar, utilice un filtro de destinatarios. Debe utilizar el Shell para crear filtros de destinatarios. Para obtener más información acerca de los filtros de destinatarios, consulte [Filtrado de destinatarios en servidores de transporte perimetral](recipient-filtering-on-edge-transport-servers-exchange-2013-help.md)

Al crear una ABP, deberá crear varias listas de direcciones en función de cómo desea que los usuarios vean las listas en Outlook o en Outlook Web App. Esta organización tiene cuatro listas de direcciones:

  - LD\_FAB\_Usuarios\_DG

  - LD\_FAB\_Contactos

  - LD\_TAIL\_Usuarios\_DG

  - LD\_TAIL\_Contactos

Este ejemplo crea la lista de dirección LD\_TAIL\_Usuarios\_DG. La lista de direcciones incluye todos los usuarios y grupos de distribución en los que el valor de CustomAttribute15 equivale a TAIL.

    New-AddressList -Name "AL_TAIL_Users_DGs" -RecipientFilter {((RecipientType -eq 'UserMailbox') -or (RecipientType -eq "MailUniversalDistributionGroup") -or (RecipientType -eq "DynamicDistributionGroup")) -and (CustomAttribute15 -eq "TAIL")}

Para obtener más información sobre la creación de listas de direcciones con filtros de destinatarios, vea [Crear una lista de direcciones mediante filtros de destinatario](https://docs.microsoft.com/es-es/exchange/address-books/address-lists/use-recipient-filters-to-create-an-address-list).

Para crear una ABP se necesita una lista de direcciones de salas. Si su organización no tiene buzones de recursos (tales como buzones de sala o de equipamiento), se recomienda crear una lista de direcciones de salas vacía. En el siguiente ejemplo se crea una lista de direcciones de salas vacía porque no hay buzones de sala en la organización.

    New-AddressList -Name AL_BlankRoom -RecipientFilter {(Alias -ne $null) -and ((RecipientDisplayType -eq 'ConferenceRoomMailbox') -or (RecipientDisplayType -eq 'SyncedConferenceRoomMailbox'))}

Sin embargo, en este escenario, Fabrikam y Contoso tienen buzones de sala. En este ejemplo se crea una lista de salas para Fabrikam mediante un filtro de destinatarios donde CustomAttribute15 equivale a FAB.

    New-AddressList -Name AL_FAB_Room -RecipientFilter {(Alias -ne $null) -and (CustomAttribute15 -eq "FAB")-and (RecipientDisplayType -eq 'ConferenceRoomMailbox') -or (RecipientDisplayType -eq 'SyncedConferenceRoomMailbox')}

La lista global de direcciones que se usa en una ABP debe ser un superconjunto de las listas de direcciones. No cree una LGD con menos objetos de los que existen en una o en todas las listas de direcciones en la ABP. En este ejemplo se crea la lista global de direcciones para Tailspin Toys que incluye todos los destinatarios que existen en las listas de direcciones y en la lista de direcciones de salas.

    New-GlobalAddressList -Name "GAL_TAIL" -RecipientFilter {(CustomAttribute15 -eq "TAIL")}

Para obtener más información, consulte [Crear una lista global de direcciones](https://docs.microsoft.com/es-es/exchange/address-books/address-lists/create-global-address-list).

Cuando se crea una OAB, debe incluir la LGD adecuada al proporcionar el parámetro *AddressLists* de New- o Set-OfflineAddressBook para garantizar que no se pierda ninguna entrada de manera inesperada. En resumen, puede personalizar el conjunto de entradas que ve un usuario o reducir el tamaño de descarga de la OAB mediante la especificación de una lista de AddressLists en AddressLists de New/Set-OfflineAddressBook. No obstante, si desea que los usuarios vean todo el conjunto de registros de la LGD en la OAB, asegúrese de que incluye la LGD en AddressLists.

En este ejemplo se crea la OAB para Fabrikam llamada OAB\_FAB.

    New-OfflineAddressBook -Name "OAB_FAB" -AddressLists "GAL_FAB"

Para obtener más información, consulte [Crear una libreta de direcciones sin conexión](https://docs.microsoft.com/es-es/exchange/address-books/offline-address-books/create-offline-address-book).

## Paso 4: Crear las ABP

Después de crear todos los objetos necesarios, entonces podrá crear la ABP. En este ejemplo se crea la ABP llamada ABP\_TAIL.

    New-AddressBookPolicy -Name "ABP_TAIL" -AddressLists "AL_TAIL_Users_DGs"," AL_TAIL_Contacts" -OfflineAddressBook "\OAB_TAIL" -GlobalAddressList "\GAL_TAIL" -RoomList "\AL_TAIL_Rooms"

Para obtener más información, consulte [Crear una directiva de libreta de direcciones](https://docs.microsoft.com/es-es/exchange/address-books/address-book-policies/create-an-address-book-policy).

## Paso 5: Asignar las ABP a los buzones de correo

El último paso del proceso es asignar la ABP al usuario. Las ABP se aplican cuando una aplicación de usuario se conecta al servicio de libreta de direcciones de Microsoft Exchange en el servidor de acceso de clientes. Si el usuario ya está conectado a Outlook o a Outlook Web App cuando se aplica la ABP a su cuenta, tendrá que cerrar y reiniciar la aplicación del cliente para poder ver las nuevas listas de direcciones y LGD.

En este ejemplo se asigna ABP\_FAB a todos los buzones donde CustomAttribute15 equivale a "FAB".

    Get-Mailbox -resultsize unlimited | where {$_.CustomAttribute15 -eq "TAIL"} | Set-Mailbox -AddressBookPolicy "ABP_TAIL"

Para obtener más información, consulte [Asignar una directiva de libreta de direcciones a usuarios de correo](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/delete-um-auto-attendant).

