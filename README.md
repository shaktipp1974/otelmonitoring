# OPENTELEMETRY AUTO INSTRUMENTATION

* Sample Math Service provide REST endpoints for add, sub,mul,div and mod operation
* There are two Spring boot Project is used to demo Observability manual Instrumentation
* Spring Boot App(frontend) exposed endpoints which subsequently called another Spring Boot App(backend)

## TECH STACK
<ol>
	<li>Spring Boot 3.2.4</li>
	<li> Spring Observability</li>
	<li>Log MDC</li>
	<li>Export Log to Loki Server</li>
</ol>

# IMP URL

## Jarger UI
- Jarger UI URL: http://localhost:30010

## Prometheus UI
- Prometheus UI URL: http://localhost:30011

## SWAGGER UI
1- Frontend App: <strong> http://localhost:30020/sppfrontend/springdoc/openapi/swagger-ui/index.html </strong> <br/>
2- Backend App: <strong> http://localhost:30019/sppbackend/springdoc/openapi/swagger-ui/index.html </strong>
3- Jaeger Hotrod App: <strong> http://localhost:30090 </strong>
   REFERENCE: https://medium.com/opentracing/take-opentracing-for-a-hotrod-ride-f6e3141f7941
              https://www.youtube.com/watch?v=fjYAU3jayVo&t=4s

# SPRING-ACTUATOR ENDPOINTS
## FRONTEND
1- Prometheus Metrics: http://localhost:30020/sppfrontend/actuator/prometheus
2- Actuator Metrics: http://localhost:30020/sppfrontend/actuator/metrics
3- Actuator Health: http://localhost:30020/sppfrontend/actuator/health

## BACKEND
1- Prometheus Metrics: http://localhost:30019/sppbackend/actuator/prometheus
2- Actuator Metrics: http://localhost:30019/sppbackend/actuator/metrics
3- Actuator Health: http://localhost:30019/sppbackend/actuator/health

# OTEL COLLECTOR DEBUG POD
## Find the pod name
```
$ k -n otel-col-ns get po
NAME                                          READY   STATUS    RESTARTS   AGE
spp-otel-gateway-collector-5d8db8ddbf-mn7sq   1/1     Running   0          3h7m
```

## Find the Container Name
```
$ k -n otel-col-ns describe po spp-otel-gateway-collector-5d8db8ddbf-mn7sq | grep -i container:
  otc-container:
  Normal  Created  10m   kubelet  Created container: debugger-f965w
```

## Create debug pod
```
$ kubectl -n otel-col-ns debug -it spp-otel-gateway-collector-5d8db8ddbf-mn7sq --target=otc-container   --image=busybox -- /bin/sh
Targeting container "otc-container". If you don't see processes from this container it may be because the container runtime doesn't support this feature.
--profile=legacy is deprecated and will be removed in the future. It is recommended to explicitly specify a profile, for example "--profile=general".
Defaulting debug container name to debugger-sv4wr.
If you don't see a command prompt, try pressing enter.
/ #

```