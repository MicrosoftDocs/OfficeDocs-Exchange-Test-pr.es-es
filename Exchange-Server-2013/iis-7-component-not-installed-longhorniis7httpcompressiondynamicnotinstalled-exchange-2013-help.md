---
title: 'Componente de IIS 7 no instalado_LonghornIIS7HttpCompressionDynamicNotInstalled: Exchange 2013 Help'
TOCTitle: Componente de IIS 7 no instalado_LonghornIIS7HttpCompressionDynamicNotInstalled
ms:assetid: d909e329-2436-43f9-af75-a5ee14e67ebf
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.longhorniis7httpcompressiondynamicnotinstalled(v=EXCHG.150)
ms:contentKeyID: 48268742
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Componente de IIS 7 no instalado\_LonghornIIS7HttpCompressionDynamicNotInstalled

 

_**Se aplica a:**Exchange Server_

_**Última modificación del tema:**2015-03-09_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Microsoft Exchange Server 2010 Setup o Microsoft Exchange Server 2007 Setup no puede instalar el rol de servidor Acceso de cliente (CAS) o el rol de servidor Buzón de correo en un equipo basado en Microsoft Windows Server 2008 o en un equipo basado en Windows Server 2008 R2 porque los componentes de Internet Information Server (IIS) 7 no están instalados.

Exchange 2010 Setup y Exchange 2007 Setup requiere que el equipo basado en Windows Server 2008 o el equipo basado en Windows Server 2008 R2 donde está instalando el rol CAS ya tenga los siguientes componentes IIS 7 instalados.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Componentes IIS 7 necesarios para el rol de servidor Acceso de cliente</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Compresión de contenido dinámico</p></td>
</tr>
<tr class="even">
<td><p>Compresión de contenido estática</p></td>
</tr>
<tr class="odd">
<td><p>Autenticación básica</p></td>
</tr>
<tr class="even">
<td><p>Autenticación de Windows</p></td>
</tr>
<tr class="odd">
<td><p>Autenticación implícita IIS 7</p></td>
</tr>
<tr class="even">
<td><p>ASP.NET</p></td>
</tr>
<tr class="odd">
<td><p>Asignación de certificados de cliente</p></td>
</tr>
<tr class="even">
<td><p>Examen de directorios</p></td>
</tr>
<tr class="odd">
<td><p>Errores HTTP</p></td>
</tr>
<tr class="even">
<td><p>Registro HTTP</p></td>
</tr>
<tr class="odd">
<td><p>Redirección HTTP</p></td>
</tr>
<tr class="even">
<td><p>Seguimiento</p></td>
</tr>
<tr class="odd">
<td><p>Filtros ISAPI</p></td>
</tr>
<tr class="even">
<td><p>Monitor de solicitudes</p></td>
</tr>
<tr class="odd">
<td><p>Contenido estático</p></td>
</tr>
</tbody>
</table>


Exchange 2010 Setup y Exchange 2007 Setup requiere que el equipo basado en Windows Server 2008 o el equipo basado en Windows Server 2008 R2 donde está instalando el rol de servidor Buzón de correo ya tenga los siguientes componentes IIS 7 instalados.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Componentes IIS 7 necesarios para el rol de servidor Buzón de correo</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Autenticación básica</p></td>
</tr>
<tr class="even">
<td><p>Autenticación de Windows</p></td>
</tr>
</tbody>
</table>


Para solucionar el problema, siga los pasos adecuados para instalar los componentes IIS 7 necesarios en el equipo de destino y, a continuación, vuelva a ejecutar Microsoft Exchange Setup.

**Instale los componentes IIS 7 para el rol de servidor Acceso de cliente usando el Administrador de servidores de Windows Server 2008**

1.  Haga clic en **Inicio**, seleccione **Herramientas administrativas** y, a continuación, haga clic en **Administrador de servidores**.

2.  En el panel de navegación izquierdo, expanda **Roles** y, a continuación, haga clic con el botón secundario en **Servidor web (IIS)** y, a continuación, haga clic en **Agregar servicios de rol**.

3.  En el panel **Seleccionar servicios de rol**, desplácese hasta **IIS**.

4.  En el área **Seguridad**, haga clic para seleccionar las siguientes casillas de verificación:
    
      - **Autenticación básica**
    
      - **Autenticación de acceso implícita**
    
      - **Autenticación de Windows**

5.  En el área **Rendimiento**, haga clic para seleccionar las siguientes casillas de verificación:
    
      - **Compresión estática**
    
      - **Compresión dinámica**

6.  En el panel **Seleccionar servicios de rol**, haga clic en **Siguiente** y, a continuación, haga clic en **Instalar** en el panel **Confirmar selecciones de instalación**.

7.  Haga clic en **Cerrar** para salir del Asistente para agregar servicios de rol.

**Instale los componentes IIS 7 para el rol de servidor Buzón de correo usando el Administrador de servidores de Windows Server 2008**

1.  Haga clic en **Inicio**, seleccione **Herramientas administrativas** y, a continuación, haga clic en **Administrador de servidores**.

2.  En el panel de navegación izquierdo, expanda **Roles** y, a continuación, haga clic con el botón secundario en **Servidor web (IIS)** y, a continuación, haga clic en **Agregar servicios de rol**.

3.  En el panel **Seleccionar servicios de rol**, desplácese hasta **IIS**.

4.  En el área **Seguridad**, haga clic para seleccionar las siguientes casillas de verificación:
    
      - **Autenticación básica**
    
      - **Autenticación de Windows**

5.  En el panel **Seleccionar servicios de rol**, haga clic en **Siguiente** y, a continuación, haga clic en **Instalar** en el panel **Confirmar selecciones de instalación**.

6.  Haga clic en **Cerrar** para salir del Asistente para agregar servicios de rol.

