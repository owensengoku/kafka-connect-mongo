# kafka-connect-mongo

## all meterials comes from https://developers.redhat.com/articles/2023/03/29/deploy-kafka-connect-container-using-strimzi#

## Instuction
```
kubectl create namespace strimzi
kubectl config set-context --current --namespace strimzi
```
- Checking
```
kubectl apply -f kafka.yaml 
```
- Checking
```
kubectl apply -f topic.yaml 
```
- Checking
```
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install mongodb bitnami/mongodb --set podSecurityContext.enabled=false,auth.enabled=false,volumePermissions.enabled=true --version 13.6.0 -n strimzi
```
- Checking
```
kubectl apply -f spam-producer.yaml 
```
- Checking
```
docker login
kubectl create secret generic quayio --from-file=.dockerconfigjson=/users/admin/.docker/config.json --type=kubernetes.io/dockerconfigjson
```
- Checking
```
kubectl apply -f kafka-connect.yaml 
```
- Checking
```
kubectl apply -f mongo-connector.yaml 
```
- Checking
```
kubectl run mongodb-client --rm --tty -i --restart='Never' --image docker.io/bitnami/mongodb:4.4.13-debian-10-r9 --command -- bash
```
- In the pod of mongo-client
```
mongo mongodb://mongodb:27017
use sampledb
use sampledb
```
- In the pod of mongo-client(Alternative)
```
curl -X POST \
     -H "Content-Type: application/vnd.kafka.json.v2+json" \
     -H "Accept: application/vnd.kafka.v2+json" \
     --data '{"records":[{"key":"jsmith","value":"alarm clock"},{"key":"htanaka","value":"batteries"},{"key":"awalther","value":"bookshelves"}]}' \
     "http://kafkarestproxy.confluent.svc.cluster.local:8082/topics/elastic-0"
```
