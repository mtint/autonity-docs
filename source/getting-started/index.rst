Starting an Autonity Network with Minikube
==========================================

Minikube allows a Kubernetes cluster to be run locally on MacOS, Windows and Linux. Using Minikube an Autonity network can be started on your local machine.

Prerequisites
-------------

To follow this tutorial you will need a basic understanding of using a terminal. In terms of software prerequsites you will need 

- git `Installation <https://git-scm.com/book/en/v2/Getting-Started-Installing-Git>`_
- minikube `Installation <https://kubernetes.io/docs/tasks/tools/install-minikube/>`_
- helm `Installation <https://helm.sh/docs/using_helm/#installing-helm>`_

From the terminal ensure that everything was correctly installed. 

.. code-block::

  git --version
  minikube version
  helm version

You should see the version numbers for the installs printed back to the terminal. 

Installing Autonity Helm
------------------------

In a folder where you keep code clone the Autonity helm repository

.. code-block::

  git clone https://github.com/clearmatics/autonity-helm.git
  cd autonity-helm

Keep this terminal open. You will be using in a minute. 

Starting Minikube
-----------------

Minikube starts a Kubernetes cluster on your local machine that you can deploy services into. You will be starting Minikube so that you can use the helm charts to start an Autonity network. 

Open a new terminal and run

.. code-block::

  minikube start 

Depending on your local environment this may start some downloads to complete the minikube installation. This step can take a while so this may be a good time to fetch coffee. Once minikube has finished booting it will print a line stating the local IP address of the cluster.

If you see the following the cluster has started and is ready to go. 

.. code-block::

  🏄  Done! Thank you for using minikube!

A few lines about you will see the IP address of the cluster printed to the console. Copy this as you will need it to launch helm. 

.. code-block::

  "minikube" IP address is 192.168.99.101

Starting Helm 
-------------

In the terminal you used in the Installing Autonity Helm section run the following command to initialise helm.

.. code-block::
  helm init
  helm install -n autonity ./

After a short while you will some output to the terminal showing that validators and observers have been deployed. 

Congratulations you have deployed an Autonity network locally!

