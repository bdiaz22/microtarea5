# Microtarea 5 - Cloud Computing (Bryan Diaz y Joe Acuña)

## Prometheus
Para el sistema de monitoreo se está utilizando prometheus, que está basado en tool kit en una base de datos de series temporales.

Para la instalación de Prometheus, por medio de helm, se ejecuta el siguiente comando para añadirlo al cluster. Para poder instalarlo tambíen tiene que estar prendido minikuve.
```
helm install prometheus prometheus-community/kube-prometheus-stack \
 --create-namespace \
 --namespace prom
```
![img1](install_prometheus.jpeg)

Para visualizar el dashboard en el localhost
![img2](prometheus_dashboard.jpeg)

## Desplegando aplicación

Se tiene que genera un cluster minikube antes de todo. 
![img3](minikube.jpeg)

Para poner a prueba las consultas y visualizarlas con Prometheus, se generará un pod con 1 CPU.

![img4](pod_estress.jpeg)

## Monitoreo de métricas

En el dashboard de Prometheus se harán queries para visualizar el consumo que genera nuestra aplicación.

```
container_cpu_usage_seconds_total{namespace!="default", namespace!="kube-system",namespace!="prom"}

```

![img5](prometheus1.jpeg)

```
rate(container_cpu_usage_seconds_total{namespace="apps"}[1m])
```

![img6](prometheus3.jpeg)

```
sum by (pod) (rate(container_cpu_usage_seconds_total{namespace="apps",pod!=""}[5m]))
```

![img7](prometheus2.jpeg)

## Conclusiones

Como conclusión, Prometheus es una herramienta que nos permite monitorear las queries que queramos en nuestra aplicación de una manera sencilla.

### Integrantes 
- Joe Acuña
- Bryan Díaz
