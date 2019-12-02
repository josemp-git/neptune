En este módulo, usted recorrerá las preferencias de juegos de consola entre un pequeño conjunto de jugadores y juegos. Explorará los puntos en común, las preferencias y hará posibles recomendaciones de juegos. Estas consultas tienen el propósito de aprender Gremlin y Amazon Neptune.

![Graph](images/graph.jpg)

1. Consulta para un vértice particular (jugador):

```
g.V().hasId('Luke').valueMap()
```
> ==>{GamerAlias=[skywalker123]}

```
g.V().has("GamerAlias","skywalker123").valueMap()
```
> ==>{GamerAlias=[skywalker123]}

```
g.V().has('GamerAlias','skywalker123')
```
> ==>v[Luke]

2. Muestra algunos de los bordes (límite 5):

```
g.E().limit(5)
```

> ==>e[e25][Luke-likes->SuperMarioOdyssey]

> ==>e[e26][Mike-likes->SuperMarioOdyssey]

> ==>e[e8][Mike-likes->CallOfDutyBO4]

> ==>e[e1][Luke-likes->HorizonZeroDawn]

> ==>e[e9][Mike-likes->GranTurismoSport]

3. Muestra algunos de los vértices (límite 4):

```
g.V().limit(4)
```
> ==>v[Luke]

> ==>v[Emma]

> ==>v[Lina]

> ==>v[Mike]

4. Cuente la centralidad en grados de los bordes entrantes para cada vértice:

```
g.V().group().by().by(inE().count())
```

> ==>{v[HorizonZeroDawn]=2, v[Luke]=0, v[ARMS]=2, v[Ratchet&Clank]=3, v[SuperMarioOdyssey]=3, v[GravityRush]=2, v[CallOfDutyBO4]=1, v[MarioKart8]=3, v[Fifa18]=1, v[Nioh]=1, v[Mike]=0, v[Knack]=2, v[Lina]=0, v[TombRaider]=2, v[GranTurismoSport]=2, v[Emma]=0}

5. Cuente la centralidad de los bordes salientes de cada vértice:

```
g.V().group().by().by(outE().count())
```
> ==>{v[HorizonZeroDawn]=0, v[Luke]=8, v[ARMS]=0, v[Ratchet&Clank]=0, v[SuperMarioOdyssey]=0, v[GravityRush]=0, v[CallOfDutyBO4]=0, v[MarioKart8]=0, v[Fifa18]=0, v[Nioh]=0, v[Mike]=8, v[Knack]=0, v[Lina]=6, v[TombRaider]=0, v[GranTurismoSport]=0, v[Emma]=2}

6. Cuente la centralidad del grado de salida de los bordes salientes de cada vértice por orden de grado:

```
g.V().project("v","degree").by().by(bothE().count()).order().by(select("degree"), decr)
```

> ==>{v=v[Luke], degree=9}

> ==>{v=v[Mike], degree=9}

> ==>{v=v[Lina], degree=6}

> ==>{v=v[Ratchet&Clank], degree=3}

> ==>{v=v[SuperMarioOdyssey], degree=3}

> ==>{v=v[MarioKart8], degree=3}

> ==>{v=v[Emma], degree=2}

> ==>{v=v[HorizonZeroDawn], degree=2}

> ==>{v=v[GranTurismoSport], degree=2}

> ==>{v=v[GravityRush], degree=2}

> ==>{v=v[TombRaider], degree=2}

> ==>{v=v[Knack], degree=2}

> ==>{v=v[ARMS], degree=2}

> ==>{v=v[Mario+Rabbids], degree=2}

> ==>{v=v[Fifa18], degree=1}

> ==>{v=v[Nioh], degree=1}

> ==>{v=v[CallOfDutyBO4], degree=1}

7. Devuelve solo los vértices que son juegos:

```
g.V().hasLabel('game')
```

> ==>v[Mario+Rabbids]

> ==>v[ARMS]

> ==>v[HorizonZeroDawn]

> ==>v[GranTurismoSport]

> ==>v[Ratchet&Clank]

> ==>v[Fifa18]

> ==>v[GravityRush]

> ==>v[Nioh]

> ==>v[TombRaider]

> ==>v[CallOfDutyBO4]

> ==>v[Knack]

> ==>v[SuperMarioOdyssey]

