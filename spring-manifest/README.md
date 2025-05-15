Continuous Delivery(CD)
- Install docker
- ```sudo apt update && sudo apt install docker.io -y```

- Grant ubuntu user access to docker
- ```sudo usermod -aG docker ubuntu```

- Install kubectl
 ```curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

      sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl

      chmod +x kubectl
      mkdir -p ~/.local/bin
      mv ./kubectl ~/.local/bin/kubectl
  ```

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
  ``` kubectl get secrets -n argocd
      kubectl edit secret argocd-initial-admin-secret -n argocd
      echo aE1tSDEzckotQkFmRHZsLQ== | base64 --decode
  ```

Hurray! The ArgoCD UI is here with you!!!!

Accessing the service
- Run ```kubectl port-forward svc/bericks-service 8000:80 --address 0.0.0.0```
- Ensure you open port 8000 and then copy the instance ip address then you can access from your browser!!!!!


