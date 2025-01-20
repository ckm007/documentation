# eSignet and Dependencies Deployment in Kubernetes cluster

## Overview

eSignet and its dependent services are deployed as microservices within a Kubernetes (K8s) cluster. This architecture leverages [Wireguard](https://www.wireguard.com/) for establishing a secure, trusted network extension to access the observation plane and privately accessible backend services.

Nginx is utilized by eSignet for the following purposes:

  * SSL termination: Handles SSL/TLS encryption and decryption to secure client-server communication.
  * Reverse Proxy: Acts as an intermediary to forward client requests to backend servers
  * CDN/Cache management: Optimizes content delivery and improves response times by caching resources.
  * Loadbalancing: Distributes incoming traffic across multiple servers to ensure high availability and performance.


The Kubernetes cluster is created and managed using [Rancher](https://rancher.com/docs/rancher/v1.3/en/kubernetes/#rancher-ui) and [rke](https://www.rancher.com/products/rke) tools.

In the reference implementation (ref-impl) of the eSignet deployment, two Kubernetes clusters are required to ensure optimal security and scalability:


## 1. One K8 cluster for observation plane:

This cluster is part of the observation plane, facilitating administrative tasks. It is intentionally kept independent of the primary cluster for enhanced security and clear segregation of roles and responsibilities.

### Key Characteristics:

* Isolation: Designed to remain internal and inaccessible to the external world as a best practice.
* Administrative Services: This cluster hosts critical services required for cluster management and monitoring.

### Components in the Observation Plane Cluster:

* Rancher: Used to manage the eSignet cluster.
* Keycloak: Provides user access management for the cluster.
* Monitoring: Log and network monitoring should be configured to ensure visibility and security.
* Container Registry (if applicable): An internal container registry can be hosted here for managing container images.

## 2. One K8 cluster for eSignet and its dependent services deployment:

This cluster runs all the eSignet and its dependent components and certain third party components to secure the cluster, API’s and data.

### Key Features:

* Comprehensive Deployment: All eSignet-related services and pre-requisites are deployed in this cluster.
* Cluster Security: Includes tools and configurations to secure the cluster environment.


### Components in the eSignet Cluster:

1. Cluster Configuration Tools:

* Istio (Service Mesh)
* NFS CSI (Container Storage Interface)
* Monitoring and Logging tools (e.g., Prometheus, Grafana, Fluentd).

2. eSignet Pre-Requisite Services: Services required for the initial setup and functioning of eSignet.
3. eSignet and Dependent Services: Core eSignet microservices and their dependencies.


## Architecture [TODO]

Architecture Diagram to be updated.


## Deployment Repos
* [k8s-infra](https://github.com/mosip/k8s-infra/tree/v1.2.0.1) : contains the scripts to install and configure Kubernetes cluster with required monitoring, logging and alerting tools.
* [eSignet](https://github.com/mosip/esignet/blob/release-1.5.x/) : Contains deployment scripts and source code for :
  * eSignet Pre-requisites services.
  * eSignet services.
  * eSignet Onboarding.
  * eSignet Api-testrig.
* [esignet-mock-services](https://github.com/mosip/esignet-mock-services/blob/release-0.10.x/) : Contains deployment script and source code for :
  * eSignet mock pre-requisites services.
  * eSignet mock services.
  * eSignet mock services onboarding.
* [esignet-signup](https://github.com/mosip/esignet-signup/tree/release-1.1.x) : Contains deployment script and source code for:
  * eSignet signup pre-requisites.
  * eSignet signup services.
  * eSignet signup onboarding pre-requisites.
  * eSignet signup onboarding.


## Pre-requisites:

Ensure all required hardware and software dependencies are prepared before proceeding with the installation.

### Hardware requirements:

* Virtual Machines (VMs) can use any operating system as per convenience.
* For this installation guide, Ubuntu OS is referenced throughout.


| Sl no. | Purpose                                                 | vCPU's | RAM   | Storage (HDD) | no. of VM's | HA                               |
| ------ | ------------------------------------------------------- | ------ | ----- | ------------- | ---------- | -------------------------------- |
| 1.     | Wireguard Bastion Host                                  | 2      | 4 GB  | 8 GB          | 1          | (ensure to setup active-passive) |
| 2.     | Observation Cluster nodes                               | 2      | 8 GB  | 32 GB         | 2          | 2                                |
| 3.     | Observation Nginx server (use Loadbalancer if required) | 2      | 4 GB  | 16 GB         | 1          | Nginx+                           |
| 4.     | eSignet Cluster nodes                                   | 8      | 32 GB | 128 GB        | 3          | Allocate etcd, control plane and worker accordingly |
| 5.     | eSignet Nginx server ( use Loadbalancer if required)    | 2      | 4 GB  | 16 GB         | 1          | Nginx+                           |


### Network Requirements:

* All the VM's should be able to communicate with each other.
* Need stable Intra network connectivity between these VM's.
* All the VM's should have stable internet connectivity for docker image download (in case of local setup ensure to have a locally accessible docker registry).
* Server Interface requirement as mentioned in below table:


| Sl no. | Purpose                  | Network Interfaces                                                                                                                                                                                                                                                                               |
| ------ | ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1.     | Wireguard Bastion Host   | *One Private interface*: that is on the same network as all the rest of nodes (e.g.: inside local NAT Network).<br><br>*One public interface*: Either has a direct public IP, or a firewall NAT (global address) rule that forwards traffic on 51820/udp port to this interface IP.                 |
| 2.     | K8 Cluster nodes         | One internal interface: with internet access and that is on the same network as all the rest of nodes (e.g.: inside local NAT Network).                                                                                                                                                        |
| 3.     | Observation Nginx server | One internal interface: with internet access and that is on the same network as all the rest of nodes (e.g.: inside local NAT Network).                                                                                                                                                        |
| 4.     | eSignet Nginx server     | *One internal interface*: that is on the same network as all the rest of nodes (e.g.: inside local NAT Network).<br><br>*One public interface*: Either has a direct public IP, or a firewall NAT (global address) rule that forwards traffic on 443/tcp port to this interface IP.                  |

### DNS requirements (TODO)

|    | Domain Name                  | Mapping details                                                     | Purpose                                                                                                                                                                                                                                           |
| -- | ---------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1. | rancher.xyz.net              | Private IP of Nginx server or load balancer for Observation cluster | Rancher dashboard to monitor and manage the kubernetes cluster.                                                                                                                                                                               |
| 2. | keycloak.xyz.net             | Private IP of Nginx server for Observation cluster                  | Administrative IAM tool (keycloak). This is for the kubernetes administration.                                                                                                                                                                        |
| 3. | sandbox.xyx.net              | Private IP of Nginx server for MOSIP cluster                        | Index page for links to different dashboards of MOSIP env. (This is just for reference, please do not expose this page in a real production or UAT environment)                                                                                   |
| 4. | api-internal.sandbox.xyz.net | Private IP of Nginx server for MOSIP cluster                        | Internal API’s are exposed through this domain. They are accessible privately over wireguard channel                                                                                                                                              |
| 5. | api.sandbox.xyx.net          | Public IP of Nginx server for MOSIP cluster                         | All the API’s that are publically usable are exposed using this domain.                                                                                                                                                                        |
| 6. | kibana.sandbox.xyx.net       | Private IP of Nginx server for MOSIP cluster                        | Optional installation. Used to access kibana dashboard over wireguard.                                                                                                                                                                         |
| 7. | kafka.sandbox.xyz.net        | Private IP of Nginx server for MOSIP cluster                        | Kafka UI is installed as part of the MOSIP’s default installation. We can access kafka UI over wireguard. Mostly used for administrative needs.                                                                                                |
| 8. | iam.sandbox.xyz.net          | Private IP of Nginx server for MOSIP cluster                        | MOSIP uses an OpenID Connect server to limit and manage access across all the services. The default installation comes with Keycloak. This domain is used to access the keycloak server over wireguard                                             |
| 9. | postgres.sandbox.xyz.net     | Private IP of Nginx server for MOSIP cluster                        | This domain points to the postgres server. You can connect to postgres via port forwarding over wireguard                                                                                                                                            |
| 10. | onboarder.sandbox.xyz.net    | Private IP of Nginx server for MOSIP cluster                        | Accessing reports of MOSIP partner onboarding over wireguard                                                                                                                                                                                         |
| 11. | eSignet.sandbox.xyz.net    | Public IP of Nginx server for MOSIP cluster                           | Accessing eSignet portal publically                                                                                                                                                                                         |
| 12. | healthservices.sandbox.xyz.net    | Public IP of Nginx server for MOSIP cluster                    | Accessing Health portal publically                                                                                                                                                                                         |
| 13. | smtp.sandbox.xyz.net         | Private IP of Nginx server for MOSIP cluster                        | Accessing mock-smtp UI over wireguard                                                                                                                                                                                                                 |

### Certificate requirements:

As only secured https connections are allowed via nginx server will need below mentioned valid ssl certificates:
* One valid wildcard ssl certificate related to domain used for accessing Observation cluster, this needs to be stored inside the nginx server VM for Observation cluster. In above e.g.: \*.org.net is the similiar example domain.
* One valid wildcard ssl certificate related to domain used for accesing eSignet K8 cluster, this needs to be stored inside the nginx server VM for eSignet cluster. In above e.g.: \*.sandbox.xyz.net is the similiar example domain.

### Tools to be installed on Personal Computers:

Follow the steps mentioned [here](https://github.com/mosip/k8s-infra/tree/v1.2.0.2/mosip/on-prem#prerequisites) to install the required tools in you personel computer to create and manage k8 cluster using RKE1.


## Installation:

Step-by-step guide to set up and configure the required components for secure and efficient operations.

### Wireguard:

Secure access solution that establishes private channels to Observation and eSignet clusters.

_If you already have a Wireguard bastion host then you may skip this step._

* A Wireguard bastion host (Wireguard server) provides secure private channel to access Observation and eSignet cluster.
* The host restricts public access, and enables access to only those clients who have their public key listed in Wireguard server.
* Wireguard listens on UDP port51820.

### Setup Wireguard Bastion server:

1. Create a Wireguard server VM with above mentioned Hardware and Network requirements.

2. Open ports and Install docker on Wireguard VM.

  *   create copy of `hosts.ini.sample` as `hosts.ini` and update the required details for wireguard VM
      `cp hosts.ini.sample hosts.ini`
  *   execute ports.yml to enable ports on VM level using ufw:
      `ansible-playbook -i hosts.ini ports.yaml`

> Note: 
> * Permission of the pem files to access nodes should have 400 permission. `sudo chmod 400 ~/.ssh/privkey.pem`
> * These ports are only needed to be opened for sharing packets over UDP.
> * Take necessary measure on firewall level so that the Wireguard server can be reachable on 51820/udp publically.
> * Make sure to clone the [k8s-infra](https://github.com/mosip/k8s-infra/tree/v1.2.0.2/mosip/on-prem#prerequisites) github repo for required scripts in above steps and perform the steps from linked directory.
> * If you already have Wireguard server for the VPC used you can skip the setup Wireguard Bastion server section.

3. execute docker.yml to install docker and add user to docker group:

```yaml
    `ansible-playbook -i hosts.ini docker.yaml`
```    

4. Setup Wireguard server

    * SSH to wireguard VM
    * Create directory for storing wireguard config files.

    ```sh
      `mkdir -p wireguard/config`
    ```  

    * Install and start wireguard server using docker as given below:

    ```sh
    sudo docker run -d \
    --name=wireguard \
    --cap-add=NET_ADMIN \
    --cap-add=SYS_MODULE \
    -e PUID=1000 \
    -e PGID=1000 \
    -e TZ=Asia/Calcutta \
    -e PEERS=30 \
    -p 51820:51820/udp \
    -v /home/ubuntu/wireguard/config:/config \
    -v /lib/modules:/lib/modules \
    --sysctl="net.ipv4.conf.all.src_valid_mark=1" \
    --restart unless-stopped \
    ghcr.io/linuxserver/wireguard
    ```
    
> Note:
>  *  Increase the no. of peers above in case more than 30 wireguard client confs (-e PEERS=30) are needed.  
>  *  Change the directory to be mounted to wireguard docker as per need. All your wireguard confs will be generated in the mounted directory (`-v /home/ubuntu/wireguard/config:/config`).


### Setup Wireguard Client in your PC and follow the below steps:


1. Install [Wireguard client](https://www.wireguard.com/install/) in your PC.

2. Assign `wireguard.conf`:

* SSH to the wireguard server VM.
* `cd /home/ubuntu/wireguard/config`
*  Assign one of the PR for yourself and use the same from the PC to connect to the server.
      
  * Create `assigned.txt` file to assign the keep track of peer files allocated and update everytime some peer is allocated to someone.

    ```sh
    peer1 :   peername
    peer2 :   xyz
    ```

  * Use `ls` cmd to see the list of peers.
  * Get inside your selected peer directory, and add mentioned changes in `peer.conf`:

    * `cd peer1`
    * `nano peer1.conf`

        * Delete the DNS IP.
        * Update the allowed IP's to subnets CIDR ip . e.g. 10.10.20.0/23

  * Share the updated `peer.conf` with respective peer to connect to wireguard server from Personel PC.
  * Add `peer.conf` in your PC’s `/etc/wireguard` directory as `wg0.conf`.

3. Start the wireguard client and check the status:

```sh
sudo systemctl start wg-quick@wg0
sudo systemctl status wg-quick@wg0
```

4. Once connected to wireguard, you should be now able to login using private IP’s.


## Observation cluster setup and configuration

### Observation K8s Cluster setup:

1. Install all the required tools mentioned in pre-requisites for PC.
  * [kubectl](https://kubernetes.io/docs/tasks/tools/#kubectl).
  * [helm](https://helm.sh/docs/intro/install/).
  * [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html).
  * rke (version 1.3.10)
  * istioctl (version v1.15.0)

2. Setup Observation Cluster node VM’s as per the hardware and network requirements as mentioned above.
3. Setup passwordless SSH into the cluster nodes via pem keys. (Ignore if VM’s are accessible via pem’s).

    *  Generate keys on your PC
       `ssh-keygen -t rsa`
    *  Copy the keys to remote observation node VM’s
       `ssh-copy-id <remote-user>@<remote-ip>`
    *  SSH into the node to check password-less SSH
       `ssh -i ~/.ssh/<your private key> <remote-user>@<remote-ip>`

> Note:
> *  Make sure the permission for `privkey.pem` for ssh is set to 400.
> *  Clone [`k8s-infra`](https://github.com/mosip/k8s-infra/tree/v1.2.0.2/rancher/on-prem) and move to required direcyory as per hyperlink.

4. Setup Observation cluster following [steps](https://docs.mosip.io/1.2.0/deploymentnew/v3-installation/on-prem-installation-guidelines#observation-k8s-cluster-setup-and-configuration).

5. Once cluster setup is completed, setup k8's cluster ingress and storage class following [steps](https://docs.mosip.io/1.2.0/deploymentnew/v3-installation/on-prem-installation-guidelines#observation-k8s-cluster-ingress-and-storage-class-setup).

6. Once Observation K8 cluster is created and configured setup nginx server for same using [steps](https://docs.mosip.io/1.2.0/deploymentnew/v3-installation/on-prem-installation-guidelines#setting-up-nginx-server-for-observation-k8s-cluster).

7. Once Nginx server for observation plave is done continue with [installation of required apps:](https://docs.mosip.io/1.2.0/deploymentnew/v3-installation/on-prem-installation-guidelines#observation-k8s-cluster-apps-installation).

  * Install Keycloak.
  * Install Rancher UI.
  * keycloak & Rancher UI Integration.

## eSignet K8 Cluster setup:

1. Setup [pre-requisites](https://github.com/mosip/k8s-infra/tree/v1.2.0.2/mosip/on-prem#prerequisites) in your personel computer.
2. Clone the Kubernetes Infrastructure Repository:

make sure to use the released tag. Specifically v1.2.0.2.

```sh
git clone -b v1.2.0.2 https://github.com/mosip/k8s-infra.git
cd k8s-infra/mosip/onprem
```

3. Create copy of hosts.ini.sample as hosts.ini. Update the IP addresses.
4. Execute [`ports.yml`](https://github.com/mosip/k8s-infra/tree/v1.2.0.2/mosip/on-prem#ports) to open all the required ports.
5. Install [Docker](https://github.com/mosip/k8s-infra/tree/v1.2.0.2/mosip/on-prem#docker) on all the required VM's.
6. Create [RKE1 K8](https://github.com/mosip/k8s-infra/tree/v1.2.0.2/mosip/on-prem#rke-cluster-setup) cluster for eSignet services hosting.
7. [Import](https://github.com/mosip/k8s-infra/tree/v1.2.0.2/mosip/on-prem#register-the-cluster-with-rancher) newly created K8 cluster to Rancher UI.


## eSignet K8 Cluster Configuration:

* Setup [NFS](https://github.com/mosip/k8s-infra/tree/v1.2.0.2/nfs#nfs-setup) for persistence in k8 cluster as well as standalone VM (Nginx VM).
* Setup [Monitoring](https://github.com/mosip/k8s-infra/tree/v1.2.0.2/monitoring#cluster-monitoring) for K8 cluster Monitoring.
* Setup [Logging](https://github.com/mosip/k8s-infra/tree/v1.2.0.2/logging#logging) for K8 cluster.
* Setup [Istio](https://github.com/mosip/k8s-infra/tree/v1.2.0.2/mosip/on-prem/istio#istio) and kiali.


## Nginx for eSignet K8 Cluster:


1. Setup [Nginx](https://github.com/mosip/k8s-infra/tree/v1.2.0.2/mosip/on-prem/nginx) for exposing services from newly created eSignet K8 cluster.


## Install eSignet and pre-requisite servivces:


2. Clone the eSignet repository: (select tag based upon the compatibility matrix)

```sh
git clone -b <tag> https://github.com/mosip/esignet.git
cd esignet
```

3. Install [pre-requisites](https://github.com/mosip/esignet/blob/release-1.5.x/deploy/README.md#install-pre-requisites) for eSignet from deploy directory.

```sh
cd deploy
```

## follow pre-requisites deployment steps:


1. [Initialiase pre-requisites](https://github.com/mosip/esignet/blob/release-1.5.x/deploy/README.md#initialise-pre-requisites) for eSignet services.
2. Install eSignet and OIDC [services](https://github.com/mosip/esignet/blob/release-1.5.x/deploy/README.md#install-esignet-and-oidc).
3. [Onboard](https://github.com/mosip/esignet/blob/release-1.5.x/deploy/README.md#onboarder) eSignet as per the plugin used for deployment.
4. Setup [api-testrig](https://github.com/mosip/esignet/tree/release-1.5.x/deploy/esignet-apitestrig#install) for detailed automated testcase execution.


## Install eSignet mock services:


1. Clone the respective repo: (select tag based upon the compatibility matrix)

```sh
git clone -b <tag> https://github.com/mosip/esignet-mock-services.git
cd esignet-mock-services
```


2. Install [pre-requisites](https://github.com/mosip/esignet-mock-services/tree/release-0.10.x?tab=readme-ov-file#install-pe-req-for-mock-services) for eSignet mock services.

3. Install [eSignet mock](https://github.com/mosip/esignet-mock-services/tree/release-0.10.x?tab=readme-ov-file#install-esignet-mock-services) services.

4. Onboard [esignet mock](https://github.com/mosip/esignet-mock-services/tree/release-0.10.x/partner-onboarder#partner-onboarder) services.


## Install eSignet signup and its pre-requisites services:

1. Clone the respective repo: (select tag based upon the compatibility matrix)


```sh
git clone -b <tag> https://github.com/mosip/esignet-signup.git
cd esignet-signup
```


2. Install [pre-requisites](https://github.com/mosip/esignet-signup/tree/release-1.1.x?tab=readme-ov-file#setup-pre-requisites-for-signup-services) for eSignet Signup services.

3. Install [eSignet signup](https://github.com/mosip/esignet-signup/tree/release-1.1.x?tab=readme-ov-file#install-signup-service) services.

4. Deploy dependencies for eSignet signup onboarder following [steps](https://github.com/mosip/esignet-signup/tree/release-1.1.x?tab=readme-ov-file#prerequisites-for-mosip-kernel-services).

5. [Onboard](https://github.com/mosip/esignet-signup/tree/release-1.1.x/partner-onboarder#partner-onboarder) eSignet signup services.
