 ## 📝 Resumen de Hallazgos y Conclusiones del EDA del Titanic

Después de realizar un Análisis Exploratorio de Datos (EDA) exhaustivo sobre el dataset de entrenamiento del Titanic, he identificado varios patrones y factores clave que influyeron significativamente en la tasa de supervivencia.

### 1. Manejo de Datos Faltantes

Se abordaron los valores nulos en tres columnas principales:
* **`Embarked` (Puerto de Embarque):** Con pocos valores faltantes (<10), se optó por imputar estos nulos con la moda (el puerto más frecuente), 'S' (Southampton), ya que es una variable categórica y esta estrategia preserva la distribución original.
* **`Age` (Edad):** Con aproximadamente 150 nulos, se imputaron los valores faltantes utilizando la mediana de la edad. Esta elección se debe a la robustez de la mediana frente a valores atípicos (bebés, personas muy mayores) y a su capacidad para representar mejor la tendencia central de la distribución de edades.
* **`Cabin` (Número de Cabina):** Dada la alta proporción de valores nulos (más del 70%), la columna original `Cabin` no se consideró directamente útil para el análisis. En su lugar, se creó una nueva característica binaria, `HasCabin` (1 si el pasajero tenía información de cabina, 0 si no), para capturar la presencia o ausencia de esta información de manera más efectiva.

### 2. Ingeniería de Características Básica

Se crearon dos nuevas características que proporcionan información más relevante para el análisis de supervivencia:
* **`FamilySize`:** Calculada como la suma de `SibSp` (hermanos/cónyuges) y `Parch` (padres/hijos) más uno (para el propio pasajero). Esta característica nos permite entender el tamaño del grupo familiar a bordo.
* **`IsAlone`:** Una característica binaria (1 si `FamilySize` es 1, 0 en caso contrario) que indica si el pasajero viajaba solo. Esta distinción es crucial para analizar el impacto de ir acompañado en la supervivencia.

### 3. Factores Clave de Supervivencia (Basado en Visualizaciones)

Los siguientes factores mostraron una fuerte correlación con la supervivencia:

* **Género (`Sex`):**
    * **Observación:** Las mujeres tuvieron una tasa de supervivencia significativamente más alta que los hombres. Esto se alinea con la política de "mujeres y niños primero" implementada durante la evacuación.
    * **Impacto:** Es, quizás, el factor más determinante para la supervivencia en este dataset.

* **Clase de Pasaje (`Pclass`):**
    * **Observación:** Se observó una clara jerarquía en las tasas de supervivencia: los pasajeros de Primera Clase tuvieron las mayores probabilidades de sobrevivir, seguidos por los de Segunda Clase, y finalmente los de Tercera Clase, que mostraron la tasa de supervivencia más baja.
    * **Impacto:** Esto podría estar relacionado con la ubicación de las cabinas (más cercanas a los botes salvavidas en clases superiores) y el acceso preferencial.

* **Edad (`Age`):**
    * **Observación:** Aunque la distribución de la edad es compleja, las visualizaciones sugieren que los niños (especialmente los más pequeños) tenían una mayor probabilidad de supervivencia, lo cual también coincide con la directriz de evacuación.
    * **Impacto:** La edad parece ser un factor, con una ventaja para los más jóvenes.

* **Estado de Acompañamiento (`IsAlone` / `FamilySize`):**
    * **Observación:** Aquellos pasajeros que viajaban solos (`IsAlone = 1`) tuvieron una tasa de mortalidad considerablemente más alta en comparación con aquellos que viajaban acompañados (cualquier `FamilySize > 1`).
    * **Impacto:** Viajar en grupo (familia o pareja) parece haber conferido una ventaja en la supervivencia, posiblemente debido a la ayuda mutua o la priorización en la evacuación de familias.

### Conclusiones Generales

El análisis del dataset del Titanic revela que la supervivencia no fue aleatoria, sino que estuvo fuertemente influenciada por factores demográficos y socioeconómicos. El género, la clase de pasaje y la situación de acompañamiento emergieron como los predictores más prominentes de si un pasajero sobrevivió al desastre.

---
