# DevOps-Project-session-replication-tomcat

![image](https://github.com/user-attachments/assets/ff20b0ea-1baa-49bc-aebd-e97e0717f01a)

**Session Replication** comes into the picture when same application runs on two servers and they access the same session information.
<br><br/>
In this demonstration I used terraform to launch two EC2 Instances and an Application LoadBalancer. In order to Install Tomcat and configure session replication I have used Ansible. As shown in the Architecture diagram above the source code is present in the GitHub Repository https://github.com/singhritesh85/tomcat-session-replication.git. Jenkins is used as a CI/CD tool, for code analysis SonaQube has been used and Maven is the build tool. Nexus Artifactory has been used to store the Artifacts. Finally the war file will be deployed in the Tomcat Server.
<br><br/>
```
The source code web.xml must keep <distriburable/> as show in the screenshot below.
```
![image](https://github.com/user-attachments/assets/8790f50a-47a5-4ac4-a2d3-b01749b3383b)

Here I have used session replication in EC2 Instances with StaticMembership rather than Multicast. 
