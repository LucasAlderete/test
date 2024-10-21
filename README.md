///////////NEO4J////////////////

Crear los nodos de personas, ciudades y países:
CREATE (john:Persona {nombre: 'John Smith', edad: 45}),
       (maria:Persona {nombre: 'María García', edad: 30}),
       (ahmed:Persona {nombre: 'Ahmed Khan', edad: 35}),
       (sophie:Persona {nombre: 'Sophie Müller', edad: 28}),
       (li:Persona {nombre: 'Li Wei', edad: 40}),
       (ana:Persona {nombre: 'Ana Silva', edad: 33}),
       (pierre:Persona {nombre: 'Pierre Dupont', edad: 50}),
       (elena:Persona {nombre: 'Elena Ivanova', edad: 29}),
       (carlos:Persona {nombre: 'Carlos Fernandez', edad: 42}),
       (mei:Persona {nombre: 'Mei Chen', edad: 37});

CREATE (:Ciudad {nombre: 'Nueva York'}),
       (:Ciudad {nombre: 'Londres'}),
       (:Ciudad {nombre: 'Tokio'}),
       (:Ciudad {nombre: 'París'}),
       (:Ciudad {nombre: 'Berlín'}),
       (:Ciudad {nombre: 'Ciudad de México'}),
       (:Ciudad {nombre: 'Pekín'}),
       (:Ciudad {nombre: 'Moscú'}),
       (:Ciudad {nombre: 'Sídney'}),
       (:Ciudad {nombre: 'Roma'});

CREATE (:Pais {nombre: 'Estados Unidos'}),
       (:Pais {nombre: 'Reino Unido'}),
       (:Pais {nombre: 'Japón'}),
       (:Pais {nombre: 'Francia'}),
       (:Pais {nombre: 'Alemania'}),
       (:Pais {nombre: 'México'}),
       (:Pais {nombre: 'China'}),
       (:Pais {nombre: 'Rusia'}),
       (:Pais {nombre: 'Australia'}),
       (:Pais {nombre: 'Italia'});
Establecer relaciones entre personas y ciudades (residencia):
MATCH (p1:Persona {nombre: 'John Smith'}),(c1:Ciudad {nombre: 'Nueva York'}),
      (p2:Persona {nombre: 'María García'}),(c2:Ciudad {nombre: 'Londres'}),
      (p3:Persona {nombre: 'Ahmed Khan'}),(c3:Ciudad {nombre: 'Tokio'}),
      (p4:Persona {nombre: 'Sophie Müller'}),(c4:Ciudad {nombre: 'París'}),
      (p5:Persona {nombre: 'Li Wei'}),(c5:Ciudad {nombre: 'Berlín'}),
      (p6:Persona {nombre: 'Ana Silva'}),(c6:Ciudad {nombre: 'Ciudad de México'}),
      (p7:Persona {nombre: 'Pierre Dupont'}),(c7:Ciudad {nombre: 'Pekín'}),
      (p8:Persona {nombre: 'Elena Ivanova'}),(c8:Ciudad {nombre: 'Moscú'}),
      (p9:Persona {nombre: 'Carlos Fernandez'}),(c9:Ciudad {nombre: 'Sídney'}),
      (p10:Persona {nombre: 'Mei Chen'}),(c10:Ciudad {nombre: 'Roma'})
CREATE (p1)-[:RESIDE_EN]->(c1), (p2)-[:RESIDE_EN]->(c2),(p3)-[:RESIDE_EN]->(c3),(p4)-[:RESIDE_EN]->(c4),
(p5)-[:RESIDE_EN]->(c5),(p6)-[:RESIDE_EN]->(c6),(p7)-[:RESIDE_EN]->(c7),(p8)-[:RESIDE_EN]->(c8),
(p9)-[:RESIDE_EN]->(c9),(p10)-[:RESIDE_EN]->(c10);