> ==>v[MarioKart8]

8. Devuelve solo los vértices que son jugadores:

```
g.V().hasLabel('person')
```
> ==>v[Luke]

> ==>v[Emma]

> ==>v[Lina]

> ==>v[Mike]

9. Recuento de juegos agrupados por género de juego:

```
g.V().hasLabel('game').groupCount().by("GameGenre")
```
> ==>{Shooter=2, Action=3, Adventure=5, Racing=2, Sports=1}

10. Recuento de juegos agrupados por desarrollador:

```
g.V().hasLabel('game').groupCount().by("Developer")
```
> ==>{Activision=1, Nintendo=3, Square Enix=1, Guerrilla Games=1, Sony Interactive Entertainment=2, Insomniac Games=1, Electronic Arts=1, Project Siren=1, Ubisoft=1, Team Ninja=1}

11. Recuento de juegos agrupados por plataforma:

```
g.V().hasLabel('game').groupCount().by("Platform")
```
> ==>{PS4=9, Switch=4}

12. ¿Cuál es la calificación promedio ponderada de MarioKart8?

```
g.V().hasLabel('game').has('GameTitle','MarioKart8').inE('likes').values('weight').mean()
```
> ==>0.6333333333333334

13. ¿Qué juegos le gustan a skywalker123?

```
g.V().has('GamerAlias','skywalker123').as('gamer').out('likes')
```
> ==>v[HorizonZeroDawn]

> ==>v[GranTurismoSport]

> ==>v[Ratchet&Clank]

> ==>v[Fifa18]

> ==>v[GravityRush]

> ==>v[SuperMarioOdyssey]

> ==>v[MarioKart8]

> ==>v[ARMS]

> ==>v[Mario+Rabbids]

14. ¿Qué juegos le gusta a skywalker123 usar el peso (mayor que)?

```
g.V().has('GamerAlias','skywalker123').outE("likes").has('weight', P.gt(0.7f))
```
> ==>e[e17][Luke-likes->Mario+Rabbids]

> ==>e[e3][Luke-likes->Ratchet&Clank]

15. ¿Qué juegos le gusta a skywalker123 usar el peso (menos que)?

```
g.V().has('GamerAlias','skywalker123').outE("likes").has('weight', P.lt(0.5f))
```
> ==>e[e1][Luke-likes->HorizonZeroDawn]

> ==>e[e2][Luke-likes->GranTurismoSport]

> ==>e[e4][Luke-likes->Fifa18]

> ==>e[e5][Luke-likes->GravityRush]

> ==>e[e21][Luke-likes->MarioKart8]

16. ¿A quién más le gustan los mismos juegos que al jugador skywalker123?

```
g.V().has('GamerAlias','skywalker123').out('likes').in('likes').dedup().values('GamerAlias')
```
> ==>forchinet

> ==>skywalker123

> ==>bringit32

> ==>smiles007

17. ¿A quién más le gustan estos juegos sin incluirse a uno mismo (skywalker123)?

```
g.V().has('GamerAlias','skywalker123').as('TargetGamer').out('likes').in('likes').where(neq('TargetGamer')).dedup().values('GamerAlias')
```
> ==>forchinet

> ==>bringit32

> ==>smiles007

18. ¿Cuáles son los otros títulos de juegos que les gustan a otros jugadores, que tienen en común?

```
g.V().has('GamerAlias','skywalker123').as('TargetGamer').out('likes').in('likes').where(neq('TargetGamer')).out('likes').dedup().values('GameTitle')
```
> ==>HorizonZeroDawn

> ==>GranTurismoSport

> ==>Nioh

> ==>TombRaider

> ==>CallOfDutyBO4

> ==>SuperMarioOdyssey

> ==>MarioKart8

> ==>ARMs

> ==>Mario+Rabbids

> ==>Ratchet&Clank

> ==>GravityRush

> ==>Knack

19. ¿Qué juegos podrían tener sentido recomendar a un jugador específico que actualmente no le gusta?

```
g.V().has('GamerAlias','skywalker123').as('TargetGamer').out('likes').aggregate('self').in('likes').where(neq('TargetGamer')).out('likes').where(without('self')).dedup().values('GameTitle')
```
> ==>Nioh

> ==>TombRaider

> ==>CallOfDutyBO4

> ==>Knack


