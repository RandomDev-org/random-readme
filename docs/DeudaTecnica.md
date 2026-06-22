# Deuda Técnica, Code Smells y Mejoras de Diseño

## 1. Code smells / deuda técnica identificada

| ID | Ubicación (archivo/módulo) | Descripción del problema | Propuesta de mejora |
|----|----------------------------|--------------------------|---------------------|
| DT-01 | `backend-gateaway/src/gateway/` | **Código Duplicado:** El método privado `send<T>(pattern, data)` para llamadas TCP está copiado textualmente en tres controladores distintos. | Crear un servicio global (`TcpClientProxyService`) o una clase abstracta `BaseGatewayController` para centralizar y reutilizar la lógica. |
| DT-02 | `map-gateway.controller.ts` y `map.controller.ts` | **Controlador Bloater:** Los controladores manejan en conjunto el CRUD de "Locales" y el CRUD de "Eventos", violando el principio SRP. | Separar la lógica en dos módulos y controladores independientes: `VenueController` y `EventController`. |
| DT-03 | Rutas de consulta en el Mapa | **Falta de Paginación:** El backend retorna colecciones completas en arrays sin límite, lo que saturará el payload JSON al crecer la base de datos. | Implementar paginación (Limit/Offset o por cursor) en `backend-maps` para proteger el rendimiento de la API. |
| DT-04 | Comunicación del API Gateway | **Ausencia de Circuit Breaker:** La conexión TCP usa un timeout fijo de 15s sin tolerancia a fallos. Si un microservicio cae, el Gateway colapsará por acumulación de peticiones. | Integrar un patrón *Circuit Breaker* (ej. con la librería `opossum`) para abrir el circuito y rechazar peticiones de inmediato si el servicio no responde. |

## 2. Mejoras de diseño futuras

- **Migración a clústeres geográficos con PostGIS:** Agrupar puntos en clústeres directamente en la base de datos antes de enviarlos, reduciendo la carga de renderizado en el Frontend y optimizando el consumo de datos móviles.
- **Implementación de Caché (Redis) para filtros frecuentes:** Almacenar temporalmente en memoria las consultas de eventos y mapas más repetidas por los usuarios, disminuyendo drásticamente las peticiones TCP hacia los microservicios y bajando el tiempo de respuesta a milisegundos.