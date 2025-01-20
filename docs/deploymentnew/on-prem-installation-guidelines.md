# On-Prem Installation Guidelines
## Overview
* This guide provides comprehensive instructions for on-premises MOSIP deployment.
* MOSIP operates as a collection of microservices hosted within Kubernetes clusters to ensure scalability, modularity, and high availability.
* The deployment process includes the following key components and configurations:
  * [Wireguard](https://www.wireguard.com/) is used as a trust network extension to access the admin, control, and observation pane along with on-field registration client connectivity to backend server.
  * MOSIP uses [Nginx](https://www.nginx.com/) server for:
    * SSL termination
    * Reverse Proxy
    * CDN/Cache management
    * Loadbalancing
  * Kubernetes (K8s) cluster creation, configuration and administration of same.
    * K8 cluster is created using the [Rancher](https://rancher.com/docs/rancher/v1.3/en/kubernetes/#rancher-ui) and [rke](https://www.rancher.com/products/rke) tools.
    * K8 cluster essentially used in V3 ref-impl architecture:
      * Observation K8 cluster
      * MOSIP application K8 cluster  
    * Setting up ingress for exposing application services outside K8 cluster.
    * Setting up storage class used as persistence in the K8 cluster.
    * Setting up Logging system to continously scrape logs out of all the pods as per need.
    * Setting up Monitoring to continously monitor logs and multiple graphs to be able to manage application and cluster better.
    * Setting alerting to make sure users are identified about crucial events as and when needed.
  * Observation K8 cluster contains:
    * Rancher Ui : application used to create manage k8 cluster. This is needed once for an organisation as it can manage multiple dev, qa and prod k8 cluster easily.
    * Kecloak : IAM tool used for defining RBAC policies for allowing access to Rancher.
  * MOSIP k8 cluster containes:
    * Pre-requisite services: Services required to support MOSIP application deployment:
      * HSM/SoftHSM : are cryptographic solutions used to securely manage and store cryptographic keys.
      * Postgres : open-source, relational database management system (RDBMS) known for its robustness, extensibility, and compliance with SQL standards.
      * Keycloak :  is an open-source Identity and Access Management (IAM) solution which provides authentication, authorization, and user management for modern applications and services.
      * ActiveMq :  is an open-source message broker which facilitates communication between distributed systems using messaging protocols, enabling asynchronous communication and decoupling between producers and consumers.
      * Kafka : is an open-source, distributed event streaming platform designed for high-throughput, fault-tolerant, and real-time data processing. It is widely used for building data pipelines, real-time analytics, and event-driven architectures.
      * Object store : is a type of storage system designed to store, retrieve, and manage unstructured data as discrete units called objects. It is highly scalable and ideal for storing vast amounts of data like multimedia files, backups, logs, and more. Popular examples include Amazon S3, Google Cloud Storage, and MinIO.
      * ABIS : (Automated Biometric Identification System) is a system designed to collect, store, and match biometric data for identification or verification purposes.
      * BioSDK : provides the necessary tools to capture, process, and match biometric data. These SDKs typically support multiple biometric modalities, such as fingerprint, face, iris, voice, and more.
      * Captcha : is a type of challenge-response test designed to determine whether the user is a human or a bot. It is used to prevent automated software from performing actions that could be harmful or disruptive, such as spamming, brute force attacks, or creating fake accounts.
      * Msg-Gateway : platform that facilitates the transmission of messages between different communication channels or systems. It acts as a bridge, enabling communication across various messaging services or protocols, such as SMS, email, push notifications, or even custom messaging services.
      * Landing page : is a standalone web-page create specifically for admin users to land them up to all the dashboards and UI's available as part of MOSIP.
      * docker-registry secrets : used to pull docker images from private/local dockerhub/registry from k8s cluster.
    * MOSIP Modules:
      * 


**MOSIP cluster** - This cluster runs all the MOSIP components and certain third party components to secure the cluster, API’s and data.

* [MOSIP External Components](https://github.com/mosip/mosip-infra/blob/v1.2.0.1/deployment/v3/external/README.md#mosip-external-components)
* [MOSIP Services](https://github.com/mosip/mosip-infra/blob/v1.2.0.1/deployment/v3/mosip/README.md#mosip-services)

### Architecture 

![](\_images/deployment\_architecture.png)

### Deployment repos

* [k8s-infra](https://github.com/mosip/k8s-infra/tree/v1.2.0.1) : contains the scripts to install and configure Kubernetes cluster with required monitoring, logging and alerting tools.
* [mosip-infra](https://github.com/mosip/mosip-infra/tree/v1.2.0.1/deployment/v3) : contains the deployment scripts to run charts in defined sequence.
* [mosip-config](https://github.com/mosip/mosip-config/tree/v1.2.0.1) : contains all the configuration files required by the MOSIP modules.
* [mosip-helm](https://github.com/mosip/mosip-helm/tree/v1.2.0.1) : contains packaged helm charts for all the MOSIP modules.

### Pre-requisites

#### Hardware requirements

* VM’s required can be with any OS as per convenience.
* Here, we are referting to Ubuntu OS throughout this installation guide.

| Sl no. | Purpose                                                 | vCPU's | RAM   | Storage (HDD) | no. ofVM's | HA                               |
| ------ | ------------------------------------------------------- | ------ | ----- | ------------- | ---------- | -------------------------------- |
| 1.     | Wireguard Bastion Host                                  | 2      | 4 GB  | 8 GB          | 1          | (ensure to setup active-passive) |
| 2.     | Observation Cluster nodes                               | 2      | 8 GB  | 32 GB         | 2          | 2                                |
| 3.     | Observation Nginx server (use Loadbalancer if required) | 2      | 4 GB  | 16 GB         | 2          | Nginx+                           |
| 4.     | MOSIP Cluster nodes                                     | 12     | 32 GB | 128 GB        | 6          | 6                                |
| 5.     | MOSIP Nginx server ( use Loadbalancer if required)      | 2      | 4 GB  | 16 GB         | 1          | Nginx+                           |

#### Network requirements

* All the VM's should be able to communicate with each other.
* Need stable Intra network connectivity between these VM's.
* All the VM's should have stable internet connectivity for docker image download (in case of local setup ensure to have a locally accesible docker registry).
* Server Interface requirement as mentioned in below table:

| Sl no. | Purpose                  | Network Interfaces                                                                                                                                                                                                                                                                                         |
| ------ | ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.     | Wireguard Bastion Host   | <p><em>One Private interface</em> : that is on the same network as all the rest of nodes (e.g.: inside local NAT Network).<br><br><em>One public interface</em> : Either has a direct public IP, or a firewall NAT (global address) rule that forwards traffic on 51820/udp port to this interface IP.</p> |
| 2.     | K8 Cluster nodes         | One internal interface: with internet access and that is on the same network as all the rest of nodes (e.g.: inside local NAT Network )                                                                                                                                                                    |
| 3.     | Observation Nginx server | One internal interface: with internet access and that is on the same network as all the rest of nodes (e.g.: inside local NAT Network).                                                                                                                                                                    |
| 4.     | Mosip Nginx server       | <p><em>One internal interface</em> : that is on the same network as all the rest of nodes (e.g.: inside local NAT Network).<br><br><em>One public interface</em> : Either has a direct public IP, or a firewall NAT (global address) rule that forwards traffic on 443/tcp port to this interface IP.</p>  |

#### DNS requirements

|     | Domain Name                  | Mapping details                                                     | Purpose                                                                                                                                                                                                                                           |
| --- | ---------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.  | rancher.xyz.net              | Private IP of Nginx server or load balancer for Observation cluster | Rancher dashboard to monitor and manage the kubernetes cluster.                                                                                                                                                                                   |
| 2.  | keycloak.xyz.net             | Private IP of Nginx server for Observation cluster                  | Administrative IAM tool (keycloak). This is for the kubernetes administration.                                                                                                                                                                    |
| 3.  | sandbox.xyx.net              | Private IP of Nginx server for MOSIP cluster                        | Index page for links to different dashboards of MOSIP env. (This is just for reference, please do not expose this page in a real production or UAT environment)                                                                                   |
| 4.  | api-internal.sandbox.xyz.net | Private IP of Nginx server for MOSIP cluster                        | Internal API’s are exposed through this domain. They are accessible privately over wireguard channel                                                                                                                                              |
| 5.  | api.sandbox.xyx.net          | Public IP of Nginx server for MOSIP cluster                         | All the API’s that are publically usable are exposed using this domain.                                                                                                                                                                           |
| 6.  | prereg.sandbox.xyz.net       | Public IP of Nginx server for MOSIP cluster                         | Domain name for MOSIP's pre-registration portal. The portal is accessible publicly.                                                                                                                                                               |
| 7.  | activemq.sandbox.xyx.net     | Private IP of Nginx server for MOSIP cluster                        | Provides direct access to `activemq` dashboard. It is limited and can be used only over wireguard.                                                                                                                                                |
| 8.  | kibana.sandbox.xyx.net       | Private IP of Nginx server for MOSIP cluster                        | Optional installation. Used to access kibana dashboard over wireguard.                                                                                                                                                                            |
| 9.  | regclient.sandbox.xyz.net    | Private IP of Nginx server for MOSIP cluster                        | Registration Client can be downloaded from this domain. It should be used over wireguard.                                                                                                                                                         |
| 10. | admin.sandbox.xyz.net        | Private IP of Nginx server for MOSIP cluster                        | MOSIP's admin portal is exposed using this domain. This is an internal domain and is restricted to access over wireguard                                                                                                                          |
| 11. | object-store.sandbox.xyx.net | Private IP of Nginx server for MOSIP cluster                        | Optional- This domain is used to access the object server. Based on the object server that you choose map this domain accordingly. In our reference implementation, MinIO is used and this domain let's you access MinIO’s Console over wireguard |
| 12. | kafka.sandbox.xyz.net        | Private IP of Nginx server for MOSIP cluster                        | Kafka UI is installed as part of the MOSIP’s default installation. We can access kafka UI over wireguard. Mostly used for administrative needs.                                                                                                   |
| 13. | iam.sandbox.xyz.net          | Private IP of Nginx server for MOSIP cluster                        | MOSIP uses an OpenID Connect server to limit and manage access across all the services. The default installation comes with Keycloak. This domain is used to access the keycloak server over wireguard                                            |
| 14. | postgres.sandbox.xyz.net     | Private IP of Nginx server for MOSIP cluster                        | This domain points to the postgres server. You can connect to postgres via port forwarding over wireguard                                                                                                                                         |
| 15. | pmp.sandbox.xyz.net          | Private IP of Nginx server for MOSIP cluster                        | MOSIP’s partner management portal is used to manage partners accessing partner management portal over wireguard                                                                                                                                   |
| 16. | onboarder.sandbox.xyz.net    | Private IP of Nginx server for MOSIP cluster                        | Accessing reports of MOSIP partner onboarding over wireguard                                                                                                                                                                                      |
| 17. | resident.sandbox.xyz.net     | Public IP of Nginx server for MOSIP cluster                         | Accessing resident portal publically                                                                                                                                                                                                              |
| 18. | idp.sandbox.xyz.net          | Public IP of Nginx server for MOSIP cluster                         | Accessing IDP over public                                                                                                                                                                                                                         |
| 19. | smtp.sandbox.xyz.net         | Private IP of Nginx server for MOSIP cluster                        | Accessing mock-smtp UI over wireguard                                                                                                                                                                                                             |

#### Certificate requirements

As only secured https connections are allowed via nginx server will need below mentioned valid ssl certificates:

* One valid wildcard ssl certificate related to domain used for accessing Observation cluster, this needs to be stored inside the nginx server VM for Observation cluster. In above e.g.: \*.org.net is the similiar example domain.
* One valid wildcard ssl certificate related to domain used for accesing Mosip cluster, this needs to be stored inside the nginx server VM for mosip cluster. In above e.g.: \*.sandbox.xyz.net is the similiar example domain.

**Tools to be installed in Personel Computers for complete deployment**

* [kubectl](https://kubernetes.io/docs/tasks/tools/#kubectl)- any client version above 1.19
* [helm](https://helm.sh/docs/intro/install/)- any client version above 3.0.0 and add below repos as well:

```
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo add mosip https://mosip.github.io/mosip-helm
```

* [Istioctl](https://istio.io/latest/docs/setup/getting-started/#download) : version: 1.15.0
* [rke](https://rancher.com/docs/rke/latest/en/installation/) : version: [1.3.10](https://github.com/rancher/rke/releases/tag/v1.3.10)
* \[Ansible]\(https://docs.ansible.com/ansible/latest/installation\_guide/intro\_installation.html: version > 2.12.4
*   Create a directory as mosip in your PC and:

    * clone k8’s infra repo with tag : 1.2.0.1 (**whichever is the latest version**) inside mosip directory.
      `git clone https://github.com/mosip/k8s-infra -b v1.2.0.1`
    * clone mosip-infra with tag : 1.2.0.1 (**whichever is the latest version**) inside mosip directory.
      `git clone https://github.com/mosip/mosip-infra -b v1.2.0.1`
    * Set below mentioned variables in bashrc

    ```
    export MOSIP_ROOT=<location of mosip directory>
    export K8_ROOT=$MOSIP_ROOT/k8s-infra
    export INFRA_ROOT=$MOSIP_ROOT/mosip-infra
    ```

    `source .bashrc`

    > Note: Above mentioned environment variables will be used throughout the installation to move between one directory to other to run install scripts.

### Installation

#### Wireguard

A Wireguard bastion host (Wireguard server) provides secure private channel to access MOSIP cluster. The host restricts public access, and enables access to only those clients who have their public key listed in Wireguard server. Wireguard listens on UDP port51820.

#### Setup Wireguard VM and wireguard bastion server
  * Move to the directory in K8s-infra containing wireguard scripts:
  ```
  cd $K8_ROOT/wireguard/
  ```
  * Follow the [steps](https://github.com/mosip/k8s-infra/tree/develop/wireguard#setup-wireguard-bastion-server) to setup wireguard Bastion server along with wireguard client in your system and connect to continue with rest of deloyment.

## Observation K8s Cluster setup and configuration
### Pre-requisites
* Install all the required tools mentioned in pre-requisites for PC.
  * kubectl
  * helm
  * ansible
  * rke (version 1.3.10)
* Setup Observation Cluster node VM’s as per the hardware and network requirements as mentioned above.
* Setup passwordless SSH into the cluster nodes via pem keys. (Ignore if VM’s are accessible via pem’s).
    *  Generate keys on your PC
       `ssh-keygen -t rsa`
    *  Copy the keys to remote observation node VM’s
       `ssh-copy-id <remote-user>@<remote-ip>`
    *  SSH into the node to check password-less SSH
       `ssh -i ~/.ssh/<your private key> <remote-user>@<remote-ip>`
> Note:
> *  Make sure the permission for `privkey.pem` for ssh is set to 400.

* Run `env-check-setup.yaml` to check if cluster nodes are fine and do not have known issues in it.
  * `cd $K8_ROOT/k8-cluster/on-prem/rke1/`
  * create copy of `hosts.ini.sample` as `hosts.ini` and update the required details for Observation k8 cluster nodes.
    * `cp hosts.ini.sample hosts.ini`
    * `ansible-playbook -i hosts.ini env-check-setup.yaml`
    * This ansible checks if localhost mapping is already present in /etc/hosts file in all cluster nodes, if not it adds the same.
### Observation plane K8 cluster creation
* Use any of the ways mentioned [here](https://github.com/mosip/k8s-infra/blob/develop/k8-cluster/on-prem/README.md) for k8 cluster creation.
* Preferred way with respect to this sandbox installation will be RKE2 as it is easy to setup and manage as compared to RKE1.
* `cd $K8_ROOT/k8-cluster/on-prem/rke2/ansible`
* Follow the [steps](https://github.com/mosip/k8s-infra/blob/develop/k8-cluster/on-prem/rke2/ansible/README.md) to setup k8 cluster using preffered way i.e. RKE2 using ansible automation.
### Observation K8s Cluster Ingress and Storage class setup
* Deploy Ingress using mentioned [steps](https://github.com/mosip/k8s-infra/tree/develop/ingress/ingress-nginx#deploy-as-nodeport) from below directory:
  ```
  cd $K8_ROOT/ingress/ingress-nginx
  ```
* Setup Storage class for observation cluster using any of the mentioned [ways](https://github.com/mosip/k8s-infra/tree/develop/storage-class).
* Recommendsation to use [NFS](https://github.com/mosip/k8s-infra/tree/develop/storage-class/nfs#readme) as storage class for this sandox consideration from below directory.
  ```
  cd $K8_ROOT/storage-class/nfs/
  ```
### Setting up nginx server for Observation K8s Cluster
* Setup Nginx server for exposing services by Observation K8 cluster using mentioned [steps](https://github.com/mosip/k8s-infra/tree/develop/nginx/observation#readme) from below mentioned directory.
  ```
  cd $K8_ROOT/nginx/observation
  ```
### Observation K8's Cluster Apps Installation
* Rancher UI : Follow the [instructions](https://github.com/mosip/k8s-infra/blob/develop/apps/rancher-ui/README.md) to setup Rancher UI in Observation k8 cluster from below mentioned directory:
  ```
  cd $K8_ROOT/apps/rancher-ui
  ```
* Keycloak and Integration with Rancher UI: Follow the [instructions](https://github.com/mosip/k8s-infra/tree/develop/apps/keycloak#readme) to install keycloak as IAM tool followed by Rancher UI integration.

### RBAC for Rancher using Keycloak

* For users in Keycloak assign roles in Rancher - **cluster** and **project** roles. Under `default` project add all the namespaces. Then, to a non-admin user you may provide Read-Only role (under projects).
* If you want to create custom roles, you can follow the steps given [here](https://github.com/mosip/k8s-infra/blob/v1.2.0.1/docs/create-custom-role.md).
* Add a member to cluster/project in Rancher:
  * Navigate to RBAC cluster members
  * Add member name exactly as `username` in Keycloak
  * Assign appropriate role like Cluster Owner, Cluster Viewer etc.
  * You may create new role with fine grained acccess control.
* Add group to to cluster/project in Rancher:
  * Navigate to RBAC cluster members
  * Click on `Add` and select a group from the displayed drop-down.
  * Assign appropriate role like Cluster Owner, Cluster Viewer etc.
  * To add groups, the user must be a member of the group.
* Creating a Keycloak group involves the following steps:
  * Go to the "Groups" section in Keycloak and create groups with default roles.
  * Navigate to the "Users" section in Keycloak, select a user, and then go to the "Groups" tab. From the list of groups, add the user to the required group.

## MOSIP K8s Cluster setup and Configuration
### Mosip K8 cluster creation:
* Install all the required tools mentioned in pre-requisites for PC.
  * kubectl
  * helm
  * ansible
  *  Rancher UI : (deployed in Observation K8 cluster)
* Setup MOSIP Cluster node VM’s as per the hardware and network requirements as mentioned above.
* Setup passwordless SSH into the cluster nodes via pem keys. (Ignore if VM’s are accessible via pem’s).
    *  Generate keys on your PC
       `ssh-keygen -t rsa`
    *  Copy the keys to remote observation node VM’s
       `ssh-copy-id <remote-user>@<remote-ip>`
    *  SSH into the node to check password-less SSH
       `ssh -i ~/.ssh/<your private key> <remote-user>@<remote-ip>`
> Note:
> *  Make sure the permission for `privkey.pem` for ssh is set to 400.

* Run `env-check-setup.yaml` to check if cluster nodes are fine and do not have known issues in it.
  * `cd $K8_ROOT/k8-cluster/on-prem/rke1/`
  * create copy of `hosts.ini.sample` as `hosts.ini` and update the required details for Observation k8 cluster nodes.
    * `cp hosts.ini.sample hosts.ini`
    * `ansible-playbook -i hosts.ini env-check-setup.yaml`
    * This ansible checks if localhost mapping is already present in /etc/hosts file in all cluster nodes, if not it adds the same.
* Use any of the ways mentioned [here](https://github.com/mosip/k8s-infra/blob/develop/k8-cluster/on-prem/README.md) for k8 cluster creation.
* Preferred way with respect to this sandbox installation will be RKE2 as it is easy to setup and manage as compared to RKE1.
* `cd $K8_ROOT/k8-cluster/on-prem/rke2/ansible`
* Follow the [steps](https://github.com/mosip/k8s-infra/blob/develop/k8-cluster/on-prem/rke2/ansible/README.md) to setup k8 cluster using preffered way i.e. RKE2 using ansible automation.
### Import MOSIP Cluster into Rancher UI
* Login as admin in Rancher console
* Select `Impor`t Existing for cluster addition.
* Select `Generic` as cluster type to add.
* Fill the `Cluster Name` field with unique cluster name and select `Create`.
* You will get the kubecl commands to be executed in the kubernetes cluster. Copy the command and execute from your PC (make sure your `kube-config` file is correctly set to MOSIP cluster).
```
e.g.:
kubectl apply -f https://rancher.e2e.mosip.net/v3/import/pdmkx6b4xxtpcd699gzwdtt5bckwf4ctdgr7xkmmtwg8dfjk4hmbpk_c-m-db8kcj4r.yaml
```
* Wait for few seconds after executing the command for the cluster to get verified.
* Your cluster is now added to the rancher management server.
### Storage Class Setup:
* k8s-infra repo contains multiple [ways](https://github.com/mosip/k8s-infra/tree/develop/storage-class) to setup and configure storage class in a k8 cluster.
* As part of this Sandbox installation will prefer to use nfs as storage class following [steps](https://github.com/mosip/k8s-infra/tree/develop/storage-class/nfs#readme) from below directory.
* `cd  $K8_ROOT/storage-class/nfs`
* Note: As part of this sandbox installation will use Nginx server VM as NFS server as well.
### Ingress Setup
* Deploy Ingress using mentioned [steps](https://github.com/mosip/k8s-infra/tree/develop/ingress/istio-mesh/nodeport#readme) from below directory:
  ```
  cd $K8_ROOT/ingress/istio-mesh/nodeport
  ```
### MOSIP cluster Logging deployment
* Setup Logging services to scrape logs of all the application pods and provide that as input to monitoring using [steps](https://github.com/mosip/k8s-infra/tree/develop/logging#readme) from below directory:
```
cd $K8_ROOT/logging
```
### MOSIP cluster Monitoring deployment
* Setup monitoring services to monitor all the application pods and use dashboards to track multiple metrics and graphs using [steps](https://github.com/mosip/k8s-infra/tree/develop/monitoring#readme) from below mentioned directory:
```
cd $K8_ROOT/monitoring
```
### MOSIP cluster Alerting deployment
* Setup alerting for MOSIP cluster for crucial cluster events using [steps](https://github.com/mosip/k8s-infra/tree/develop/alerting#readme) from below directory:
```
cd $K8_ROOT/alerting
```
## Setting up nginx server for MOSIP K8s Cluster
* Setup Nginx server for exposing services of MOSIP K8 cluster using mentioned [steps](https://github.com/mosip/k8s-infra/tree/develop/nginx/mosip#readme) from below mentioned directory.
  ```
  cd $K8_ROOT/nginx/mosip
  ```

## MOSIP External Dependencies setup
External Dependencies are set of external requirements that are needed for functioning of MOSIP’s core services like DB, Object Store, HSM etc.
```
cd $INFRA_ROOT/deployment/v3/external/all
./install-all.sh
```
Click [here](https://docs.mosip.io/1.2.0/deploymentnew/v3-installation/mosip-external-dependencies) to check the detailed installation instructions of all the external components.
### MOSIP Modules Deployment
Now that all the Kubernetes cluster and external dependencies are already installed, will continue with MOSIP service deployment.
```
cd $INFRA_ROOT/deployment/v3/mosip/all
./install-all.sh
```
Check detailed [MOSIP Modules Deployment](https://docs.mosip.io/1.2.0/deploymentnew/v3-installation/mosip-modules-deployment) installation steps.
