# tekton-ci-cd-privateregistry-k8s

Following is the steps to deploy simple hello  application using ci/cd with tekton on k8s with private registry

1. first we need to create the private docker registry locally for that go to the location of docker-compose directory and use

     -->   $ mkdir auth
     -->   $ yum install httpd -y
     -->   $ htpasswd -Bbn <name-of-user> <password> > auth/htpasswd
     -->   $ docker-compose up -d

2.  then login to they private docker registry  using created user 

     --> $ docker login localhost:5000

3.  After that go to they worker node and create following file 

     --> $ cat /etc/docker/daemon.json 
          {
               "insecure-registries": ["name-of-hostname-of-privateregistry:5000"]
          }

4.  restart the docker on worker node

5.  create secret for pull and push image to they private registry
 
      --> $ kubectl create secret docker-registry name-of-secret --docker-server=localhost:5000 --docker-username= name-of-user  --docker-password=password 

6.  create service,role and rolebinding for that use service.yaml file

7.  create pipelineresource that will pull the code and dockerfile from github for that use the git-resource.yaml file

8.  crete the build and push task for pull the code from github and build and push the image into they registry for that use task-build-image.yaml file

9.  deploy the pod for that create the task and use the task-deploy.yaml file

10. create pipeline for that use pipeline.yaml file

11. create pipelinerun using pipeline-run file and update the parameter value





   
 
