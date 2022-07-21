# Exemplos de código do curso Observabilidade/Monitoramento (Alura) 
<br>

## Projetos/pastas separados pelos cursos:
- ### [/prometheus-grafana/](https://github.com/TomazWill/observabilidade-alura/tree/master//prometheus-grafana)
  - Curso: Observabilidade: coletando métricas de uma aplicação com Prometheus
  - Monitoramento: Prometheus, Grafana e Alertmanager

<br>

---
<br>



## Instruções do projeto `prometheus-grafana` ##########

### Rodando projeto pelo docker
```sh
cd prometheus-grafana && \
docker-compose up
```

### Rodando aplicação java
```sh
cd prometheus-grafana/app && \
sh start.sh
```

### Endereços do projeto
```sh
# metricas do projeto java
http://localhost/metrics

# prometheus
http://localhost:9090/

# grafana
http://localhost:3000/
```

### Queries para Prometheus (PromQL)
```sh
# Pega o estado de threads da jvm
jvm_threads_states_threads{application="app-forum-api", state="runnable"}

# Taxa das requests com erros (diferentes das familias de 200.* e 300.* )
http_server_requests_seconds_count{application="app-forum-api",method=~"GET|POST", status!~"2..|3..", uri!="/actuator/prometheus"} offset 1m

# Taxa de crescimento das requests
increase(http_server_requests_seconds_count{application="app-forum-api", uri!="/actuator/prometheus"} [1m])

# Taxa de crescimento das requests com agregador
sum(increase(http_server_requests_seconds_count{application="app-forum-api", uri!="/actuator/prometheus"} [1m]))

# Pega o número de requisições por segundo (nos ultimos 5min)
irate(http_server_requests_seconds_count{application="app-forum-api", uri!="/actuator/prometheus"} [5m])

# Pega o número de requisições por segundo com agregador (nos ultimos 5min)
sum(irate(http_server_requests_seconds_count{application="app-forum-api", uri!="/actuator/prometheus"} [5m]))
```


<br>

---
<br>


###	**REFERÊNCIAS**
- Cursos: <br>
  - [Observabilidade com Prometheus](https://cursos.alura.com.br/course/observabilidade-prometheus "Observabilidade com Prometheus")
  - [Monitoramento: Prometheus, Grafana e Alertmanager](https://cursos.alura.com.br/course/monitoramento-prometheus-grafana-alertmanager "Monitoramento: Prometheus, Grafana e Alertmanager")
