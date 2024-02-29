### kubernetes
# kubernetes manifest files
# K8s Challenge
!!!

1. Create a Pod with two containers with a shared volume; use manifest file: shared-volume.yaml.
   - create a test file blog.txt inside the first container in /tmp/blog:

'''
$kubectl exec -i -t pod/volume-share-devops -c volume-container-devops-1 -- /bin/bash
'''

   - test file blog.txt should exist too in second container since they are using the same volume:

    '''
    $kubectl exec -i -t pod/volume-share-devops -c volume-container-devops-1 -- ls /tmp/blog
    '''

2. Deploy a static website using configmaps, deployment and service; manifest file: nginx-deployment.yaml.

3. Deploy a Grafana tools and expose using NodePort on port 3200: grafana-deployment.yaml.

