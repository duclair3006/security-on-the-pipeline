# security-on-the-pipeline

########  Securing a pipeline

continue scan the code for vulnerabilty:
       - sonarqube 
       - gitlab scanner
       - gitOps action scanner
       
       
Docker images:
      Dockerfile:
         - never use latest images tag 
         - do not use ADD to remotely download package 
         - make sure all files or directories that are copied into the docker
           images goes through a secure scanning server
         - do not run images inside the container as root to solve such issue since
           root are default user for container add USER 1000 or USER 999 to you
             dockerfile.
         - Do not called or use images in your dockerfile that are not approved 
           by the securuty team
         - Do not called or use images in your dockerfile that did not pass the security scan 
         

      
      harden images:
            - prebuild images from Harbor
      
      continue scan of the images:
             - docker scan 
             - harbor 
             - Snyk
             - gitOps
             

Pipeline:
   Jenkins:
     - use jenkins security to limit project accesssiblity
     - All on demand containers used by jenkins should have approve base images 
     - All jenkins agent most be secure or pass the security test 
     - All jenkins agent must be only accessible by the user jenkins
     - if using on demand VM as jenkins agent make sure the provider image has been scanned 
       and has passed all security test.
     -  never use a public AMI for exampel images as jenkins agent on the pipeline.
     - all secret involve on the pipeline must be placed and secure on a vault server


    Image repository:
      - on use private repository 
      - use private docker host repository such as nexus

    kubernetes:
      - All service type of the application must be ClusterIP only 
      - use RBAC to limit and manage user access to the cluster
      - Do not share the kubeconfig file to any user accessing the cluster but 
          instead give them access via a secure bastion server.
      - enable key rotation to your K8S cluster
      - place  a secure (with ssl) loadBalancer or ingress controller in front of all application service
      - user should never have access directly to any  service inside the cluster
      - use bitnamie seal secret to manage all your application secret
      - use PodSecurityPolicy to dictate what type of pod should be deploy on the cluster
      
      
      
Application Access:
     -  only allow application accessiblity through a secure DNS with ssl enable.

VIrtual Machine:
  - always scan all virtual machines involving application with software such as tenable
