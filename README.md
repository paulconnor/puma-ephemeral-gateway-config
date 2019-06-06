# puma-ephemeral-gateway-config
Testing data for ephemeral gateway pipeline

# Contains a single service /demo
returns HTML based on values set in src/main/gateway/config/env.properties & src/main/gateway/config/services.yml

# Demo

SCOPE
![Scope](https://github.com/paulconnor/puma-ephemeral-gateway-config/blob/master/scope.png)

1. Add the following to your local hosts file
  34.96.65.179 nexus.sandbox2.apimgcp.com docker.sandbox2.apimgcp.com
  35.241.32.56 jenkins.sandbox2.apimgcp.com
  34.95.87.222 grafana.sandbox2.apimgcp.com
  35.241.1.167 kibana.sandbox2.apimgcp.com
  35.244.75.18 gateway.sandbox2.apimgcp.com

2. Clone this Git repo to your own account

3. Modify Jenkins to use your Git Repo
- Login to http://jenkins.sandbox2.apimgcp.com/login
- Configure the test-job pipeline with your git repo (two places in general settings)
![Jenkins->test-job->Congigure->general #1](https://github.com/paulconnor/puma-ephemeral-gateway-config/blob/master/jenkins1.png)
...
...
...
![Jenkins->test-job->Congigure->general #2](https://github.com/paulconnor/puma-ephemeral-gateway-config/blob/master/jenkins2.png)

4. Show existing service
- http://gateway.sandbox2.apimgcp.com/demo

5. Modify Cluster and Service properties
This can be done via Policy Manager and exporting to Git using the Gradle plug-in. Or to get started you can just edit the values directly in your Git repo as follows:
  - Cluster: change the value of envPropColor in src/main/gateway/config/env.properties to a different color
  - Service: change the value of servicePropColor in src/main/gateway/config/services.yml to a different color

6. Run the test-job in jenkins to pull down the changes from Git, build a new docker container, publish to Nexus Docker repo and relaunch from there into gcloud/kubernetes
- Use "build with parameters" and accept default values for the parameters

7. Supporting services / applications 
It can take a few minutes for the gateway to restart. Look at the following while you are waiting
- Logs: http://kibana.sandbox2.apimgcp.com/ (click on Discover)
![Kibana](https://github.com/paulconnor/puma-ephemeral-gateway-config/blob/master/kibana.png)

- Metrics: https://grafana.sandbox2.apimgcp.com/ (click on the following dashboard - Home/Gateway-service-metrics)
![grafana](https://github.com/paulconnor/puma-ephemeral-gateway-config/blob/master/grafana.png)

- Docker Repo: https://nexus.sandbox2.apimgcp.com/
![Nexus](https://github.com/paulconnor/puma-ephemeral-gateway-config/blob/master/nexus.png)


8. Show updated service 
- http://gateway.sandbox2.apimgcp.com/demo