Establecer relaciones entre ciudades y países:
MATCH (c1:Ciudad {nombre: 'Nueva York'}),(p1:Pais {nombre: 'Estados Unidos'}),
      (c2:Ciudad {nombre: 'Londres'}),(p2:Pais {nombre: 'Reino Unido'}),
      (c3:Ciudad {nombre: 'Tokio'}),(p3:Pais {nombre: 'Japón'}),
      (c4:Ciudad {nombre: 'París'}),(p4:Pais {nombre: 'Francia'}),
      (c5:Ciudad {nombre: 'Berlín'}),(p5:Pais {nombre: 'Alemania'}),
      (c6:Ciudad {nombre: 'Ciudad de México'}),(p6:Pais {nombre: 'México'}),
      (c7:Ciudad {nombre: 'Pekín'}),(p7:Pais {nombre: 'China'}),
      (c8:Ciudad {nombre: 'Moscú'}),(p8:Pais {nombre: 'Rusia'}),
      (c9:Ciudad {nombre: 'Sídney'}),(p9:Pais {nombre: 'Australia'}),
      (c10:Ciudad {nombre: 'Roma'}),(p10:Pais {nombre: 'Italia'})
CREATE (c1)-[:ESTA_EN]->(p1),(c2)-[:ESTA_EN]->(p2),(c3)-[:ESTA_EN]->(p3),(c4)-[:ESTA_EN]->(p4),
(c5)-[:ESTA_EN]->(p5),(c6)-[:ESTA_EN]->(p6),(c7)-[:ESTA_EN]->(p7),(c8)-[:ESTA_EN]->(p8),
(c9)-[:ESTA_EN]->(p9),(c10)-[:ESTA_EN]->(p10);

Establecer relaciones entre personas:
MATCH (p1:Persona {nombre: 'John Smith'}),(p2:Persona {nombre: 'María García'}),(p3:Persona {nombre: 'Ahmed Khan'}),(p4:Persona {nombre: 'Sophie Müller'}),(p5:Persona {nombre: 'Li Wei'}),(p6:Persona {nombre: 'Ana Silva'}),(p7:Persona {nombre: 'Pierre Dupont'}),(p8:Persona {nombre: 'Elena Ivanova'}),(p9:Persona {nombre: 'Carlos Fernandez'}),(p10:Persona {nombre: 'Mei Chen'})
CREATE (p1)-[:AMIGO_DE]->(p2), (p2)-[: AMIGO_DE]->(p1),
(p2)-[:AMIGO_DE]->(p3),(p3)-[: AMIGO_DE]->(p2),
(p4)-[:AMIGO_DE]->(p5),(p5)-[:RESIDE_EN]->(p4),
(p4)-[:AMIGO_DE]->(p6),(p6)-[:RESIDE_EN]->(p4),
(p5)-[:AMIGO_DE]->(p6),(p6)-[:AMIGO_DE]->(p5),
(p7)-[:AMIGO_DE]->(p8),(p8)-[:AMIGO_DE]->(p7),
(p7)-[:AMIGO_DE]->(p9),(p9)-[:AMIGO_DE]->(p7),
(p9)-[:AMIGO_DE]->(p10),(p10)-[:AMIGO_DE]->(p9),
(p1)-[:AMIGO_DE]->(p10),(p10)-[:AMIGO_DE]->(p1);


2. Consultas Básicas:
   - Encuentra todas las personas en la base de datos.
MATCH (p:Persona) RETURN p;

   - Encuentra todas las ciudades en la base de datos.
MATCH (c:Ciudad) RETURN c;

   - Encuentra todas las relaciones de residencia en la base de datos.
MATCH ()-[r:RESIDE_EN]->() RETURN r;

3. Filtrado y Coincidencia:
   - Encuentra todas las personas mayores de 30 años que viven en un país específico.
MATCH (p:Persona)-[:RESIDE_EN]->(:Ciudad)-[:ESTA_EN]->(:Pais {nombre: 'Alemania'})
WHERE p.edad > 30
RETURN p;

   - Encuentra todas las ciudades en un país específico.
MATCH (c:Ciudad)-[:ESTA_EN]->(:Pais {nombre: 'Japón'}) RETURN c;

   - Encuentra todas las personas llamadas "Juan" que viven en ciudades con más de 1 millón de habitantes.
MATCH (p:Persona {nombre: 'Juan'})-[:RESIDE_EN]->(c:Ciudad) WHERE c.poblacion > 1000000 RETURN p;

4. Patrones de Búsqueda:
   - Encuentra todas las personas que viven en la misma ciudad.
