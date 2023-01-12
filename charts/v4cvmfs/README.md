# v4cvmfs

This application v4a (Varnish for ATLAS) creates a Varnish web reverse proxy and configures it in a way needed to proxy CVMFS requests.

**NOTE**:
For this to work a node must be labeled with "varnish: cvmfs"
Node must have an IP visible from all the WNs that will use it.
Server will be accessible at `http://<IP>:6081`.

## Configuration

Values description:

* _Site_:  This variable is used in monitoring. REQUIRED
* _acl_: This is a semicolumn separated list of IP ranges of the WNs allowed to use this proxy. REQUIRED
* backends: the default list is good for any US site. Should be of the form:

    ``` yaml
    backends:
      - name: fermilab_2
        host: 2620:6a:0:8421::244
        port: 8000
      - name: bnl_1
        host: 192.12.15.180
        port: 8000
    ```

* varnish_size: "28G" - should be ~20% smaller than the value given in _resources.requests.memory_.
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
