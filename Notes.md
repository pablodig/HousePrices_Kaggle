## Lecciones de House Pricing:

Hacer el pre-procesamiento de los datos. Reemplazar datos faltantes (nan).
Es bueno hacer merge del df train y el test para poder pre-procesar todo de la misma manera.
De esta forma se evita cometer errores.

**Versión 1: (mean/mode missing values imputation and RandomForestRegressor - Marian)**
Los datos faltantes (missing values = nan) fueron reemplazados por la media o por la moda de esa variable dependiendo si se trata de
variables numéricas o categóricas, respectivamente.
Se usó RandomForestRegressor ya que es uno de los más faciles de usar y además maneja bien variables numéricas y categóricas.
Además no necesita pre-procesamiento de los datos (normalización, estandarización) aunque puede que eso lo mejore.
En esta versión se recortaron las features que describen los datasets. Se pasó de un total de alrededor de 200 features a menos de 20. 
Esto acelera mucho el entrenamiento, predicción y funcionamiento general del algoritmo. Las features seleccionadas fueron aquellas
que mejor correlacionan con la variable a predecir (SalePrice). El modelo se optimizó realizando randomized y grid search.
Si bien este predictor funciona bastante bien y es muy rápido obtuvo un puntaje de ~0.16 quedando en el peloton de los 10 mil mejores.

**Versión 2: (mean/mode missing values imputation and RandomForestRegressor - Pablo)**
Los datos faltantes se imputaron de la misma manera que en la Versión 1.
Se procedió de forma similar a la de la versión 1 pero se utilizaron inicialmente todas las features. 
Para el modelo final se descartaron aquellas features que menos contribuyen al modelo según las importancias medias de estas features
en un ensayo de cross-validación. El modelo se optimizó realizando una randomized search. 
De esta forma se mejoró la predicción obteniendo un puntaje de ~0.15 y quedando en el grupo de los 9-10 mil mejores.
**<ins>nota</ins>**: chequear como quedó entrenado el modelo final (hiperparámetros y fiteo).

**Versión 3: (mean/mode missing values imputation and RandomForestRegressor - Marian)**
Los datos faltantes se imputaron de la misma manera que en la Versión 1.
Se abordó nuevamente el problema usando conceptos aprendidos de la versión 1 y 2. En este caso se decidieron utilizar todas las
features con las que se cuenta en los datos. Se optimizó el modelo realizando randomized y grid search, intentando obtener
los mejores hiperparámetros (nota: realizar la grid search de ~320 modelos tardo cerca de 2 hs, esto se debe a que tiene muchas features).
Por ahora este es el modelo que realiza las mejores predicciones, obteniendo un puntaje de ~0.1448 y quedando en la posición ~7900.
**<ins>nota</ins>**: acordarse siempre de entrenar el modelo final con el dataset entero!!

**Versión 4: (Knn (3 neighbors) missing values imputation and RandomForestRegressor - Marian)**
Los datos faltantes se imputaron de una nueva manera: se usaron valores vecinos para asignarle un valor a los faltantes (KNN con n_estimators=3
y weight según distancia). Se utilizaron todas las features. Se optimizó el modelo realizando randomized y grid search, intentando obtener
los mejores hiperparámetros. Por ahora este es el modelo que realiza las mejores predicciones, obteniendo un puntaje de ~0.1442 y quedando en la posición ~7800.


**¿Cómo mejorar el modelo?**
* Mejorar la imputación de los nan values. Vimos que hacerlo con Knn (usando 3 vecinos) ya produce una mejora. Explorar mejor este campo.
* Cambiar de algoritmo: pasar de RandomForest a XGBoost?
