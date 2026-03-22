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
