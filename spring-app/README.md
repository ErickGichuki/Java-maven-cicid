- execute locally ```java -jar target/spring-boot-web.jar```
- Execute the Maven targets to generate the artifacts ```mvn clean package```
- The docker way:
- build the image ```docker build -t ultimate-cicd-pipeline:v1 .```
- ```docker run -d -p 8010:8080 -t ultimate-cicd-pipeline:v1```
- configuring sonarqube: 

    ```apt install unzip```
    ```adduser sonarqube```
    ```wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.4.0.54424.zip```
    ```unzip *```
    ```chmod -R 755 /home/sonarqube/sonarqube-9.4.0.54424```
    ```chown -R sonarqube:sonarqube /home/sonarqube/sonarqube-9.4.0.54424```
    ```cd sonarqube-9.4.0.54424/bin/linux-x86-64/```
    ```./sonar.sh start```
- access the server on ```http://<ip-address>:9000```