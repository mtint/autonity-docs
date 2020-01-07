## System Operator Monitor basic parameters for node health and performance

### Prerequisites

1. Two terminal windows.

### Steps

1. Run MiniKube.

2. Start HELM inside the CLUSTER.

3. Install the `autonity-demo` chart with Prometheus and Grafana to be able to visualise network performance:

```
helm install --name autonity-demo --namespace test1 charts-ose.clearmatics.com/autonity-demo --set global.prometheus.enabled=true,global.grafana.enabled=true
```

This chart deploys an Autonity network and enables Prometheus and Grafance.

4. Open another terminal window and run the following commands to set the Prometheus server URL to port localhost:9090

```
export POD_NAME=$(kubectl get pods --namespace test1 -l "app=prometheus,component=server" -o jsonpath="{.items[0].metadata.name}")
kubectl --namespace test1 port-forward $POD_NAME 9090
```

5. Open a browser and navigate to the URL http://localhost:9090 to check the Prometheus server.

6. Follow the following steps to be able to check the system metrics:

  a. Login credentials are required for the Grafana dashboard. To get the login credentials:
    - The username is `admin`.
    - To get the password run the following command:

  ```
  kubectl get secret --namespace test1 autonity-demo-grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
  ```

  b. Forward Grafana dashboard to localhost http://localhost:3000 by running the following command:

  `kubectl --namespace test1 port-forward svc/autonity-demo-grafana 3000:80`

  c. Open a browser and navigate to the URL http://localhost:3000 and login using the login credentials returned on the previous steps.

7. Using Grafana dashboard the network performace can be monitored.