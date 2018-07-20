---
title: 'No en el sitio/dominio del maestro de esquema_NotInSchemaMasterDomain: Exchange 2013 Help'
TOCTitle: No en el sitio/dominio del maestro de esquema_NotInSchemaMasterDomain
ms:assetid: 5e44eb33-4c30-4c3d-ba68-5c30bef1731f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.notinschemamasterdomain(v=EXCHG.150)
ms:contentKeyID: 48268186
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# No en el sitio/dominio del maestro de esquema\_NotInSchemaMasterDomain

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2016-12-09_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La instalación de Microsoft® Exchange Server 2007 no puede continuar porque el equipo que ejecuta el programa de instalación no se encuentra en el mismo sitio o dominio del servicio directorio de Active Directory® que el servidor al que se ha asignado la función de maestro de esquema de dominio, también conocida como FSMO (Flexible Single Master Operations).

La instalación de Exchange 2007 requiere que el controlador de dominio que sirve como maestro de esquema de dominio esté en el mismo sitio y dominio que el equipo local que ejecuta el programa de instalación de Exchange.

El maestro de esquema de dominio controla todas las actualizaciones y modificaciones que se realizan en el esquema de Active Directory.

Para resolver este problema, ejecute el programa de instalación de Exchange Server 2007 con los modificadores **/prepareschema** y **/prepareAD** desde el mismo sitio y dominio que el esquema de dominio maestro.

Para obtener más información acerca de los modificadores de setup **/prepareschemay/PrepareAD**, vea el tema de documentación de producto de Exchange 2007 "Cómo preparar Active Directory y los dominios" (<https://go.microsoft.com/fwlink/?linkid=78453>)

Puede usar la herramienta Maestro de esquema para identificar la función. Sin embargo, el archivo Schmmgmt.dll deberá estar registrado para que esta herramienta esté disponible como un complemento MMC.

Para ver el maestro de esquema actual

1.  En el símbolo del sistema, escriba **regsvr32 schmmgmt.dll**.
    

    > [!NOTE]
    > <STRONG>RegSvr32</STRONG> se ha registrado correctamente si se muestra el siguiente cuadro de diálogo:<BR>DllRegisterServer in schmmgmt.dll succeeded.



2.  Para abrir una nueva consola de administración, haga clic en **Inicio**, en **Ejecutar** y, a continuación, escriba **mmc**.

3.  En el menú de la consola, haga clic en **Agregar o quitar complemento**.

4.  Haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar un complemento independiente**.

5.  Seleccione **Active Directory Schema** y, a continuación, haga clic en **Agregar**.

6.  "Active Directory Schema" se mostrará así en Agregar o quitar complemento. Haga clic en **Cerrar** y, a continuación, haga clic en **Aceptar** para volver a la consola.

7.  Seleccione **Active Directory Schema** para que las secciones **Clases** y **Atributos** se muestren en la parte derecha.

8.  Haga clic con el botón secundario en **Active Directory Schema** y, a continuación, haga clic en **Operations Master**.

9.  Se mostrará el maestro de esquema actual.

Después de identificar el maestro de esquema actual, determine en qué subred de ubica el maestro de esquema. A continuación, use uno de los métodos siguientes para instalar Exchange:

  - Modifique la subred en el servidor de Exchange y muévalo al sitio donde se encuentra el maestro de esquema. A continuación, instale Exchange.

  - Fuerce temporalmente un cambio de pertenencia al sitio en el servidor de Exchange y, a continuación, instale Exchange. Después de instalar Exchange, vuelva el servidor de Exchange a su sitio original.

Para forzar la pertenencia al sitio

1.  En el servidor donde desea instalar Exchange, inicie el Editor del registro. Para hacerlo, haga clic en **Inicio**, haga clic en **Ejecutar**, escriba **regedit** y, a continuación, haga clic en **Aceptar**.

2.  Busque la siguiente subclave del Registro:
    
    **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\Netlogon\\Parameters**

3.  Cree el siguiente valor **Cadena**:
    
    Nombre de valor: **Nombre de sitio**
    
    Tipo de valor: **REG\_SZ**
    
    Datos de valor: **\<sitio\_que\_contiene\_el\_maestro\_esquema\>**

4.  Salga del Editor del registro y reinicie el servicio Netlogon. Esta acción fuerza al servidor Exchange a participar en el sitio que ha especificado.

5.  Instale Exchange

6.  Elimine la entrada del registro que agregó en el paso 3.

7.  Reinicie el servicio Netlogon. Esta acción devuelve Exchange al sitio original.

