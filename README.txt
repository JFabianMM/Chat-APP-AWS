# These are the steps to run the chat app 
# in AWS.

# ------------------------------------
# Enter to folder microserviceAuthorization
cd microserviceAuthorization
      
# Create the backend2 image
docker build -t authorization90:1 .

# push the image to a repository, if is dockerhub, then: 
docker tag authorization90:1 fabianmm34/chatapp:authorization90
docker push fabianmm34/chatapp:authorization90
# if is AWS ECR, then 
create the repository on ECR called authorization90 
docker tag authorization90:1 121503602521.dkr.ecr.us-east-2.amazonaws.com/authorization90:1
docker push 121503602521.dkr.ecr.us-east-2.amazonaws.com/authorization90:1


# ------------------------------------
# Enter to folder microserviceBackend
cd microserviceBackend
      
# Create the backend2 image
docker build -t backend90:1 .

# push the image to a repository, if is dockerhub, then: 
docker tag backend90:1 fabianmm34/chatapp:backend90
docker push fabianmm34/chatapp:backend90
# if is AWS ECR, then 
create the repository on ECR called backend90 
docker tag backend90:1 121503602521.dkr.ecr.us-east-2.amazonaws.com/backend90:1
docker push 121503602521.dkr.ecr.us-east-2.amazonaws.com/backend90:1

# ------------------------------------
# Enter to folder microserviceGraphql
cd microserviceGraphql     
	
# Create the graphql90 image
docker build -t graphql90:1 .

# push the image to a repository, if is dockerhub, then: 
docker tag graphql90:1 fabianmm34/chatapp:graphql90
docker push fabianmm34/chatapp:graphql90   
# if is AWS ECR, then 
create the repository on ECR called graphql90 
docker tag graphql90:1 121503602521.dkr.ecr.us-east-2.amazonaws.com/graphql91:1
docker push 121503602521.dkr.ecr.us-east-2.amazonaws.com/graphql91:1

# ------------------------------------
# Enter to the file microserviceFrontend
cd microserviceFrontend    

# Create the frontend90 image
docker build -t frontend90:1 .

# push the image to a repository, if is dockerhub, then: 
docker tag frontend90:1 fabianmm34/chatapp:frontend90
docker push fabianmm34/chatapp:frontend90  
# if is AWS ECR, then 
create the repository on ECR called frontend90 
docker tag frontend90:1 121503602521.dkr.ecr.us-east-2.amazonaws.com/frontend90:1
docker push 121503602521.dkr.ecr.us-east-2.amazonaws.com/frontend90:1 

# ------------------------------------
# Create the nginx2 image
docker build -t nginx90:1 .

# push the image to a repository, if is dockerhub, then: 
docker tag nginx90:1 fabianmm34/chatapp:nginx90
docker push fabianmm34/chatapp:nginx90  
# if is AWS ECR, then 
create the repository on ECR called nginx90 
docker tag nginx90:1 121503602521.dkr.ecr.us-east-2.amazonaws.com/nginx90:1
docker push 121503602521.dkr.ecr.us-east-2.amazonaws.com/nginx90:1 


1.- Necesito crear el cluster.
2.- Necesito agregar el Addon al cluester (Amazon EBS CSI Driver). 
3.- Necesito crear el volume en EC2 > Volumes > vol-069d6a3b117b5571c. 
4.- Attach the volume to a device. 

# Apply the next manifests:
kubectl create -f secret.yaml
kubectl apply -f storageClass.yaml
kubectl patch storageclass gp2 -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'
kubectl apply -f claim.yaml && kubectl apply -f pv.yaml
kubectl apply -f mongodb1.yaml
kubectl apply -f mongodb2.yaml
kubectl apply -f mongodb3.yaml
kubectl apply -f service1.yaml
kubectl apply -f service2.yaml
kubectl apply -f service3.yaml
kubectl apply -f backend.yaml 
kubectl apply -f frontend.yaml
kubectl apply -f graphql.yaml
kubectl apply -f authorization.yaml
kubectl apply -f nginx.yaml  
kubectl apply -f nginx-controller.json
kubectl apply -f nginx-service.json 

# Verify all with  
kubectl get all 