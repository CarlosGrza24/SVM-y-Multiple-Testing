# A3.1 – SVM y Multiple Testing

Este proyecto analiza datos de **expresión génica** de distintos tipos de cáncer utilizando métodos estadísticos y modelos de **Máquinas de Vectores de Soporte (SVM)**.  
El objetivo es identificar genes diferencialmente expresados entre los tipos de cáncer y comparar el desempeño de tres kernels de SVM: **lineal**, **polinomial (grado 3)** y **radial (RBF)**.

La base de datos utilizada fue proporcionada en clase y contiene **83 muestras** y **2308 variables de entrada**, que representan la expresión estandarizada de distintos genes.  
La variable de salida toma valores del **1 al 4**, correspondientes a los diferentes tipos de cáncer.

---

## Datos utilizados

- **83 muestras** (filas).  
- **2308 genes** (variables de entrada).  
- **Variable de salida (`y`)**: tipo de cáncer (1, 2, 3 o 4).  
- Cada valor representa la **expresión estandarizada** de un gen.  
- No se reportan valores faltantes.  

---

## Metodología

### 1. Importación y revisión de datos
- Se cargó la base `A3.1_Khan.csv` en el entorno de trabajo.  
- Se verificó la ausencia de valores faltantes y se visualizaron las primeras filas para confirmar la estructura.  
- Se calcularon las diferencias de medias entre las clases **2 y 4** para todos los genes y se imprimieron los **10 genes con mayor diferencia**.  
- Se comentó el posible significado de estas diferencias desde un punto de vista de inferencia biológica.

---

### 2. Prueba t y corrección por múltiples comparaciones
- Se aplicó la **prueba t de Student** para comparar las medias entre las clases 2 y 4 para cada gen.  
- Se obtuvieron los valores t y p, que indican si existen diferencias significativas entre grupos.  
- Para evitar falsos positivos, se aplicaron tres métodos de corrección:  
  - **Bonferroni** (más estricto).  
  - **Holm** (intermedio).  
  - **Benjamini-Hochberg (BH-FDR)** (más flexible).  
- Se mostró la cantidad de genes significativos para cada método y se imprimieron los **10 más importantes de cada uno**.

---

### 3. ANOVA (Análisis de varianza) entre las cuatro clases
- Se separaron los datos en las clases 1, 2, 3 y 4.  
- Se aplicó la prueba **ANOVA de una vía** mediante `f_oneway()` para comparar las medias de cada gen entre las cuatro clases.  
- Se aplicaron las mismas tres correcciones (Bonferroni, Holm y BH-FDR) para controlar el error por pruebas múltiples.  
- Se imprimió cuántos genes resultaron significativos y los **10 con menor p-value** bajo el método BH-FDR.  

---

### 4. Entrenamiento de modelos SVM
- Se seleccionaron las **200 variables más significativas** del ANOVA para reducir el costo computacional.  
- Se dividieron los datos en **70 % entrenamiento** y **30 % prueba** utilizando `train_test_split(..., stratify=y)`.  
- Se entrenaron tres modelos SVM con diferentes kernels:  
  - **Lineal**.  
  - **Polinomial (grado 3)**.  
  - **Radial (RBF)**.  
- Los datos fueron estandarizados con `StandardScaler()` antes del entrenamiento para mejorar el rendimiento de los modelos.

---

### 5. Evaluación y comparación de modelos
- Se evaluó el desempeño de los tres modelos usando las métricas **Accuracy** y **F1-score (ponderado)**.  
- Se graficaron las **matrices de confusión** para los tres kernels utilizando el mapa de color *plasma* para facilitar la comparación visual.  
- Se discutieron los resultados observados y se identificó qué modelo tuvo mejor rendimiento en la clasificación de los tipos de cáncer.  

---

## Archivos del proyecto

- [Reporte en ipynb](A3.1_648241.ipynb)
- [Reporte en html](A3.1_648241.html)  
- [A3.1_Khan.csv](A3.1_Khan.csv)  
