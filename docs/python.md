1. Ejecute el siguiente comando para instalar el paquete gremlinpython en su instancia EC2:

```
sudo pip install gremlinpython
```

2. Ejecute el siguiente comando para guardar su código Python como ***gremlin.py***:

```
echo "from __future__  import print_function  # Python 2/3 compatibility

from gremlin_python import statics
from gremlin_python.structure.graph import Graph
from gremlin_python.process.graph_traversal import __
from gremlin_python.process.strategies import *
from gremlin_python.driver.driver_remote_connection import DriverRemoteConnection

graph = Graph()

remoteConn = DriverRemoteConnection('wss://neptunedbcluster-ckvkuf0ce2au.cluster-cixrzw8bfsbk.us-east-1.neptune.amazonaws.com:8182/gremlin','g')
g = graph.traversal().withRemote(remoteConn)

print(g.V().limit(5).toList())
remoteConn.close()" > gremlin.py
```

3. Ejecute el siguiente comando:

```
python gremlinexample.py
```

La consulta de Gremlin al final de este ejemplo devuelve los vértices (g.V (). Limit (5)) en una lista. Esta lista se imprime con la función de impresión estándar de Python.