# Multiverse-application
  In this project we are going to use the below list of tools.

1. Gitlab -- source code Management tool.
2. Terraform  - (Infrastructure as a code) provisions infrastructure in AWS cloud.
3. Ansible - (configuration management tool) Configure Gitlab runner and also install docker and nginx on nodes
4. S3 Bucket - To store terraform state file
5. NFS server - To store logs on multiple containers.
6. AWS container Registry - To store Docker images.

Step 1:  Create 3 repositories in Gitlab where one repo for project code, one for terraform scripts and another for ansible scripts.
Step 2: Create a jump server in AWS and install terraform and ansible in the jumphost. 
Step 3:  Clone the terraform and ansible repos in the jumphost.
Step 4: create IAM role with all required permissions to create infra in AWS as well as to connect to s3 bucket and AWS container registry, and attach to the jumphost.
step 5: Run the terraform scripts which creates VPC, Public subnets, private subnets, Internet gateway, Nat gateway and security groups and RDS. Also creates EC2 instances in the public subnet and RDS in private subnets.
Step 6:  Create ssh keys in jumphost and add those ssh keys in authorizeds_keys in newly created ec2 instances. This is for ansible communication with the nodes.
Step 7: Add the EC2 instances ip addresses in the Ansible inventory and execute ansible playbook which configure Gitlab-runners with tags, install docker and also based on requirement install nginx.
Step 8: Create pipelines in Gitlab by specifying various stages in gitlab-ci.yaml file and specify tags.
Step 9: We can configure auto-deploy for dev, uat and preprod environment, which triggers pipeline once we commit changes to specific branch.
Step 10: Its best practice to trigger pipelines manually from gitlab console for prod deployment.
Step 11: once we trigger pipeline, the code will build in respective gitlab-runner instances and push the docker images to the container registry and deploy the application with this image. In the pipeline we can add additional shell scripts to check service status post deployment.


<img width="1747" alt="Screenshot 2021-06-27 at 1 04 48 PM" src="https://user-images.githubusercontent.com/71361741/123570713-ce3b6f80-d796-11eb-914d-8217f5a637e4.png">
