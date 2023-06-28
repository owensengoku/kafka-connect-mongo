# Airflow

## Instruction

- https://airflow.apache.org/docs/helm-chart/stable/index.html

```
helm repo add apache-airflow https://airflow.apache.org
helm upgrade --install airflow apache-airflow/airflow --namespace airflow --create-namespace
kubectl config set-context --current --namespace airflow
```

- Helm template
```
helm template airflow apache-airflow/airflow > tmp.yaml
==== OR ====
mkdir tmp
helm template airflow apache-airflow/airflow --output-dir tmp
```
