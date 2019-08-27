# Funciones


## ¿Cuándo deberías escribir una función?


### Práctica

1. ¿Por qué `TRUE` no es un parámetro para `rescale01()`? ¿Qué pasaría si `x` está contenido en un valor único perdido y `na.rm` fuese `FALSE`?

1. En la segunda variante de `rescale01()`, los valores infinitos se dejan sin cambio. Reescribe `rescale01()` así `-Inf` is convertido a 0, y `Inf` es convertido a 1.

1. Practica convertir los siguientes fragmentos de código en funciones. Piensa en lo que hace cada función. ¿Cómo lo llamarías? ¿Cuántos argumentos necesita? ¿Puedes reescribirlo para ser más expresivo o menos duplicado?

 
 ```r
 mean(is.na(x))
 
 x / sum(x, na.rm = TRUE)
 
 sd(x, na.rm = TRUE) / mean(x, na.rm = TRUE)
 ```

1. Sigue <http://nicercode.github.io/intro/writing-functions.html>
para escribir tus propias funciones para computar la variancia y el sesgo de un vector numérico.

1. Escribe `both_na()`, una función que toma dos vectores de la misma longitud y retorna el número de posiciones que tiene `NA` en ambos vectores.

1. ¿Qué hacen las siguientes funciones? ¿Por qué son tan útiles aún cuando son tan cortas?

 
 ```r
 is_directory <- function(x) file.info(x)$isdir
 is_readable <- function(x) file.access(x, 4) == 0
 ```

1. Lee el [complete lyrics](https://en.wikipedia.org/wiki/Little_Bunny_Foo_Foo)
 de "Pequeño conejito Foo Foo". There's a lot of duplication in this song.
 Extiende el ejemplo inicial de pipes para recrear la canción completa, usar las funciones para reducir la duplicación.


## Las funciones son para los humanos y las computadoras


### Ejercicios

1. Lee el código fuente para cada una de las siguientes tres funciones, interpreta que hacen, y luego propone nombres mejores.

 
 ```r
 f1 <- function(string, prefix) {
 substr(string, 1, nchar(prefix)) == prefix
 }
 f2 <- function(x) {
 if (length(x) <= 1) return(NULL)
 x[-length(x)]
 }
 f3 <- function(x, y) {
 rep(y, length.out = length(x))
 }
 ```

1. Toma una función que hayas escrito recientemente y tómate 5 minutos para pensar un mejor nombre para la función y para sus argumentos.

1. Compara y contrasta `rnorm()` y `MASS::mvrnorm()`. ¿Cómo podrías hacerlas más consistentes?

1. Argumenta porqué `norm_r()`,`norm_d()` etc sería una mejor opción que `rnorm()`, `dnorm()`. Argumenta lo contrario.

## Ejecución condicional


### Ejercicios

1. ¿Cuál es la diferencia entre `if` and `ifelse()`? Lea cuidadosamente la ayuda y construya tres ejemplos que ilustren las diferencias claves.


1. Escriba una función de saludo que diga "buenos días", "buenas tardes" o "buenas noches", según la hora del día. (Sugerencia: use un argumento de tiempo que por defecto es `lubridate::now()`, eso hará que sea más fácil probar su función).

1. Implemente una función `fizzbuzz`. Toma un solo número como entrada. Si el número es divisible por tres, devuelve "fizz". Si es divisible por cinco, devuelve "buzz". Si es divisible por tres y cinco, devuelve "fizzbuzz". De lo contrario, devuelve el número. Asegúrese de escribir primero el código de trabajo antes de crear la función.

1. ¿Cómo podría usar `cut()` para simplificar una sentencia if-else anidada?

 
 ```r
 if (temp <= 0) {
 "freezing"
 } else if (temp <= 10) {
 "cold"
 } else if (temp <= 20) {
 "cool"
 } else if (temp <= 30) {
 "warm"
 } else {
 "hot"
 }
 ```

 ¿Cómo cambiarías la sentencia a `cut()` si hubieras usado `<`en lugar de `<=`? ¿Cuál es la otra ventaja principal de `cut()` para este problema? (Sugerencia: ¿qué sucede si tienes muchos valores en `temp`?)

1. ¿Qué sucedería si usaras `switch()` con un valor numérico?

1. ¿Qué haría la sentencia `switch()`? ¿Qúe sucedería si `x` fuera “e”?

 
 ```r
 switch(x,
 a = ,
 b = "ab",
 c = ,
 d = "cd"
 )
 ```

 Experimente, luego lea cuidadosamente la documentación.


## Function arguments


### Ejercicios

1. ¿Qué realizan las `commas(letters, collapse = "-")`? ¿Por qué?

1. Sería bueno si se pudiera suplantar múltiples caracteres al argumento `pad`,
 ej., `rule("Title", pad = "-+")`. ¿Por qué esto actualmente no funciona? ¿Cómo podrías solucionarlo?

1. ¿Qué realiza el argumento `trim` a la función `mean()`? ¿Cuándo podrías utilizarla?

1. El valor de defecto para el argumento `method` a `cor()` es
 `c("pearson", "kendall", "spearman")`. ¿Qué significa esto? ¿Qué valor se utiliza por defecto?
