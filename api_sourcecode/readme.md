# API

<HR>

### 🧰 Código Fuente
El código fuente de la API de AquaWatch está desarrollado en NestJS que permite gestionar, procesar y exponer datos en tiempo real relacionados con el consumo de agua, utilizando MySQL como base de datos y TypeORM como ORM para la interacción con la BD.
Repositorio oficial:
https://github.com/BraytoGBDX/AquaBrym.git

<BR>

### 🧠 Operaciones CRUD Básicas
La API de AquaWatch implementa operaciones CRUD para las principales entidades del sistema, entre ellas:

1. 🙍‍♂️ **Usuarios**
        Crear usuario (registro).
        Consultar usuario por ID o listado general.
        Actualizar datos de usuario.
        Eliminar usuario.
2. 🧮 **Mediciones**
        Registrar nueva medición de consumo de agua.
        Actualizar registro de medición.
        Eliminar registro.

3. 🚨 **Alertas**
        Crear alerta automática por consumo alto.
        Consultar alertas generadas.
        Actualizar estado de alerta (leída/no leída).
        Eliminar alerta.


<BR>

### Listado de EnPoints de las Entidades
| Método | Endpoint              | Descripción                      |
| ------ | --------------------- | -------------------------------- |
| POST   | `/api#/Users/UsersController_create`| Crea un nuevo usuario|
| GET    | `/api#/Users/UsersController_findAll`| Lista todos los usuarios|
| GET    | `/api#/Sensors/SensorsController_findOne`| Obtiene un usuario por ID|
| PATCH  | `/api#/Sensors/SensorsController_update`| Actualiza un usuario|
| DELETE | `/api#/Users/UsersController_remove`| Elimina un usuario|
| POST   | `/api#/Sensors/SensorsController_create`| Registra un sensor |
| GET    | `/api#/Sensors/SensorsController_findAll`| Lista de todos los sensores|
| GET    | `/api#/Sensors/SensorsController_findOne` | Obtiene un sensor por ID      |
| PATCH  | `/api#/Sensors/SensorsController_update` | Actualiza un sensor          |
| DELETE | `/api#/Sensors/SensorsController_remove` | Elimina un sensor            |
| POST   | `/api#/Bills/BillsController_create`| Registra una Bills |
| GET    | `/api#/Bills/BillsController_findAll`| Lista de todos los Bills|
| GET    | `/api#/Bills/BillsController_findOne` | Obtiene una Bills por ID      |
| PATCH  | `/api#/Bills/BillsController_update` | Actualiza una Bills         |
| DELETE | `/api#/Bills/BillsController_remove` | Elimina una Bills            |
| POST   | `/api#/SensorReadings/SensorReadingsController_create`| Crea una nueva lectura del sensor|
| GET    | `/api#/SensorReadings/SensorReadingsController_findAll`| Lista todos las lecturas del sensor|
| GET    | `/api#/SensorReadings/SensorReadingsController_findOne`| Obtiene una lectura por ID|
| PATCH  | `/api#/SensorReadings/SensorReadingsController_update`| Actualiza una lectura del sensor|
| DELETE | `/api#/SensorReadings/SensorReadingsController_remove`| Elimina una lectura del sensor|
| POST   | `/api#/Entities/EntitiesController_create`| Crea un nueva Entidad|
| GET    | `/api#/Entities/EntitiesController_findAll`| Lista todas las Entidades|
| GET    | `/api#/Entities/EntitiesController_findOne`| Obtiene una Entidad por ID|
| PATCH  | `/api#/Entities/EntitiesController_update`| Actualiza una Entidad|
| DELETE | `/api#/Entities/EntitiesController_remove`| Elimina una Entidad|
| POST   | `/api#/Alerts/AlertsController_create`| Crea un nueva Alerta|
| GET    | `/api#/Alerts/AlertsController_findAll`| Lista todas las Alertas|
| GET    | `/api#/Alerts/AlertsController_findOne`| Obtiene una Alerta por ID|
| PATCH  | `/api#/Alerts/AlertsController_update`| Actualiza una Alerta|
| DELETE | `/api#/Alerts/AlertsController_remove`| Elimina una Alerta|

<BR>

### Screenshots (Capturas de Pantalla)
<div align="center">
  <img src="/img/users.png" width="500"/>
  <img src="/img/sensors.png" width="500"/>
  <img src="/img/bills.png" width="500"/>
  <img src="/img/alertas.png" width="500"/>
  <img src="/img/sensor.png" width="500"/>
</div>

<BR>

### Endpoints que utiliza ML (Machine Learning)
La API incluye endpoints que utilizan modelos de Machine Learning para:

° Detección de patrones anormales que podrían indicar fugas.
  Estos modelos se entrenan con datos recopilados por el dispositivo IoT y procesados en la nube.

### Listado de EnPoints de las Entidades
| Método | Endpoint              | Descripción                      |
| ------ | --------------------- | -------------------------------- |
| POST   | `/api#/SensorReadings/SensorReadingsController_create`|Realiza la lectura sobre la medición del agua|

<div align="center">
  <img src="/img/sensor.png" width="500"/>
</div>
