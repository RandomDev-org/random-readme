# Casos de Prueba – C1-01
 

| ID   | Qué se debe hacer (acción / entrada) | Salida esperada |
|------|--------------------------------------|-----------------|
| CP-01 | **Búsqueda exitosa con filtros:** Seleccionar Género: "Rock", Tipo: "Concierto" y Ubicación: "Santiago". Hacer clic en "Aplicar Filtros". | El mapa muestra únicamente los pines que coinciden con los criterios. Tiempo de carga inferior a 3 segundos. |
| CP-02 | **Búsqueda sin resultados:** Seleccionar Género: "Electrónica", Tipo: "Tocata" y aplicar filtros en una zona geográfica sin eventos registrados. | El mapa se limpia por completo y queda vacío. Se muestra un aviso visual de "sin resultados" en menos de 3 segundos. |
| CP-03 | **Rendimiento bajo carga:** Con una BD masiva de eventos, abrir la pestaña *Red (Network)* del navegador y aplicar un filtro amplio (todos los géneros y tipos en toda la ciudad). | Las peticiones HTTP (`GET /map/events` o `/nearby`) pasan por el API Gateway/TCP y el Frontend dibuja los pines en un tiempo total (Waterfall) < 3.00 segundos. |
| CP-04 | **Actualización dinámica (Bounds):** Hacer *zoom out* y arrastrar la vista del mapa hacia otra región del país para cambiar los límites geográficos. | El sistema detecta automáticamente los nuevos límites (*bounds*), solicita los datos y renderiza los pines de la nueva zona en menos de 3 segundos. |


