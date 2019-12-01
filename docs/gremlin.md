1. Consulta para un vértice particular (jugador):

```
g.V().hasId('Luke').valueMap()
```
> ==>{GamerAlias=[skywalker123]}

```
g.V().has("GamerAlias","skywalker123").valueMap()
```
==>{GamerAlias=[skywalker123]}

```
g.V().has('GamerAlias','skywalker123')
```
==>v[Luke]

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
==>v[Luke]
==>v[Emma]
==>v[Lina]
==>v[Mike]
