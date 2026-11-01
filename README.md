# Matriz de Pruebas y Checklist de Aceptación — FORMA MVP

## 1. Información general

- **Proyecto:** FORMA
- **Documento:** Matriz de pruebas y checklist de aceptación
- **Versión:** 1.0
- **Responsable:** Thomas — QA / Tester
- **Objetivo:** Verificar las funcionalidades esenciales del MVP antes de cada demo o release.

---

## 2. Alcance de las pruebas

### 2.1 Tienda web

- [ ] 
- [ ] 
- [ ] 

### 2.2 POS

- [ ] 
- [ ] 
- [ ] 

### 2.3 Administración

- [ ] 
- [ ] 
- [ ] 

---


## 3. Matriz de casos de prueba

| ID | CASO DE PRUEBA | DATOS DE ENTRADA | PASOS | RESULTADO ESPERADO | ESTADO |
|---|---|---|---|---|---|
| QA-01 | Verificar disponibilidad del backend y configuración CORS |Método: GET URL: /api/health Headers: Origin: http://localhost:5173 | 1 Iniciar servidor backend en puerto 3000. 2. Enviar petición GET a /api/health con encabezado Origin. 3. Verificar código de estado HTTP. 4. Verificar encabezado Access-Control-Allow-Origin. 5. Validar estructura del cuerpo JSON. |HTTP 200 OK, encabezado Access-Control-Allow-Origin retornado correctamente, y cuerpo JSON { "success": true, "data": { "status": "ok", ... } } confirmando disponibilidad del servicio.| PASÓ |
| QA-02 | Consultar catálogo de productos activos y opciones de personalización | Método: GET. Endpoint: `/api/products`. | 1. Enviar una petición GET. 2. Revisar los productos devueltos. 3. Verificar que estén activos y contengan sus opciones de personalización. | Devuelve una lista de productos activos (`activo: true`) con sus respectivas opciones de personalización. | PENDIENTE |
| QA-03 | Filtrar productos por categoría | Método: GET. Endpoint: `/api/products?categoria=Prendas`. | 1. Enviar una petición GET con el parámetro categoria. 2. Revisar los productos devueltos. 3. Comprobar que todos pertenezcan a la categoría solicitada. 4. Verificar el comportamiento con diferentes mayúsculas y minúsculas. | Devuelve únicamente productos de la categoría Prendas y aplica correctamente el filtro sin depender de mayúsculas o minúsculas. | PENDIENTE |
| QA-04 | Validar cálculo del total y snapshots de pedidos | Método: POST. Endpoint: `/api/orders`. Datos: producto, cantidad, opciones de personalización y descuento. | 1. Enviar una solicitud de creación de pedido. 2. Verificar el cálculo del total. 3. Consultar el pedido guardado. 4. Comprobar que los snapshots conserven los datos originales. | El total coincide con `((base + extras) * cantidad) - descuento` y los snapshots conservan los datos originales del pedido. | PENDIENTE |
| QA-05 | Validar aplicación de cupones y restricción de descuentos acumulables | Métodos: POST. Endpoints: `/api/promotions/validate` y `/api/orders`. Datos: código de cupón y datos del pedido. | 1. Validar un cupón. 2. Comprobar el descuento. 3. Crear un pedido aplicando el cupón. 4. Intentar acumular descuentos no permitidos. | El cupón válido aplica el descuento correspondiente y el backend rechaza la acumulación de descuentos no permitida. | PENDIENTE |
| QA-06 | Validar transiciones permitidas de estados de pedidos | Método: PATCH. Endpoint: `/api/orders/:id/status`. Datos: ID del pedido y nuevo estado. | 1. Cambiar el pedido de RECIBIDO a EN_PREPARACION. 2. Cambiarlo a LISTO. 3. Cambiarlo a ENTREGADO. 4. Intentar transiciones inválidas y reabrir pedidos finalizados. | Permite las transiciones RECIBIDO → EN_PREPARACION → LISTO → ENTREGADO y rechaza transiciones inválidas o reaperturas. | PENDIENTE |
| QA-07 | Verificar bloqueo de entrega por saldo pendiente | Método: PATCH. Endpoint: `/api/orders/:id/status`. Datos: ID de pedido con saldo pendiente y estado ENTREGADO. | 1. Crear o seleccionar un pedido con saldo pendiente. 2. Intentar cambiar su estado a ENTREGADO. 3. Revisar la respuesta del backend. | Rechaza la operación con HTTP 400 y código de error `ORDER_PENDING_PAYMENT`. | PENDIENTE |
| QA-08 | Validar registro de anticipos y pago total | Método: POST. Endpoint: `/api/payments`. Datos: ID del pedido, monto y método de pago. | 1. Registrar un anticipo equivalente al 50% del pedido. 2. Verificar el estado del pago. 3. Registrar el saldo restante. 4. Comprobar el estado final. | El primer pago actualiza `estado_pago` a ANTICIPO_PARCIAL y el segundo cambia el estado a PAGADO. | PENDIENTE |
| QA-09 | Verificar consulta pública y segura del seguimiento de pedidos | Método: GET. Endpoint: `/api/orders/tracking/:referencia?contacto=...`. Datos: referencia del pedido y contacto asociado. | 1. Enviar una petición sin autenticación. 2. Proporcionar referencia y contacto válidos. 3. Verificar el estado devuelto. 4. Comprobar que no se expongan datos sensibles. | Devuelve el estado actual del pedido sin requerir autenticación ni exponer información sensible. | PENDIENTE |

