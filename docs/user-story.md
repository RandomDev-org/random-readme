# Historias de Usuario

---

### 1. Músico 
**Historia de Usuario:**

Como músico, quiero poder buscar, visualizar y confirmar mi asistencia a locales musicales interactivos en el mapa, para poder conectar físicamente con otros músicos afines a mi género y mantener un registro de mi participación en la escena local.

**Criterios de Aceptación:**
* Escenario 1: Búsqueda y filtrado
  - Dado que accedo al mapa interactivo de la plataforma.
  - Cuando aplico los filtros de "género musical" o "tipo de espacio" (ej. Jam Session, Ensayo).
  - Entonces el mapa debe mostrar únicamente los recintos que coincidan con mi búsqueda, indicando si el lugar está verificado o es sugerido por la comunidad.


* Escenario 2: Información actualizada y asistencia
  - Dado que selecciono un local específico en el mapa.
  - Cuando visualizo su ficha técnica.
  - Entonces debo poder ver sus horarios, backline disponible y un botón para "Confirmar Asistencia".


* Escenario 3: Interacción comunitaria
  - Dado que he confirmado mi asistencia a un evento o local.
  - Cuando otros músicos revisen la ficha de ese lugar.
  - Entonces mi perfil debe aparecer en la lista de "Músicos que asistirán", permitiendo la conexión previa.

---

### 2. Público
**Historia de Usuario:**


Como miembro del público, quiero poder filtrar en el mapa los locales y eventos de música en vivo según mi ubicación y gustos, para encontrar fácilmente un lugar actualizado donde salir a disfrutar de la música.

**Criterios de Aceptación:**
* Escenario 1: Descubrimiento geolocalizado
  - Dado que abro la aplicación buscando un panorama.
  - Cuando el sistema detecta o ingreso mi ubicación actual.
  - Entonces debo ver los locales con música en vivo más cercanos renderizados en menos de 3 segundos.


* Escenario 2: Claridad de la oferta
  - Dado que encuentro un evento que me interesa en el mapa.
  - Cuando hago clic en el marcador del local.
  - Entonces se debe desplegar una tarjeta con los nombres del artistas que van, horario, tipo de música y si el evento tiene costo de entrada o es gratuito entre otros.

---

### 3. Dueño de Local
**Historia de Usuario:**

Como dueño de un local, quiero reclamar mi espacio en el mapa y poder publicar mis propios eventos, atrayendo así a músicos y público directamente a mi establecimiento.

**Criterios de Aceptación:**
* Escenario 1: Verificación de identidad
  - Dado que mi local aparece en el mapa creado por la comunidad pero no tengo control sobre él.
  - Cuando completo el flujo de "Reclamar local" adjuntando la documentación requerida.
  - Entonces mi ficha recibe una insignia visual de "Local Verificado" que genera confianza en los usuarios.


* Escenario 2: Publicación de eventos
  - Dado que he accedido a mi perfil de dueño verificado.
  - Cuando selecciono "Añadir evento" y guardo los datos (fecha, género, formato etc). Entonces el evento se ancla automáticamente al marcador de mi local en el mapa y es visible para todos los músicos y público en la zona.

---

### 4. Productor
**Historia de Usuario:**

Como productor musical, quiero consultar el mapa para visualizar qué artistas se presentan frecuentemente en los locales y leer las reseñas de la comunidad, para identificar talentos emergentes de manera eficiente.

**Criterios de Aceptación:**
* Escenario 1: Trazabilidad de artistas
  - Dado que estoy buscando talento de un género específico.
  - Cuando selecciono locales etiquetados con ese género.
  - Entonces puedo ver el historial de los músicos o bandas que más se han presentado allí recientemente.


* Escenario 2: Contacto y redes
  - Dado que identifico a un músico o banda interesante en la ficha de un local.
  - Cuando hago clic en su perfil.
  - Entonces tengo acceso directo a sus redes sociales (Instagram, Spotify, etc.) para realizar un seguimiento de su trabajo.

---

### 5. Entidad Cultural
**Historia de Usuario:**

Como entidad cultural, quiero registrar y publicar espacios públicos o centros culturales en el mapa con un sello oficial, para aumentar su visibilidad y promover la participación ciudadana en actividades artísticas gratuitas.

**Criterios de Aceptación:**
* Escenario 1: Visibilidad de espacios públicos
  - Dado que opero desde una cuenta con el rol de "Entidad Cultural".
  - Cuando registro un nuevo espacio (anfiteatro, plaza, centro cultural) en la plataforma.
  - Entonces este aparece en el mapa interactivo destacado con un sello institucional, diferenciándolo de los locales comerciales privados.


* Escenario 2: Gestión en tiempo real
  - Dado que la programación municipal cambia frecuentemente.
  - Cuando edito los horarios o disponibilidad del espacio en el sistema.
  - Entonces la comunidad visualiza la actualización en tiempo real en sus mapas, evitando confusiones de uso.


### [Ver problemática](./problem.md)