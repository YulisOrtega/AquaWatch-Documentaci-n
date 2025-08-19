# Proceso ETL (Extracción, Transformación y Carga)

## Importación de Librerías
import os
import numpy as np
import pandas as pd
import sqlalchemy as sa
import matplotlib.pyplot as plt
!pip install pymysql
import pymysql

pd.set_option('display.max_columns', 50)

## Carga de Datos
DB_USER = os.getenv("DB_USER", "root")
DB_PASS = os.getenv("DB_PASS", "1234")
DB_HOST = os.getenv("DB_HOST", "localhost")
DB_PORT = os.getenv("DB_PORT", "3306")
DB_NAME = os.getenv("DB_NAME", "aqua_db")

conn_str = f"mysql+pymysql://{DB_USER}:{DB_PASS}@{DB_HOST}:{DB_PORT}/{DB_NAME}"
engine = sa.create_engine(conn_str, pool_pre_ping=True)

with engine.connect() as con:
    version = con.exec_driver_sql("SELECT VERSION()").scalar()
print("Conexión OK. MySQL versión:", version)

## Creación del Dataframe
for col in ["timestamp", "created_at"]:
    if col in df_readings.columns:
        df_readings[col] = pd.to_datetime(df_readings[col], errors='coerce')

if "installation_at" in df_sensors.columns:
    df_sensors["installation_at"] = pd.to_datetime(df_sensors["installation_at"], errors='coerce')

for col in ["created_at","updated_at","period_start","period_end","issued_at","due_date"]:
    if col in df_bills.columns:
        df_bills[col] = pd.to_datetime(df_bills[col], errors='coerce')

df_rs = df_readings.merge(df_sensors.rename(columns={"id":"sensor_id"}), on="sensor_id", how="left")
df_rse = df_rs.merge(df_entities.rename(columns={"id":"entity_id"}), on="entity_id", how="left", suffixes=("_sensor","_entity"))
df_rse.head()

## Análisis Exploratorio de los datos (EDA)
print("=== Info df_rse ===")
print(df_rse.info())

print("\n=== Nulos por columna ===")
print(df_rse.isna().sum().sort_values(ascending=False).head(20))

print("\n=== Duplicados (por id lectura) ===")
dup_count = df_rse.duplicated(subset=['id']).sum() if 'id' in df_rse.columns else df_rse.duplicated().sum()
print("Duplicados:", dup_count)

print("\n=== Describe numérico ===")
display(df_rse.select_dtypes(include=['number']).describe())

print("\n=== Top entidades por volumen total (litros) ===")
if "volume_liters" in df_rse.columns and "entity_id" in df_rse.columns:
    top_entities = df_rse.groupby("entity_id")["volume_liters"].sum().sort_values(ascending=False).head(10)
    display(top_entities)

df = df_rse.copy()

if "flow_rate_lpm" in df.columns:
    df["flow_rate_lpm"] = df.groupby("sensor_id")["flow_rate_lpm"].transform(
        lambda s: s.fillna(s.median())
    )

if "volume_liters" in df.columns:
    df["volume_liters"] = df["volume_liters"].fillna(0)

if "id" in df.columns:
    before = len(df)
    df = df.drop_duplicates(subset=["id"])
    print(f"Duplicados eliminados: {before - len(df)}")

if "timestamp" in df.columns:
    df["date"] = pd.to_datetime(df["timestamp"], errors='coerce').dt.date
    df["hour"] = pd.to_datetime(df["timestamp"], errors='coerce').dt.hour

print("Shape limpio:", df.shape)
df.head()

## Visualización de Datos (2 a 5 gráficas)
# 7.1 Serie temporal de consumo diario total (litros)
if {"volume_liters","timestamp"}.issubset(df.columns):
    daily = df.set_index(pd.to_datetime(df["timestamp"], errors='coerce')).resample('D')["volume_liters"].sum()
    plt.figure()
    daily.plot()
    plt.title("Consumo total diario (litros)")
    plt.xlabel("Fecha")
    plt.ylabel("Litros")
    plt.show()

# 7.2 Histograma de caudal (lpm)
if "flow_rate_lpm" in df.columns:
    plt.figure()
    df["flow_rate_lpm"].dropna().plot(kind="hist", bins=30)
    plt.title("Distribución de caudal (lpm)")
    plt.xlabel("lpm")
    plt.ylabel("Frecuencia")
    plt.show()

# 7.3 Top 10 entidades por volumen total
if {"entity_id","volume_liters"}.issubset(df.columns):
    top10 = df.groupby("entity_id")["volume_liters"].sum().sort_values(ascending=False).head(10)
    plt.figure()
    top10.plot(kind="bar")
    plt.title("Top 10 entidades por consumo total (litros)")
    plt.xlabel("entity_id")
    plt.ylabel("Litros")
    plt.xticks(rotation=45)
    plt.tight_layout()
    plt.show()

# 7.4 Alertas por mes
if not df_alerts.empty:
    alerts = df_alerts.copy()
    alerts["detected_at"] = pd.to_datetime(alerts["detected_at"], errors='coerce')
    monthly_alerts = alerts.set_index("detected_at").resample("ME")["id"].count() if "id" in alerts.columns else alerts.set_index("detected_at").resample("M").size()
    plt.figure()
    monthly_alerts.plot(kind="bar")
    plt.title("Alertas por mes")
    plt.xlabel("Mes")
    plt.ylabel("Conteo")
    plt.xticks(rotation=45)
    plt.tight_layout()
    plt.show()

## Exportación del Data SET (.csv)
OUTPUT_PATH = r"C:\Users\BraytoGBDX\Desktop\dataset_clean.csv"
df.to_csv(OUTPUT_PATH, index=False, encoding="utf-8")
print("Archivo exportado:", OUTPUT_PATH)
