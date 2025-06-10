# GASOLINERAS

Principales cambios realizados:
1. Estructura modular:

crear_esquema(): Prepara la base de datos
obtener_estaciones(): Lee todas las estaciones de la tabla
cargar_inventario_estacion(): Procesa una estación específica
procesar_todas_las_estaciones(): Coordina todo el proceso

2. Procesamiento dinámico:

Lee automáticamente todas las estaciones de la tabla estacion
Para cada estación busca un archivo {estacion_id}.xlsx
Procesa cada archivo encontrado con la misma lógica original

3. Mejoras añadidas:

Manejo de errores robusto: Continúa procesando aunque falle una estación
Logging detallado: Muestra progreso y resultados de cada estación
Resumen final: Statistics de estaciones procesadas vs fallidas
Validación de archivos: Verifica que existe cada Excel antes de procesarlo

4. Configuración flexible:

Variable RUTA_BASE_EXCEL para cambiar la carpeta base
Función opcional agregar_estaciones_ejemplo() para testing

5. Estructura de archivos esperada:
C:\Users\sistemas\Desktop\gasolinas\
├── 1.xlsx  (para estación con ID 1)
├── 2.xlsx  (para estación con ID 2)
├── 3.xlsx  (para estación con ID 3)
└── ...





```mermaid
flowchart TD
    A[Inicio del Programa] --> B[Conectar a Base de Datos MySQL]
    B --> C{¿Conexión exitosa?}
    C -->|No| D[Mostrar error y terminar]
    C -->|Sí| E[Consultar tabla 'estaciones']
    E --> F[Obtener lista de gasolineras activas]
    F --> G[Leer archivo Excel diario]
    G --> H{¿Excel existe y es válido?}
    H -->|No| I[Registrar error - Excel no encontrado]
    H -->|Sí| J[Parsear datos del Excel]
    J --> K[Validar estructura del Excel]
    K --> L{¿Datos válidos?}
    L -->|No| M[Registrar errores de validación]
    L -->|Sí| N[Iniciar procesamiento por gasolinera]
    N --> O[Tomar siguiente gasolinera de la lista]
    O --> P{¿Gasolinera existe en Excel?}
    P -->|No| Q[Registrar gasolinera sin datos]
    P -->|Sí| R[Extraer datos de inventario]
    R --> S[Validar datos de inventario]
    S --> T{¿Datos consistentes?}
    T -->|No| U[Registrar error de datos]
    T -->|Sí| V[Preparar registro para tabla inventario]
    V --> W[Insertar en tabla 'inventario']
    W --> X{¿Inserción exitosa?}
    X -->|No| Y[Registrar error de BD]
    X -->|Sí| Z[Confirmar registro exitoso]
    Z --> AA{¿Quedan gasolineras?}
    Q --> AA
    U --> AA
    Y --> AA
    AA -->|Sí| O
    AA -->|No| BB[Generar reporte de procesamiento]
    BB --> CC[Cerrar conexión a BD]
    CC --> DD[Fin del programa]
    
    I --> EE[Terminar con error]
    M --> EE
    D --> EE
``` 
    style A fill:#90EE90
    style DD fill:#FFB6C1
    style EE fill:#FFA07A
    style B fill:#87CEEB
    style G fill:#DDA0DD
    style W fill:#F0E68C
 
