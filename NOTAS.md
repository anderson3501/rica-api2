# NOTAS – RICA API

## El corte: qué va en cada servicio

Antes de separar `rica-api`, se define qué componentes pertenecerán a cada nuevo servicio.

| Paquete / clase actual | Destino |
|---|---|
| `investigadores.*` (dominio, aplicación, infraestructura) | `investigadores-service` |
| `publicaciones.*` | `publicaciones-service` |
| `compartido.GlobalExceptionHandler` | Se duplica en ambos servicios |
| `compartido.RecursoNoEncontradoException` | Se duplica en ambos servicios |
| `plataforma.StatusController` | Se duplica en ambos servicios, adaptando `/api/status` para cada uno |
| `plataforma.CorsConfig` | Se duplica en ambos servicios |
| `plataforma.ArranqueInformativo` | Se descarta |
| `plataforma.SaludoInstitucionalService` | Se descarta |

### Decisión de arquitectura

La duplicación de las clases de `compartido` y `plataforma` es intencional. Al separar la aplicación en servicios independientes, cada servicio necesita su propio manejo de errores, configuración y endpoint de estado.

Una alternativa sería crear una librería o módulo común versionado de forma independiente, conocido como **shared kernel**, para compartir estos elementos. Sin embargo, esto queda fuera del alcance del taller.

Esta decisión es una consecuencia de aplicar **Database per Service** y buscar que cada servicio pueda evolucionar y desplegarse de manera independiente.