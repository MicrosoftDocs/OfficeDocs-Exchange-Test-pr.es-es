---
title: 'Exportar los resultados de la búsqueda de exhibición de documentos electrónicos a un archivo PST: Exchange 2013 Help'
TOCTitle: Exportar los resultados de la búsqueda de exhibición de documentos electrónicos a un archivo PST
ms:assetid: bc47f5f9-d056-4b69-b669-ae65fad541c8
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn440164(v=EXCHG.150)
ms:contentKeyID: 59636658
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exportar los resultados de la búsqueda de exhibición de documentos electrónicos a un archivo PST

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2017-09-07_

Puede utilizar la herramienta de exportación de eDiscovery en Centro de administración de Exchange (EAF) para exportar los resultados de una búsqueda de eDiscovery In situ a un archivo de datos de Outlook, que también se denomina un archivo PST. Los administradores pueden distribuir los resultados de la búsqueda a otras personas dentro de su organización, como un administrador de recursos humanos o registros, o para oponerse a un asesor en casos legales. Después de exportan los resultados de la búsqueda a un archivo PST, usted u otros usuarios pueden abrir en Outlook para revisar o imprimir mensajes devueltos en los resultados de la búsqueda. También se pueden abrir archivos PST en eDiscovery de terceros y aplicaciones de informes. Este tema muestra cómo hacer esto, así como solucionar los problemas que puedan existir.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: el tiempo varía en función de la cantidad y el tamaño de los resultados de búsqueda que se exportarán.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "eDiscovery local" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - El equipo que utilice para exportar los resultados de la búsqueda a un archivo PST debe cumplir los siguientes requisitos del sistema:
    
      - Versiones de 32 o 64 bits de Windows 7 y versiones posteriores
    
      - Microsoft.NET Framework 4.7
    
      - Un explorador compatible:
        
          - Internet Explorer 10 y versiones posteriores
            
            O bien
        
          - Mozilla Firefox o Google Chrome. Si usa cualquiera de estos navegadores, asegúrese de instalar la extensión *ClickOnce*. Para instalar el complemento ClickOnce, consulte [Complementos ClickOnce de Mozilla](https://addons.mozilla.org/en-us/firefox/search/?q=clickonce%26cat=1%2c0%26appver=%26platform=) o [ClickOnce para Google Chrome](https://chrome.google.com/webstore/search/clickonce?_category=extensions).

  - Necesita un buzón activo adjunto a la cuenta que desea exportar.

  - Compruebe que la configuración de la intranet local está configurada correctamente en Internet Explorer. Asegúrese de que **https://\*.outlook.com** se agrega a la zona de la intranet local.

  - Asegúrese de que no se muestran las siguientes direcciones URL en la zona de sitios de confianza:
    
      - https://\*.outlook.com
    
      - https://r4.res.outlook.com
    
      - https://\*.res.outlook.com

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Usar el Centro de administración de Exchange para exportar los resultados de la búsqueda de eDiscovery local a un archivo PST

1.  Vaya a **Administración del cumplimiento** \> **Suspensión y exhibición de documentos electrónicos local**.

2.  En la vista de lista, seleccione la búsqueda de exhibición de documentos electrónicos local cuyos resultados quiere exportar y, luego, haga clic en **Exportar a un archivo PST**.
    
    ![Exportar a un archivo PST](images/Dn440164.1ebee2ac-89b3-49fa-b70c-a07c9a65f958(EXCHG.150).gif "Exportar a un archivo PST")  

3.  En la ventana de la **herramienta de exportación de PST de exhibición de documentos electrónicos**:
    
      - Haga clic en **Examinar** para especificar la ubicación donde quiere descargar el archivo PST.
    
      - Haga clic en la casilla **Habilitar desduplicación** para excluir los mensajes duplicados. Solo se incluirá una instancia de cada mensaje en el archivo PST.
    
      - Haga clic en la casilla **Incluir elementos no aptos para la búsqueda** si quiere incluir los elementos del buzón que no pudieron buscar (por ejemplo, los mensajes con datos adjuntos de tipos de archivo que Exchange Search no pudo indizar). Los elementos no aptos para la búsqueda se exportan a un archivo PST independiente.
        

        > [!IMPORTANT]
        > La inclusión de elementos que no se pueden buscar al exportar resultados de la búsqueda de exhibición de documentos electrónicos tarda más cuando los buzones contienen muchos elementos que no se pueden buscar. Para reducir el tiempo necesario para exportar los resultados de la búsqueda y evitar grandes archivos de exportación de PST, tenga en cuenta las siguientes recomendaciones: 
        > <UL>
        > <LI>
        > <P>Cree varias búsquedas de exhibición de documentos electrónicos que cada una busque un número menor de buzones de origen.</P>
        > <LI>
        > <P>Si va a exportar todo el contenido del buzón dentro de un intervalo de fechas específico (no especificando ninguna palabra clave en los criterios de búsqueda), todos los elementos que no se pueden buscar dentro de ese intervalo de fechas se incluirán automáticamente en los resultados de la búsqueda. Por lo tanto, no active la casilla <STRONG>Incluir elementos que no se pueden buscar</STRONG>.</P></LI></UL>



4.  Haga clic en **Inicio** para exportar los resultados de búsqueda a un archivo PST.
    
    Se mostrará una ventana con información de estado sobre el proceso de exportación.

## Más información

  - Puede reducir el tamaño del archivo de exportación PST si exporta solo los elementos que no se pueden buscar. Para ello, cree o edite una búsqueda, especifique una fecha de inicio en el futuro y después quite las palabras clave del cuadro **Palabras clave**. Esto hará que no se devuelvan resultados de búsqueda. Al copiar o exportar los resultados de la búsqueda y activar la casilla **Incluir elementos que no se pueden buscar**, solo los elementos que no se pueden buscar se copiarán al buzón de detección o se exportarán al archivo PST.

  - Si habilita la desduplicación, se exportarán todos los resultados de la búsqueda en un solo archivo PST. Si no habilita la desduplicación, se exportará un archivo PST independiente por cada buzón incluido en la búsqueda. Y, como se explicó anteriormente, los elementos no aptos para la búsqueda se exportan a un archivo PST independiente.

  - Además de los archivos PST que contienen los resultados de búsqueda, se exportan otros dos archivos:
    
      - Un archivo de configuración (en formato de archivo .txt) que contiene información sobre la solicitud de exportación a PST, como el nombre de la búsqueda de exhibición de documentos electrónicos que se exportó, la fecha y la hora de la exportación, si estaban habilitadas las opciones de desduplicación y los elementos no aptos para la búsqueda, la consulta de búsqueda y los buzones de origen en los que se realizó la búsqueda.
    
      - Un registro de resultados de búsqueda (en formato de archivo .csv) que contiene una entrada por cada mensaje devuelto en los resultados de búsqueda. Cada entrada identifica el buzón de origen donde se encuentra el mensaje. Si habilitó la desduplicación, le permite identificar todos los buzones que contienen un mensaje duplicado.

  - El nombre de la búsqueda es la primera parte del nombre de archivo de cada archivo que se exporta. Además, se anexa la fecha y la hora de la solicitud de exportación al nombre de archivo de cada archivo PST y al registro de resultados.

  - Para más información sobre la desduplicación y los elementos no aptos para la búsqueda, consulte:
    
      - [Estimate, preview, and copy search results](in-place-ediscovery-exchange-2013-help.md)
    
      - [Elementos no aptos para la búsqueda en la exhibición de documentos electrónicos de Exchange](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md)

  - Para exportar los resultados de búsqueda de exhibición de documentos electrónicos desde el Centro de exhibición de documentos electrónicos de SharePoint o SharePoint Online, consulte [Exportar contenido de exhibición de documentos electrónicos y crear informes](https://go.microsoft.com/fwlink/p/?linkid=324757).

## Solución de problemas


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Síntoma</th>
<th>Posible causa</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>No se puede exportar a un archivo PST.</p></td>
<td><ul>
<li><p>No hay ningún buzón activo adjunto a la cuenta. Para exportar el archivo PST, debe tener una cuenta activa.</p></li>
<li><p>Su versión de Internet Explorer está obsoleta. Intente actualizar Internet Explorer a la versión 10 o posterior o pruébelo con otro navegador.</p></li>
<li><p>Los criterios de búsqueda especificados en la consulta <strong>Filtro basado en criterios</strong> son incorrectos. Por ejemplo, se especifica un nombre de usuario en lugar de una dirección de correo electrónico. Para obtener más información sobre cómo filtrar en función de los criterios, consulte <a href="modify-an-in-place-ediscovery-search-exchange-2013-help.md">Modificar una búsqueda de exhibición de documentos electrónicos local</a>.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>No se pueden exportar los resultados de la búsqueda en un equipo concreto. La exportación funciona según lo esperado en otro equipo.</p></td>
<td><p>Se guardaron credenciales incorrectas de Windows en el <strong>Administrador de credenciales</strong>. Borre las credenciales y vuelva a iniciar sesión.</p></td>
</tr>
<tr class="odd">
<td><p>La herramienta de exportación de PST de exhibición de documentos electrónicos no se iniciará.</p></td>
<td><p>La configuración de la zona de la intranet local no está configurada correctamente en Internet Explorer. Asegúrese de que *.outlook.com, *.office365.com, *.sharepoint.com y *.onmicrosoft.com aparezcan en los sitios de confianza de la zona de la intranet local.</p>
<p>Para agregar estos sitios a la zona de confianza de Internet Explorer, consulte <a href="https://windows.microsoft.com/es-es/windows/security-zones-adding-removing-websites#1tc=windows-7">Zonas de seguridad: agregar o quitar sitios web</a>.</p></td>
</tr>
</tbody>
</table>

