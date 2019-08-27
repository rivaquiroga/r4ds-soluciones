# Iteración

## Bucles _for_

### Ejercicios

1.  Escribir bucles _for_ para:

    1. Calcular la media de cada columna en `mtautos`.
    2. Determinar el tipo de cada columna en `vuelos`.
    3. Calcular el número de valores únicos en cada columna de `iris`.
    4. Genera 10 normales aleatorias para cada valor de $\mu = -10$, $0$, $10$ y $100$.
    
    Piensa en el resultado, la secuencia y el cuerpo __antes__ de empezar a escribir
    el bucle.

2.  Elimina el bucle _for_ en cada uno de los siguientes ejemplos tomando
     ventaja de una función existente que trabaja con vectores:
    
    
    ```r
    out <- ""
    for (x in letters) {
      out <- stringr::str_c(out, x)
    }
    
    x <- sample(100)
    sd <- 0
    for (i in seq_along(x)) {
      sd <- sd + (x[i] - mean(x)) ^ 2
    }
    sd <- sqrt(sd / (length(x) - 1))
    
    x <- runif(100)
    out <- vector("numeric", length(x))
    out[1] <- x[1]
    for (i in 2:length(x)) {
      out[i] <- out[i - 1] + x[i]
    }
    ```

3.  Combina tus habilidades para escribir funciones y bucles _for_:

    1. Escribe un bucle _for_ que imprima (_`prints()`_) la letra de la canción de niños
       "Cinco ranitas verdes".

    2. Convierte la canción infantil "10 monitos saltaban en la cama" en una función. Generalizar
       a cualquier cantidad de monitos en cualquier estructura para dormir.

    3. Convierte la canción "99 botellas de cerveza en la pared" en una función.
       Generalizar a cualquier cantidad, de cualquier tipo de recipiente que contenga 
       cualquier líquido sobre cualquier superficie.

4.  Es común ver bucles _for_ que no preasignan la salida y en su lugar
    aumentan la longitud de un vector en cada paso:
     
    
    ```r
    output <- vector("integer", 0)
    for (i in seq_along(x)) {
      output <- c(output, lengths(x[[i]]))
    }
    output
    ```
    
    ¿Cómo afecta esto el rendimiento? Diseña y ejecuta un experimento.

## Variaciones de bucles _for_

### Ejercicios

1.  Imaginemos que tenemos un directorio lleno de archivos CSV que queremos leer.
    Tenemos sus ubicaciones en un vector, 
    `files <- dir("data/", pattern = "\\.csv$", full.names = TRUE)`, y ahora
    queremos leer cada uno con `read_csv()`. Escribe un bucle _for_ que los
    cargue en un solo _data frame_.

1.  ¿Qué pasa si utilizamos `for (nm in names(x))` y `x` no tiene _names_?
    ¿Qué pasa si solo algunos elementos están nombrados (_named_ en inglés) 
    ¿Qué pasa si los nombres (_names_ en inglés) no son únicos?

1.  Escribe una función que imprima el promedio de cada columna numérica en un
	  _data frame_, junto con su nombre. Por ejemplo, `mostrar_promedio(iris)` debe imprimir:
    
    
    ```r
    mostrar_promedio(iris)
    #> Sepal.Length: 5.84
    #> Sepal.Width:  3.06
    #> Petal.Length: 3.76
    #> Petal.Width:  1.20
    ```
    
    (Desafío adicional: ¿qué función utilizamos para asegurarnos que los números
    queden alineados a pesar que los nombres de las variables tienen diferentes longitudes?)
    
1.  ¿Qué hace este código? ¿cómo funciona? 

    
    ```r
    trans <- list( 
      disp = function(x) x * 0.0163871,
      am = function(x) {
        factor(x, labels = c("auto", "manual"))
      }
    )
    for (var in names(trans)) {
      mtcars[[var]] <- trans[[var]](mtcars[[var]])
    }
    ```

## Bucles _for_ vs. funcionales

### Ejercicios

1.  Lee la documentación para `apply ()`. En el caso 2d, ¿qué dos bucles _for_ generaliza?

2. Adapta `col_summary ()` para que solo se aplique a las columnas numéricas. 
	Es posible que desees comenzar con la función `is_numeric ()` que devuelve un vector lógico que tenga un _TRUE_ por cada columna numérica.
	
## Las funciones _map_ (mapa en inglés)

### Ejercicios

1. Escribe un código que use una de las funciones de map para:

    1. Calcular la media de cada columna en `mautos`.
    1. Obtener de que tipo es cada columna en `vuelos`.
    1. Calcular la cantidad de valores únicos en cada columna de `iris`.
    1. Generar diez normales aleatorias para cada $\mu = -10$, $0$, $10$, and $100$.

1.  ¿Cómo puedes crear un vector tal que para cada columna en un cuadro de datos indique si
    corresponde o no a un factor?

1.  ¿Qué ocurre si usas las funciones map en vectores que no son listas?
    ¿Qué hace `map(1:5, runif)`? ¿Por qué?

1.  ¿Qué hace `map(-2:2, rnorm, n = 5)`? ¿Por qué?
    ¿Qué hace `map_dbl(-2:2, rnorm, n = 5)`? ¿Por qué?

1.  Reescribe `map(x, function(df) lm(mpg ~ wt, data = df))` para eliminar
    todas las funciones anónimas.


## Otros patrones para los loops for

### Ejercicios

1.  Implementa tu propia versión de `every()` usando un loop for. Comparala con
    `purrr::every()`. ¿Qué hace la versión de purrr que la tuya no hace?

1.  Crea una mejora de `col_sum()` que aplique una función de resumen a cada
    columna numérica en un data frame.

1.  Un posible equivalente de `col_sum()` es:

    
    ```r
    col_sum3 <- function(df, f) {
      is_num <- sapply(df, is.numeric)
      df_num <- df[, is_num]
    
      sapply(df_num, f)
    }
    ```
    
    Pero tiene una cantidad de bugs que queda ilustrada con las siguientes entradas:

    
    ```r
    df <- tibble(
      x = 1:3, 
      y = 3:1,
      z = c("a", "b", "c")
    )
    # OK
    col_sum3(df, mean)
    # Has problems: don't always return numeric vector
    col_sum3(df[1:2], mean)
    col_sum3(df[1], mean)
    col_sum3(df[0], mean)
    ```
    
    ¿Cuál es la causa de esos bugs?