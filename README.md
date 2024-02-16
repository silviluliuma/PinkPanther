
![10_copy](https://github.com/silviluliuma/ih_datamadpt0923_project_m3/assets/138609959/b5d21f28-50b5-4d98-9958-9470d35dedd4)
# ih_datamadpt0923_project_m3
Kaggle Diamond Competition. Proyecto de Machine Learning para la predicción del precio de los diamantes según el dataset de Kaggle.

![Captura de Pantalla 2024-02-16 a las 14 13 41](https://github.com/silviluliuma/ih_datamadpt0923_project_m3/assets/138609959/69731506-9c18-4439-b4c1-c9161f7d97bf)

## Data Exploration (EDA) 

Relación entre los distintos tipos de corte del diamante y sus respectivos precios. El corte de peor calidad ("fair") parece partir siempre de un precio más alto y se mantiene en un precio más elevado que el resto.

![Captura de Pantalla 2024-02-16 a las 13 32 10](https://github.com/silviluliuma/ih_datamadpt0923_project_m3/assets/138609959/121b019f-0c5c-4e79-8fd1-490f485fa790)

Relación entre los distintos tipos de color del diamante y sus respectivos precios. El color considerado de peor calidad (J) es, de nuevo, el que parte de un mayor precio inicial y el que mantiene un precio más elevado.

![Captura de Pantalla 2024-02-16 a las 13 34 25](https://github.com/silviluliuma/ih_datamadpt0923_project_m3/assets/138609959/3d245d82-d556-45eb-9a66-d23a5583c722)

Relación entre los tipos de claridad del diamante y sus respectivos precios. Ocurre lo mismo, los dos peores tipos de claridad ("I1, SI1"), tienen los precios más elevados.

![Captura de Pantalla 2024-02-16 a las 13 35 33](https://github.com/silviluliuma/ih_datamadpt0923_project_m3/assets/138609959/cb0a991a-d156-4a19-9241-a68209b58eaf)

En función de estos análisis, se asigna un valor numérico que oscila entre 0 y 1 a cada tipo de corte, color y claridad del diamante y con el que se pretende reflejar las jerarquía entre los mismos.

![Captura de Pantalla 2024-02-16 a las 13 38 09](https://github.com/silviluliuma/ih_datamadpt0923_project_m3/assets/138609959/27b09339-c63f-464b-bd67-ef1cfcc20675)

## Data Preprocessing and Data Cleaning

Como se observa en las anteriores imágenes, también es necesario ocuparse de los outliers de las variables numéricas de nuestro dataset. Como el formato de entrega requiere 13485 filas, no es suficiente con eliminar los outliers, por lo que aquellos outliers que se encuentren por debajo del límite inferior tomarán el valor de este, al igual que aquellos que se encuentren por encima del superior, que tomarán el valor de este último.  

![Captura de Pantalla 2024-02-16 a las 13 43 19](https://github.com/silviluliuma/ih_datamadpt0923_project_m3/assets/138609959/47e2f8bb-3cfa-4171-b4be-2da4d957d22d)

Con los outliers ya eliminados, se procede a la sustitución de los valores 0 por la media de los valores de cada columna (en este caso, sirve con la media porque ya no existen outliers que vayan a desajustar el cálculo).

## Scaling and Feature Engineering

Se ha probado a escalar los datos tanto con StandardScaler() como con RobustScaler(), produciéndose en ambos casos un detrimento en el valor de la RMSE, la métrica empleada para valorar los modelos en esta competición. 

Igualmente, se han creado y combinado numerosas features (volumen, densidad, color+corte, color+claridad, etc.), sin ninguna mejora significativa e, incluso, en algunos casos, con un nuevo detrimento. Por esta razón, se han conservado las features originales, eliminando únicamente "city", cuya aportación era prácticamente nula para nuestro modelo. 

## Models

![pantera-154](https://github.com/silviluliuma/ih_datamadpt0923_project_m3/assets/138609959/a3b22270-4065-423f-918d-1fe734e76abc)

Se han utilizado varios modelos de regresión para la predicción del precio de los diamantes: LinearRegression, RandomForest, XGBoost, LGBM y ExtraTrees. De estos cinco modelos, XGBoost y LGBM son los que presentan unas mejores métricas, seguidos por ExtraTrees y RandomForest y quedando muy alejados de LinearRegression, que en este caso concreto no es de ninguna utilidad. 

![Captura de Pantalla 2024-02-16 a las 14 12 27](https://github.com/silviluliuma/ih_datamadpt0923_project_m3/assets/138609959/9d869567-68eb-48d3-b1ea-6c320ded2689)

![Captura de Pantalla 2024-02-16 a las 14 12 39](https://github.com/silviluliuma/ih_datamadpt0923_project_m3/assets/138609959/7ff3b744-5218-44e6-a2cf-29841b8f38ac)

Se han probado distintas combinaciones de modelos, data processing y feature engineering y se han anotado los resultados en una tabla de registros para su posterior consulta. En la imagen, los registros están ordenados según la media ponderada de los resultados obtenidos en local y los obtenidos en kaggle para poder elegir cuáles presentar a la competición (aquellos con una media de RMSE más baja, en este caso el 009 y el 011).

![Captura de Pantalla 2024-02-16 a las 14 06 00](https://github.com/silviluliuma/ih_datamadpt0923_project_m3/assets/138609959/52059b83-257d-4bd2-ad62-ca6f9c2f7152)

En el caso del 009, se trata de un modelo XGBoost con los siguientes parámetros de GridSearch: {'learning_rate': 0.11, 'max_depth': 5, 'n_estimators': 348}

En el caso del 011, se trata de un modelo LGBM con los siguientes parámetros de GridSearch: LGBMRegressor(bagging_fraction=0.1, bagging_freq=0, feature_fraction=1,learning_rate=0.05, max_depth=15, min_data_in_leaf=2, n_estimators=123, num_leaves=120)
![1fed4c42da2ac11d6d6d6ebd32fdefbe](https://github.com/silviluliuma/ih_datamadpt0923_project_m3/assets/138609959/22ad9ae3-af98-4c75-b677-c6363acd078e)
