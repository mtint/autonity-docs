Ethstats (optional)
=========================================

`Ethstats helm chart`_

Deploy
~~~~~~

.. code:: bash

    helm install -n autonity-platform ./ --set global.ethstats.enabled=true


Usage
~~~~~

1. Forward port for web access by running these commands in the same shell:

    .. code:: bash

        kubectl port-forward svc/ethstats 8080:80

2. Login into dashboard using URL: http://localhost:8080

.. _Ethstats helm chart: https://github.com/clearmatics/autonity-helm/tree/master/helm-charts/ethstats