MATCH (p1:Persona)-[:RESIDE_EN]->(c:Ciudad)<-[:RESIDE_EN]-(p2:Persona) RETURN p1, p2;

   - Encuentra todas las personas que viven en ciudades del mismo país.
MATCH (p1:Persona)-[:RESIDE_EN]->(:Ciudad)-[:ESTA_EN]->(pais:Pais)<-[:ESTA_EN]-(:Ciudad)<-[:RESIDE_EN]-(p2:Persona) RETURN p1, p2;

   - Encuentra el país con la mayor población de personas mayores de 40 años.
MATCH p=shortestPath((a:Persona)-[:RESIDE_EN*]-(b:Persona)) WHERE a.nombre = 'Juan' AND b.nombre = 'Pedro' RETURN p;

5. Agregación y Ordenamiento:
   - Encuentra la persona más joven en la base de datos.
MATCH (p:Persona) RETURN p ORDER BY p.edad ASC LIMIT 1;

   - Encuentra la ciudad con más residentes.
MATCH (c:Ciudad)<-[:RESIDE_EN]-() RETURN c, COUNT(*) AS num_residentes ORDER BY num_residentes DESC LIMIT 1;

   - Encuentra el país con la mayor cantidad de ciudades.
MATCH (pais:Pais)<-[:ESTA_EN]-(:Ciudad) RETURN pais, COUNT(*) AS num_ciudades ORDER BY num_ciudades DESC LIMIT 1;

6. Modificación de Datos:
   - Agrega una nueva ciudad y país a la base de datos con residentes existentes.
CREATE (:Ciudad {nombre: 'Buenos Aires'}),
       (:Pais {nombre: 'Argentina'});

MATCH (persona:Persona {nombre: 'John Smith'}), (ciudad:Ciudad {nombre: 'Buenos Aires'})
CREATE (persona)-[:RESIDE_EN]->(ciudad);

   - Crea una nueva relación de residencia entre una persona existente y una ciudad existente.
MATCH (persona:Persona {nombre: 'María García'}), (ciudad:Ciudad {nombre: 'Londres'})
CREATE (persona)-[:RESIDE_EN]->(ciudad);

   - Modifica la población de una ciudad.
MATCH (ciudad:Ciudad {nombre: 'Buenos Aires'})
SET ciudad.poblacion = 3000000;

7. Consultas Avanzadas:
   - Encuentra el país con la mayor cantidad de personas menores de 30 años.
MATCH (pais:Pais)<-[:ESTA_EN]-(:Ciudad)<-[:RESIDE_EN]-(p:Persona) 
WHERE p.edad < 30 
RETURN pais, COUNT(*) AS num_jovenes ORDER BY num_jovenes DESC LIMIT 1;

   - Encuentra si existe alguna cadena de residencia entre personas de diferentes países.
MATCH p=(:Persona)-[:RESIDE_EN*]->() RETURN DISTINCT p LIMIT 1;

   - Encuentra todas las personas que tienen conexiones de residencia en al menos tres ciudades diferentes.
MATCH (persona:Persona)-[:RESIDE_EN]->(ciudad:Ciudad)
WITH persona, COUNT(DISTINCT ciudad) AS num_ciudades
WHERE num_ciudades >= 3
RETURN persona;

8. Patrones de Recomendación:
   - Sugiere ciudades potenciales para vivir a una persona específica basada en las ciudades donde viven sus amigos.
MATCH (persona:Persona {nombre: 'Elena Ivanova'})-[:AMIGO_DE]->(amigo)-[:RESIDE_EN]->(ciudad)
WITH ciudad, COUNT(DISTINCT amigo) AS numAmigos
ORDER BY numAmigos DESC
RETURN ciudad.nombre AS ciudad, numAmigos

   - Sugiere países potenciales para visitar a una persona específica basada en los países donde residen sus amigos.
MATCH (:Persona {nombre: 'Ahmed Khan'})-[:AMIGO_DE]->(amigo)-[:RESIDE_EN]->(ciudad)
RETURN ciudad.nombre AS Ciudad, COUNT(*) AS AmigosEnCiudad
ORDER BY AmigosEnCiudad DESC;

9. Consultas de Rendimiento:
    - Analiza y optimiza consultas que podrían tener un rendimiento lento en grandes conjuntos de datos.
