# Registro de Prompts - Trabajo Final‌‌‌​‌​‌‌​﻿‍‍​﻿​​​﻿‍‌​﻿‌‌​﻿‌​‌‍‌‌‌‍‌‍‌‍​﻿‌‍​‌‌‍​‌​﻿‌﻿‌‍‌​‌‍‌‌‌‍‌‍​﻿​‌‌‍​‌‌‍‌‌

**Alumno:** Rafael Librero

**Fecha:** 19/03/2026

**IA utilizada:** ChatGPT

---

## COMO USAR ESTE ARCHIVO

Este archivo tiene **DOS PARTES** muy diferentes:

| Parte | Que es | Como debe verse |
|-------|--------|-----------------|
| **PARTE 1** | Tus 3 prompts reales | Lenguaje NATURAL, con errores, informal |
| **PARTE 2** | Blueprint generado por IA | Perfecto, profesional, estructurado |

### REGLA IMPORTANTE

> **Los prompts de la Parte 1 deben ser COPIA EXACTA de lo que escribiste.**
>
> NO los pases por la IA para "mejorarlos". NO corrijas errores.
> Si escribiste "como ago un controllr rest en spring" con errores,
> eso es lo que debes pegar.
>
> **El sistema detecta automaticamente si los prompts fueron "limpiados".**
> Prompts perfectos en la Parte 1 = SOSPECHOSO.

---

# PARTE 1: Mis Prompts Reales (3 minimo)

> Copia y pega EXACTAMENTE lo que le escribiste a la IA.
> Incluye errores, lenguaje informal, todo. Eso demuestra autenticidad.

---

## Prompt A: Infraestructura Docker

**Contexto:** Quería levantar mi aplicación Spring Boot con PostgreSQL en Docker

**Mi prompt exacto (copiado tal cual):**
```
quiero un docker-compose para mi app spring boot con postgres y adminer, ten en cuenta el de la pizzeria 
```

**Que paso:** [ ] Funciono  [ x ] Funciono parcial  [ ] No funciono

**Que aprendi:** Aprendí que PostgreSQL no crea tablas ni datos automáticamente como H2, 
que debo usar spring.sql.init.mode=always

---

## Prompt B: API REST Spring Boot

**Contexto:** Estaba aprendiendo cómo manejar respuestas HTTP correctamente en Spring Boot y cómo estructurar mis controllers.

**Mi prompt exacto (copiado tal cual):**
```
que diferencia entre response entity o devolver Driver, mi objeto, en el controller?
```

**Que paso:** [ x ] Funciono  [ ] Funciono parcial  [ ] No funciono

**Que aprendi:** Aprendí que devolver directamente el objeto funciona para casos simples,
pero ResponseEntity me da control sobre códigos de estado, por ejemplo.

---

## Prompt C: Funcionalidad Avanzada

**Contexto:** Quería centralizar el manejo de errores en mi API para no repetir lógica en cada endpoint.

**Mi prompt exacto (copiado tal cual):**
```
que es @controlleradvice?
```

**Que paso:** [ x ] Funciono  [ ] Funciono parcial  [ ] No funciono

**Que aprendi:** Aprendí que @ControllerAdvice permite manejar excepciones de forma centralizada con métodos @ExceptionHandler

---
---

# PARTE 2: Blueprint Final (generado por IA)

> Esta parte la genera la IA AL FINAL de tu trabajo.
> Le pides a la IA que resuma tu proyecto como un blueprint profesional.
> Esta parte SI debe verse perfecta y estructurada.

**Prompt para generar esto:**
Copia este prompt en tu IA favorita cuando termines tu proyecto:

```
Tengo un proyecto Spring Boot con estas entidades: [LISTA TUS ENTIDADES].
Las relaciones son: [LISTA TUS RELACIONES].
Los endpoints son: [LISTA TUS ENDPOINTS].
Genera un blueprint profesional que resuma la arquitectura del proyecto,
incluyendo: entidades con sus campos, relaciones, endpoints REST,
y tecnologias usadas.
```

**Blueprint generado:**

### Arquitectura del Proyecto Spring Boot – F1 BoxBox

#### Entidades y Campos

