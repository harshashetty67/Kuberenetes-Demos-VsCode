# Kubernetes Services :

### All the service objects in Kubernetes are JSON objects and it is stored in the ETCD store in the control pane of Master node.

=========================================

### - Cluster IP :

     - Default service type in kubernetes.
     - Only for internal communication within the cluster.
     - Kube-proxy in the node is responsible for traffic forwarding like a router.
     - Kube-Proxy is the only component of the node that is accessible from outside.
     - Cluster Ip matches the deployment/replica-set matching the pod label defined in the service yaml file.

```
    Internal Service Discovery :
     - Internal service has virtual IP and DNS name
     - Service deployed in the namespace can be accessed by any POD in the same name-space with URL "http://{service-name}"  or  "http://{cluster-IP}"
     - But, for a pod from another namespace to access the pod in different namespace it should call the service in this format "http://{service-name}/{namespace}" or  "http://{cluster-IP}"
     - We need CoreDNS or KubeDNS extension for the DNS resolution to work internally.
```

==============================================

### - Node Port :

```
- Extension to ClusterIp that provides external communication.
- NodePort value range from 30000-39999.
- NodePort registers the node port value with the kube-proxy of each node and the kube-proxy will route the request to Cluster-IP service.
- Cluster-IP will be having the endpoint mapping to each pod under a deployment/replica-set - When we create ClusterIp endpoint objects for each pod is created and maintained for routing the request to each pod just like load-balancing (round-robin).
- These endpoints mapping is managed by the Endpoint Controller.
- This approach has limitations - a). Client need to send request to any one node b). Sharing Node-IP with external client is not secure practice. 3). Not reliable as node might change in future.

```

=============================================

### - Load Balancer :

```
- Kubernetes provides ClusterIP and NodePort, but it also has support for Load-Balancer (Implementation of load-balancer is done by third-party vender like Microsoft, Amazon etc.)

- Creation load-balancer is done by CSP's on our behalf - only if we are using managed kubernetes Services.
```
