# Installation d'un Master :
### Mettre à jour la machine et configurer le fichier /etc/hosts: 
$ apt update / yum update
$ echo "127.0.0.1 `hostname`" >> /etc/hosts

### Récupérer et installer kubectl

curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes release/release/stable.txt)/bin/linux/amd64/kubectl 
chmod +x ./kubectl
mv ./kubectl /usr/local/bin/kubectl

### Récupérer et installer kubeadm
$ git clone https://github.com/data-8/kubeadm-bootstrap
$ ./kubeadm-bootstrap/install-kubeadm.bash

### Finaliser l'installation :
$ sudo -E ./kubeadm-bootstrap/init-master.bash    ( -E pour prendre en compte les vars d'environnement tel qu'un proxy par exemple ! )

# Installation d'un worker :
### Mettre à jour la machine et configurer le fichier /etc/hosts: 
$ apt update / yum update
$ echo "127.0.0.1 `hostname`" >> /etc/hosts
$ echo "@MASTER HostnameMaster" >>  /etc/hosts

### Récupérer et installer kubectl
$ curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
$ chmod +x ./kubectl
$ mv ./kubectl /usr/local/bin/kubectl

### Récupérer et installer kubeadm
$ git clone https://github.com/data-8/kubeadm-bootstrap
$ ./kubeadm-bootstrap/install-kubeadm.bash

# Enregistrement du worker
### Sur le master, générer un token :
$ kubeadm token create --print-join-command
et puis on copie l'output ( la commande retournée ) dans le worker.

### Vérifier le cluster
$ kubectl get nodes
