# APLICACIONES DISTRIBUIDAS (HTTP, SOCKETS, HTML, JS,MAVEN, GIT)

Una aplicacion para consultar los datos de la pelicula de cine deseada. La busqueda se hace por titulo, utilizando el API "omdbapi.com" e implementando cache.

## Instrucciones para ejecutar

A continuacion, dejo respectivas instrucciones para correr el proyecto adecuadamente tras obtener la direccion a este repositorio GitHub. Igualmente, mas abajo dejare evidencia detallada para garantizar que se entienda su implementacion. La aplicacion debe usarse para fines de prueba y desarrollo.

### Requisitos previos

Para descargar la aplicacion, ya estando aqui, se necesita un equipo de computo con las siguientes caracteristicas:

```
- Java instalado

- Maven instalado

- JavaScript instalado

- Conexion a internet

- Explorador web

- (OPCIONAL) Personal API key Omdbapi

- (RECOMENDACION) Tener todo actualizado
```
Esta guia no incluye tutoria para la descarga e instalacion de los anteriores mencionados. Si no cuenta con algo, o no sabe, le recomiendo ver algun video en Youtube.

### Instalando

Paso a paso

```
1. Descargar el codigo: Bajar el .ZIP correspondiente al repositorio.

2. Extraer el contenido del archivo comprimido.

3. Abrir el Shell de su preferencia.

4. Desde el Shell, muevase a la ubicacion donde extrajo el archivo .ZIP (Deberia estar dentro de la carpeta llamada  "ARQUITECTURAS-EMPRESARIALES-TALLER-1-master").

5. Desde el Shell, escriba "mvn package" (este comando compila, construye y empaqueta el proyecto en un .JAR).

6. Desde el Shell, escriba "java -cp target/Taller1-1.0-SNAPSHOT.jar edu.escuelaing.app.App" para ejecutar la aplicacion.
   Deberia ver un mensaje diciendo "Listo para recibir... ".

7. Abra su explorador web de preferencia y busque en una pestaña incognita lo siguiente: "localhost:35001" (SIN LAS COMILLAS).

8. Entonces, tendra acceso a un software que le permite consultar toda la informacion de peliculas relacionada al cine.

9. Para hacerlo, debe buscar la pelicula que le interesa por su titulo original, el cual muy seguramente este escrito en ingles, y posteriormente debe pulsar sobre el
   boton "Submit" para enviar la solicitud al API de la pelicula que busca.
   En pantalla podra ver toda la informacion que el API pudo proveer sobre su eleccion.
```

Puede hacer cuantas consultas quiera. Para cerrar el servicio puede introducir en el campo de texto cualquier cadena que inicie con un espacio en blanco, por ejemplo " _", y el servidor se apagara enseguida. 

```
Una vez haya terminado, puede cerrar el servicio introduciendo en el campo de texto " _" y el servidor se apagara enseguida.

```

¡¡"Oppenheimer" salio apenas hace unas semanas a las salas de cine, pero la API ya puede obtener todos sus datos!!

## Ejecucion de las pruebas

La aplicacion cuenta con pruebas automatizadas, tanto unitarias como concurrentes. Para demostrar las pruebas de concurrencia, es necesario que el servidor web este en pleno funcionamiento mientras se corren las pruebas. Para ello, tendremos que abrir 2 Shells al mismo tiempo: en uno ejecutaremos primero "java -cp target/Taller1-1.0-SNAPSHOT.jar edu.escuelaing.app.App", una vez aparezca en pantalla el mensaje "Listo para recibir...", en el otro pondremos el comando "mvn test".

NOTA: Para abortar el shell con el servidor encendido, podemos presionar "CTRL" + "C".

### Pruebas unitarias

Se hicieron 5 pruebas unitarias a 3 metodos.

