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
sudo apt-get install jenkins -y

- Install docker as agent
- ```sudo apt update```
    ```sudo apt install docker.io -y```
- Grant jenkins and ubuntu user permissions to docker daemon
 ```sudo su - ```
 ```usermod -aG docker jenkins```
 ```usermod -aG docker ubuntu```
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
- Install docker pipeline, SonarQube scanner
- To integrate sonar with jenkins we'll setup the cred.
- Click on > My Account > Security > Give a token name and > Generate > Copy the token.
- Go back to Jenkins Dashboard under credentials add the secret with secret text kind and id as sonarqube

Role of SonarQube
- Ensuring code quality, security. It detects bugs, enforces cooding standards, measures code coverage, identifies code smells and improves maintainability.

Continuous Delivery(CD)
- Install docker
- ```sudo apt update && sudo apt install docker.io -y```

- Grant ubuntu user access to docker
- ```sudo usermod -aG docker ubuntu```

- Install kubectl
- ```curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"```

- ```sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl```

- ```chmod +x kubectl```
- ```mkdir -p ~/.local/bin```
- ```mv ./kubectl ~/.local/bin/kubectl```

- Install Kind from the official docs.
- Create a cluster ```kind create cluster --name=erics```
- Verify the cluster is created ```kind get clusters```
- To delete a cluster ```kind delete cluster --name=erics```
- Context ```kubectl config get-contexts```
- To get the nodes ```kubectl get nodes```

Install ArgoCD from the official docs
- Verify the pods creation ```kubectl get pods -n argocd``` or to watch while they are being created```kubectl get pods -n argocd -w```.
- Port forwading ```kubectl port-forward svc/argocd-server -n argocd 8080:443 --address 0.0.0.0```.
- Proceed to the argo UI the username is ```admin``` by default then the password you have to get it by:
  - ```kubectl get secrets -n argocd```
  - ```kubectl edit secret argocd-initial-admin-secret -n argocd```
  - ```echo aE1tSDEzckotQkFmRHZsLQ== | base64 --decode```

Hurray! The ArgoCD UI is here with you!!!!


