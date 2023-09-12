# ELK IMPLEMENTATION

Check The OFFICIAL LINK for updates
https://www.elastic.co/guide/en/cloud-on-k8s/current/k8s-quickstart.html

STEPS
**1 . Deploy ECK(Elastic Cloud on Kubernetes) with helm**

Install ECK custom resource definations (CRDS) using helm chart 

helm repo add elastic https://helm.elastic.co

helm repo update

helm install elastic-operator elastic/eck-operator -n elastic-system --create-namespace

Change the node affinity as per needs in helmechart affinity: {} section
Use the below commands to get the values
_helm show values elastic/eck-operator >> values.yml  
helm install elastic-operator elastic/eck-operator -f values.yml -n elastic-system --create-namespace_

To Change node affinty
affinity:
  nodeAffinity:
    requiredDuringSchedulingIgnoredDuringExecution:
      nodeSelectorTerms:
      - matchExpressions:
        - key: pool
          operator: In
          values:
          - elk-pool

**2. Install Elastic Search Cluster**     
kubectl get elasticsearch
kubectl get pods 
kubectl get svc 
PASSWORD=$(kubectl get secret quickstart-es-elastic-user -o go-template='{{.data.elastic | base64decode}}')
curl -u "elastic:$PASSWORD" -k "https://quickstart-es-http:9200"
kubectl port-forward service/quickstart-es-http 9200
curl -u "elastic:$PASSWORD" -k "https://localhost:9200"

**3. Install a Kibana Instance**
kubectl get elasticsearch
kubectl get pods 
kubectl get svc 
kubectl port-forward service/quickstart-kb-http 5601
In there we need to configure Discover 

**4. Install Filebeats**
kubectl get beats
kubectl get pods 


















   
