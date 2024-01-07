# Chapter 12 Adding Logging and Tracing to Services
## Sample codes Execuion Environment
### Docker
```bash
docker compose pull
docker compose up -d
docker compose ps
docker compose logs
docker compose logs -f
docker compose down

```
### Podman Machine
#### If Your OS Is Windows
##### Install WSL2
```bash
wsl --install --no-distribution

// Wait for about 15 minutes

wsl --version
WSL version： 2.0.9.0
kernel version： 5.15.133.1-1
WSLg version： 1.0.59
MSRDC version： 1.2.4677
Direct3D version： 1.611.1-81528511
DXCore version： 10.0.25131.1002-220531-1700.rs-onecore-base2-hyp
Windows version： 10.0.19045.3803
```
If you encounter troubles, refer -> https://learn.microsoft.com/zh-tw/windows/wsl/install-manual
###### prepared script in Powershell
```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```
#### Podman Operation
* Reference
https://github.com/containers/podman/blob/main/docs/tutorials/podman-for-windows.md

###### Basic Command
* Create podman VM                 
```bash
 podman machine init
```
* Start podman VM                 
```bash
 podman machine start
```

* Stop podman VM                 
```bash
 podman machine stop
```
* Remove podman VM                 
```bash
 podman machine rm 
```
* Enter podman VM                 
```bash
podman machine ssh
ifconfig
yum install htop
yum install nmon
df -H
docker compose pull
docker compose up -d
```
### Vagrant
* Create /Start VM                 
```bash
 vagrant up
``` 
* Stop VM                 
```bash
 vagrant halt
```
* Remove VM                 
```bash
 vagrant destroy
```
* Enter VM                 
```bash
 vagrant ssh 
 df -H
// sudo apt install -y openjdk-17-jdk curl wget jq maven
cd /vagrant

docker compose pull
docker compose up -d
docker compose ps
docker compose logs
docker compose logs -f
docker compose down

wget -O elastic-apm-agent-1.43.0.jar https://repo1.maven.org/maven2/co/elastic/apm/elastic-apm-agent/1.43.0/elastic-apm-agent-1.43.0.jar  -P /~
 
```
* server-jar command
```
export ELASTIC_APM_APPLICATION_PACKAGES=com.packt.modern.api.*
export ELASTIC_APM_TRACE_METHODS=com.packt.modern.api.*
export ELASTIC_APM_STACK_TRACE_LIMIT=180
export ELASTIC_APM_TRACE_METHODS_DURATION_THRESHOLD=50ms
export ELASTIC_APM_SERVER_URLS=http://localhost:8200
export ELASTIC_APM_SERVICE_NAME=server
java -javaagent:/home/vagrant/elastic-apm-agent-1.43.0.jar -jar  /vagrant/server/target/chapter12-server-0.0.1.jar
```

* client-jar command
```
export ELASTIC_APM_APPLICATION_PACKAGES=com.packt.modern.api.*
export ELASTIC_APM_TRACE_METHODS=com.packt.modern.api.*
export ELASTIC_APM_STACK_TRACE_LIMIT=180
export ELASTIC_APM_TRACE_METHODS_DURATION_THRESHOLD=50ms
export ELASTIC_APM_SERVER_URLS=http://localhost:8200
export ELASTIC_APM_SERVICE_NAME=clinet

java -javaagent:/home/vagrant/elastic-apm-agent-1.43.0.jar -jar  /vagrant/client/target/chapter12-client-0.0.1.jar
```
##### Client Test
```bash
curl http://10.100.198.101:8081/charges
```
## Common Issues
### Fix “Why I can not ssh to my Vagrant host? vagrant@master: Permission denied (publickey)”
* Solution:
  * If you have no publickey
    ```bash
    $ ssh-keygen -t rsa -b 4096
    ```
  * Modify Vagrantfile
    ```
      Vagrant.configure("2") do |config|
        config.vm.box = "debian/bullseye64"
        
        config.ssh.insert_key = false
        config.ssh.private_key_path = ['~/.vagrant.d/insecure_private_key', '~/.ssh/id_rsa']
        config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/authorized_keys"

        config.vm.provider "virtualbox" do |vb|
          vb.memory = 2048
          vb.cpus = 2
        end
    ```  
### Fix “Too long: must have at most 262144 bytes”
* Solution:  ``kubectl apply -f xyz --server-side``
* scenarios:
  * [In ArgoCD](https://foxutech.medium.com/how-to-fix-too-long-must-have-at-most-262144-bytes-in-argocd-2a00cddbbe99)
  * [In kube-prometheus](https://blog.ediri.io/kube-prometheus-stack-and-argocd-25-server-side-apply-to-the-rescue)
* Server-Side Apply (SSA) has been generally available in Kubernetes [since the v1.22 release](https://kubernetes.io/blog/2021/08/06/server-side-apply-ga/) in August 2021.  