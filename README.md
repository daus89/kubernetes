# kubernetes
## kubernetes manifest files
## K8s Challenge

Includes imperative commands to create manifest files faster.


1. Create a Pod with two containers with a shared volume; use manifest file: shared-volume.yaml.
   - create a test file blog.txt inside the first container in /tmp/blog:

```
   $kubectl exec -i -t pod/volume-share-devops -c volume-container-devops-1 -- /bin/bash
```
   - test file blog.txt should exist too in second container since they are using the same volume:

```
   $kubectl exec -i -t pod/volume-share-devops -c volume-container-devops-1 -- ls /tmp/blog
```

2. Deploy a static website using configmaps, deployment and service; manifest file: nginx-deployment.yaml.

3. Deploy a Grafana tools and expose using NodePort on port 3200: grafana-deployment.yaml.

4. Deploy a tomcat app, it could be better if I mount some storage too: tomcat-deployment.yaml

5. Update a deployment image, rollback to previous revision.
```
   kubectl set image deployment/nginx-deployment nginx-container=nginx:latest
```
   #to rollback to specific revision
```
   kubectl rollout history deployment/nginx-deployment
   kubectl rollout undo deployment/nginx-deployment --to-revision=1
```

6. Deploy a LAMP stack using deployment
   - Create a config map php-config for php.ini with variables_order = "EGPCS" data.
   - Create a deployment named lamp-wp
   - Create two containers under it. First container must be httpd-php-container using image webdevops/php-apache:alpine-3-php7 and second container must be mysql-container from image mysql:5.6. Mount php-config configmap in httpd container at /opt/docker/etc/php/php.ini location.
   - Create kubernetes generic secrets for mysql related values like myql root password, mysql user, mysql password, mysql host and mysql database. Set any values of your choice.
   - Add some environment variables for both containers:
   - MYSQL_ROOT_PASSWORD, MYSQL_DATABASE, MYSQL_USER, MYSQL_PASSWORD and MYSQL_HOST. Take their values from the secrets you created. Please make sure to use env field (do not use envFrom) to define the name-value pair of environment variables.
   - Create a node port type service lamp-service to expose the web application, nodePort must be 30008.
   - Create a service for mysql named mysql-service and its port must be 3306.
   - We already have /tmp/index.php file on jump_host server
   - Copy this file into httpd container under Apache document root i.e /app and replace the dummy values for mysql related variables with the environment variables you have set for mysql related parameters. Please make sure you do not hard code the mysql related details in this file, you must use the environment variables to fetch those values.
