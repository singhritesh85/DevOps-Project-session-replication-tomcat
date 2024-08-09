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

Here I have used session replication in EC2 Instances with StaticMembership rather than Multicast. The Jenkinsfile which I have used for CI/CD deployment is availabe with this Repository.  

Create the database jwt and table USER in MySQL as shown in the screenshot below before running the Jenkins Job.
![image](https://github.com/user-attachments/assets/934fd984-31c6-4269-9b3b-7b0435f252d8)
![image](https://github.com/user-attachments/assets/7b30172d-398b-417c-8407-c0a2be0e6417)
![image](https://github.com/user-attachments/assets/ab32e127-cc2d-431c-8b56-342cb6fb45a3)

After running the Jenkins Job the screenshot for SonarQube, Nexus Artifactory and entry inside the database jwt's USER table is as shown below.

![image](https://github.com/user-attachments/assets/f9a57bc5-d791-4058-8864-778de0642e65)
![image](https://github.com/user-attachments/assets/b12874d8-7c6b-404d-8aee-fa3f625d100b)
![image](https://github.com/user-attachments/assets/ec26bce2-4bf1-4cc2-84e1-1d882d3e1fed)

To run the Jenkins Job successfully webhook had been created in SonarQube and modified the /etc/resolv.conf file on SonarQube and on Jenkins Slave Node as shown in the screenshot below (You can also achieve this by creating a new DHCP option set, I had already discussed regarding this in earlier project You can refer https://github.com/singhritesh85/DevOps-Project-2tier-WebApp-Deployment/blob/main/Complications-which-you-may-face/complications.md ).
![image](https://github.com/user-attachments/assets/1bfaf933-1e58-491b-b8c7-81b6de0fefe9)
![image](https://github.com/user-attachments/assets/367fff64-ffaf-4490-81e8-1c15f1213280)
![image](https://github.com/user-attachments/assets/a28d96ce-b089-49a2-8190-95f414dfac22)

The entry for Route53 to create the record set in hosted zone is as shown below.
![image](https://github.com/user-attachments/assets/531b471a-4e06-4ef6-8bad-b3240ff7fa95)

Finally access the newly created URL as shown in the screenshot below.
![image](https://github.com/user-attachments/assets/e14b5df5-948b-4f97-9a81-3608e9cc6492)
![image](https://github.com/user-attachments/assets/7683fac5-2fa1-4543-a769-7f0ae1d1faf5)
![image](https://github.com/user-attachments/assets/01097504-7428-4a5b-bd29-10bd505b66c8)

Now open the Tomcat Manager as shown in the screenshot below and be asured about the session replication.
![image](https://github.com/user-attachments/assets/47c4554e-c05b-4f99-b1af-aa4384c4bdc8)
![image](https://github.com/user-attachments/assets/d855b518-3481-4dd8-be9f-c9d07353aea6)
![image](https://github.com/user-attachments/assets/893d5cd4-03c8-4bd5-b01d-fe01ee45d353)
![image](https://github.com/user-attachments/assets/b9778f87-1cde-44b1-a7e9-b0561b1d58ea)
<br><br/>
<br><br/>
<br><br/>
<br><br/>
<br><br/>
```
Source Code:- https://github.com/singhritesh85/tomcat-session-replication.git 
```
<br><br/>
<br><br/>
<br><br/>
<br><br/>
<br><br/>
```
References

https://ashok198510.hashnode.dev/cloud-native-two-tier-application-deployment-with-eks-tomcat-and-rds-in-aws
https://github.com/Ashoksana/aws-rds-java.git
https://tomcat.apache.org/tomcat-8.5-doc/cluster-howto.html
```