---

## 4. Checklist previo a la demo

### Preparación

- [ ] 
- [ ] 
- [ ] 

### Tienda web

- [ ] 
- [ ] 
- [ ] 

### POS

- [ ] 
- [ ] 
- [ ] 

### Administración

- [ ] 
- [ ] 
- [ ] 

### Calidad general

- [ ] 
- [ ] 
- [ ] 

---

## 5. Criterios de aceptación

**Aprobación**
Todas las pruebas críticas pasan y el flujo principal de la demo funciona de principio a fin.

**Aprobación con observaciones**
Las funciones críticas pasan y solo quedan defectos menores documentados.

**Rechazo**
Falla una función esencial, se pierden datos, los precios son incorrectos o existen vulnerabilidades relevantes de permisos.

---

## 6. Registro de defecto

| ID | CASO RELACIONADO | DESCRIPCIÓN | PASOS PARA REPRODUCIR | RESULTADO ESPERADO | SEVERIDAD | ESTADO |
| --- | --- | --- | --- | --- | --- | --- |
| BUG-01 |  |  |  |  |  |  |
| BUG-02 |  |  |  |  |  |  |
| BUG-03 |  |  |  |  |  |  |
| BUG-04 |  |  |  |  |  |  |
| BUG-05 |  |  |  |  |  |  |
| BUG-06 |  |  |  |  |  |  |
| BUG-07 |  |  |  |  |  |  |
| BUG-08 |  |  |  |  |  |  |
| BUG-09 |  |  |  |  |  |  |

---

## 7. Control de ejecución

| FECHA | VERSIÓN APROBADA | RESPONSABLE | PRUEBAS APROBADAS | PRUEBAS FALLIDAS | DECISIÓN |
| --- | --- | --- | --- | --- | --- |
| MM-DD-AA |  |  |  |  |  |
| MM-DD-AA |  |  |  |  |  |
| MM-DD-AA |  |  |  |  |  |
| MM-DD-AA |  |  |  |  |  |
| MM-DD-AA |  |  |  |  |  |
| MM-DD-AA |  |  |  |  |  |
| MM-DD-AA |  |  |  |  |  |
| MM-DD-AA |  |  |  |  |  |
| MM-DD-AA |  |  |  |  |  |
