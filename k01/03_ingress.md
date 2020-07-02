## What  is Kubernetes Ingress?

Kubernetes Ingress is not a Kubernetes Service. Very simplified its just a Pod which redirects requests to other internal (ClusterIP) services. This Pod itself is made reachable through a Kubernetes Service, most commonly a LoadBalancer.

## Why to use?
You use it to make internal services reachable from outside your cluster. It saves you precious static IPs, as you won’t need to declare multiple LoadBalancer services. Also it allows for much more configuration and easier setup.

## Ingress Controllers
You must have an ingress controller to satisfy an Ingress. Only creating an Ingress resource has no effect. You may need to deploy an Ingress controller such as ingress-nginx. You can choose from a number of Ingress controllers.
e.g. Nginx, HAProxy, Kong, Istio and Envoy based ingress controllers and many more.

## Ingress rules
Each HTTP rule contains the following information:

An optional host. In this example, no host is specified, so the rule applies to all inbound HTTP traffic through the IP address specified. If a host is provided (for example, foo.bar.com), the rules apply to that host.
- A list of paths (for example, /testpath), each of which has an associated backend defined with a serviceName and servicePort. Both the host and path must match the content of an incoming request before the load balancer directs traffic to the referenced Service.
- A backend is a combination of Service and port names as described in the Service doc. HTTP (and HTTPS) requests to the Ingress that matches the host and path of the rule are sent to the listed backend.
- A default backend is often configured in an Ingress controller to service any requests that do not match a path in the spec.

### Default Backend
An Ingress with no rules sends all traffic to a single default backend. The default backend is typically a configuration option of the Ingress controller and is not specified in your Ingress resources.

If none of the hosts or paths match the HTTP request in the Ingress objects, the traffic is routed to your default backend
