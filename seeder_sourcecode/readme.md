# SEEDER
---

### Código Fuente
En este [repositorio](https://github.com/BraytoGBDX/AquaBrym.git) se incluye el código fuente del **Seeder** desarrollado en `NestJS` y `TypeORM`, encargado de generar datos simulados para pruebas.

El archivo principal se encuentra en:
```
/src/seeder/seeder.service.ts
```

Este seeder genera:
1. **Usuarios** (`User`)
2. **Entidades** (`Entity`) asociadas a cada usuario
3. **Sensores** (`Sensor`) por entidad
4. **Facturas** (`Bill`) con consumo y cargos calculados
5. **Lecturas de sensores** (`SensorReading`) con caudal, volumen y pulsos
6. **Alertas** (`Alert`) con niveles: `info`, `warning`, `critical`

---

### Respaldo de la BD Vacía (Sin datos Generados)
En la carpeta `/database/` se incluye:
```
/database/aquabrym_empty.sql
```
Este archivo contiene únicamente la **estructura** de la base de datos sin datos cargados, lista para importarse en PostgreSQL/MySQL.

---

### Capturas de pantalla

<img src="/img/4.png">
<img src="/img/3.png">
<img src="/img/2.png">
<img src="/img/1.png">

---


### Listado de EndPoint para Generar datos simulados

| Método | Endpoint   | Parámetros        | Descripción |
|--------|-----------|-------------------|-------------|
| POST   | `/seeder` | `count: number`   | Ejecuta el proceso de generación de datos masivos (usuarios, entidades, sensores, facturas, lecturas y alertas) |

**Ejemplo de petición:**
```bash
curl -X POST http://localhost:3000/seeder
-H "Content-Type: application/json" 
-d '{"count": 1000000}'
```

---

### Respaldo de BD con 1 millón de registros
En la carpeta `/database/` se incluye:
```
/database/aquabrym_full.sql
```
Este archivo contiene **1 millón de registros** generados por el seeder, con datos realistas para pruebas de carga y rendimiento.
