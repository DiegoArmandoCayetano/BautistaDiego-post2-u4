🛒 Sistema de Pedidos con Observer y Strategy
📌 Descripción

Este proyecto implementa un sistema de gestión de pedidos utilizando patrones de diseño de comportamiento en Java con Spring Boot.

Se aplican los siguientes patrones:

Observer → Para notificar eventos de pedidos (confirmación y cancelación)
Strategy → Para aplicar diferentes tipos de descuentos de forma dinámica
🧠 Patrones Implementados
🔔 Observer (Eventos de Pedido)

Cuando un pedido cambia de estado, se generan eventos que son escuchados por diferentes componentes del sistema sin acoplamiento directo.

📤 Publicador
GestorPedidosService
Publica eventos:
PedidoConfirmadoEvent
PedidoCanceladoEvent
📥 Suscriptores
EmailNotifier → Envía notificaciones
InventarioUpdater → Actualiza el stock
AuditoriaLogger → Registra acciones

✔ El publicador NO conoce a los suscriptores

💰 Strategy (Motor de Descuentos)

El sistema permite cambiar el tipo de descuento en tiempo de ejecución sin modificar el código del carrito.

🎯 Estrategias disponibles
DescuentoTemporada → 20%
DescuentoVIP → 30%
DescuentoCupon → Descuento fijo de $15.000
🧩 Contexto
CarritoService
Permite:
Activar estrategia
Calcular total con descuento
Listar estrategias disponibles

✔ Las estrategias se inyectan automáticamente con Spring (@Service)

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/249770df-d239-4643-a92e-f3fd2f1ed08e" />


# Pedidos Comportamiento — Patrones Chain of Responsibility y Command

## Descripción
Sistema de procesamiento de pedidos que implementa dos patrones de comportamiento:
- **Chain of Responsibility:** cadena de validación secuencial (stock, monto, crédito).
- **Command + Undo:** operaciones reversibles sobre el pedido (confirmar, aplicar descuento).

## Tecnologías
- Java 17
- Spring Boot 3.2.0
- JUnit 5
- Maven 3.8+

## Flujo del sistema
1. El pedido entra a la cadena de validación (Stock → Monto → Crédito).
2. Si pasa todas las validaciones, se ejecutan los comandos (Confirmar, Descuento).
3. El historial permite deshacer la última acción (undo).


Chain of Responsibility
Valida un pedido pasándolo por una cadena de tres validadores en secuencia. Si uno falla, el pedido es rechazado y la cadena se detiene. Si todos pasan, el pedido queda aprobado.
Pedido → ValidadorStock → ValidadorMonto → ValidadorCredito → APROBADO
ValidadorStock: cantidad <= 10 unidades
ValidadorMonto: total >= $5.000
ValidadorCredito: cliente con crédito aprobado

Command + Undo
Encapsula cada acción sobre el pedido como un objeto que sabe ejecutarse y deshacerse. El HistorialComandos guarda los comandos en una pila y permite revertir el último ejecutado.
ComandoConfirmar: cambia el estado a CONFIRMADO, el undo restaura el estado anterior.
ComandoAplicarDescuento: aplica un porcentaje de descuento al total, el undo restaura el total original.
   
5. <img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/617eafda-56e8-4c7b-9a99-96da6916a2c4" />
