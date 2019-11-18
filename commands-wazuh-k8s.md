
```bash

# create k8s namespace,storageClass
kubectl apply -f base/wazuh-ns.yaml
kubectl apply -f base/gce-pd-storage-class.yaml

# create PVs
kubectl apply -f pv/wazuh-elasticsearch.yaml
kubectl apply -f pv/wazuh-manager-master.yaml

# deploy ElasticSearch
kubectl apply -f elastic_stack/elasticsearch/elasticsearch-svc.yaml
kubectl apply -f elastic_stack/elasticsearch/single-node/elasticsearch-api-svc.yaml
kubectl apply -f elastic_stack/elasticsearch/single-node/elasticsearch-sts.yaml

# deploy Kibana and Nginx
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
#kubectl apply -f wazuh_managers/wazuh-workers-svc.yaml

kubectl apply -f wazuh_managers/wazuh-master-conf.yaml
#kubectl apply -f wazuh_managers/wazuh-worker-0-conf.yaml
#kubectl apply -f wazuh_managers/wazuh-worker-1-conf.yaml

kubectl apply -f wazuh_managers/wazuh-master-sts.yaml
#kubectl apply -f wazuh_managers/wazuh-worker-0-sts.yaml
#kubectl apply -f wazuh_managers/wazuh-worker-1-sts.yaml

# 
kubectl explain statefulset.spec.template.spec.containers.volumeMounts

```

```bash
# CLEAN SCRIPT

# BETTER TO GO WORKLOADS TO DELETE PODS
kubectl get pods --namespace wazuh
kubectl delete pods wazuh-elasticsearch-0 --namespace wazuh
kubectl delete pods wazuh-kibana-68b55686cb-hlfjn --namespace wazuh
kubectl delete pods wazuh-kibana-68b55686cb-vvz5d --namespace wazuh
kubectl delete pods wazuh-logstash-7887bf7cbf-x4mj8 --namespace wazuh
kubectl delete pods wazuh-logstash-7887bf7cbf-kn697 --namespace wazuh
kubectl delete pods wazuh-manager-master-0 --namespace wazuh
kubectl delete pods wazuh-nginx-679f76b648-vbmp2 --namespace wazuh
kubectl delete pods wazuh-nginx-679f76b648-lbgn2 --namespace wazuh

# Clean services
kubectl get services --namespace wazuh
kubectl delete services elasticsearch --namespace wazuh
kubectl delete services kibana --namespace wazuh
kubectl delete services logstash --namespace wazuh
kubectl delete services wazuh --namespace wazuh
kubectl delete services wazuh-nginx --namespace wazuh
kubectl delete services wazuh-cluster --namespace wazuh
kubectl delete services wazuh-elasticsearch --namespace wazuh

# Delete PVCs

# Delete PVs
kubectl get pv --namespace wazuh
kubectl delete pv wazuh-elasticsearch --namespace wazuh
kubectl delete pv wazuh-manager-master --namespace wazuh
```