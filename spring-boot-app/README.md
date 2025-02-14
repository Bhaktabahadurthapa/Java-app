# Spring Boot based Java web application
 
This is a simple Sprint Boot based Java application that can be built using Maven. Sprint Boot dependencies are handled using the pom.xml 
at the root directory of the repository.

This is a MVC architecture based application where controller returns a page with title and message attributes to the view.

## Execute the application locally and access it using your browser

Checkout the repo and move to the directory

```
git clone https://github.com/Bhaktabahadurthapa/Java-app
cd spring-boot-app/JenkinsFile
```

Execute the Maven targets to generate the artifacts

```
mvn clean package
```

The above maven target stroes the artifacts to the `target` directory. You can either execute the artifact on your local machine
(or) run it as a Docker container.

** Note: To avoid issues with local setup, Java versions and other dependencies, I would recommend the docker way. **


### Execute locally (Java 11 needed) and access the application on http://localhost:8080

```
java -jar target/spring-boot-web.jar
```

### The Docker way

Build the Docker Image

```
docker build -t ultimate-cicd-pipeline:v1 .
```

```
docker run -d -p 8010:8080 -t ultimate-cicd-pipeline:v1
```

Hurray !! Access the application on `http://<ip-address>:8010`


## Next Steps

### Configure a Sonar Server locally

```
apt install unzip
adduser sonarqube
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.4.0.54424.zip
unzip *
chmod -R 755 /home/sonarqube/sonarqube-9.4.0.54424
chown -R sonarqube:sonarqube /home/sonarqube/sonarqube-9.4.0.54424
cd sonarqube-9.4.0.54424/bin/linux-x86-64/
./sonar.sh start
```
Hurray !! Now you can access the `SonarQube Server` on `http://<ip-address>:9000`

### Install Docker
```
sudo apt update
sudo apt install docker.io
```
### Grant Jenkins user and Ubuntu user permission to docker deamon.
```
sudo su - 
usermod -aG docker jenkins
usermod -aG docker ubuntu
systemctl restart docker
```
Once you are done with the above steps, it is better to restart Jenkins.
http://<ec2-instance-public-ip>:8080/restart


### jenkins slowness issue sloved by change the IP address
```
cd /var/lib/jenkins/
sudo nano jenkins.model.JenkinsLocationConfiguration.xml
sudo systemctl restart jenkins
sudo systemctl enable jenkins

```
then change the NEW EC2 instance IP address.

 ### Minikube start 
 ```
  minikube start
  minikube start --memory=2900 --driver=docker
 ```
### Debian/Ubuntu (Official) for Installing **Trivy**
```
sudo apt-get install wget apt-transport-https gnupg
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | gpg --dearmor | sudo tee /usr/share/keyrings/trivy.gpg > /dev/null
echo "deb [signed-by=/usr/share/keyrings/trivy.gpg] https://aquasecurity.github.io/trivy-repo/deb generic main" | sudo tee -a /etc/apt/sources.list.d/trivy.list
sudo apt-get update
sudo apt-get install trivy

To remove old Docker images:
docker image prune -a
docker container prune
<<<< To output the scan results in a table: >>>>
trivy image --format table <Image_Name>
```
#### Github and Git
```
git init
git add .
git status
git commit -m "v1 chnage"
or git remote add origin https://github.com/OWNER/REPOSITORY.git  
git push origin main --force 
```

### ArgoCD cluster install and link: https://operatorhub.io/operator/argocd-operator
```
minikube start
minikube start --memory=2900 --driver=docker or hyperkit
kubectl get pods -n argocd
kubectl get svc -n argocd
kubectl edit svc argocd-server -n argocd    < change NodePort>
minikube service argocd-server -n argocd
kubectl get secret -n argocd
kubectl edit secret argocd-initial-admin-secret -n argocd
echo U2UxekNkVEVlZlNNeC10VQ== | base64 -d

```
### Expose the deployment k8s 
```
kubectl get deploy
minikube service deploy_name
kubectl get nodes -o wide
kubectl get svc

```




