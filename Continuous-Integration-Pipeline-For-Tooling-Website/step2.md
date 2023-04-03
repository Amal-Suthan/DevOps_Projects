# INSTALL AND CONFIGURE JENKINS SERVER

Step 1 – Install Jenkins server

1. Create an AWS EC2 server based on Ubuntu Server 20.04 LTS and name it "Jenkins"

2. Install JDK (since Jenkins is a Java-based application)

```
sudo apt update
sudo apt install default-jdk-headless
```

3. Install Jenkins

```
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > \
    /etc/apt/sources.list.d/jenkins.list'
sudo apt update
sudo apt-get install jenkins
```

Make sure Jenkins is up and running

```
sudo systemctl status jenkins
```

4. By default Jenkins server uses TCP port 8080 – open it by creating a new Inbound Rule in your EC2 Security Group

![project-9-2](https://user-images.githubusercontent.com/64862440/229538605-3996aa0a-a316-4eb9-ab22-5f288c702818.png)


5. Perform initial Jenkins setup.
From your browser access http://<Jenkins-Server-Public-IP-Address-or-Public-DNS-Name>:8080

You will be prompted to provide a default admin password

  
![project-9-3](https://user-images.githubusercontent.com/64862440/229539156-59e41130-dbed-4bc5-82cf-8988091dff33.png)

  
Retrieve it from your server:
  
```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
  
Then you will be asked which plugings to install – choose suggested plugins.
 

![project-9-4](https://user-images.githubusercontent.com/64862440/229539329-a02bfe0b-a1f9-4114-afe9-97e8ef9957ca.png)

  
Once plugins installation is done – create an admin user and you will get your Jenkins server address.

The installation is completed!
  

![project-9-5](https://user-images.githubusercontent.com/64862440/229539425-8ddb06c5-de14-4a98-9a2a-62ad8f90a3ab.png)
  

Step 2 – Configure Jenkins to retrieve source codes from GitHub using Webhooks
In this part, you will learn how to configure a simple Jenkins job/project (these two terms can be used interchangeably). This job 
will will be triggered by GitHub webhooks and will execute a ‘build’ task to retrieve codes from GitHub and store it locally on 
Jenkins server.

1. Enable webhooks in your GitHub repository settings
  
  
![project-9-6](https://user-images.githubusercontent.com/64862440/229539542-e380a129-197b-4713-bad8-5be9eb0ca2a6.png)

  
![project-9-7](https://user-images.githubusercontent.com/64862440/229539629-3934029e-303f-4b68-9ea0-49f265822350.png)

  
2. Go to Jenkins web console, click "New Item" and create a "Freestyle project"
  

![project-9-8](https://user-images.githubusercontent.com/64862440/229539726-70bfc8cd-a21d-40d4-8a42-1dbd6cd1b372.png)

  
To connect your GitHub repository, you will need to provide its URL, you can copy from the repository itself
  
  
![project-9-9](https://user-images.githubusercontent.com/64862440/229539802-c52144e6-ccfd-4b92-99a8-29387acf9446.png)

  
In configuration of your Jenkins freestyle project choose Git repository, provide there the link to your Tooling GitHub repository 
and credentials (user/password) so Jenkins could access files in the repository.


![project-9-10](https://user-images.githubusercontent.com/64862440/229539896-61bde822-05b5-4078-acff-5d9cab100c67.png)

  
  
Save the configuration and let us try to run the build. For now we can only do it manually.
Click "Build Now" button, if you have configured everything correctly, the build will be successfull and you will see it under #1
  
  
![project-9-11](https://user-images.githubusercontent.com/64862440/229539978-27a08921-0048-4082-9e67-938a5cde075c.png)

  
You can open the build and check in "Console Output" if it has run successfully.

If so – congratulations! You have just made your very first Jenkins build!

But this build does not produce anything and it runs only when we trigger it manually. Let us fix it.

3. Click "Configure" your job/project and add these two configurations
Configure triggering the job from GitHub webhook:

  
![project-9-12](https://user-images.githubusercontent.com/64862440/229540153-a2b28d2a-e54c-4a0b-836b-2df30b132893.png)

Configure "Post-build Actions" to archive all the files – files resulted from a build are called "artifacts".
  

![project-9-13](https://user-images.githubusercontent.com/64862440/229540252-f3012add-2399-4e9f-8757-456e2b07d1fb.png)

  
Now, go ahead and make some change in any file in your GitHub repository (e.g. README.MD file) and push the changes to the master branch.

You will see that a new build has been launched automatically (by webhook) and you can see its results – artifacts, saved on Jenkins
server.


![project-9-14](https://user-images.githubusercontent.com/64862440/229540360-218317d5-64e8-4908-85b9-228a0c971da9.png)

  
You have now configured an automated Jenkins job that receives files from GitHub by webhook trigger (this method is considered as
‘push’ because the changes are being ‘pushed’ and files transfer is initiated by GitHub). There are also other methods: trigger one 
job (downstreadm) from another (upstream), poll GitHub periodically and others.

By default, the artifacts are stored on Jenkins server locally

  
```
ls /var/lib/jenkins/jobs/tooling_github/builds/<build_number>/archive/
```
