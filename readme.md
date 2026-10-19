SIGED — Sistema de Gestión Escolar Digital

Objetivo
Digitalizar el registro de asistencia y calificaciones de un centro educativo, y facilitar el seguimiento oportuno del estudiantado por parte de docentes, coordinación académica y familias.

Problema que resuelve
Hoy el registro de notas y asistencia se hace en cuadernos y hojas de cálculo separadas. Esto genera pérdida de tiempo al consolidar información, errores de transcripción y poca comunicación con los padres, que se enteran de las ausencias semanas después. SIGED centraliza y automatiza ese proceso.

Funcionalidades principales
- **RF01** Registro de asistencia diaria por estudiante y sección.
- **RF02** Ingreso de calificaciones por evaluación con cálculo automático del promedio.
- **RF03** Reportes consolidados de notas y asistencia por grado o sección.
- **RF04** Notificación automática a los padres cuando se registra una ausencia.
- **RF05** Alerta de riesgo académico cuando un estudiante supera el límite de inasistencias.

Arquitectura seleccionada
Arquitectura **en capas sobre un modelo cliente-servidor**: interfaz (frontend), lógica de negocio (backend/API) y base de datos, con servicios de apoyo desacoplados (autenticación, notificaciones y reportes). Principio aplicado: separación de responsabilidades. Riesgo conocido: el backend, como intermediario único, puede volverse un cuello de botella si el sistema crece.

Organización frontend / backend
| Parte | Responsabilidad |
|---|---|
| **Frontend** | Mostrar formularios de asistencia y calificaciones, y paneles de consulta para docentes, coordinación y padres. No contiene reglas de negocio ni accede directamente a la base de datos. |
| **Backend (API)** | Validar datos, aplicar las reglas de negocio (promedios, límites de inasistencia), controlar permisos por rol y coordinar los servicios de autenticación, notificaciones y reportes. Es el único que lee y escribe en la base de datos. |

**Comunicación:** el frontend envía peticiones HTTP a la API del backend (estilo REST, intercambio de datos en JSON). El backend verifica la identidad y el rol del usuario, procesa la operación, consulta o guarda en la base de datos y devuelve la respuesta al frontend. Cuando se registra una ausencia, el backend también invoca el servicio de notificaciones

Herramientas utilizadas
- GitHub (repositorio y control de versiones)
- GitHub Projects (tablero Kanban) y GitHub Issues (seguimiento de tareas)
- Visual Paradigm Online (diagramas UML y de arquitectura)
- Microsoft Word / PDF (documentación)

Estado actual del proyecto
**Versión 0.1.0 — versión inicial de diseño y planificación.** Requisitos, modelos UML, arquitectura y gestión del avance están documentados. La implementación de los módulos de asistencia y calificaciones está en progreso; notificaciones, reportes y alertas están pendientes.

 Estructura del repositorio
```
/docs
  /requisitos      Análisis y especificación de requisitos
  /uml             Casos de uso, clases, secuencia y actividades
  /arquitectura    Diseño arquitectónico
  /gestion         Gestión del avance y comunicación con interesados
README.md
CHANGELOG.md
```

Registro de cambios
Ver [CHANGELOG.md](CHANGELOG.md).
