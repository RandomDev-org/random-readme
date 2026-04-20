# Requisitos Extrafuncionales

## Resumen de Atributos Seleccionados

### Prioridad Alta

| Atributo | Descripción                                                                                                                 |
|:---------|:----------------------------------------------------------------------------------------------------------------------------|
| Rendimiento / Eficiencia | El mapa debe cargar y mostrar marcadores en menos de 3 segundos.                                                            |
| Disponibilidad (Fiabilidad) | La aplicación debe estar disponible el 99.5% del tiempo. El sistema debe recuperarse automáticamente de errores temporales. |
| Usabilidad | La aplicación debe ser usable sin capacitación previa. Debe funcionar correctamente en dispositivos móviles y escritorio.   |
| Escalabilidad | El sistema debe soportar hasta 10,000 usuarios concurrentes sin degradación. Permitir migración futura a microservicios.    |

### Prioridad Media

| Atributo | Descripción                                                                                                                      |
|:---------|:---------------------------------------------------------------------------------------------------------------------------------|
| Seguridad | Implementar autenticación. Autorización basada en roles. Validar y sanitizar entradas. |

### Prioridad Baja

| Atributo | Descripción                                                                                           |
|:---------|:------------------------------------------------------------------------------------------------------|
| Mantenibilidad | Mantener separación clara entre módulos. Documentar APIs y arquitectura.                              |
| Interoperabilidad | Soportar Chrome, Firefox, Safari etc.                                                                 |
| Recuperabilidad | Realizar backups diarios. Implementar logging y alertas.                                              |

