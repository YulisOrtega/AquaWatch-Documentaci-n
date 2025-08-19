💧 Documentación del Modelo No Supervisado para Agrupamiento de Consumos
📌 Propuesta de aplicación

El análisis no supervisado se utiliza para descubrir patrones y agrupar registros de consumo de agua sin necesidad de etiquetas previas.
Esto permite:

👥 Identificar grupos de usuarios con consumos similares.

🔎 Detectar comportamientos comunes o atípicos.

📊 Facilitar la segmentación y el análisis exploratorio de los datos.

⚙️ Elección del mecanismo a utilizar

Se seleccionó el algoritmo KMeans, un método de clustering ampliamente utilizado por:

⚡ Su eficiencia en grandes volúmenes de datos.

👁️ Ser fácil de interpretar y visualizar.

📊 Su capacidad de encontrar grupos naturales en los datos.

📖 Marco teórico

Aprendizaje no supervisado:
Técnica que analiza datos sin etiquetas para encontrar patrones, estructuras o agrupamientos.

KMeans:
Algoritmo que divide los datos en K grupos minimizando la distancia entre cada punto y su centroide.

Distancia Euclidiana:
  
	\[
	d(x, y) = \sqrt{\sum_{i=1}^{n} (x_i - y_i)^2}
	\]

Criterio de optimización (Inercia):
  
	\[
		ext{Inercia} = \sum_{k=1}^{K} \sum_{x_i \in C_k} ||x_i - \mu_k||^2
	\]
	Donde $\mu_k$ es el centroide del cluster $k$.

🖥️ Aplicación del mecanismo

Ejemplo en Python:

from sklearn.cluster import KMeans

# Entrenamiento y predicción
kmeans = KMeans(n_clusters=2, random_state=42)
df['cluster'] = kmeans.fit_predict(X)

📊 Gráficos generados
![📈 Histograma por cluster](graficas/histograma_cluster.png)  
![📊 Boxplot por cluster](graficas/boxplot_cluster.png)  
![🔍 Conteo por cluster](graficas/conteo_cluster.png)  


📈 Histograma: muestra la frecuencia de consumo en cada grupo.

📊 Boxplot: permite comparar la variabilidad de consumos.

🔍 Conteo por cluster: visualiza el tamaño de cada grupo.

✅ Resultados obtenidos.

El modelo KMeans permitió identificar:

🟢 Grupos de registros con patrones de consumo similares.

📊 Diferencias claras en la distribución entre clusters.

🔎 Segmentos útiles para análisis exploratorio y toma de decisiones.

🏁 Conclusión de la fase del proyecto

Esta fase es clave para el análisis exploratorio y la segmentación:

🤝 Facilita estrategias personalizadas según el tipo de usuario.

🚨 Ayuda a descubrir patrones ocultos que no son evidentes a simple vista.

💡 Mejora la comprensión global del consumo de agua dentro del sistema.