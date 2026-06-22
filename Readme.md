# musicSpot
Proyecto universitario para la asignatura Fundamentos de Ingeniería de Software. Entrega numero 3

## Descripción del sistema
Plataforma colaborativa que conecta a músicos, productores, público y dueños de locales a través de un mapa interactivo de espacios musicales.
 
## Historia de usuario implementada
| ID    | Nombre                    | Issue |
|-------|---------------------------|-------|
| Cu-01 |[Búsqueda y descubrimiento de eventos](https://github.com/RandomDev-org/random-readme/issues/23) | #23    |

 
## Artefactos del proyecto
| Artefacto                          | Ubicación / enlace          |
|------------------------------------|-----------------------------|
| Modelo de dominio                  | [Link](docs/domain-model.md)           |
| Diagrama de casos de uso           | [Link](docs/diagarama_casosdeuso.png)  |
| Especificación de HU               | [Link](docs/EspecificacionHU.md)      |
| Diagrama de estados                | [Link](docs/diagrama_estados.png)           |
| Diagrama de despliegue y comp.     | [Link](https://github.com/RandomDev-org/random-readme/blob/main/docs/diagrama_despliegue.png)           |
| Diagrama de componentes            | [Link](https://github.com/RandomDev-org/random-readme/blob/main/docs/diagrama_componentes.png)           |
| Diagrama de secuencia              | [Link](https://github.com/RandomDev-org/random-readme/blob/main/docs/diagrama_secuencias.png)           |
| Casos de prueba                    | [Link](docs/CasosDePrueba.md)     |
| Deuda técnica / code smells        | [Link](docs/DeudaTecnica.md)      |
 
## Instrucciones de instalación y ejecución
### Requisitos previos
```
docker compose up --build
```

### Instalación y ejecución (sin Docker)
# Como prender el proyecto sin docker
## Paso 1 
clonar todos los proyectos

[Frontend](https://github.com/RandomDev-org/backend-maps)
[Backend gateway](https://github.com/RandomDev-org/backend-gateaway)
[Backend maps](https://github.com/RandomDev-org/backend-maps)
[Backend profile](https://github.com/RandomDev-org/backend-profile)
## Paso 2
Ir a cada proyecto y ejecutar:

backends:
```
npm i
npm run start:dev
```

frontend:
```
npm i
npm run dev
```

### Instalación y ejecución (con Docker)  <!-- si aplica (bonus) -->
## Como prender el proyecto
# Paso 1:
Clonar los repositorios dentro de una misma carpeta raiz.
```
carpeta raiz/
├── backend-gateaway/   (docker-compose.yml)
├── backend-maps/       (Dockerfile)
├── backend-profile/    (Dockerfile)
└── frontend/           (Dockerfile + nginx.conf)
```

# Paso 2:
ir a `backend-gateaway` y ejecutar `docker compose up --build`

# Stacks utilizados

Frontend: React + vite
Backend: Microservicios con NestJS
 
## Responsabilidades del equipo
| Integrante | Rol(es) | Ítems de la rúbrica a cargo |
|------------|---------|-----------------------------|
| [Jason Monroy] | [Technical Developer]   | [Desarrollo]                     |
| [Vicente Tapia] | [Arquitecto]   | [Análisis]                     |
| [Eduardo Blanchard] | [Quality Assurance]   | [Pruebas, Calidad]                     |
| [Benjamín Isasmendi] | [Lead Developer]   | [Desarrollo, Pruebas]                     |
| [Ignacio Rivera] | [Scrum Master]   | [Desarrollo, Diseño]                     |
 
## Bonus (opcional)
- Contenedores: [sí] — docker-compose en ./docker-compose.yml
- Spec-driven development: [sí] — especificaciones en ./openspecs/
  
# MusicSpot - Informe de Calidad

## Arquitectura del Proyecto

```
┌─────────────┐     ┌──────────────────┐     ┌──────────────────┐
│  Frontend   │────▶│  API Gateway     │────▶│  backend-maps    │
│  (React +   │     │  (NestJS HTTP)   │     │  (NestJS TCP)    │
│   Vite)     │     │  :3000           │     │  :3001           │
│  :80 (Docker)│     │                  │     │                  │
│  :5173 (dev) │     │                  │────▶│  backend-profile │
└─────────────┘     └──────────────────┘     │  (NestJS HTTP+TCP)│
                                             │  :3002/:4002     │
                                             └──────────────────┘
                                                      │
                                                     ┌▼──────────────┐
                                                     │  PostgreSQL   │
                                                     │  - locations  │
                                                     │  - profile_db │
                                                     └───────────────┘
```

**Stack:** NestJS, TypeORM, PostGIS, PostgreSQL, React, Vite, Docker, TCP Transport.

---

## 1. Casos de Prueba

### Historia de Usuario
> Como aficionado a la música, quiero buscar eventos en un mapa interactivo filtrando por género, ubicación y tipo de evento, para encontrar fácilmente conciertos y tocatas de mi interés.

**Criterios de Aceptación:**
1. El sistema debe ofrecer un panel de búsqueda con filtros combinados (género, ubicación, tipo).
2. Los resultados deben actualizarse en el mapa con un tiempo de respuesta menor a 3 segundos tras aplicar el filtro.

### CP-01: Búsqueda exitosa con filtros combinados
| Campo | Detalle |
|---|---|
| **Precondiciones** | Sistema en línea. Base de datos con al menos un evento de género "Rock", tipo "Concierto" en la zona visible del mapa. |
| **Pasos** | 1. Abrir el mapa interactivo.<br>2. En el panel lateral, seleccionar género "Rock".<br>3. Navegar/mover el mapa a una zona donde existan venues con eventos de Rock.<br>4. Observar los resultados. |
| **Resultado esperado** | El mapa muestra pines solo para los venues que tienen eventos de Rock. Los pines aparecen en menos de 3 segundos. |

### CP-02: Búsqueda sin resultados
| Campo | Detalle |
|---|---|
| **Precondiciones** | Sistema en línea. No existen eventos de "Jazz" en la zona visible del mapa. |
| **Pasos** | 1. Abrir el mapa.<br>2. Seleccionar género "Jazz".<br>3. Aplicar filtro. |
| **Resultado esperado** | El mapa se limpia de pines. La barra lateral muestra "Sin resultados" con mensaje amigable. Tiempo de respuesta < 3s. |

### CP-03: Actualización por navegación del mapa (Bounds)
| Campo | Detalle |
|---|---|
| **Precondiciones** | Eventos creados en distintas zonas geográficas (Santiago, Valparaíso). |
| **Pasos** | 1. Abrir el mapa.<br>2. Arrastrar el mapa de Santiago a Valparaíso.<br>3. Esperar a que el mapa cargue los nuevos bounds. |
| **Resultado esperado** | El sistema detecta el cambio de bounds y solicita los venues de la nueva zona vía `GET /map/points/bounds`. Los pines de Santiago desaparecen y aparecen los de Valparaíso. Respuesta < 3s. |

### CP-04: Registro de usuario
| Campo | Detalle |
|---|---|
| **Precondiciones** | El email no está registrado previamente. |
| **Pasos** | 1. Ir a "Iniciar Sesión".<br>2. Hacer clic en "Registrarse".<br>3. Ingresar nombre, email y contraseña.<br>4. Enviar formulario. |
| **Resultado esperado** | Se crea el perfil. Se retorna un token JWT. El usuario queda autenticado en la sesión. |

### CP-05: Inicio de sesión
| Campo | Detalle |
|---|---|
| **Precondiciones** | El usuario ya está registrado. |
| **Pasos** | 1. Ir a "Iniciar Sesión".<br>2. Ingresar email y contraseña.<br>3. Enviar formulario. |
| **Resultado esperado** | Se valida la credencial (bcrypt). Se retorna un token JWT. El navbar muestra el nombre del usuario y menú desplegable. |

### CP-06: Publicar un local con imagen
| Campo | Detalle |
|---|---|
| **Precondiciones** | Usuario autenticado. |
| **Pasos** | 1. Ir a "Publicar local".<br>2. Completar nombre, tipo, dirección (buscar con Nominatim).<br>3. Seleccionar una imagen (se comprime a 1200px, JPEG 80%).<br>4. Enviar formulario. |
| **Resultado esperado** | El local se guarda en la base de datos con la imagen como data URL Base64 en el campo `poster`. El mapa muestra el nuevo venue. |

### CP-07: Validación de rendimiento (< 3s)
| Campo | Detalle |
|---|---|
| **Precondiciones** | Base de datos poblada con 1000+ venues. Herramientas de desarrollador abiertas. |
| **Pasos** | 1. Abrir la pestaña Network.<br>2. Navegar el mapa a una zona con muchos venues.<br>3. Medir el tiempo total de la petición `GET /map/points/bounds`. |
| **Resultado esperado** | La petición HTTP se completa en menos de 3 segundos (incluyendo viaje TCP al microservicio y consulta PostGIS). |

---

## 2. Deuda Técnica

| ID | Descripción | Impacto | Solución Propuesta |
|---|---|---|---|
| **DT-01** | **Falta de paginación** en endpoints `GET /map/points` y `GET /map/events`. Actualmente retornan colecciones completas. | Cuando la BD crezca a miles de registros, el payload será enorme y superará los 3s de respuesta. | Implementar paginación offset o cursor-based en backend-maps con TypeORM (`skip`/`take`). |
| **DT-02** | **Timeouts fijos (15s)** sin Circuit Breaker en el gateway. Si un microservicio TCP cae, el gateway mantiene la conexión abierta 15s por cada petición. | Bajo carga, el event loop del gateway se satura y deja de responder. | Integrar `opossum` (Circuit Breaker). Si 3 peticiones fallan seguidas, el circuito se abre y rechaza inmediatamente con 503. |
| **DT-03** | **Secrets en texto plano** en `app.module.ts` (fallbacks `'postgres'`, `'super-secret-key'`). Si el `.env` no está presente, la app arranca con valores inseguros. | Riesgo de seguridad en producción. | Usar `Joi` con `@nestjs/config` para validar que las variables críticas existan. Si no existen, la app debe fallar al arrancar con un error claro. |
| **DT-04** | **Sin autenticación en capa TCP**. Cualquier proceso que se conecte al puerto TCP interno (3001, 4002) puede enviar mensajes sin validar. | Un atacante dentro de la red interna podría modificar o leer datos directamente. | Implementar un token de servicio compartido o un guard TCP que valide el origen de las peticiones. |
| **DT-05** | **Columnas `poster` como `text`** en lugar de almacenamiento externo (S3, Cloudinary). Las data URLs Base64 se guardan completas en la BD. | La BD crece innecesariamente. Las consultas espaciales se vuelven lentas al tener que leer campos grandes. | Migrar a un bucket S3 o Cloudinary y guardar solo la URL en la BD. La subida debe hacerse desde el frontend directo al storage. |

---

## 3. Code Smells (Olores de Código)

### CS-01: Código Duplicado (Duplicated Code)
- **Ubicación:** `backend-gateaway/src/gateway/auth/`, `map/`, `profile/` (3 controladores).
- **Problema:** El método `private async send<T>(pattern, data)` con try/catch, timeout(15000), RpcException handling y `OnModuleInit` con `client.connect()` está copiado exactamente igual en los 3 controladores.
- **Refactor:** Extraer a un servicio `TcpClientService` inyectable o una clase abstracta `BaseGatewayController`.

### CS-02: Controlador Blooter (Large Class)
- **Ubicación:** `backend-maps/src/map/map.controller.ts` y `backend-gateaway/src/gateway/map/map-gateway.controller.ts`.
- **Problema:** Un solo controlador maneja CRUD de venues **y** CRUD de eventos. Viola el Principio de Responsabilidad Única (SRP).
- **Refactor:** Separar en `VenueController` y `EventController`.

### CS-03: Obsesión por Primitivos (Primitive Obsession)
- **Ubicación:** `backend-gateaway/src/gateway/map/map-gateway.controller.ts` (rutas `findNearby`, `findByBounds`).
- **Problema:** `@Query('lat') lat: string` se parsea con `parseFloat()` manualmente en lugar de usar DTOs con `class-validator` y `@Type(() => Number)`.
- **Refactor:** Crear DTOs `QueryNearbyDto` y `QueryBoundsDto` con decoradores de validación, y dejar que el `ValidationPipe` global de NestJS haga la conversión automática.

### CS-04: Variables y imports no utilizados
- **Ubicación:** `frontend/src/app/components/` (múltiples archivos).
- **Problema:** Se encontraron imports de lucide-react (`MapPin`) y hooks (`useEffect`) que no se usaban, así como variables declaradas pero nunca leídas (`prefs` en ProfilePage).
- **Refactor:** Activar `noUnusedLocals: true` en el `tsconfig.json` y limpiar periódicamente con `tsc --noEmit`.

### CS-05: Tipado genérico en microservicios
- **Ubicación:** `backend-maps/src/map/map.service.ts` y controladores TCP.
- **Problema:** Los handlers TCP reciben `@Payload() dto: any` o `Record<string, unknown>` en lugar de los DTOs tipados.
- **Refactor:** Tipar estrictamente los payloads TCP con los DTOs existentes (`CreatePointDto`, `UpdatePointDto`, etc.).

---

## 4. Mejoras de Diseño Propuestas

### 4.1 Diagrama de Componentes (Propuesto)

```
┌──────────────┐     ┌─────────────────┐     ┌──────────────────┐
│   Frontend   │     │   API Gateway   │     │  backend-maps    │
│  React+Vite  │────▶│  Express/NestJS │────▶│  NestJS TCP      │
│  :5173/80    │     │  :3000          │     │  :3001           │
│              │     │  + Circuit      │     │  + Pagination    │
│  + Imagen    │     │    Breaker      │     │  + Cache Redis   │
│    compresión│     │  + Rate Limit   │     └──────────────────┘
│  + Base64→S3 │     │  + JWT Guard    │              │
└──────────────┘     └─────────────────┘     ┌───────▼──────────┐
                     │                       │  PostgreSQL      │
                     │                       │  + PostGIS       │
                     │  backend-profile       │  + Paginación    │
                     │  NestJS HTTP+TCP      └──────────────────┘
                     │  :3002/:4002
                     │  + JWT Auth
                     │  + Perfiles
                     │  + Preferencias
                     └─────────────────┘
```

### 4.2 Mejoras Prioritarias

| Prioridad | Mejora | Esfuerzo | Beneficio |
|---|---|---|---|
| 🔴 Alta | Paginación en endpoints de mapa | 2 días | Escalabilidad + rendimiento < 3s |
| 🔴 Alta | Circuit Breaker en gateway | 1 día | Resiliencia del sistema |
| 🟡 Media | Migrar imágenes a S3/Cloudinary | 3 días | Rendimiento BD + escalabilidad |
| 🟡 Media | Secrets con Joi (validación al arrancar) | 0.5 días | Seguridad en producción |
| 🟢 Baja | Separar VenueController de EventController | 1 día | Mantenibilidad |
| 🟢 Baja | Crear TcpClientService compartido | 0.5 días | Eliminar código duplicado |

---

## 5. Guía de Ejecución Rápida

### Local (sin Docker)
```powershell
# 1. backend-maps (TCP :3001)
cd backend-maps
npm run start:dev

# 2. backend-profile (HTTP :3002, TCP :4002)
cd backend-profile
npm run start:dev

# 3. backend-gateaway (HTTP :3000)
cd backend-gateaway
npm run start:dev

# 4. frontend (Vite :5173)
cd frontend
npm run dev
```

### Docker
```powershell
cd backend-gateaway
docker compose up --build
```

| Servicio | URL |
|---|---|
| Frontend | http://localhost |
| API Gateway | http://localhost:3000 |
| Profile (Swagger) | http://localhost:3002/api/docs |

### Orden de arranque (local)
1. PostgreSQL (local o Docker)
2. backend-maps
3. backend-profile
4. backend-gateaway
5. frontend

---

## 6. Estructura del Repositorio

```
Repositorios/
├── backend-gateaway/     # API Gateway (NestJS HTTP → TCP)
│   ├── docker-compose.yml
│   └── Dockerfile
├── backend-maps/         # Microservicio de mapas (NestJS TCP)
│   └── Dockerfile
├── backend-profile/      # Microservicio de perfiles (NestJS HTTP+TCP)
│   └── Dockerfile
└── frontend/             # Frontend React + Vite
    ├── Dockerfile
    └── nginx.conf
```
