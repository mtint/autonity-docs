## Encrypt and authenticate all node to node communications

Deploy a private Autonity network onto a Kubernetes cluster using the Helm package manager.

#### Scenario 1: On Local Computer

##### Step 1: Install Infrastructure

1. Install git.

2. Install MiniKube.

**Linux**

Follow the steps [here](https://kubernetes.io/docs/tasks/tools/install-minikube/) or [here](https://kubernetes.io/blog/2019/03/28/running-kubernetes-locally-on-linux-with-minikube-now-with-kubernetes-1.14-support/) to install MiniKube on Linux.


3. Install HELM.

**Linux**

Follow the steps [here](https://helm.sh/docs/using_helm/#installing-helm) to install HELM


##### Step 2: Deploy Autonity network

1. Start MiniKube.

`minikube start`

The following messages should be returned to know that MiniKube was started successfully:

```
Starting local Kubernetes v1.10.0 cluster...
Starting VM...
Getting VM IP address...
Moving files into cluster...
Setting up certs...
Connecting to cluster...
Setting up kubeconfig...
Starting cluster components...
Kubectl is now configured to use the cluster.
Loading cached images from config file.

```

2. Initialise HELM inside the MiniKube cluster created in the previous steps.

`helm init`

The following messages should be returned:

```
$HELM_HOME has been configured at /home/se/.helm.

Tiller (the Helm server-side component) has been installed into your Kubernetes Cluster.

Please note: by default, Tiller is deployed with an insecure 'allow unauthenticated users' policy.
To prevent this, run `helm init` with the --tiller-tls-verify flag.
For more information on securing your installation see: https://docs.helm.sh/using_helm/#securing-your-helm-installation
```

3. Download the HELM chart that will deploy the network:

`git clone https://github.com/clearmatics/charts-ose.git`

4. Install the HELM chart in the cluster as follows:

```
cd ./charts-ose/stable/autonity-network
helm install -n autonity-network ./
```

The following messages should be returned if the HELM chart is installed successfully and the Autonity network is deployed within the cluster:

```
NAME:   autonity-network
LAST DEPLOYED: Fri Oct 25 14:34:45 2019
NAMESPACE: default
STATUS: DEPLOYED

RESOURCES:
==> v1/ConfigMap
NAME                    DATA  AGE
autonity-network-tests  1     24s
genesis                 0     24s
genesis-template        1     24s
nginx-conf              1     24s
observers               2     24s
operator-governance     2     24s
operator-treasury       2     24s
validators              8     24s

==> v1/Pod(related)
NAME                          READY  STATUS    RESTARTS  AGE
observer-0-5dd5c9ccc9-vtj8z   0/2    Init:0/1  0         24s
validator-0-748b69c97-2z2zr   0/2    Init:0/1  0         24s
validator-1-6667678cbc-rbg7w  0/2    Init:0/1  0         24s
validator-2-646d4d7489-jrctj  0/2    Init:0/1  0         24s
validator-3-66d69c7cc9-qwg7d  0/2    Init:0/1  0         24s

==> v1/Role
NAME           AGE
secrets-write  24s

==> v1/RoleBinding
NAME           AGE
secrets-write  24s

==> v1/Secret
NAME                 TYPE    DATA  AGE
account-pwd          Opaque  1     24s
observers            Opaque  1     24s
operator-governance  Opaque  1     24s
operator-treasury    Opaque  1     24s
validators           Opaque  4     24s

==> v1/Service
NAME         TYPE       CLUSTER-IP     EXTERNAL-IP  PORT(S)                               AGE
observer-0   ClusterIP  10.96.170.117  <none>       8545/TCP,8546/TCP,30303/TCP,6060/TCP  24s
validator-0  ClusterIP  10.102.98.125  <none>       8545/TCP,8546/TCP,30303/TCP,6060/TCP  24s
validator-1  ClusterIP  10.98.197.252  <none>       8545/TCP,8546/TCP,30303/TCP,6060/TCP  24s
validator-2  ClusterIP  10.108.5.247   <none>       8545/TCP,8546/TCP,30303/TCP,6060/TCP  24s
validator-3  ClusterIP  10.106.31.125  <none>       8545/TCP,8546/TCP,30303/TCP,6060/TCP  24s

==> v1/ServiceAccount
NAME                SECRETS  AGE
autonity-initiator  1        24s

==> v1beta1/Deployment
NAME         READY  UP-TO-DATE  AVAILABLE  AGE
observer-0   0/1    1           0          24s
validator-0  0/1    1           0          24s
validator-1  0/1    1           0          24s
validator-2  0/1    1           0          24s
validator-3  0/1    1           0          24s


NOTES:
==== Autonity ====

# To get autonity validators account password type:
kubectl -n default get secrets account-pwd -o 'go-template={{index .data "account.pwd"}}' | base64 --decode; echo ""

# Get private key of first observer (id == 0)
kubectl -n default get secrets observers -o 'go-template={{index .data "0.private_key"}}' | base64 --decode; echo ""

# Get private key of Governance Operator
kubectl -n default get secrets operator-governance -o 'go-template={{index .data "0.private_key"}}' | base64 --decode; echo ""

# Get private key of Treasury Operator
kubectl -n default get secrets operator-treasury -o 'go-template={{index .data "0.private_key"}}' | base64 --decode; echo ""

# Get list of addresses for each validator
kubectl -n default get configmap validators -o yaml |grep .address

# Get genesis.json
kubectl -n default get configmap genesis -o yaml --export=true

# Forward rpcapi validator-0 to localhost
kubectl -n default port-forward svc/validator-0 8545:8545
# Forward wsapi validator-0 to localhost
kubectl -n default port-forward svc/validator-0 8546:8546

# Example JSON-RPC requests:



### HTTP(s)-RPC ###
curl -X POST -H "Content-Type: application/json" \
    \
    \
    --data '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1}' \
    http://localhost:8545

### WS(s)-RPC ###
docker run -it --rm --net=host \
    \
     monotykamary/wscat \
    \
    \
     -c ws://127.0.0.1:8546 \
     -x '{"method":"eth_blockNumber","params":[],"id":1}'
```