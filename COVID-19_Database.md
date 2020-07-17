# COVID-19_Database

Esta extensa base de datos contiene imagenes de radiografias de torax de pacientes pronosticados con COVID-19, Neumonia (generalizando varios tipos de neumonia) y radiografias de pacientes que no presentaron ninguna anormalidad.

Las bases de datos que se usaron para la construccion de **COVID-19_Database** se colocan a continuacion:

* **COVID-19 Image Data Collection:** https://github.com/ieee8023/covid-chestxray-dataset 
* **Figure 1 COVID-19 Chest X-ray Dataset Initiative:** https://github.com/agchung/Figure1-COVID-chestxray-dataset 
* **RSNA Pneumonia Detection Challenge:** https://www.kaggle.com/c/rsna-pneumonia-detection-challenge/data 
* **Actualmed COVID-19 Chest X-ray Dataset Initiative:** https://github.com/agchung/Actualmed-COVID-chestxray-dataset#actualmed-covid-19-chest-x-ray-dataset-initiative 
* **COVID-19 Radiography Database:** https://www.kaggle.com/tawsifurrahman/covid19-radiography-database 

En este repositorio se adjuntara el resultado final del contenido de COVID-19_Database, pero incluyo el procedimiento de forma que, quede constancia de los algoritmos aplicados para llegar al contenido final de **COVID-19_Database.**

## Procedimiento
  
Cada una de estas bases de datos cuenta con un "**metadata.csv**" en el que se etiqueta a cada imagen con el tipo de anormalidad que presenta. Para llevar una clasificacion ordenada de principio a fin, se tomo la decision de usar algoritmos de clasificacion realizados con la herramienta de Python "**Jupyter Notebook**". Es importante mencionar que los algoritmos de clasificacion estan usando el "metadata" en su extension "**.xlsx**" habiendo realizado un proceso de separacion de datos por comas.

Lo primero que debemos hacer es tener descargadas las bases de datos antes mencionadas y dentro de una sola carpeta, a la cual, podremos darle el nombre "PROYECTO" o el que mejor nos convenga.

Se crea una carpeta destino con el nombre "DATASET" y dentro de ella, otras carpetas con los nombres:

* Data_separada_Cohen
* Data_separada_Figure1_SOLO_COVID
* Data_convertida_separada_RSNA**
* Data_separada_ActualMed_SOLO_COVID
  
Se excluye del proceso de clasificacion a la base de datos "**COVID-19 Radiography Database**" debido a que se encuentra en una correcta organizacion y etiquetacion de la clase en el nombre propio de la imagen.

### Clasificacion de la base de datos "COVID-19 Image Data Collection"

Dentro de la carpeta "**Data_separada_Cohen**" vamos a crear dos carpetas adicionales y las llamaremos "COVID" y "PNEUMONIA"

Abrimos y corremos el algoritmo de clasificacion, teniendo presente que las variables "savepath" "cohen_imgpath" y "cohen_xlsxpath" podran variar dependiendo en donde hayamos descargado las bases de datos mencionadas al inicio de este repositorio. A continuacion adjunto el link.

### Clasificacion de la base de datos "Figure 1 COVID-19 Chest X-ray Dataset Initiative"

La carpeta "**Data_separada_Figure1_SOLO_COVID**" sera la carpeta destino en donde podremos colocar el resultado de la clasificacion de imagenes solo con COVID-19.

Debido a la escacez de imagenes dentro de esta base de datos en comparacion con las otras antes mencionadas, se tomo la decision de realizar una clasificacion manual para esta base de datos en donde solo se tomo en cuenta las imagenes de radiografias que presentaron COVID-19.

### Clasificacion de la base de datos "RSNA Pneumonia Detection Challenge"

Dentro de la carpeta "**Data_convertida_separada_RSNA**" vamos a crear dos carpetas adicionales y las llamaremos "NEUMONIA" y "NORMAL"

Abrimos y corremos el algoritmo de clasificacion, teniendo presente que las variables "savepath" "rsna_imgpath" y "rsna_xlsxpath" podran variar dependiendo en donde hayamos descargado las bases de datos mencionadas al inicio de este repositorio. A continuacion adjunto el link.

