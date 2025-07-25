```mermaid

flowchart TD
    A[Inicio: Cliente llama por pérdida o robo] --> B[Agente recibe llamada en Genesys]
    B --> C[Agente solicita 3 últimos dígitos del documento]
    C --> D[Agente valida identidad en TelcoID]
    D --> E{¿Identidad validada?}

    E -- No --> M[Agente informa que no puede continuar]
    M --> Y[Fin del proceso sin éxito]

    E -- Sí --> F[Agente crea ticket en TPTicket]
    F --> G[Ticket es enviado al Back Office]

    G --> H[Back Office revisa ticket]
    H --> I{¿Ticket completo y correcto?}
    
    I -- No --> J[Ticket devuelto al agente para corrección]
    J --> F

    I -- Sí --> K[Ticket entra a cola de espera]
    K --> L{¿Especialista disponible?}

    L -- No --> W[Esperar disponibilidad] --> K

    L -- Sí --> N[Especialista toma el caso]
    N --> O[Ejecuta bloqueo en BlockPhone]
    O --> P{¿Bloqueo exitoso?}

    P -- No --> Q[Escala el caso o reporta error]
    Q --> R[Ticket queda en seguimiento]
    R --> Z1[Fin con seguimiento pendiente]

    P -- Sí --> S[Confirma bloqueo completado]
    S --> T[Ticket cerrado en sistema]
    T --> U[Cliente es informado si vuelve a llamar]
    U --> Z2[Fin del proceso exitoso]

