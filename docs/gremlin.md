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

==>{v[HorizonZeroDawn]=2, v[Luke]=0, v[ARMS]=2, v[Ratchet&Clank]=3, v[SuperMarioOdyssey]=3, v[GravityRush]=2, v[CallOfDutyBO4]=1, v[MarioKart8]=3, v[Fifa18]=1, v[Nioh]=1, v[Mike]=0, v[Knack]=2, v[Lina]=0, v[TombRaider]=2, v[GranTurismoSport]=2, v[Emma]=0}
5.