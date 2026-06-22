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
| Modelo de dominio                  | [docs/domain-model.md]           |
| Diagrama de casos de uso           | [docs/diagarama_casosdeuso.png]  |
| Especificación de HU               | [docs/EspecificacionHU.md]      |
| Diagrama de estados                | [docs/diagrama_estados.png]           |
| Diagrama de despliegue y comp.     | [enlace o imagen]           |
| Diagrama de componentes            | [enlace o imagen]           |
| Diagrama de secuencia              | [enlace o imagen]           |
| Casos de prueba                    | [docs/CasosDePrueba.md]     |
| Deuda técnica / code smells        | [docs/DeudaTecnica.md]      |
 
## Instrucciones de instalación y ejecución
### Requisitos previos
[docker compose up --build]
### Variables de entorno
[Lista de variables necesarias]
### Instalación y ejecución (sin Docker)
[Comandos paso a paso]
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
| [Nombre 1] | [Rol]   | [Ítems]                     |
| [Nombre 2] | [Rol]   | [Ítems]                     |
| [Nombre 1] | [Rol]   | [Ítems]                     |
| [Nombre 2] | [Rol]   | [Ítems]                     |
| [Nombre 1] | [Rol]   | [Ítems]                     |
 
## Bonus (opcional)
- Contenedores: [sí] — docker-compose en ./docker-compose.yml
- Spec-driven development: [sí] — especificaciones en ./openspecs/