### Clasificacion de la base de datos "Actualmed COVID-19 Chest X-ray Dataset Initiative"

La carpeta "**Data_separada_ActualMed_SOLO_COVID**" sera la carpeta destino en donde podremos colocar el resultado de la clasificacion de imagenes solo con COVID-19.

Abrimos y corremos el algoritmo de clasificacion, teniendo presente que las variables "savepath" "actmed_imgpath" y "actmed_xlsxpath" podran variar dependiendo en donde hayamos descargado las bases de datos mencionadas al inicio de este repositorio. A continuacion adjunto el link.

### Combinacion de resultados pertenecientes a la misma clase

Se crean tres carpetas adicionales dentro de la carpeta "DATASET" con los nombres:

* COVID
* NO COVID_vn
* NORMAL

Dentro de estas carpetas se colocan las imagenes pertenecientes a los resultados obtenidos por los algoritmos de clasificacion. Este paso es demasiado simple y se lo puede realizar de forma manual.

Finalmente tendremos preparada una organizacion de los 5 datasets anteriormente mencionados en tres carpetas que resumiran los 3 diferentes tipos de clase que contendra **COVID-19_Database**.

### Cantidad de datos obtenidos por los algorimos de clasificacion por cada Dataset
 
 
| Base de Datos | COVID-19 | Neumonia | Normal | 
|---------------|----------|----------|--------|
| **COVID-19 Image Data Collection** | 415 | 40 | 0 | 
| **Figure 1 COVID-19 Chest X-ray Dataset Initiative** | 35 | 0 | 0 |
| **RSNA Pneumonia Detection Challenge** | 0 | 6012 | 20672 |
| **Actualmed COVID-19 Chest X-ray Dataset Initiative** | 58 | 0 | 0 |
| **COVID-19 Radiography Database** | 219| 1345 | 1341 |
| **Total por caso**  | 727 | 7397 | 22013 |
| **Total general** | 30137 |


### Division de COVID-19_Database en conjuntos de entrenamiento y prueba

El objetivo principal de la construccion de esta base de datos es servir para el entrenamiento de una red neuronal convolucional y por ende necesitaremos dividir el Dataset hasta el momento obtenido con las clasificaciones previamente realizadas, en dos conjuntos de datos. Para el conjunto de datos de entrenamiento se ha decidido tomar el **%70** de COVID-19_Database y para el conjunto de prueba el **%30** restante. Para llevar a cabo esta division, se usara un algoritmo desarrollado con la herramienta de Python "Jupyter Notebook".

El proposito de este algoritmo, ademas de dividir el set de datos, es realizar una **adecuacion** de las imagenes tanto en color como en resolucion o tamaño de la imagen, con el objetivo de obtener una base de datos lista para el entrenamiento de la red. Dicho esto, la resolucion de las imagenes que se encontraran dentro de "train y "test" seran de **480 x 480 pixeles (tamaño que puede cambiarse editando el algoritmo en las variables "ROW" y "COL")** y por el motivo de que algunas de estas imagenes presentaban un coloramiento se decidio realizar un cambio de imagen RGB a escala de grises.

El resultado de usar el algoritmo seran dos carpetas "train" y "test", las cuales tendran imagenes en escala de grises de tamaño 480 x 480 y con su debida etiqueta en el nombre de la imagen acompañado de una numeracion que ira desde el 0.

Para realizar esto creamos dos carpetas destinos dentro de la carpeta "DATASET" con el nombre de "train" y "test" y usamos el algoritmo en el link adjuntado.

**Nota: Las direcciones cambiaran dependiendo en donde se haya instalado la carpeta "DATASET" o la carpeta "PROYECTO".**

### Resultado de la division de COVID-19_Database



| Carpeta | COVID-19 | Neumonia | Normal | Total por carpeta|
|---------|----------|----------|--------|-------|
| **train** | 508 | 5177 | 15409 | 21094 |
| **test** | 219 | 2220 | 6604 | 9043 |





  

  
  
  
  
