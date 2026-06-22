# MusicSpot
Proyecto universitario para la asignatura Fundamentos de Ingeniería de Software. 
Este Readme corresponde a la Entrega numero 3
para revisar el readme correspondiente a la entrega numero 2 revisar el .MD de legado [Link](readme.md(legacy))

## Descripción del sistema
MusicSpot Plataforma colaborativa que conecta a músicos, productores, público y dueños de locales a través de un mapa interactivo de espacios musicales los cuales permiten poder organizar diferentes eventos, actividades y entre otros.
 
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
- Tener [Docker Desktop](https://www.docker.com/products/docker-desktop/) (Solo para instalacion con docker)
- Cuenta en Github
- NestJS
- PostGreSql
- React/Vite
  
  


# Instalación y ejecución (sin Docker)
### Paso 1 
Clonar todos los proyectos con
```powershell
Git Push NombreProyecto
```

- [Frontend](https://github.com/RandomDev-org/backend-maps)
- [Backend gateway](https://github.com/RandomDev-org/backend-gateaway)
- [Backend maps](https://github.com/RandomDev-org/backend-maps)
- [Backend profile](https://github.com/RandomDev-org/backend-profile)
  
### Paso 2
Ir a cada proyecto y ejecutar:

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

# Instalación y ejecución (con Docker)   
## Como prender el proyecto
### Paso 1:
Clonar los repositorios dentro de una misma carpeta raiz.
```
Ejemplo:
carpeta raiz/
├── backend-gateaway/   (docker-compose.yml)
├── backend-maps/       (Dockerfile)
├── backend-profile/    (Dockerfile)
└── frontend/           (Dockerfile + nginx.conf)
```

### Paso 2:
Ejecutar `docker compose up --build` tal que:
```powershell
cd backend-gateaway
docker compose up --build
```

### Servicios Implementados
| Servicio | URL |
|---|---|
| Frontend | http://localhost |
| API Gateway | http://localhost:3000 |
| Profile (Swagger) | http://localhost:3002/api/docs |

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
