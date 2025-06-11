Estructura de las Tablas
**Tabla "Partidos"**

ID del Partido (Primary Key)
Equipo Local
Equipo Visitante
Fecha del Partido
Liga/Torneo
Estado (Programado/En Curso/Finalizado)
Resultado Local (número)
Resultado Visitante (número)

**Tabla "Usuarios"**

ID Usuario (Primary Key)
Nombre
Email
Saldo/Puntos

**Tabla "Apuestas" (nueva tabla necesaria)**

ID Apuesta (Primary Key)
Usuario (Link a tabla Usuarios)
Partido (Link a tabla Partidos)
Predicción Local
Predicción Visitante
Fecha de Apuesta
Puntos Apostados
Estado (Pendiente/Ganada/Perdida)

## PASOS

### Implementación del Formulario
Opción 1: Formulario Nativo de Airtable

Crea un formulario desde la tabla "Apuestas"
Configura los campos:

Selector de Usuario (dropdown)
Selector de Partido (dropdown con fórmula que muestre "Equipo A vs Equipo B - Fecha")
Campos numéricos para predicciones
Campo de puntos a apostar



Opción 2: Integración con Typeform + Zapier

Crea un Typeform con:

Pregunta de selección múltiple para partidos disponibles
Campos numéricos para resultados
Campo de email del usuario


Conecta via Zapier para enviar datos a Airtable

Opción 3: Formulario Web Personalizado
Puedes crear un formulario HTML que use la API de Airtable:
javascript// Ejemplo básico de envío a Airtable
const enviarApuesta = async (datos) => {
  const response = await fetch(`https://api.airtable.com/v0/${BASE_ID}/Apuestas`, {
    method: 'POST',
    headers: {
      'Authorization': `Bearer ${API_KEY}`,
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({
      records: [{
        fields: {
          'Usuario': [datos.usuarioId],
          'Partido': [datos.partidoId],
          'Predicción Local': datos.predLocal,
          'Predicción Visitante': datos.predVisitante
        }
      }]
    })
  });
};

## Automatizaciones Recomendadas

Filtro de Partidos Disponibles: Automatización que solo muestre partidos con estado "Programado"
Validación de Apuestas: Script que verifique:

El partido no ha comenzado
El usuario tiene saldo suficiente
No existe apuesta previa del mismo usuario para ese partido


Cálculo de Resultados: Automatización que compare predicciones vs resultados reales cuando el partido finalice

Configuración del Formulario Dinámico
Para que el formulario solo muestre partidos disponibles, puedes usar:

Vista filtrada en Airtable (solo partidos futuros)
Fórmula en el campo de selección: {Equipo Local} & " vs " & {Equipo Visitante} & " - " & {Fecha}

## Proyecto compartido en AIRTABLE

Proyecto compartido en Airtable

https://airtable.com/appkqT31ZcotLQZNn/tblpHyB6QC1eQX009/viwriluEGoIEWzyGA?blocks=hide