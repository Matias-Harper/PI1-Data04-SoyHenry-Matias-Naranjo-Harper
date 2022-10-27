# Proyecto Individual 1- Data 04- Soy Henry
## Matías Naranjo Harper
# Data Engineering

En este trabajo se presenta un proceso de ETL (extract, transform and load) a partir de un conjunto de datos dado.
Los datos provienen de diferentes tipos de archivos que deberan ser trabajados y normalizados con el objetivo de crear un DER y dejarlos almacenados en un archivo con la extensión .db. Considerando la carga incremental de los archivos “precio_semana_……”

# Procesar los diferentes datasets.
Se procedió a cargar los diferentes archivos aportados para el trabajo y convertirlos a DataFrame de Pandas para poder ser normalizados. En el video se muestra el paso a paso del proceso de normalización que finalmente se encapsuló en una función para su utilización de manera simple.
La totalidad de archivos fueron procesados solo desde Pandas a excepción del archivo Excel que fue abierto en el programa y separado antes de su ingesta.

Archivos precio_semana: trabajado en el archivo "Trabajo_Precio_sem_Granfuncion.ipynb"
Se realizó una función que realiza las acciones que se comentan al lado del código.


En el archivo Sucursal.csv (Trabajado en "Trabajo_Sucursal.ipynb") únicamente se cambió el nombre de la columna “id” por “sucursal_id”

Y en el último archivo producto.parquet ("Trabajo_Producto.ipynb") se eliminaron las columnas que contemplaban tres categorías, esto puede revertirse si así lo desea el cliente. El área de data las considero obsoletas al tener vacías 72034 filas de un total de 72038 filas, nos genera un 99,99% de espacios vacíos. Sumando las 3 columnas deberíamos considerar 72038x3 espacios de memoria dedicados a esto.
Además de esto la columna “id” fue renombrada como “producto_id”. Para esta funcion tambien tuvimos que utilizar las funciones “sacaguion” y “llevar_13”

# Crear un archivo DB con el motor de SQL que quieran.
Al ser completada la etapa de ingesta y normalización de los archivos se creó la base de datos “P1_v1” en MySQL y se cargó desde python utilizando pymysql y sqlalchemylas las tablas Sucursal y Producto.
A la función de normalización se le adjunto la carga en la base de datos lo que permite que se normalice y carguen los datos ingresados en ella

Diagrama del trabajo de ETL

![](https://github.com/Matias-Harper/PI1--Data-04--Soy-Henry-Mat-as-Naranjo-Harper/blob/main/diagrama%20etl.png)

#Propuestas para el cliente:

- Generar 3 columnas nuevas desde sucursal_id, considerando que el mismo está compuesto por banderaId-comercioId-sucursalId esto nos permitirá filtrar de manera más óptima por bandera,comercio o sucursal.
Además de esto se propone sacar los guiones intermedios para mejorar la performance de las consultas, para esto se deberá colocar cero antes de los datos para poder conservar su relación.
Por ejemplo si se definen 4 cifras para cada uno el valor 45-33-2 deberá ser transformado primero en 0045-0033-0002 y luego a 004500330002

- Se propone adjuntar fecha de carga de los datos de precio_semana . Esto permitirá diferenciarlos por fecha 

- Solucionar en conjunto con el área que corresponda los valores duplicados en productos_id, cuenta con 255 productos con el id duplicado y diferente producto

# Breve explicación en video: https://youtu.be/jnBRPVw4VVg
