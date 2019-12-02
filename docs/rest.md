Amazon Neptune proporciona un endpoint HTTPS para consultas de Gremlin. La interfaz REST es compatible con Gremlin versión 3.4.1.

Los siguientes ejemplos usan ***curl*** para enviar una consulta Gremlin a través de HTTP ***POST***. La consulta se envía en formato JSON en el cuerpo del post. Antes de lanzar cada uno de los comandos, sustituya ***su-endpoint-neptune*** por el valor de ***DBClusterEndpoint***.

1. Dentro de su instancia EC2 ejecute los comandos. Si aún se encuentra dentro de la consola de Gremlin, ejecute el siguiente comando para salir:

```
:exit
```

2. Muestra algunos de los vértices (límite 4):

```
curl -X POST -d '{"gremlin":"g.V().limit(4)"}' https://su-endpoint-neptune:8182/gremlin
```

3. Muestra algunos de los bordes (límite 5):

```
curl -X POST -d '{"gremlin":"g.E().limit(5)"}' https://su-endpoint-neptune:8182/gremlin

```


También puede enviar consultas a través de solicitudes HTTP ***GET***:

4. Devuelve solo los vértices que son juegos:

```
curl -G "https://su-endpoint-neptune:8182?gremlin=g.V().hasLabel('game')"

```

5. Devuelve solo los vértices que son jugadores:

```
curl -G "https://su-endpoint-neptune:8182?gremlin=g.V().hasLabel('person')"

```

6. ¿Qué juegos le gustan al jugador skywalker123?

```
curl -G "https://su-endpoint-neptune:8182?gremlin=g.V().has('GamerAlias','skywalker123').as('gamer').out('likes')"
```
