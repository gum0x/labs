# Vagrant files to load a kubernetes cluster lab

OS: CentOS 7
Last Kubernetes stable 

Please, note this is for testing pourposes. Do not use it in sensitive environments. 

# Start clustr

Go to kube-master
  cd kube-master
  vagrant up

Once kubernetes cluster finish the set up, copy the "join" command printed on the last lines of the output. 

    default: You can now join any number of machines by running the following on each node
    default: as root:
    default:
    default:   kubeadm join 192.168.33.10:6443 --token <TOKEN> --discovery-token-ca-cert-hash sha256:<SHA256>

Now, go to kube-node dir and start the node machine. 
  cd kube-node1
  vagrant up

When node get installed eneter on the node with "vagrant ssh" and get root in order to join the node on the cluster
    sudo su -
    kubeadm join 192.168.33.10:6443 --token <TOKEN> --discovery-token-ca-cert-hash sha256:<SHA256>

Check in the server, node joins correctly. It will take some seconds:
   kubectl get nodes

# Set up kubectl in your desktop to work with the cluster
Copy /etc/kubernetes/admin.conf into your local machine. Each time you ask for kubectl, specify --kubeconfig=<kubeconfig file>

You can declare a temporal alias to make it easy to work with the lab.
alias kubectl="kubectl --kubeconfig=/tmp/kubeconfig"




