
```bash

# create k8s ??variables,labelles??
kubectl apply -f base/wazuh-ns.yaml
kubectl apply -f base/gce-pd-storage-class.yaml

# 
kubectl apply -f elastic_stack/elasticsearch/elasticsearch-svc.yaml
kubectl apply -f elastic_stack/elasticsearch/elasticsearch-api-svc.yaml
kubectl apply -f elastic_stack/elasticsearch/elasticsearch-sts.yaml

# 
kubectl apply -f elastic_stack/kibana/kibana-svc.yaml
kubectl apply -f elastic_stack/kibana/nginx-svc.yaml

kubectl apply -f elastic_stack/kibana/kibana-deploy.yaml
kubectl apply -f elastic_stack/kibana/nginx-deploy.yaml

# deploy Logstash
kubectl apply -f elastic_stack/logstash/logstash-svc.yaml
kubectl apply -f elastic_stack/logstash/logstash-deploy.yaml

# deploy Wazuh
kubectl apply -f wazuh_managers/wazuh-master-svc.yaml
kubectl apply -f wazuh_managers/wazuh-cluster-svc.yaml
kubectl apply -f wazuh_managers/wazuh-workers-svc.yaml

kubectl apply -f wazuh_managers/wazuh-master-conf.yaml
kubectl apply -f wazuh_managers/wazuh-worker-0-conf.yaml
kubectl apply -f wazuh_managers/wazuh-worker-1-conf.yaml

kubectl apply -f wazuh_managers/wazuh-master-sts.yaml
kubectl apply -f wazuh_managers/wazuh-worker-0-sts.yaml
kubectl apply -f wazuh_managers/wazuh-worker-1-sts.yaml

```