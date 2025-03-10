# <h1 align=center> **PROYECTO INDIVIDUAL Nº2** </h1>


# <h1 align=center>**`Data Analytics`**</h1>


# <h2 align=center>**`Análisis del sector de telecomunicaciones en Argentina`**</h2>


<p align="center">
<img src="imagenes\mapa.png" height=500>
</p>


<p align="center">


**En este proyecto se realiza una análisis exhaustivo de la realidad del mercado de telecomunicaciones, más específicamente del servicio del internet en la Republica Argentina los últimos 10 años. Se analizan los valores históricos y las oportunidades de crecimiento de la industria en las diferentes provincias del país.**
</p>


## DATOS


Dataset del servicio de internet en Argentina de Ente Nacional de Comunicaciones (ENACOM) en https://indicadores.enacom.gob.ar/datos-abiertos


<p align="center">
<img src="imagenes\enacom.png" height=50>
</p>


## ETL


Se extrajeron las tablas de la página oficial, se le aplicó una serie de transformaciones para posibilitar su uso posterior y se guardaron las nuevas tablas listas para utilizar en la aplicación BI.
Entre las modificaciones que se realizaron se tiene:


+ Se transformaron a csv las hojas del documento que se consideraron relevantes para el trabajo. No se convirtieron todas las tablas, porque varias tenían datos redundantes entre sí. Las tablas seleccionadas fueron `Acc_vel_loc_sinrango`, `Acceso por velocidad`, `Velocidad % por prov`, `Accesos_tecnologias_localidad`, `Acceso Por Tecnologia`, `Dial-BAf`, `Penetracion-hogares`, `Penetracion-población` y `Ingresos`.


+ Poner en formato **title** y aplicar **strip** las columnas `Provincia`, `Partido` y `Localidad`


+ Crear los rangos de velocidades y sumar los valores correspondientes para cada nueva columna para las tablas que lo necesitaran


+ Corregir errores de tipeo (como datos cargados para el cuarto trimestre del 2024 que en realidad es el 4 trimestre del 2023)


+ Cambiar los valores de conteo nan por 0 y se acomoda el formato de los números para sacar los puntos de miles


+ Limpiar comentarios y asteriscos presentes al final de algunas tablas


+ Se renombran las columnas para mantener el formato


Una vez que se disponibilizaron todas las tablas relevante se generaron transformaciones para que los datos sean más eficientes.


+ Se unen en una sola tabla todas las columnas importantes de las tablas que tiene las columnas:


**` Año | Trimestre | Provincia `**


+ + velocidad_fechas
+ + velocidad_promedio
+ + tipo_acceso
+ + cada_100_hogares
+ + cada_100_hab




+ Se unen en una sola tabla todas las columnas importantes de las tablas que tiene las columnas:


**` Provincia | Partido | Localidad `**


+ + acceso_localidad
+ + velocidad_loc
Y se eliminan las filas con faltantes por ser pocas y con valores poco relevantes


+ A la tabla `Ingresos` se le agrega una columna con el ingreso en dólares para tener una perspectiva más real de las ganancias.


### De esta forma se obtienen tres tablas con los datos más importantes


## EDA


En esta etapa se analizan los datos obtenidos después de las transformaciones.


### Faltantes:


> Por la forma en la que se realizaron las transformaciones ninguna de las tres tablas tiene valores faltantes.


<p align="center">
<img src="imagenes\faltantes.png" height=400>
</p>


### Duplicados:


> De igual manera, ninguna de las tablas tenia duplicados.


### Variables cuantitativas


Las tablas presentaban muchas columnas numéricas, principalmente con conteos para los diferentes lugares en diferentes trimestres. Pero algunas otras columnas eran índices o promedios que permiten hacer algunas conclusiones más profundas como la `velocidad media de bajada en Mbps`:


<p align="center">
<img src="imagenes\velocidad.png" height=400>
</p>


De esta gráfica se puede analizar, por ejemplo, que la mayoria del pais tiene velocidades relativamente bajas, ya que las barras se acumulan a la izquierda, pero también el rango llega a valores relativamente altos, por lo que se puede deducir que hay muy pocos puntos muy privilegiados donde la velocidad es muy superior.


Otro ejemplo es la columna `accesos cada 100 habitantes` que permite ver la evolución de cada provincia con el paso de los años, como en la siguiente gráfica de burbujas:


<p align="center">
<img src="imagenes\accesos.png" height=450>
</p>


En esta gráfica el tamaño de las burbujas muestra la cercanía en el tiempo. Es por esto que las provincias donde se forma una figura cónica muestran una evolución continua, mientras que las figuras más irregulares muestran retroceso en la cantidad de accesos. Además hay provincias que con los años hicieron saltos grandes mientras otras tienen una evolución más estancada.


Finalmente una gráfica similar pero con diferente significado:


<p align="center">
<img src="imagenes\cordoba.png" height=400>
</p>


En este gráfico cada burbuja es una localidad y su tamaño es la cantidad de registros que tienen. Entonces se está graficando como Córdoba es la provincia que más accesos con mejores velocidades tienen en su localidad más grande (Capital).


<p align="center">
Todo el proceso de ETL y EDA se realizó en una Jupyter notebook en Google colab con excepción de la conversión a csv que se realizó en Excel.
</p>


<p align="center">
<img src="imagenes\jupyter.png" height=200>
</p>


## Dashboard


Una vez que se consiguieron las tres tablas y se estudió sus columnas se las cargó a la herramienta BI donde se realizan las gráficas que explican los datos con un hilo narrativo y mostrando los puntos claves del dataset.


<p align="center">
<img src="imagenes\portada.png" height=500>
</p>


Un ejemplo de estos análisis es este gráfico donde se representa el KPI de crecimiento trimestral de accesos cada 100 hogares, donde particularmente en Córdoba, se ve como desde el segundo trimestre del 2018 el crecimiento fue prácticamente siempre positivo:


<p align="center">
<img src="imagenes\cordoba2.png" height=500>
</p>


Además se calcularon otros KPI como el crecimiento de las ganancias y las ganancias por usuario. Con estos KPI y otras métricas se desarrolló un relato que permite conocer a profundidad los datos y plantear las oportunidades de negocio que se presentan.


<p align="center">
El dashboard se realizó en PowerBI.
</p>


<p align="center">
<img src="imagenes\powerbi.png" height=200>
</p>


## Conclusiones finales

+ Provincias con muy pocas conexiones pero grandes población como Tucumán y Mendoza.

+ Provincias como Córdoba y Santa Fe tienen un aumento porcentual de acceso mantenidamente positivo en los últimos 5 años.

+ Tendencia a tener velocidades más rápidas, pero se tienen más de un millón de clientes con velocidades menores a 6 Mbps en Buenos Aires.

+ Provincias mas pequeñas del interior tienen mucho más porcentaje de su población con velocidades bajas, como La Pampa, Salta y Santiago del Estero.

+ Económicamente hablando, como muchos otros negocios en este país, los ingresos son muy variables. Viendo los últimos 10 años, el promedio de crecimiento es positivo, con fluctuaciones de un 1%. 

+ Además, los ingresos por cliente son cada vez menores, lo que indica que el servicio se hizo cada vez más accesible para la población, pero se podría plantear una mejora del servicio a la vez que se sube la el costo del servicio.
