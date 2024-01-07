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

wget -O /home/vagrant/elastic-apm-agent.jar https://repo1.maven.org/maven2/co/elastic/apm/elastic-apm-agent/1.45.0/elastic-apm-agent-1.45.0.jar
 
```
* server-jar command
```
export ELASTIC_APM_APPLICATION_PACKAGES=com.packt.modern.api.*
export ELASTIC_APM_TRACE_METHODS=com.packt.modern.api.*
export ELASTIC_APM_STACK_TRACE_LIMIT=180
export ELASTIC_APM_TRACE_METHODS_DURATION_THRESHOLD=50ms
export ELASTIC_APM_SERVER_URLS=http://localhost:8200
export ELASTIC_APM_SERVICE_NAME=server
java -javaagent:/home/vagrant/elastic-apm-agent.jar -jar  /vagrant/server/target/chapter12-server-0.0.1.jar
```

* client-jar command
```
export ELASTIC_APM_APPLICATION_PACKAGES=com.packt.modern.api.*
export ELASTIC_APM_TRACE_METHODS=com.packt.modern.api.*
export ELASTIC_APM_STACK_TRACE_LIMIT=180
export ELASTIC_APM_TRACE_METHODS_DURATION_THRESHOLD=50ms
export ELASTIC_APM_SERVER_URLS=http://localhost:8200
export ELASTIC_APM_SERVICE_NAME=clinet

java -javaagent:/home/vagrant/elastic-apm-agent.jar -jar  /vagrant/client/target/chapter12-client-0.0.1.jar
```
##### Client Test
```bash
curl http://10.100.198.101:8081/charges
```
1. Open the Kibana home page in the browser : ```http://10.100.198.101:5600/app/home#/```
1. Click on the hamburger menu in the top-left corner. Click on the **Discover** option in the menu .
1. This should open the **Discover** page .If this your first time opening the page, you must **create an index pattern** that will filter out the indexes available in Elasticsearch . 
1. If you are using Kibana **7.x** , the title is "Create index pattern"; otherwise, if you are using Kibana **8.x**, the title is **Create data view** .
1. Here, you should enter the index name (**modern-api**) given in the Logstash configuration in the ELK stack’s Docker Compose file .
1. Here, you can also provide a name for the data view and an index pattern. You can keep the default value of **@timestamp** for **Timestamp field**.
1. Then, click on the **Save data view to Kibana** button.
1. You can add the filter query to the **Search** textbox and the **Date/Duration** menu at the top right of the **Discover** page.
1. Query criteria can be input using the **Kibana Query Language (KQL)**, which allows you to add different comparator and logical operators. For more information, refer to https://www.elastic.co/guide/en/kibana/master/kuery-query.html.


The searched **Discovery** page also shows the graph that shows the number of calls made during a particular period. You can generate more logs and reveal any errors, and then you can use different criteria to filter the results and explore further.

You can also save the searches and perform more operations, such as customizing the dashboard. Please refer to https://www.elastic.co/guide/en/kibana/master/index.html for more information.

1. Open the Zipkin home page in the browser : ```http://10.100.198.101:9411/```
1. Paste the copied trace ID in the **Search by trace ID** textbox in the top-right corner (highlighted in green) and then press *Enter*.


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