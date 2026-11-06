# Auditoría de almacén · Project Agenda

Maqueta interactiva de la modificación de códigos, el reporte de códigos en Excel y el campo SAP Movement en Bill of Materials.

Es un prototipo en un solo archivo (`index.html`): no tiene backend, base de datos ni conexión con SAP. Todos los datos y personas son ficticios, y los cambios se pierden al recargar la página.

## Cómo verla

Abra `index.html` en el navegador (doble clic). Necesita internet para cargar la fuente Roboto y la librería que genera el Excel.

## Qué muestra

- **Code Request:** lista de códigos, botón *Report* y menú ⋯ en Actions con View, Edit, Delete, Modification Requested y Modification History según el estado.
- **Modification Requests (pestaña nueva):** solicitudes con estado Pending, Completed o Rejected, edición del código con vista previa de cambios y detalle de auditoría.
- **Report:** calendario para elegir el rango, por defecto el mes actual, y descarga de un Excel con el consolidado arriba y el detalle debajo.
- **Viewing as (encabezado):** cambia de usuario para probar permisos. Solo el rol Stockroom edita o rechaza solicitudes.

El enlace normal muestra las pestañas Code Request y Modification Requests. Los BOM tienen su propio enlace, con *SAP Movement*, timeline y reporte con el flujo completo (Created, Sent, Approved o Rejected, Requested, Delivery parcial o total, Signed, SAP y SAP Movement Modified): https://nataliahuertasn.github.io/Auditoria-Almacen-Project-Agenda/?view=bom

## Reglas pendientes de confirmar

Están marcadas como `DECISIÓN` en `index.html`.

| Tema | Regla usada en la maqueta |
|---|---|
| Opción Modification Requested | Sale en todas las filas de Code Request; solo se activa en códigos que ya tienen código SAP |
| Código con solicitud pendiente | Se puede seguir usando, pero no admite otra solicitud |
| Estado final del código | Vuelve al estado que tenía antes de la solicitud |
| Permisos | Cualquiera solicita; solo Stockroom edita o rechaza |
| Solicitudes erradas | Se agrega el estado Rejected, con motivo |
| BOM existentes | Conservan sus valores al editar un código |
| Detalle del reporte | Una fila por solicitud; cada modificación adicional va en una fila debajo, sin repetir la solicitud |
| Periodo del reporte | Incluye las solicitudes recibidas en el periodo y las anteriores que tuvieron una modificación en el periodo |
| Consolidado | Approved cuenta las solicitudes con código creado, aunque hoy estén en Modification Requested |
| Modification Status | Una modificación completada se muestra como Approved |
| SAP Movement | Solo dígitos y obligatorio para marcar el check; las entregas antiguas se pueden completar |
| Quantity Created, PA Code, Color, Alloy y Unit of Measure | Campos supuestos: falta validarlos contra el modelo real |

## Datos para el acta mensual

El acta está fuera de alcance. Cada solicitud guarda solicitante, fechas, motivo, responsable y cambios campo por campo, y cada entrega guarda su SAP Movement, así que el acta se podrá generar por mes a partir de esos datos.
