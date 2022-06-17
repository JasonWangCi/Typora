```java
Sample commands:
Install the latest LTS version: brew install jenkins-lts
##Install a specific LTS version: brew install jenkins-lts@YOUR_VERSION

  
Start the Jenkins service: brew services start jenkins-lts
Restart the Jenkins service: brew services restart jenkins-lts
Update the Jenkins version: brew upgrade jenkins-lts
```



找到密码：

 sudo cd /Users/jason/.jenkins/secrets

cat initialAdminPassword



Localhost:8080



https://www.jenkins.io/download/lts/macos/





```java
docker run -d  \                                     
--name jk -u root \
-p 9090:8080  \
-v /var/jenkins_home:/var/jenkins_home  \
jenkinsci/blueocean
```





![image-20220616111516367](/Users/jason/Library/Application Support/typora-user-images/image-20220616111516367.png)
