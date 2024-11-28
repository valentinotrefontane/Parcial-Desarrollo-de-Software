
<h1> Enunciado a realizar </h1>

Magneto quiere reclutar la mayor cantidad de mutantes para poder luchar contra los X-Mens.
Te ha contratado a ti para que desarrolles un proyecto que detecte si un humano es mutante basándose en su secuencia de ADN.
Para eso te ha pedido crear un programa con un método o función con la siguiente firma:
boolean isMutant(String[] dna);
En donde recibirás como parámetro un array de Strings que representan cada fila de una tabla de (NxN) con la secuencia del ADN. Las letras de los Strings solo pueden ser: (A,T,C,G), las cuales representa cada base nitrogenada del ADN.

Sabrás si un humano es mutante, si encuentras más de una secuencia de cuatro letras iguales, de forma oblicua, horizontal o vertical.


Desafíos:

Nivel 1:
Programa en java spring boot que cumpla con el método pedido por Magneto utilizando una arquitectura en capas de controladores, servicios y repositorios.

Nivel 2:
Crear una API REST, hostear esa API en un cloud computing libre (Render), crear el servicio “/mutant/” en donde se pueda detectar si un humano es mutante enviando la secuencia de ADN mediante un HTTP POST con un Json el cual tenga el siguiente formato:
POST → /mutant/
{ “dna”:["ATGCGA","CAGTGC","TTATGT","AGAAGG","CCCCTA","TCACTG"]
}
En caso de verificar un mutante, debería devolver un HTTP 200-OK, en caso contrario un 403-Forbidden

Nivel 3:
Anexar una base de datos en H2, la cual guarde los ADN’s verificados con la API. Solo 1 registro por ADN.
Exponer un servicio extra “/stats” que devuelva un Json con las estadísticas de las verificaciones de ADN: {“count_mutant_dna”:40, “count_human_dna”:100: “ratio”:0.4}
Tener en cuenta que la API puede recibir fluctuaciones agresivas de tráfico (Entre 100 y 1 millón de peticiones por segundo). Utilizar Jmeter
Test-Automáticos, Code coverage > 80%, Diagrama de Secuencia / Arquitectura del sistema.

<h1>Instrucciones de uso </h1>

<h2> isMutant </h2>

Para utilizar el agoritmo de deteccion de mutantes debemos enviar un array de Strings en formato Json bajo el nombre "stringDna".

Por ejemplo si enviamos el siguiente DNA a https://1erParcial-desarrollo-de-software.onrender.com/mutant

```json

{
    "stringDna": [
                "GACCG",
                "ACCGA",
                "AGCGA",
                "AAACA",
                "GCAAA"
    ]
}

 
```
Devolvera dependiendo si es mutante o no, true o false, tambien en formato json

```json

{
    "mutant": true
}

```
Aqui un ejemplo de un DNA humano.

```json

{
    "stringDna": [
                "GAGAA",
                "GGTAA",
                "GTCTG",
                "GGTAA",
                "AAGAA"
    ]
}

```


```json
{
    "mutant": false
}
```

<h2>📖 Estadisticas | GET /stats </h2>

Si enviamos una peticion al siguiente link, nos devolvera en formato Json, la cantidad de mutantes y humanos detectados, asi como su proporcion.

Ejemplo

```json

{
    "count_mutant_dna": 3,
    "count_human_dna": 2,
    "ratio": 1.5
}

```

<h1> Diagrama de secuencia </h1>


<h3> Si el DNA pedido ya existe en la base de datos</h3>

![Diagrama de secuencai  Mutantes Existe el ADN](https://github.com/user-attachments/assets/cc1699b5-fae2-4e80-a5d1-91673e52d1f8)

<h3> Si el DNA pedido no existe en la base de datos y debe ser verificado</h3>

![Secuencia  Mutantes no existe el ADN](https://github.com/user-attachments/assets/ce9aa70a-ee5f-4864-8ccc-2aaa951d1b78)

<h3> Uso del endpoint /stats </h3>

![Secuencia  Stats](https://github.com/user-attachments/assets/ea43419d-d6bd-42ce-a811-4fef49b3c8db)

Valentino Trefontane 3k9
