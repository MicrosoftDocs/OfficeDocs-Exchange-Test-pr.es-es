---
title: 'Modificar, deshabilitar o quitar una directiva de uso compartido: Exchange 2013 Help'
TOCTitle: Modificar, deshabilitar o quitar una directiva de uso compartido
ms:assetid: 714af42d-ca29-4bb4-ac48-f0b3d4fd1c15
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ657460(v=EXCHG.150)
ms:contentKeyID: 49895703
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Modificar, deshabilitar o quitar una directiva de uso compartido

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-02-15_

El hecho de compartir directivas permite que los usuarios individuales de la organización de Exchange compartan la información de disponibilidad de los calendarios con otras organizaciones federadas, con organizaciones de Exchange no federadas y con usuarios individuales de Internet. Durante el curso de operaciones habituales, puede cambiar algunas propiedades de la directiva de uso compartido, como por ejemplo modificar las reglas de uso compartido, cambiar el nivel de acceso de disponibilidad, deshabilitar temporalmente una directiva de uso compartido o eliminar una por completo.

Para obtener más información acerca del uso compartido federado, consulte [Uso compartido](sharing-exchange-2013-help.md)

Para obtener información acerca de cómo crear una directiva de uso compartido, consulte [Crear una directiva de uso compartido](create-a-sharing-policy-exchange-2013-help.md)

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada «Permisos de calendario y uso compartido» en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Usar el EAC para modificar una directiva de uso compartido

1.  Vaya a **organización** \> **uso compartido**.

2.  Bajo **Uso compartido individual**, seleccione una directiva de uso compartido y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En **directiva de uso compartido**, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar")

4.  En **regla de uso compartido**, modifique las reglas de uso compartido según corresponda. Puede cambiar opciones como el dominio con el que quiere compartir información, y el nivel de uso compartido para las citas de calendario. Al finalizar, haga clic en **guardar** para cerrar el cuadro de diálogo **reglas de uso compartido**.

5.  En **directiva de uso compartido**, haga clic en **guardar** para actualizar la directiva de uso compartido.

## Usar el EAC para establecer una directiva de uso compartido como directiva de uso compartido predeterminada

1.  Vaya a **organización** \> **uso compartido**.

2.  Bajo **Uso compartido individual**, seleccione una directiva de uso compartido y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En **directiva de uso compartido** , active la casilla **Hacer que esta sea mi directiva de uso compartido predeterminada**.

4.  Haga clic en **guardar** para actualizar la directiva de uso compartido.

## Usar el EAC para deshabilitar una directiva de uso compartido

1.  Vaya a **Organización** \> **Uso compartido**.

2.  Bajo **Uso compartido individual**, seleccione compartir una directiva.

3.  En la columna **Activada**, desmarque la casilla de la directiva de uso compartido que desea deshabilitar.

## Usar el EAC para quitar una directiva de uso compartido


> [!IMPORTANT]
> Antes de quitar una directiva de uso compartido, ésta debe eliminarse de todos los buzones de usuarios.



1.  Vaya a **organización** \> **uso compartido**.

2.  Bajo **Uso compartido individual**, seleccione una directiva de uso compartido y, a continuación, haga clic en **Eliminar**![Eliminar icono](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Eliminar icono").

3.  En la advertencia, haga clic en **sí** para eliminar la directiva de uso compartido.

## Usar el Shell para modificar, deshabilitar o eliminar una directiva de uso compartido

  - Este ejemplo modifica la directiva de uso compartido Contoso para contoso.com, que es un dominio fuera de su organización. Esta directiva permite a los usuarios en el dominio Contoso ver información de disponibilidad simple.
    
        Set-SharingPolicy -Identity Contoso -Domains 'sales.contoso.com: CalendarSharingFreeBusySimple'

  - En este ejemplo se agrega un segundo dominio a la directiva de uso compartido Contoso. Cuando agrega un dominio a una directiva existente, debe incluir todos los dominios incluidos anteriormente.
    
        Set-SharingPolicy -Identity Contoso -Domains 'contoso.com: CalendarSharingFreeBusySimple', 'atlanta.contoso.com: CalendarSharingFreeBusyReviewer', 'beijing.contoso.com: CalendarSharingFreeBusyReviewer'

  - En este ejemplo se establece la directiva de uso compartido Contoso como directiva predeterminada.
    
        Set-SharingPolicy -Identity Contoso -Default $True

  - En este ejemplo se deshabilita la directiva de uso compartido Contoso.
    
        Set-SharingPolicy -Identity "Contoso" -Enabled $False

  - El primer ejemplo quita la directiva de uso compartido Contoso. El segundo ejemplo quita la directiva de uso compartido Contoso y suprime la confirmación de que desea eliminar la directiva.
      ```
        Remove-SharingPolicy -Identity Contoso
      ```
      ```
        Remove-SharingPolicy -Identity Contoso -Confirm
      ```
      
Para obtener más información acerca de la sintaxis y los parámetros, consulte [Set-SharingPolicy](https://technet.microsoft.com/es-es/library/dd297931\(v=exchg.150\)) y [Remove-SharingPolicy](https://technet.microsoft.com/es-es/library/dd351071\(v=exchg.150\)).

