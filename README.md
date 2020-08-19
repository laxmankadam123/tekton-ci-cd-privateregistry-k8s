# tekton-ci-cd-privateregistry-k8s

Following is the steps to deploy simple hello world application using ci/cd with tekton on k8s with private registry

1. we need to create secret for docker credentials for that use 

$ kubectl create secret docker-registry <secret-name> --docker-server=<server-name> --docker-username <user-name>  --docker-password <Password> 

2. create service,role and rolebinding for deploy the application into they cluster for that check service.yaml file

$ kubectl apply -f service.yaml

3. create private docker registry into your local machine for that check the docker-compose is install on your machine after that go they location of docker-compose directory  and   create auth directory 
$ mkdir auth
$ yum install httpd -y
$ htpasswd -Bbn <user-name> <password> > auth/htpasswd

then run they command 
$ docker-compose up -d

now your private registry is set then login into they user that mentioned in they htpasswd onto your registry host



   
