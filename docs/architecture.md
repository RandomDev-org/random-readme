# Arquitectura del software
```mermaid
graph TD
%% Estilos
classDef front fill:#61dafb,stroke:#20232a,stroke-width:2px,color:#20232a;
classDef back fill:#ea2845,stroke:#20232a,stroke-width:2px,color:#fff;
classDef db fill:#336791,stroke:#20232a,stroke-width:2px,color:#fff;

    %% Nodos
    subgraph Capa_Presentacion [Frontend]
        UI[Vite React]:::front
    end

    subgraph Capa_Logica [Backend NestJS]
        Gateway[API Gateway / Routing]:::back
        
        subgraph Modulos_Independientes [Diseño Modular]
            Perfil[Módulo de perfil]:::back
            Mapa[Módulo de mapa y locales]:::back
            Gamificación[Módulo de gamificación]:::back
        end
        
        Gateway --> Perfil
        Gateway --> Mapa
        Gateway --> Gamificación
    end

    subgraph Capa_Datos [Capa de Datos]
        Postgres[(PostgreSQL con PostGIS)]:::db
    end

    %% Flujos
    UI <-->|HTTPS / JSON| Gateway
    Perfil <-->|ORM| Postgres
    Mapa <-->|Queries Espaciales| Postgres
    Gamificación <-->|Persistencia| Postgres
```

## Justificación del modelo
Elegimos un modelo de tres capas (frontend, backend y datos) con un backend estructurado como monolito modular.
Esta decisión reduce significativamente la complejidad operativa inicial frente
a una arquitectura de microservicios puros, lo que permite un desarrollo
más ágil para el equipo. Al mismo tiempo, mantiene una estricta separación
de responsabilidades, asegurando que el código sea cohesivo, escalable
y preparado para una futura migración a microservicios si la carga del sistema lo requiere.

### Definición de Módulos

---

#### Módulo de Perfil

##### Responsabilidad:
- Gestión centralizada de la identidad y autenticación del usuario.
- Control de acceso basado en roles (USUARIO con PERFIL que tiene ROL específico).
- Mantenimiento de la integridad de datos de usuario y seguridad de credenciales.

##### Datos que maneja:
- USUARIO: id, email, contraseña, nombre, fecha_registro, estado activo
- PERFIL: id, rol, biografia, ubicación, foto
- RED_SOCIAL: hooks con Instagram, Spotify, YouTube, SoundCloud, Twitter, Facebook etc
- PORTAFOLIO: eventos participados, géneros tocados, historial de shows (específico para Músicos)
- Preferencias de usuario: géneros_preferidos, filtros guardados, notificaciones

##### Interacción con otros módulos:
- **Con Mapa**: Proporciona información de usuario para filtrar eventos según sus preferencias. Recibe actualizaciones de confirmación de asistencia a eventos.
- **Con Gamificación**: Notifica eventos de usuario (registro, confirmación, reseña) para asignación de puntos. Recibe datos de XP, nivel actual y ranking para mostrar en perfil.

---

#### Módulo de Mapa

##### Responsabilidad:
- Gestión completa del ciclo de vida de puntos de interés (CRUD: Create, Read, Update, Delete).
- Validación de coordenadas geoespaciales usando PostGIS.
- Procesamiento de queries espaciales: distancia, proximidad, área de influencia.
- Filtrado y búsqueda avanzada de locales según múltiples criterios.
- Verificación de puntos sugeridos por comunidad vs. verificados por dueños.

##### Datos que maneja:
- PUNTO_INTERES: id, nombre, descripción, latitud, longitud, dirección, teléfono, capacidad, tipo (Bar, Sala, Plaza, Centro Cultural, etc.)
- CATEGORIA: clasificación de tipos de espacios
- HORARIO: días de semana, horas apertura/cierre, indicador de música en vivo por día
- EVENTO: fecha, hora, género, artistas, precio, capacidad, confirmación por dueño
- VERIFICACION: estado de verificación (Pendiente, Verificado, Rechazado), documentos adjuntos
- RESENA: calificaciones 1-5, comentarios, estado de verificación por asistencia
- ASISTENCIA: confirmaciones de usuarios a eventos, historial

##### Interacción con otros módulos:
- **Con Perfil**: Recibe datos de usuario (preferencias, rol) para filtrar resultados. Consulta información de artistas/dueños.
- **Con Gamificación**: Emite eventos: confirmar_asistencia, crear_evento_verificado, escribir_reseña, validar_informacion. Recibe datos de ranking para mostrar credibilidad de usuarios.

---

#### Módulo de Gamificación

##### Responsabilidad:
- Cálculo y asignación de puntos de experiencia (XP) basados en acciones específicas.
- Gestión de progresión de niveles.
- Administración de logros y insignias desbloquead por hitos.
- Cálculo de rankings globales, por rol y por ciudad geográfica.
- Retención de usuarios mediante motivación gamificada.

##### Datos que maneja:
- PUNTOS: id, id_usuario, tipo_accion, puntos_ganados, fecha
- LOGRO: id, id_usuario, tipo, nombre, descripción, icono, fecha_obtencion, oculto
- RANKING: id_usuario, posicion_global, posicion_por_rol, posicion_por_ciudad, puntos_totales
- GAMIFICACION: id_usuario, puntos_xp_total, nivel_actual, racha_dias_consecutivos

##### Tabla de puntos por acción:
- Registrar nuevo lugar: 50 XP
- Confirmar asistencia evento: 10 XP
- Escribir reseña: 25 XP
- Crear evento verificado: 75 XP
- Validar información de lugar: 15 XP
- Racha 7 días consecutivos: 100 XP bono

##### Interacción con otros módulos:
- **Escucha eventos de Mapa**: Cuando usuario confirma asistencia, escribe reseña, crea evento, etc. Automáticamente calcula y asigna XP.
- **Consultas desde Perfil**: Envía datos de XP, nivel, logros y ranking para mostrar en perfil de usuario.
- **Notificaciones**: Emite eventos cuando usuario sube de nivel o desbloquea logro para notificar en tiempo real.

---