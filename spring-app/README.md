- install java
```sudo apt update```
```sudo apt install openjdk-17-jre```
- install jenkins:
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins

- Install docker as agent
- ```sudo apt update```
    ```sudo apt install docker.io```
- Grant jenkins user permissions to docker daemon
 ```sudo su - ```
 ```usermod -aG docker jenkins```
 ```systemctl restart docker```
- execute locally ```java -jar target/spring-boot-web.jar```
- Execute the Maven targets to generate the artifacts ```mvn clean package```
- The docker way:
- build the image ```docker build -t ultimate-cicd-pipeline:v1 .```
- ```docker run -d -p 8010:8080 -t ultimate-cicd-pipeline:v1```
- configuring sonarqube: 

    ```apt install unzip```
    ```adduser sonarqube```
    ```sudo su - sonarqube```
    ```wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.4.0.54424.zip```
    ```unzip *```
    ```chmod -R 755 /home/sonarqube/sonarqube-9.4.0.54424```
    ```chown -R sonarqube:sonarqube /home/sonarqube/sonarqube-9.4.0.54424```
    ```cd sonarqube-9.4.0.54424/bin/linux-x86-64/```
    ```./sonar.sh start```
- access the server on ```http://<ip-address>:9000```