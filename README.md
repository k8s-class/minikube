# minikube
How to setup and run minikube

  Minikube runs a single node Kubernetes cluster inside a linux VM.
        It is for users who want to just test it out or use for development.

            minikube : curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && chmod +x minikube && sudo cp minikube /usr/local/bin/ && rm minikube

            Full :

            curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && chmod +x minikube && sudo cp minikube /usr/local/bin/ && rm minikube
            curl -Lo kubectl https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl && chmod +x kubectl && sudo cp kubectl /usr/local/bin/ && rm kubectl

            export MINIKUBE_WANTUPDATENOTIFICATION=false
            export MINIKUBE_WANTREPORTERRORPROMPT=false
            export MINIKUBE_HOME=$HOME
            export CHANGE_MINIKUBE_NONE_USER=true
            mkdir -p $HOME/.kube
            touch $HOME/.kube/config

            export KUBECONFIG=$HOME/.kube/config
            sudo -E minikube start --vm-driver=none

            # this for loop waits until kubectl can access the api server that Minikube has created
            for i in {1..150}; do # timeout for 5 minutes
               kubectl get po &> /dev/null
               if [ $? -ne 1 ]; then
                  break
              fi
              sleep 2
            done

            Test Minikube :

            kubectl run hello-kubernetes --image=gcr.io/google_containers/echoserver:1.4 --port=8080

            kubectl expose deployment hello-kubernetes --type=NodePort

            kubectl describe service hello-kubernetes

            minikube service hello-kubernetes --url
