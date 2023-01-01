# tcp-init

One of the simplest TCP Connection Check tools, ever.

Designed as a Kubernetes Init Container, this will perform the most basic of checks with a TCP Connection to verify if a site/service is up.

Standard timeout of 5 seconds is applied, and upon failure, will crash loop retry the init container until successful.

Example usage in a Kubernetes Deployment Manifest:

initContainers:
  - name: wait-for-something
    image: nhillsdonuk/tcp-init
    env:
    - name: TCPHOST
      value: "kubernetes-service-name"
    - name: TCPPORT
      value: "30000"
    command:
      - ruby
    args:
    - init-tcp.rb