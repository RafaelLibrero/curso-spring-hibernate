# Preguntas de Comprensión

---

## 1. Infraestructura
Si la app intenta conectarse a PostgreSQL antes de que el contenedor esté listo, no va a poder conectarse y va a tirar errores.
Esto pasa porque la base de datos todavía está arrancando y no acepta conexiones. Para solucionarlo,
se puede hacer que la app espere un poco antes de intentar conectarse.

---

## 2. JPA
El método `findAll()` trae todos los registros de la tabla a la vez, y si hay muchos, como 100,000, puede ser muy lento
y consumir mucha memoria. Para evitar eso, se puede usar **paginación** o hacer consultas con filtros.

---

## 3. API REST
Un error **400** pasa cuando lo que envía el usuario no está bien, por ejemplo, si intento crear un piloto sin nombre.
La API me dice “Bad Request” porque no se cumplen las reglas de validación.  
Un error **500** pasa cuando algo falla en el servidor, no por culpa del usuario, por ejemplo, 
si la app intenta guardar un resultado pero la base de datos da un error inesperado.

---

## 4. Escalabilidad
Si la app pasa de 100 a 10,000 usuarios, los contenedores actuales no van a aguantar tanta carga. 
Habría que poner varias copias del contenedor de la app o poner una réplica,
y quizás usar caching para no consultar todo cada vez.