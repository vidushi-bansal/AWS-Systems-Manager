# AWS SYSTEMS MANAGER  
It is a group of different capabilities and functionalities which Amazon gives us free of cost. When you have your EC2 instances (Windows or Linux), you are going to do a certain task such as executing a certain shell script that could install a software or update an existing one. AWS Systems Manager can do these kind of things for you. 
  
## Demo  
### Create an IAM role for AWS SSM.  
1. Go to Roles.  
2. Click Create Role.  
3. Select EC2 service and attach AmazonEC2RoleforSSM Role.  
![Policy](https://github.com/vidushi-bansal/AWS-Systems-Manager/blob/main/Policy.png)  
  
### Launch EC2 instances  
1. Launch an EC2 Instance.  
![Launch-1](https://github.com/vidushi-bansal/AWS-Systems-Manager/blob/main/1.png)  
![Launch-2](https://github.com/vidushi-bansal/AWS-Systems-Manager/blob/main/2.png)  
![Launch-3](https://github.com/vidushi-bansal/AWS-Systems-Manager/blob/main/3.png)  
2. Add count to 2.  
![Launch-4](https://github.com/vidushi-bansal/AWS-Systems-Manager/blob/main/4.png)  
3. Give and IAM role to your EC2 instance to let AWS system Manager manage it.  
![ROLE](https://github.com/vidushi-bansal/AWS-Systems-Manager/blob/main/Role.png)  
[NOTE: To let AWS System Manager manage your instance, you need to install AWS SSM agents to your instances as well. With Amazon Linux2 latest images, this agent comes pre-installed]  
4. Launch the instance.  
  
### Apply RUN command  
1. Go to aws SSM console [https://console.aws.amazon.com/systems-manager/].  
2. Choose RUN Command from the console.  
![RUN](https://github.com/vidushi-bansal/AWS-Systems-Manager/blob/main/RUN.png)  
3. Click on Run a Command.  
4. Choose Run command.  
   In the Command document list, choose a Systems Manager document.  
   I am choosing Configure Docker.  
![DOCKER](https://github.com/vidushi-bansal/AWS-Systems-Manager/blob/main/Docker.png)   
5. In the Command parameters section, specify values for required parameters. I choose install parameter.  
![INSTALL](https://github.com/vidushi-bansal/AWS-Systems-Manager/blob/main/Install.png)  
6. In the Targets section, identify the instances on which you want to run this operation by specifying tags, selecting instances manually, or specifying a resource group.  
![TARGET](https://github.com/vidushi-bansal/AWS-Systems-Manager/blob/main/Target.png)  
7. For Other parameters:  
> For Comment, enter information about this command.  
> For Timeout (seconds), specify the number of seconds for the system to wait before failing the overall command execution.  
8. For Rate control:  
> For Concurrency, specify either a number or a percentage of instances on which to run the command at the same time.  
> For Error threshold, specify when to stop running the command on other instances after it fails on either a number or a percentage of instances. For example, if you specify three errors, then Systems Manager stops sending the command when the fourth error is received. Instances still processing the command might also send errors.  
![Rate-Control](https://github.com/vidushi-bansal/AWS-Systems-Manager/blob/main/Rate-control.png)  
9. For Output options, to save the command output to a file, select the Write command output to an S3 bucket box. Enter the bucket and prefix (folder) names in the boxes.  
![S3](https://github.com/vidushi-bansal/AWS-Systems-Manager/blob/main/S3.png)  
10. In the SNS notifications section, if you want notifications sent about the status of the command execution, select the Enable SNS notifications check box.  
11. You can perform the same actions on this page by using the AWS Command Line Interface (CLI) tools.  
![CLI](https://github.com/vidushi-bansal/AWS-Systems-Manager/blob/main/CLI.png)  
11. Choose Run.  
![cmd-status-1](https://github.com/vidushi-bansal/AWS-Systems-Manager/blob/main/cmd-status-1.png)  
![cmd-status-2](https://github.com/vidushi-bansal/AWS-Systems-Manager/blob/main/cmd-status-2.png)  
  
### Lets check and confirm id docker has been installed in the instances or not.  
  
1. ssh into any instance.  
```bash
ssh ec2-user@<IP-Address>  
```
2. Run:   
```bash
sudo docker ps  
```
![Docker-ps](https://github.com/vidushi-bansal/AWS-Systems-Manager/blob/main/docker-ps.png)  
3. Checking the stdout file created in S3:
> Updating yum  
> Installation docker through yum  
> Starting docker service  
> Installation complete  
==========================================================================