Teórica
    - Utiliza índices para mejorar el rendimiento de ciertas consultas, por ejemplo, para buscar personas por su nombre o edad.
CREATE INDEX FOR (p:Persona) ON (p.nombre);
CREATE INDEX FOR (p:Persona) ON(p.edad);
CREATE INDEX FOR (c:Ciudad) ON (c.nombre);
CREATE INDEX FOR (c:Ciudad) ON (c.poblacion);
CREATE INDEX FOR (p:Pais) ON (p.nombre);


10. Eliminación de Datos:
   - Elimina una ciudad específica de la base de datos y todas sus relaciones de residencia.
MATCH (c:Ciudad {nombre: 'Londres'}) DETACH DELETE c;

MATCH (ciudad:Ciudad {nombre: 'Londres'})<-[rel:RESIDE_EN]-(persona:Persona)
DELETE rel, ciudad;

   - Elimina todas las relaciones de residencia de personas menores de 25 años.
MATCH ()-[r:RESIDE_EN]-(p:Persona) 
WHERE p.edad < 25 
DELETE r;

   - Elimina todos los nodos y relaciones de la base de datos.
MATCH (n) DETACH DELETE n;

/////////////////REDIS/////////////////
ZADD peliculas_imdb 7.7 "The theory of everything"
ZADD peliculas_imdb 8.0 "The Imitation Game"
ZADD peliculas_imdb 8.3 "Amelie"
ZADD peliculas_imdb 9.3 "The Shawshank Redemption"
ZADD peliculas_imdb 9.2 "The Godfather"
ZADD peliculas_imdb 8.8 "Fight Club"
ZADD peliculas_imdb 8.7 "Matrix"
ZADD peliculas_imdb 7.8 "Titanic"
ZADD peliculas_imdb 8.1 "Jurassic Park"
ZADD peliculas_imdb 7.9 "ET"

Posteriormente, ejecuta los comandos que permitan obtener los siguientes resultados:
•	Todas las películas en orden creciente de acuerdo al score
ZRANGE peliculas_imdb 0 -1 WITHSCORES

•	Todas las películas en orden decreciente de acuerdo al score 
ZREVRANGE peliculas_imdb 0 -1 WITHSCORES

•	Las dos mejores películas junto a su puntaje
ZREVRANGE peliculas_imdb 0 1 WITHSCORES

•	En qué posición (decreciente) se encuentra la película “The Imitation Game” ZREVRANK peliculas_imdb "The Imitation Game"

•	Películas cuyo puntaje se encuentra entre 8 y 10

ZRANGEBYSCORE peliculas_imdb 8 10 WITHSCORES

