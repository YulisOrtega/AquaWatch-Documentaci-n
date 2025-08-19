🌊 Modelo Supervisado para Detección de Consumos Anómalos
📌 Propuesta de aplicación

El análisis supervisado se utiliza para la generación de un modelo capaz de identificar consumos anómalos de agua en registros provenientes de sensores.
Esto permite:

🔎 Automatizar la detección de comportamientos inusuales.

📢 Generar alertas tempranas.

💡 Proporcionar recomendaciones personalizadas a los usuarios.

⚙️ Elección del mecanismo a utilizar

Se seleccionó el algoritmo Random Forest Classifier, un método de aprendizaje supervisado basado en:

🌲 Construcción de múltiples árboles de decisión.

🗳️ Voto mayoritario para la clasificación.

🛡️ Robustez ante datos ruidosos.

📊 Posibilidad de interpretar la importancia de cada variable.

📖 Marco teórico.

Aprendizaje supervisado:
Entrenar un modelo con datos etiquetados (X, y) para que aprenda a predecir la etiqueta de nuevos registros.

Random Forest:
Un ensamble de árboles de decisión. Cada árbol se entrena con una muestra aleatoria del dataset y la predicción final se obtiene como la moda de todas las predicciones individuales.

Fórmula de entropía (para árboles de decisión):
      H(S)=−i=1∑c​pi​log2​pi​


Donde $p_i$ es la proporción de la clase $i$ en el conjunto $S$.

Métricas de evaluación:
      Precisioˊn = TP + FPTP​Recall = TP+FNTP​F1 = 2 ⋅ Precisioˊn + RecallPrecisioˊn ⋅ Recall​

🖥️ Aplicación del mecanismo

Ejemplo en Python:

from sklearn.ensemble import RandomForestClassifier

# Entrenamiento del modelo
clf = RandomForestClassifier(n_estimators=100, random_state=42)
clf.fit(X_train, y_train)

# Predicción en datos de prueba
predicciones = clf.predict(X_test)

📊 Gráficos generados
![📈 Histograma de consumo](graficas/histograma_consumo.png)  
![📊 Boxplot consumo](graficas/boxplot_consumo.png)  
![🔍 Conteo anomalías](graficas/conteo_anomalias.png)  


📈 Histograma: muestra la distribución de consumos.

📊 Boxplot: resalta valores atípicos.

🔍 Conteo: diferencia entre registros normales y anómalos.

✅ Resultados obtenidos

El modelo entrenado logró:

🟢 Identificar correctamente los registros anómalos.

📊 Obtener métricas de precisión, recall y F1-score satisfactorias.

👁️ Visualizar diferencias claras entre consumos normales y atípicos en los gráficos.

🏁 Conclusión de la fase del proyecto

Esta fase es fundamental para:

🤖 Dotar al sistema de capacidades inteligentes.

🚨 Permitir la detección automática de consumos atípicos.

⚡ Mejorar la eficiencia en la gestión del recurso hídrico.

👥 Aportar valor agregado al usuario final mediante recomendaciones basadas en datos reales y análisis estadístico.