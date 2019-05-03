Grafana (optional)
=========================================

`Grafana helm chart`_   deploy Grafana_ monitoring system.
Grafana dashboard used to show prometheus metrics and require prometheus subchart installed

Configuration
~~~~~~~~~~~~~

* Templates for dashboards stored in `./files/grafana/dashboards`_
* Map ``grafana:`` in main chart `values.yaml`_


Deploy
~~~~~~

.. code:: bash

    helm install -n autonity-platform ./ --set global.prometheus.enabled=true,global.grafana.enabled=true

Usage
~~~~~

1. Get and save password for admin-GUI access:

    .. code:: bash

       kubectl get secret autonity-platform-grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo


2. Forward port for web access by running these commands in the same shell:
    .. code:: bash

            export POD_NAME=$(kubectl get pods -l "app=grafana,release=autonity-platform" -o jsonpath="{.items[0].metadata.name}")
            kubectl port-forward $POD_NAME 3000

3. Login into dashboard using:
    * URL: http://localhost:3000
    * username: admin
    * password: (password from step ``1``)

What does each metrics means you can read in `wiki article Metrics-and-Monitoring`_

Alerting
~~~~~~~~

1. Configure `notification channel`_
2. Configure `Alerting Rules`_ for your dashboard

How is it works?
~~~~~~~~~~~~~~~~
* After installation grafana will use datasource Prometheus from prometheus subchart
* Subchart also will load pre-configured dashboard for Autonity

.. _Grafana: https://grafana.com/
.. _./files/grafana/dashboards: https://github.com/clearmatics/autonity-helm/tree/master/files/grafana/dashboards
.. _values.yaml: https://github.com/clearmatics/autonity-helm/blob/master/values.yaml
.. _Grafana helm chart: https://github.com/helm/charts/tree/master/stable/grafana
.. _wiki article Metrics-and-Monitoring: https://github.com/clearmatics/autonity/wiki/Metrics-and-Monitoring
.. _notification channel: https://grafana.com/docs/alerting/notifications/
.. _Alerting Rules: https://grafana.com/docs/alerting/rules/
