# Actividad02-Bactracking-grafo-dirigido-Tomas-Bravo-Quinteroo
# PROGIIIIG1-ACT02  
  
## INTEGRANTES  
- Tomás Bravo Quintero
  
## HECHOS  
  
conexion(vancouver, edmonton, 16).  
conexion(vancouver, calgary, 13).  
conexion(edmonton, saskatoon, 12).  
conexion(saskatoon, winnipeg, 20).  
conexion(saskatoon, calgary, 9).  
conexion(calgary, regina, 14).

## Reglas
## Verificar si hay conexión directa entre dos ciudades.
hay_conexion_directa(Ciudad1, Ciudad2) :-
````
conexion(Ciudad1, Ciudad2, _).
````

## Obtener conexiones de cada ciudad
conexiones_de(Ciudad, ConexionesDesde, ConexionesHacia) :-
```
findall([Ciudad, Destino, Costo], conexion(Ciudad, Destino, Costo), ConexionesDesde),

findall([Origen, Ciudad, Costo], conexion(Origen, Ciudad, Costo), ConexionesHacia).
```

## Hallar el camino entre 2 ciudades con terminales

camino(Inicio, Fin, Camino, Costo) :-
```
camino(Inicio, Fin, [Inicio], Camino, 0, Costo).
```
camino(Fin, Fin, _, [Fin], Costo, Costo).

camino(Actual, Fin, Visitados, [Actual|Camino], CostoActual, CostoTotal) :-
```
conexion(Actual, Siguiente, CostoArista),

\+ member(Siguiente, Visitados),

NuevoCosto is CostoActual + CostoArista,

camino(Siguiente, Fin, [Siguiente|Visitados], Camino, NuevoCosto, CostoTotal).

```
## Determinar si un nodo tiene aristas.
tiene_aristas(Nodo) :-
```
conexion(Nodo, _, _).  % Nodo con al menos una arista saliente

```
tiene_aristas(Nodo) :-
```
conexion(_, Nodo, _).  % Nodo con al menos una arista entrante

```
## Hallar el precio a viajar de X a Z pasando por Y.
costo_via(X, Y, Z, CostoTotal) :-
```
conexion(X, Y, Costo1),

conexion(Y, Z, Costo2),

CostoTotal is Costo1 + Costo2.
```
## Verificar si se puede viajar de una ciudad a otra
puede_viajar(Inicio, Fin, Camino, Costo) :-
```
camino(Inicio, Fin, Camino, Costo).
```

## Ver si hay un camino entre 2  ciudades
existe_camino(Inicio, Fin) :-
```
puede_viajar(Inicio, Fin, _, _), !.
```
existe_camino(_, _) :-
```
false.
```

## Posibles preguntas

## Existe una conexión entre Saskatoon y Vancouver?

No existe conexión ni directa ni mediante otras rutas.

<img width="1912" height="1126" alt="image" src="https://github.com/user-attachments/assets/06a60903-fcf1-4847-9b21-32b43aadfaab" />


## Con qué nodos está conectado Regina y cual es el costo de cada conexión?

Regina esta conectada con:

Regina sale a Winnipeg, costando 4.
Regina sale a Saskatoon, costando 7.

Calgary sale a Regina, costando 14.

<img width="1912" height="1012" alt="image" src="https://github.com/user-attachments/assets/d4407e5b-32b7-493c-a3d2-0739792c6d4a" />

## Construir una regla para determinar si un nodo tiene aristas.

Todos tienen aristas, ya sean entrantes o salientes.

<img width="1910" height="1067" alt="image" src="https://github.com/user-attachments/assets/6f8904ad-500b-4653-981e-5d764af679a7" />


## Construir una regla para determinar cuál es el costo para ir de un nodo X a un Z pasando por Y.

Sale costo cuando hay conexiones entre las 3 ciudades, en caso de que no
haya conexión o la dirección del grafo no sea válida va a dar como salida false.

<img width="1892" height="1058" alt="image" src="https://github.com/user-attachments/assets/784cc4cd-070d-4f6d-8ded-a6740035b96a" />

## Es posible viajar desde Edmonton a Calgary?

<img width="1918" height="1071" alt="image" src="https://github.com/user-attachments/assets/48abf131-24e6-4074-8a88-6ea9ef728cea" />

## Función existe camino

Nos permite saber si hay conexión entre ciudades, ya sea directa o pasando por varias ciudades, solo devolviendo true o false sea el caso.

<img width="1907" height="1072" alt="image" src="https://github.com/user-attachments/assets/aa964702-bdd1-40d5-a098-49f7e42a8045" />