•	Películas que tengan un puntaje menor que 8
ZRANGEBYSCORE peliculas_imdb -inf (8 WITHSCORES

 
PFADD Website1_HyperLogLog 122 100 123 122 200 219 315
PFADD Website2_HyperLogLog 111 356 678 999 514 167 908
PFADD Website3_HyperLogLog 234 567 789 235 908 210 217
PFADD Website4_HyperLogLog 777 111 345 098 786 908 100

Se requiere que almacenes los datos anteriores en la estructura más idónea, y posteriormente ejecutes los comandos que permitan responder a la siguiente interrogante:
•	Cantidad de usuarios únicos que visitaron cada uno de los sitios webs en el período analizado
PFCOUNT Website1_HyperLogLog
PFCOUNT Website2_HyperLogLog
PFCOUNT Website3_HyperLogLog
PFCOUNT Website4_HyperLogLog


/////////////////////MONGO //////////////////////
Crear la colección players

db.players.insertOne({name:'Luka Modric', height: 180, weight:143, dob: new Date
(1985,9,9,0,0), preferred_foot: 'right', hobbies:['Playing football','Watching TV
series','Swimming']});


Consultas y operaciones:

	Obtener todos los jugadores que tengan preferred_foot “left” y pesen más de 170 libras (weight > 170).
db.players.find({ $and: [{ preferred_foot: 'left' },{ weight: { $gt: 170 } }] })

	Documentos que no poseen el campo height.
db.players.find({ height: { $exists: false } })

	Jugadores con preferred_food igual a right, que tengan como hobbies Playing football o Video games o que pesen menos de 150 libras.
db.players.find({ $and: [{ preferred_foot: 'right' },{ $or:[{ hobbies: {$in: ['Playing football', 'Video games']} }, { weight: { $lt: 150 } }] } ] })

	Jugadores cuyo nombre comience con la letra S.
db.players.find({ name: { $regex: /^S/i } })

	Jugadores cuyo nombre termine con la letra i.
db.players.find({ name: { $regex: /i$/i } })

	Agregar a David Silva un hobbie 'natación' (ver push).
db.players.updateOne({ name: 'David Silva' },{ $push: { hobbies: 'natación' } })

	Se puede obtener todos los nombres de players (ver find)
db.players.find({}, { name: 1, _id: 0 })

	Listar los jugadores por altura descendente (ver sort)
db.players.find().sort({ height: -1 })

	Cuál es el número de documentos que cumplen peso de más de 180. (ver count)
db.players.find({ weight: { $gt: 180 } }).count()

	Cuantos jugadores hay por pierna preferida (ver unwind)
db.players.aggregate([{ $unwind: "$ preferred_foot " }, 
				{ $group: { _id: "$pierna_preferida", count: { $sum: 1 } }} ])
 


db.createCollection('bandas')


db.bandas.insertMany([
{nombre:'Ver K Bitch', genero: 'Instrumental', fecha_inscripcion: new Date(2018,0,20,0,0), discos: ['Planeta Esmeralda (2005)','Causalidades (2005)','Meridiano (2006)','Apichonados (2007)','Dios Agujero Negro (2008)'], barrio: 'Versalles', integrantes: 1},
{nombre:'Trotamundos', genero: 'Indie', fecha_inscripcion: new Date(2017,10,30,0,0), discos: 'Hecho Bolita (2014)', barrio: 'Villa Luro', integrantes: 4},
{nombre:'Efecto Alfons', genero: 'Rock', estilo: 'Power Trío', fecha_inscripcion: new Date(2017,10,27,0,0), discos: 'Efecto Alfons (2000)', barrio: 'Barracas', integrantes: 3},
{nombre:'Marcelo Giullitti', genero: 'Solista', fecha_inscripcion: new Date(2017,10,26,0,0), barrio: 'Agronomia', integrantes: 1},
{nombre:'Afterlife', genero: 'Rock', estilo: 'Rock Alternativo', fecha_inscripcion: new Date(2017,10,14,0,0), barrio: 'Balvanera', integrantes: 5},
{nombre:'Virginia Ferreyra', genero: 'Rock', estilo: 'Rock Pop', fecha_inscripcion: new Date(2017,10,14,0,0), barrio: 'Villa del Parque', integrantes: 1},
{nombre:'LMV', genero: 'Pop', fecha_inscripcion: new Date(2017,10,10,0,0), barrio: 'La Lucila', integrantes: 6},
{nombre:'Efecto Alfons', genero: 'Rock', estilo: 'Power Trío', fecha_inscripcion: new Date(2017,10,6,0,0), discos: 'Efecto Alfons (1995)', barrio: 'Barracas', integrantes: 3},
{nombre:'Tantas Preguntas', genero: 'Punk', estilo: 'Punk Rock', fecha_inscripcion: new Date(2017,9,27,0,0), discos: ['Libre Albedrio (2006)','Despues de Todo (2006)'], barrio: 'Moreno', integrantes: 3},
{nombre:'Tal Vez de Paso', genero: 'Pop', estilo: 'Pop Rock', fecha_inscripcion: new Date(2017,9,26,0,0), barrio: 'Puerto Madero', integrantes: 4},
{nombre:'La Surtida Folck', genero: 'Folklore', fecha_inscripcion: new Date(2017,9,25,0,0), barrio: 'Berazategui', integrantes: 7},
{nombre:'Jaydee M', genero: ['Hip Hop','Rap'], fecha_inscripcion: new Date(2017,9,24,0,0), barrio: 'Barracas', integrantes: 1}
])


	Todas las bandas en orden creciente de acuerdo al número de integrantes
db.bandas.find().sort({ integrantes: 1 })

	Las dos bandas con mayor número de integrantes
db.bandas.find().sort({ integrantes: -1 }).limit(2)

	Suma un integrante más a todas las bandas
db.bandas.updateMany({}, { $inc: { integrantes: 1 } })

	Bandas cuyo género es Rock
db.bandas.find({ genero: 'Rock' })

	Bandas que han lanzado disco en el año 2006
db.bandas.find({ discos: { $regex: '\(2006\)' } })

	Cantidad de Bandas en el barrio Barracas
db.bandas.find({ barrio: 'Barracas' }).count()


/////////////CASSANDR/////////////////////////////////////////////////////////
Tabla usuarios
CREATE TABLE usuarios (
    id UUID PRIMARY KEY,
    nombre TEXT,
    email TEXT,
    password TEXT,
    productos_publicados MAP<UUID, TIMESTAMP>,      -- Mapa de producto_id a fecha
    productos_comentados LIST<FROZEN<tuple<UUID, TIMESTAMP, TEXT>>>,  -- Lista de tuplas (producto_id, fecha, comentario)
    productos_calificados LIST<FROZEN<tuple<UUID, TIMESTAMP, INT>>>   -- Lista de tuplas (producto_id, fecha, calificación)
);

Tabla productos
CREATE TABLE productos (
    id UUID PRIMARY KEY,
    titulo TEXT,
    tags TEXT,
    descripcion TEXT,
    categorias SET<TEXT>    -- Conjunto de nombres de categorías
);

Tabla categorias
CREATE TABLE categorias (
    nombre TEXT PRIMARY KEY,
    fecha_creacion TIMESTAMP,
    descripcion TEXT
);

Insertar un usuario
INSERT INTO usuarios (id, nombre, email, password) 
VALUES (uuid(), 'Juan Perez', 'juan.perez@example.com', 'password123');

Insertar un producto
INSERT INTO productos (id, titulo, tags, descripcion, categorias) 
VALUES (uuid(), 'El gran libro', 'libros,educacion', 'Un libro educativo', {'Libros'});

Insertar una categoría
INSERT INTO categorias (nombre, fecha_creacion, descripcion) 
VALUES ('Libros', toTimestamp(now()), 'Categoría de Libros');



Publicar un producto
UPDATE usuarios 
SET productos_publicados = productos_publicados + {<producto_id> : toTimestamp(now())}
WHERE id = <usuario_id>;

Comentar un producto
UPDATE usuarios 
SET productos_comentados = productos_comentados + [(<producto_id>, toTimestamp(now()), 'Excelente libro')]
WHERE id = <usuario_id>;

Calificar un producto
UPDATE usuarios 
SET productos_calificados = productos_calificados + [(<producto_id>, toTimestamp(now()), 5)]
WHERE id = <usuario_id>;

Añadir una categoría a un producto
UPDATE productos 
SET categorias = categorias + {'Libros'}
WHERE id = <producto_id>;


1. Obtener la información de usuario por ID de usuario
SELECT * FROM usuarios WHERE id = <usuario_id>;

2. Obtener la información de producto por ID de producto
SELECT * FROM productos WHERE id = <producto_id>;

3. Obtener todos los productos publicados por un usuario particular (nombre usuario)
SELECT id FROM usuarios WHERE nombre = 'Juan Perez';
SELECT productos_publicados FROM usuarios WHERE id = <usuario_id>;
SELECT * FROM productos WHERE id IN (<producto_id1>, <producto_id2>, ...);

4. Obtener todos los usuarios que comentaron un producto particular (nombre producto)
SELECT id FROM productos WHERE titulo = 'El gran libro';
SELECT id, nombre, productos_comentados FROM usuarios;

5. Obtener que producto calificó un usuario 'X' por fecha
SELECT id FROM usuarios WHERE nombre = 'X';
SELECT productos_calificados FROM usuarios WHERE id = <usuario_id>;
SELECT * FROM productos WHERE id IN (<producto_id1>, <producto_id2>, ...);


Esta es solo una forma de resolver el ejercicio, quizás la más compleja.
Otra manera que pueden probar de hacer, y que a pesar de ser más larga la creación y carga es más sencilla a la hora de realizar consultas. La idea de esta segunda manera de resolver el ejercicio es crear tablas para cada tipo de relación:
•	usuario_publica_producto
•	usuario_comenta_producto
•	usuario_califica_producto
•	producto_pertenece_categoria
