Minikube
==========================================

Minikube allows a Kubernetes cluster to be run locally on MacOS, Windows and Linux. Using Minikube an Autonity network can be started on your local machine.

Prerequisites
-------------

To follow this tutorial you will need a basic understanding of using a terminal. In terms of software prerequsites you will need

- `Installation git <https://git-scm.com/book/en/v2/Getting-Started-Installing-Git>`_
- `Installation minikube  <https://kubernetes.io/docs/tasks/tools/install-minikube/>`_
- `Installation helm <https://helm.sh/docs/using_helm/#installing-helm>`_

From the terminal ensure that everything was correctly installed.

.. code:: bash

    git --version
    minikube version
    helm version

You should see the version numbers for the installs printed back to the terminal.


Starting Minikube
-----------------

Minikube starts a Kubernetes cluster on your local machine that you can deploy services into. You will be starting Minikube so that you can use the helm charts to start an Autonity network.

Open a new terminal and run

.. code:: bash

    minikube start

Depending on your local environment this may start some downloads to complete the minikube installation. This step can take a while so this may be a good time to fetch coffee. Once minikube has finished booting it will print a line stating the local IP address of the cluster.

If you see the following the cluster has started and is ready to go.

.. code:: bash

    🏄  Done! Thank you for using minikube!


Deploy Tiller to the cluster and configure helm
-----------------------------------------------

Run the following command to initialise helm:
It will deploy tiller into cluster and give your possibilities to deploy packages using helm

.. code:: bash

    helm init
