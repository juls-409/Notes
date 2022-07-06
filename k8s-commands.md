minikube start then kubectl get pod
Once we start it, we can use our kubectl commands

Can do kubectl create command. We don't create pods , we create deployment
kubectl create deployment <name> --image=<imagelocation>

deployment - > replicaset - > pod

### kubectl apply commands in order
    
    kubectl apply -f mongo-secret.yaml
    kubectl apply -f mongo.yaml
    kubectl apply -f mongo-configmap.yaml 
    kubectl apply -f mongo-express.yaml

### kubectl get commands

    kubectl get pod
    kubectl get pod --watch
    kubectl get pod -o wide
    kubectl get service
    kubectl get secret
    kubectl get all | grep mongodb

### kubectl debugging commands

    kubectl describe pod mongodb-deployment-xxxxxx
    kubectl describe service mongodb-service
    kubectl logs mongo-express-xxxxxx

### give a URL to external service in minikube

    minikube service mongo-express-service

## Example of where to put things 

Env variables -> Deployment.yaml
ConfigMap -> DB url
Creds -> Secret

## To have external requests -> use external service

# How to use Image?

Look at dockerhub. For ports, env variables

create deployment , don't want vals in deployment, create secret. Create secret before deployment. Reference those values using `valueFrom`

Apply secret, then can do a 'get secret'. Then we apply our deployment file.

# Can do a kubectl get all <- will show entire architecture

### Can do a kubectl describe pod <podname>

# Difference between label of deployment n pod. If change one mess up in service?'

Validate service is attached to correct pod
1. kubectl describe service <serviceName>
2. kubectl describe pod <podName>
3. Check see if endpoints match

# Now creating external part of APP express server

Which DB to connect to
    MONGOdb address & Cred
        Do by env variables



Two diff images used for two deployment files. MongoDB and MongoExpress

Our config map defines our DB URL based off of name OF Service. Auto grabs url based on service name because service has its ip defined.

1. CONFIGMAP
2. THEN DEPLOYMENT
3. LOG it to see logs
4. NOW create external service 


HOW to make external???  by doing type: LoadBalancer

ALso nodeport is where we access our server

INTERNAL service type by default is CLusterIP. LoadBalancer gets internal and external ip address
