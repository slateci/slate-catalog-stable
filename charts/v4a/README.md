# v4a


[Varnish](https://varnish-cache.org/intro/) is a caching HTTP reverse proxy.  It caches responses from a HTTP server and then serves 
that to clients.  Varnish for ATLAS (v4a) creates a Varnish instance that is configured to proxy [Frontier](http://frontier.cern.ch/) requests.  


**NOTE**:
For this to work a node must be labeled with "varnish: frontier-slate"
Node must have an IP visible from all the worker nodes (WNs) that will use it.
Server will be accessible at `http://<IP>:6081`.

## Configuration


| Parameter | Default     | Description |
|-----------|-------------|-------------|
| Site | None | Name of the site the instance is associated with. This variable is used in monitoring. *REQUIRED* | 
| acl | None | This is a semicolumn separated list of IP ranges of the WNs allowed to use this proxy. *REQUIRED* | 
| varnish_mem | 24G | Memory that varnish will use, should be ~20% smaller than the value given in _resources.requests.memory_. | 
| varnish_transient_mem | 1G | Maximum size of individual objects that are not being streamed | 
| monitoring.es | true | Send data to elasticsearch |
| monitoring.snmp | true | Allow SNMP monitoring, requires port 3401 to be accessible |
| ports.varnish_port | 6081 | Port that varnish will listen on |
| resources |  See below | memory and cpu resources for the varnish pod |

The default for the resources is :
``` yaml
    resources:
      requests:
        cpu: "4"
        memory: "33Gi"
      limits:
        cpu: "48"
        memory: "48Gi"
    ```

