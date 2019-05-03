Deploy autonity-helm
====================

In a folder where you keep code clone the Autonity helm repository

.. code:: bash

    git clone https://github.com/clearmatics/autonity-helm.git -b v0.4.2
    cd autonity-helm
    helm dependency update
    helm install -n autonity-platform ./

After a short while you will some output to the terminal showing that validators and observers have been deployed.

Congratulations you have deployed an Autonity network locally!