Primero estan las pruebas del metodo "getTitle" de la clase "App".
Estas pruebas verifican que el método devuelve el resultado correcto al obtener la información de una película en formato JSON.
Por ejemplo, para la pelicula "Hola" podemos obtener la informacion completa de ella, en formato JSON, gracias al API y la direccion web "https://www.omdbapi.com/?t=Hola&apikey=2017f520", por tanto es importante rectificar que "app.getTitle("Hola")" sea equivalente, pues es importante que los mensajes que devuelva el servidor sean completos y esten en el formato correcto.
```
{\"Title\":\"Hola\",\"Year\":\"2005\",\"Rated\":\"N/A\",\"Released\":\"01 Mar 2005\",\"Runtime\":\"61 min\",\"Genre\":\"N/A\",\"Director\":\"Ana Ynsaurralde\",\"Writer\":\"Ana Ynsaurralde\",\"Actors\":\"Raquel Adoler, Julieta Buschiazzo, Gabriel Coba\",\"Plot\":\"N/A\",\"Language\":\"Spanish\",\"Country\":\"Argentina\",\"Awards\":\"N/A\",\"Poster\":\"N/A\",\"Ratings\":[{\"Source\":\"Internet Movie Database\",\"Value\":\"5.2/10\"}],\"Metascore\":\"N/A\",\"imdbRating\":\"5.2\",\"imdbVotes\":\"5\",\"imdbID\":\"tt0451761\",\"Type\":\"movie\",\"DVD\":\"N/A\",\"BoxOffice\":\"N/A\",\"Production\":\"N/A\",\"Website\":\"N/A\",\"Response\":\"True\"}
```
Para los otros 2 metodos, es conveniente revisar la documentacion respectiva pues en ella se explican sus funcionamientos y propositos.

### Y pruebas de concurrencia

En estas pruebas automatizadas, se envian 20 solicitudes al servidor desde un cliente Java. Importante estas pruebas para verificar el correcto manejo de las consultas por parte del servidor web.
Lo que se hizo fue comprobar si cada una de las respuestas de las solicitudes era correcta, de acuerdo a los valores previamente definidos y guardados, en una estructura de datos sencilla, para comparar con la respuesta que obtenia el servidor.

```
Title: Halloween II
HTTP/1.1 200 OK
Content-Type: application/json

{"Title":"Halloween II","Year":"1981","Rated":"R","Released":"30 Oct 1981","Runtime":"92 min","Genre":"Horror","Director":"Rick Rosenthal","Writer":"John Carpenter, Debra Hill","Actors":"Jamie Lee Curtis, Donald Pleasence, Charles Cyphers","Plot":"While Dr. Loomis hunts for Michael Myers, a traumatized Laurie is rushed to Haddonfield Memorial Hospital, and The Shape is not far behind her.","Language":"English","Country":"United States","Awards":"1 win & 3 nominations","Poster":"https://m.media-amazon.com/images/M/MV5BMjZmYjg0ODctOTIyYy00YzhkLTgyMzEtNjUyY2JiZjVmYzI2XkEyXkFqcGdeQXVyMTQxNzMzNDI@._V1_SX300.jpg","Ratings":[{"Source":"Internet Movie Database","Value":"6.5/10"},{"Source":"Rotten Tomatoes","Value":"33%"},{"Source":"Metacritic","Value":"40/100"}],"Metascore":"40","imdbRating":"6.5","imdbVotes":"96,871","imdbID":"tt0082495","Type":"movie","DVD":"19 Oct 2015","BoxOffice":"$25,533,818","Production":"N/A","Website":"N/A","Response":"True"}
Concurrent Test: true
```

## Implementacion

Una forma adicional de ejecutar el programa, permitiendo realizar busquedas manuales desde el cliente Java (sin necesidad de un explorador web), es, desde un IDLE de Java, ejecutar la clase App (servidor) seguida de la clase HttpClient (cliente). Una vez hecho esto, podremos ver informacion de peliculas desde la pantalla de resultado de el cliente Http, y podremos peliculas tal y como si fuese desde el browser (omitiendo la agradable interfaz). Al igual que desde el browser, podemos apagar el Sever introduciendo " _" en el campo de busqueda y luego enviando.

## Built With

* [Java](http://www.dropwizard.io/1.0.2/docs/) - The web framework used
* [Maven](https://maven.apache.org/) - Dependency Management
* [omdbapi](https://www.omdbapi.com) - API externo
* [HTTP](https://www.omdbapi.com) - API externo
* [SOCKETS](https://www.omdbapi.com) - API externo
* [HTML](https://www.omdbapi.com) - API externo
* [JavaScript](https://www.omdbapi.com) - API externo
* [Git/Github](https://www.omdbapi.com) - API externo
* [JSON](https://www.omdbapi.com) - API externo

## Contributing

Please read [CONTRIBUTING.md](https://gist.github.com/PurpleBooth/b24679402957c63ec426) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/your/project/tags). 

## Authors

* **Billie Thompson** - *Initial work* - [PurpleBooth](https://github.com/PurpleBooth)

See also the list of [contributors](https://github.com/your/project/contributors) who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Hat tip to anyone whose code was used
* Inspiration
* etc

