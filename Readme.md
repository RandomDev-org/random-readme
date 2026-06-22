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
