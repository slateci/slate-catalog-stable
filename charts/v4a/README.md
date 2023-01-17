# v4a

This application v4a (Varnish for ATLAS) creates a Varnish web reverse proxy and configures it in a way needed to proxy Frontier requests.

**NOTE**:
For this to work a node must be labeled with "varnish: frontier-slate"
Node must have an IP visible from all the WNs that will use it.
Server will be accessible at `http://<IP>:6081`.

## Configuration

Values description:

* _Site_:  This variable is used in monitoring. REQUIRED
* _acl_: This is a semicolumn separated list of IP ranges of the WNs allowed to use this proxy. REQUIRED
* varnish_mem: "24G" - should be ~20% smaller than the value given in _resources.requests.memory_.
* varnish_transient_mem: "1G" - max size of individual objects if not streaming content.
* monitoring.es - default is true
* monitoring.snmp - default is true and it requires one more port free (3401)
* ports.varnish_port - default is 6081 but can be changed
* resources - the default is:

    ``` yaml
    resources:
      requests:
        cpu: "4"
        memory: "33Gi"
      limits:
        cpu: "48"
        memory: "48Gi"
    ```
