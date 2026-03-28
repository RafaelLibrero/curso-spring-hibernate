# Trabajo Final — Rafael Librero

## Blueprint elegido
F1 BoxBox — Gestión de la temporada de Fórmula 1

## Descripcion
La aplicación **F1 BoxBox API** es un servicio RESTful que permite consultar y administrar información de la temporada de Fórmula 1.  
Permite gestionar pilotos, equipos, carreras y resultados de cada Gran Premio, así como el historial de equipos de los pilotos.

## Entidades

| Entidad | Campos principales | Relaciones |
|---------|-------------------|------------|
| Team | teamName, logo, points, active | OneToMany con Driver, ManyToMany con Driver (historial previo) |
| Driver | driverName, carNumber, flag, imagen, points | ManyToOne con Team, ManyToMany con Team (previous_teams), OneToMany con Result |
| Race | raceName, image, location, endDate, status | ManyToOne con Driver (winnerDriver), OneToMany con Result |
| Result | position, points | ManyToOne con Driver, ManyToOne con Race |

## Endpoints de la API

### Drivers
| Verbo | URL | Descripcion |
|-------|-----|-------------|
| GET | `/api/drivers` | Listar todos los pilotos |
| GET | `/api/drivers/{id}` | Consultar piloto por ID |
| POST | `/api/drivers` | Crear un nuevo piloto |
| PUT | `/api/drivers/{id}` | Actualizar piloto existente |
| DELETE | `/api/drivers/{id}` | Eliminar piloto |
| GET | `/api/drivers/search` | Buscar pilotos por nombre |
| GET | `/api/drivers/ranking` | Listar pilotos ordenados por puntos descendentes |

### Teams
| Verbo | URL | Descripcion |
|-------|-----|-------------|
| GET | `/api/teams` | Listar todos los equipos |
| GET | `/api/teams/{id}` | Consultar equipo por ID |
| POST | `/api/teams` | Crear un nuevo equipo |
| PUT | `/api/teams/{id}` | Actualizar equipo existente |
| DELETE | `/api/teams/{id}` | Eliminar equipo |

### Races
| Verbo | URL | Descripcion |
|-------|-----|-------------|
| GET | `/api/races` | Listar todas las carreras |
| GET | `/api/races/{id}` | Consultar carrera por ID |
| POST | `/api/races` | Crear una nueva carrera |
| PUT | `/api/races/{id}` | Actualizar carrera existente |
| DELETE | `/api/races/{id}` | Eliminar carrera |

### Results
| Verbo | URL | Descripcion |
|-------|-----|-------------|
| GET | `/api/results` | Listar todos los resultados |
| GET | `/api/results/{id}` | Consultar resultado por ID |
| POST | `/api/results` | Registrar resultado de una carrera |
| PUT | `/api/results/{id}` | Actualizar resultado existente |
| DELETE | `/api/results/{id}` | Eliminar resultado |

## Como ejecutar

```bash
# Con Docker
docker compose up -d

# Sin Docker (H2)
mvn spring-boot:run