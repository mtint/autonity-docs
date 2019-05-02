Prometheus (optional)
=========================================

`Prometheus helm chart`_   deploy Prometheus_ monitoring system.

Configuration
~~~~~~~~~~~~~

* Configmap with server settings prometheus_configmap.yaml_
* Maps ``prometheus:`` in main chart values.yaml_


Deploy
~~~~~~

.. code:: bash

    helm install -n autonity-platform ./ --set global.prometheus.enabled=true

How is it works?
~~~~~~~~~~~~~~~~
* ``Autonity`` has internal metrics that described in `wiki article Metrics-and-Monitoring`_. It can be available through the `ipc` inside the pod
* Pod ``validator`` or ``observer`` has sidecar container `prometheus-exporter` that can connect to the `ipc` and expose prometheus metrics
* Prometheus-server can autodiscover it using `kubernetes service discovery based on annotation`_

.. _Prometheus: https://prometheus.io/docs/introduction/overview
.. _prometheus_configmap.yaml: https://github.com/clearmatics/autonity-helm/blob/master/templates/prometheus_configmap.yaml
.. _values.yaml: https://github.com/clearmatics/autonity-helm/blob/master/values.yaml
.. _Prometheus helm chart: https://github.com/helm/charts/tree/master/stable/prometheus
.. _wiki article Metrics-and-Monitoring: https://github.com/clearmatics/autonity/wiki/Metrics-and-Monitoring
.. _kubernetes service discovery based on annotation: https://prometheus.io/docs/prometheus/latest/configuration/configuration/#endpoints