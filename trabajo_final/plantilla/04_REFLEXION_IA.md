# Reflexion IA — 3 Momentos Clave

---

## Bloque A: Infraestructura Docker

### Momento Arranque
Lo primero que hice fue pedirle a la IA que me ayudara a crear un docker-compose.yml y un Dockerfile para
levantar mi aplicación Spring Boot junto con PostgreSQL y un panel web tipo Adminer.

### Momento Error
Cuando probé la configuración, la aplicación no encontraba ninguna tabla ni datos en PostgreSQL. 
Me di cuenta de que esto no pasaba con H2, que levantaba todo automáticamente en memoria. 
La app fallaba al arrancar y me volví loco buscando qué pasaba. 
Finalmente entendí que necesitaba configurar spring.sql.init.mode=always

### Momento Aprendizaje
Aprendí la gran diferencia entre H2 y PostgreSQL: H2 es “mágica” porque crea todo automáticamente, 
pero PostgreSQL requiere inicialización explícita y persistencia.

---

## Bloque B: API REST Spring Boot

### Momento Arranque
Lo primero que hice fue preguntarle a la IA: “¿Cuál es la diferencia entre devolver un ResponseEntity
o devolver directamente mi objeto, como Driver, en el controller?”.
Quería entender cuál era la forma correcta de estructurar mis endpoints y 
cómo manejar los códigos de estado HTTP de manera correcta.

### Momento Error
Al principio devolvía directamente mis objetos (Driver) en los endpoints, pensando que Spring se encargaba de todo. 
Pero cuando quería devolver un error 404 o un mensaje personalizado, no podía controlarlo fácilmente.

### Momento Aprendizaje
Aprendí que devolver el objeto directamente está bien para casos simples, 
pero ResponseEntity me da control completo sobre la respuesta HTTP.

---

## Bloque C: Funcionalidad Avanzada

### Momento Arranque
Quería mejorar el manejo de errores en mi API, así que le pregunté a la IA: “¿Qué es @ControllerAdvice?”.
Mi objetivo era no repetir código de manejo de excepciones en cada endpoint y centralizarlo.

### Momento Error
Al principio intenté capturar errores con try-catch en cada controller,
pero el código se volvió repetitivo y desordenado.

### Momento Aprendizaje
Aprendí que @ControllerAdvice permite centralizar el manejo de errores de manera elegante. 
Puedo definir métodos con @ExceptionHandler para capturar excepciones específicas o genéricas y 
devolver ResponseEntity con códigos de estado y mensajes personalizados.