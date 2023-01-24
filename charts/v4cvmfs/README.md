# v4cvmfs

[Varnish](https://varnish-cache.org/intro/) is a caching HTTP reverse proxy.  It caches responses from a HTTP server and then serves 
that to clients.  Varnish for CVMFS (v4cvmfs) creates a Varnish instance that is configured to proxy CVMFS requests.  It can be used as an 
alternative to [frontier squid](https://github.com/slateci/slate-catalog-stable/tree/master/charts/osg-frontier-squid). 

**NOTE**:
For this to work a node must be labeled with "varnish: cvmfs"
Node must have an IP visible to all the worker nodes (WNs) that will use it.
Server will be accessible at `http://<IP>:6081`.

## Configuration



| Parameter | Default     | Description |
|-----------|-------------|-------------|
| Site | None | Name of the site the instance is associated with. This variable is used in monitoring. *REQUIRED* | 
| acl | None | This is a semicolumn separated list of IP ranges of the WNs allowed to use this proxy. *REQUIRED* |
| backends | See below | Yaml with list of CVMFS servers | 
| varnish_mem | 24G | Memory that varnish will use, should be ~20% smaller than the value given in _resources.requests.memory_ (see below).  | 
| varnish_transient_mem | 1G | Maximum size of individual objects that are not being streamed | 
| monitoring.es | true | Send monitoring data to elasticsearch |
| monitoring.snmp | true | Allow SNMP monitoring, requires port 3401 to be accessible |
| ports.varnish_port | 6081 | Port that varnish will listen on |
| resources |  See below | memory and cpu resources for the varnish pod |


The default for the backends is :
``` yaml
    backends:
      - name: fermilab_2
        host: 2620:6a:0:8421::244
        port: 8000
      - name: bnl_1
        host: 192.12.15.180
        port: 8000
```

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
