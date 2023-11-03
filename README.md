# Proyecto_game
Proyecto individual I para crear un MVP (Minimum Viable Product) consumible segun los criterios de API REST o RESTful, para recomendar de manera personalizada videojuegos para cada usuario (usuario-item). Para el análisis de sentimiento se utiliza la libreria TextBlob y para el entrenamiento del modelo del sistema de recomendación se utiliza la librería surprice. 

## Transformaciones
En primer lugar se procede a abrir los datasets y transformar del formato json a csv. En esta etapa se procede a desanidar los campos necesarios para su posterior utilización en las funciones. 

## Feature Engineering: 
A partir del dataset user_reviews se realiza un 'sentiment_analysis' utilizando la librería TextBlob. Según cada comentario se utiliza el valor '0' si es malo, '1' si es neutral y '2' si es positivo. 

## Desarrollo API: 
Se disponibilizan los datos de la empresa usando el framework FastAPI. Para acceder utilice el siguiente link:

https://proyecto-game-5-eda.onrender.com/docs

Las consultas propuestas son las siguientes:

  1) def PlayTimeGenre( genero : str ): Debe devolver año con mas horas jugadas para dicho género.
  Ejemplo de retorno: {"Año de lanzamiento con más horas jugadas para Género X" : 2013}
  
  2) def UserForGenre( genero : str ): Debe devolver el usuario que acumula más horas jugadas para el género dado y una lista de la acumulación de horas jugadas por año.
  Ejemplo de retorno: {"Usuario con más horas jugadas para Género X" : us213ndjss09sdf, "Horas jugadas":[{Año: 2013, Horas: 203}, {Año: 2012, Horas: 100}, {Año: 2011, Horas:   23}]}
  
  3) def UsersRecommend( año : int ): Devuelve el top 3 de juegos MÁS recomendados por usuarios para el año dado. (reviews.recommend = True y comentarios positivos/neutrales)
  Ejemplo de retorno: [{"Puesto 1" : X}, {"Puesto 2" : Y},{"Puesto 3" : Z}]
  
  4) def UsersNotRecommend( año : int ): Devuelve el top 3 de juegos MENOS recomendados por usuarios para el año dado. (reviews.recommend = False y comentarios negativos)
  Ejemplo de retorno: [{"Puesto 1" : X}, {"Puesto 2" : Y},{"Puesto 3" : Z}]
  
  5) def sentiment_analysis( año : int ): Según el año de lanzamiento, se devuelve una lista con la cantidad de registros de reseñas de usuarios que se encuentren    
   categorizados con un análisis de sentimiento. Ejemplo de retorno: {Negative = 182, Neutral = 120, Positive = 278}

## Análisis exploratorio de los datos: (Exploratory Data Analysis-EDA)

A grandes rasgos, se tiene un dataset con videojuegos de la platafoma Steam Games con descripción sobre estos como el género o etiquetas en general y el precio, otro dataframe con los usuarios registrados y las horas jugadas totales para cada juego y por último los reviews de estos usuarios hacia cada juego. 

Hay 32133  juegos y 58459 usuarios, de los cuales 25485 usuarios,  dejaron 58431 comentarios sobre los juegos. 

Luego de este analisis general se realiza un reconocimiento de las variables más importantes para la recomendación, se categorizan algunas de ellas y se muestran en gráficos. En este punto se debe aclarar que debido a ser este un MVP, se redujeron las variables a utilizar en el ML a lo mínimo necesario que requiere la libreria surprice en sus propuestas básicas, estas son: user_id, item_id y sentimente, que es la "puntuación" del usuario hacia determinado juego, que se obtiene del análisis de sentimiento y que tiene tres opciones. Puntuación negativa, nula o positiva.

## Modelo de aprendizaje automático:

Para armar un sistema de recomendación, se procede a entrenar el modelo de machine learning, para ello se utiliza la librería surprice, ingestando los datos como un dataframe y utlizando el método TrainTestSplit. Puede ver la documentación oficial aquí: https://surprise.readthedocs.io/en/stable/getting_started.html#train-test-split-and-the-fit-method

El modelo entrenado se guardo con la librería joblib, obteniendo un archivo .pkl que será consumido por la función de recomendación. 

Para probar el sistema de recomendación, se puede abrir el documento df_ML.csv provisto en Github y elegir un usuario o probar con los siguientes usuarios:

76561197970982479
evcentric
js41637
ApxLGhost
72947282842
wayfeng
pikawuu2
Sammeh00
Michaelele

## Video 
En el enlace puede ver un video de la API en Render y su funcionamieto
 
