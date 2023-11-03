# Prometheus-and-Grafana-setup-using-helm

![image](https://github.com/Adabala123/Prometheus-and-Grafana-setup-using-helm/assets/96461586/ae4ea01e-422d-470c-b17b-068df98eca40)

                                                    **Install Helm3**
# Download scripts
    curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3

# provide permission
    sudo chmod 700 get_helm.sh

# Execute script to install
    sudo ./get_helm.sh

**Implementation steps**
# We need to add the Helm Stable Charts for your local client. Execute the below command:

    helm repo add stable https://charts.helm.sh/stable

# Add prometheus Helm repo
    helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
    helm search repo prometheus-community

# Create Prometheus namespace
    kubectl create namespace prometheus

# Install kube-prometheus-stack

Below is helm command to install kube-prometheus-stack. The helm repo kube-stack-prometheus (formerly prometheus-operator) comes with a grafana deployment embedded.

    helm install stable prometheus-community/kube-prometheus-stack -n prometheus

Lets check if prometheus and grafana pods are running already
    kubectl get pods -n prometheus

This confirms that prometheus and grafana have been installed successfully using Helm.
In order to make prometheus and grafana available outside the cluster, use LoadBalancer or NodePort instead of ClusterIP.

# Edit Prometheus Service
    kubectl edit svc stable-kube-prometheus-sta-prometheus -n prometheus

# Edit Grafana Service
    kubectl edit svc stable-grafana -n prometheus
    kubectl get svc -n prometheus

![image](https://github.com/Adabala123/Prometheus-and-Grafana-setup-using-helm/assets/96461586/c0e4ebb0-f342-4a77-9fc8-5ac5094125de)

Access Grafana UI in the browser

Get the URL from the above screenshot and put in the browser

while opening the grafrana dashboard we need username and password 

kubectl get secret --namespace default grafana -o yaml

passowrd is encrypt so have to do decrypt using below command

echo "YwRtaw4=" | openssl base64 -d : echo


