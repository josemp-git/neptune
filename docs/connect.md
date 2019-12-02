1. Estando conectado en la instancia de EC2, ejecute el siguiente comando y asegúrese que el valor de ***hosts*** corresponda a su cluster de Neptune (DBClusterEndpoint) :

```
cat ~/ apache-tinkerpop-gremlin-console-3.4.1/conf/neptune-remote.yaml
```

2. Ejecute los siguiente comando para iniciar la consola de Gremlin:

```
cd ~/apache-tinkerpop-gremlin-console-3.4.1
```

```
bin/gremlin.sh
```

Deberá ver la siguiente pantalla:

![Gremlin Console](images/gremlinconsole.png)

3. En el prompt de gremlin>, ejecute el siguiente comando para conectarse a la instancia de Neptune:

```
:remote connect tinkerpop.server conf/neptune-remote.yaml
```

4. En el prompt de gremlin>, ejecute el siguiente comando para cambiar a modo remoto. Esto envía todas las consultas de Gremlin a la conexión remota.

```
:remote console
```

5. Ingrese lo siguiente para enviar su primera consulta:

```
g.V().limit(1)
```

6. ***Opcional***: si requiere salir de la consola de Gremlin, ejecute el siguiente comando en el prompt:

```
:exit
```