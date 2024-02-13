
# Docker in Docker

What is DOCKER IN DOCKER?(DinD)
  Docker-in-Docker means we can run Docker containers inside another Docker container.

In Docker world One process communicate with Other process is because od "Unix Socket"
  # cd /run/containerd/
  # ls -i
    
There are two ways to create Docker in Docker     
         1. Lauch Container by sharing Host Docker Socket
           (-v /run/containerd/:/run/containerd/ )
            
         2. Give all capabilities to the container (--privileged)
                 --privileged  <> Give extended privileges to this container

What is Privileged capabilities:
  When we create container have very limited power(not root power) or Capabilities,that not able to Launch 'New container in it',
  
but Running in "--privileged" mode to new container give All capabilities to Start Dockerin it .


       ::By using 2nd way DinD (Give all capabilities to the container) ::
           
Prerequisite: AWS account
 
Step 1-
      install and Start docker service   {DOCKER 1st}
         #yum install docker -y
         #systemctl start docker

Step 2-
      pull docker image (Docker provides a pre-created image for Docker inside Docker)
        #docker pull docker

step 3-
      lauch new container by adding all capabilities to the container
        #docker run -dit --privileged --name myDinD docker
        
![Screenshot 2024-02-13 155059](https://github.com/Pratikshinde55/Docker-in-Docker/assets/145910708/f3fd7600-aa03-4830-8380-dc48c2c91dfc)

Step 4-
      Attach new container(myDinD) in that container install docker again.
                                                {DOCKER 2 inside DOCKER1}
        # docker exec -it myDinD sh

![Screenshot 2024-02-13 155842](https://github.com/Pratikshinde55/Docker-in-Docker/assets/145910708/6a0d7150-cb53-47a2-974a-5189da2b77e2)

Step 5-
      Here docker installed inside container (check in myDinD)
        #docker info

        ![Screenshot 2024-02-13 160449](https://github.com/Pratikshinde55/Docker-in-Docker/assets/145910708/63f5a542-22d6-459b-92ae-e59003633ebc)

      All docker command run in myDinD that 'Docker inside Docker'
        # docker ps
        # docker images
        # docker pull docker

![Screenshot 2024-02-13 160549](https://github.com/Pratikshinde55/Docker-in-Docker/assets/145910708/de5d86f7-d97a-4682-b0a3-012eedacb2b2)

Step 6-
      We also launch Docker in Containerized docker {DOCKER 3 inside DOCKER 2}
        #docker run -dit --privileged --name myDinD2 docker
        # docker exec -it myDinD2 sh

![Screenshot 2024-02-13 161159](https://github.com/Pratikshinde55/Docker-in-Docker/assets/145910708/03ded95f-78d3-4178-a174-2146ab465d75)

Step 7-
      Here All DinD setup Done
         A.Docker host  (Docker 1)
         B.myDinD container (Docker 2 inside Docker 1)
         C.myDinD2 container (Docker 3 inside Docker 2)

  ![Screenshot 2024-02-13 162357](https://github.com/Pratikshinde55/Docker-in-Docker/assets/145910708/c0dfea90-e5a4-4bf7-aae4-a974d1a839e1)