1. **Driver**
  - `driverId`: Long, PK
  - `driverName`: String, obligatorio, 2-100 caracteres
  - `carNumber`: int, positivo
  - `team`: Team, relación muchos a uno
  - `previous_teams`: List<Team>, relación muchos a muchos
  - `flag`: String
  - `imagen`: String
  - `points`: int, positivo o cero

2. **Race**
  - `raceId`: Long, PK
  - `raceName`: String, obligatorio, 2-100 caracteres
  - `image`: String
  - `location`: String
  - `endDate`: Date
  - `winnerDriver`: Driver, relación muchos a uno
  - `status`: Enum RaceStatus

3. **Result**
  - `resultId`: Long, PK
  - `position`: int, 1–22
  - `points`: int, 0–25
  - `driver`: Driver, relación muchos a uno, obligatorio
  - `race`: Race, relación muchos a uno, obligatorio

4. **Team**
  - `teamId`: Long, PK
  - `teamName`: String, obligatorio, 2-100 caracteres
  - `logo`: String
  - `drivers`: List<Driver>, relación uno a muchos
  - `points`: int, positivo o cero
  - `active`: boolean, obligatorio

---

#### Relaciones Principales

- **Driver ↔ Team**: Muchos a uno (`Driver.team`)
- **Driver ↔ Previous Teams**: Muchos a muchos (`Driver.previous_teams`)
- **Race ↔ Driver**: Muchos a uno (`Race.winnerDriver`)
- **Result ↔ Driver**: Muchos a uno (`Result.driver`)
- **Result ↔ Race**: Muchos a uno (`Result.race`)
- **Team ↔ Driver**: Uno a muchos (`Team.drivers`)

---

#### Endpoints REST

**CRUD para todas las entidades:**

- **DriverController**
  - GET `/drivers` – listar todos
  - GET `/drivers/{id}` – obtener por id
  - POST `/drivers` – crear
  - PUT `/drivers/{id}` – actualizar
  - DELETE `/drivers/{id}` – eliminar
  - GET `/drivers/ranking` – listar drivers por puntos
  - GET `/drivers/search?name=...` – buscar por nombre

- **RaceController**
  - GET `/races`
  - GET `/races/{id}`
  - POST `/races`
  - PUT `/races/{id}`
  - DELETE `/races/{id}`

- **ResultController**
  - GET `/results`
  - GET `/results/{id}`
  - POST `/results`
  - PUT `/results/{id}`
  - DELETE `/results/{id}`

- **TeamController**
  - GET `/teams`
  - GET `/teams/{id}`
  - POST `/teams`
  - PUT `/teams/{id}`
  - DELETE `/teams/{id}`

---

#### Manejo de Errores

- `@ControllerAdvice` para manejo global de excepciones
- Uso de `ResponseEntity` para devolver códigos HTTP y mensajes personalizados
- Validaciones con `jakarta.validation` en cada entidad

---

#### Tecnologías Usadas

- **Backend:** Spring Boot 4, Java 21
- **Persistencia:** Spring Data JPA, Hibernate, PostgreSQL
- **Validación:** Jakarta Validation (Bean Validation)
- **Contenedores:** Docker, Docker Compose
- **Base de Datos Web:** Adminer
- **Construcción:** Maven
- **Buenas prácticas:** DTOs opcionales, ResponseEntity para endpoints, healthchecks en Docker

---

## Resumen Final

| Pregunta | Respuesta                                                                                                                                                                                                                                     |
|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Total de prompts usados | 100 aprox                                                                                                                                                                                                                                     |
| Herramienta mas usada | ChatGPT                                                                                                                                                                                                                                       |
| Prompt mas util | "quiero un docker-compose para mi app spring boot con postgres y adminer, ten en cuenta el de la pizzeria" <br/> El más útil porque me ahorró muchos dolores de cabeza y al tener otro archivo de referencia el resultado fue bastante bueno. |
| Prompt que NO funciono | "Generame un CRUD de mis entidades team y race igual que driver"<br/> Tenía fallos pequeños pero molestos que tuve que revisar y arreglar.                                                                                                    |
| Tiempo total estimado | 4 horas                                                                                                                                                                                                                                       |
| Que harias diferente | Documentaría mejor los healthchecks y probaría primero en H2 para entender cómo funcionan los endpoints antes de migrar a PostgreSQL                                                                                                          |
