
## Segundo titulo


```mermaid
sequenceDiagram
    actor Cliente
    participant Sistema as Sistema MercadoLibre
    participant MercadoPago
    actor Vendedor
    participant Logistica as Logística (Mercado Envíos)

    Cliente->>Sistema: Buscar producto
    Sistema-->>Cliente: Mostrar resultados (stock, precio)
    Cliente->>Sistema: Seleccionar producto y comprar
    Sistema->>MercadoPago: Solicitar autorización de pago
    alt Pago exitoso
        MercadoPago-->>Sistema: Confirmación
        Sistema->>Vendedor: Notificar "Nueva venta"
        Vendedor->>Sistema: Confirmar despacho
        Sistema->>Logistica: Generar guía de envío
        Logistica-->>Sistema: Estado "En camino"
        Sistema-->>Cliente: Notificar seguimiento
        Logistica->>Cliente: Entregar pedido
        Cliente->>Sistema: Confirmar recepción
        Sistema->>Vendedor: Liberar pago
        Cliente->>Sistema: Calificar transacción
    else Pago fallido
        MercadoPago-->>Sistema: Rechazo
        Sistema-->>Cliente: Pedir otro método
    end