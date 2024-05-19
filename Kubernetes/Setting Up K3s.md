## 1. Setting Up Debian Hosts
This is pretty simple. Just set the following information as such:
```
Hostname: ControlPlane1 or WorkerNode1 or K3sDatastore or K3sLoadBalancer
User: david
```

Make sure you enable the ssh server and run 
```bash
sudo usermod -aG sudo david
```
to add the david user to the sudo group. Once you log into the machines, make sure they are updated.

## 2. Setting Up The Database Servers
## 3. Setting Up The Load Balancer