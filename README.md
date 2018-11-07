# How to setup and run minikube with ingress controller


 - sudo apt-get install virtualbox virtualbox-ext-pack curl
 - curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
 - chmod u+x minikube
 - sudo mv -v minikube /usr/local/bin
 - minikube start
 - kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/mandatory.yaml
 - minikube addons enable ingress
