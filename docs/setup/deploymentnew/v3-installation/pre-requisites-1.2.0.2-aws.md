# Pre-requisites:

## Hardware Requirements

VM’s required have any Operating System and can be selected as per convenience.\
In this installation guide, we are referring to `Ubuntu OS` throughout.

|   | **Purpose**                         | **vCPU’s** | **RAM** | **Storage (HDD)** | **no. of VM’s** | **HA**                           |
| - | ----------------------------------- | ---------- | ------- | ----------------- | --------------- | -------------------------------- |
| 1 | Wireguard Bastion Host              | 2          | 4 GB    | 8 GB              | 1               | (ensure to setup active-passive) |
| 2 | Rancher Cluster nodes (EKS managed) | 2          | 8 GB    | 32 GB             | 2               | 2                                |
| 3 | Mosip Cluster nodes (EKS managed)   | 8          | 32 GB   | 64 GB             | 6               | 6                                |

## Network Requirements

* All the VM's should be able to communicate with each other.
* Need stable Intra network connectivity between these VM's.
* All the VM's should have stable internet connectivity for docker image download (in case of local setup ensure to have a locally accesible docker registry).
* During the process, we will be creating two loadbalancers as mentioned in the first table below:
* Server Interface requirement as mentioned in the second table:

| **Loadbalancer**                         | **Purpose**                                                                                                                                                                                                                   |
| ---------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Private loadbalancer Observation cluster | <p>This will be used to access Rancher dashboard and keycloak of observation cluster.</p><p>Note: access to this will be restricted only with wireguard key holders.</p>                                                      |
| Public loadbalancer MOSIP cluster        | <p>This will be used to access below mentioned services:</p><ul><li>Pre-registration</li><li>Esignet</li><li>IDA</li><li>Partner management service api’s</li><li>Mimoto</li><li>Mosip file server</li><li>Resident</li></ul> |
| Private loadbalancer MOSIP cluster       | <p>This will be used to access all the services deployed as part of the setup inclusing external as well as all the MOSIP services.</p><p>Note: access to this will be restricted only with wireguard key holders.</p>        |

|   | **Purpose VM**         | **Network Interfaces**                                                                                                                                                                                                                                                                            |
| - | ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1 | Wireguard Bastion Host | <ul><li>One Private interface: that is on the same network as all the rest of nodes. (Eg: inside local NAT Network )</li><li>One public interface: Either has a direct public IP, or a firewall NAT (global address) rule that forwards traffic on 51820/udp port to this interface ip.</li></ul> |

## DNS Requirements

|    | **Domain name**                                                     | **Mapping details**                    | **Purpose**                                                                                                                                                                                                                                     |
| -- | ------------------------------------------------------------------- | -------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1  | [rancher.xyz.net](http://rancher.xyz.net)                           | Load balancer of Observation cluster   | Rancher dashboard to monitor and manage the kubernetes cluster. You can share an existing rancher cluser.                                                                                                                                       |
| 2  | [keycloak.xyz.net](http://keycloak.xyz.net)                         | Load balancer of Observation cluster   | Administrative IAM tool (keycloak). This is for the kubernetes administration.                                                                                                                                                                  |
| 3  | [sandbox.xyx.net](http://sandbox.xyx.net)                           | Private Load balancer of MOSIP cluster | Index page for links to different dashboards of Mosip env. (This is just for reference, Please do not expose this page in a real production or uat environment)                                                                                 |
| 4  | [api-internal.sandbox.xyz.net](http://api-internal.sandbox.xyz.net) | Private Load balancer of MOSIP cluster | Internal API’s are exposed through this domain. They are accessible privately over wireguard channel                                                                                                                                            |
| 5  | [api.sandbox.xyx.net](http://api.sandbox.xyx.net)                   | Public Load balancer of MOSIP cluster  | All the API’s that are publically usable are exposed using this domain.                                                                                                                                                                         |
| 6  | [prereg.sandbox.xyz.net](http://prereg.sandbox.xyz.net)             | Public Load balancer of MOSIP cluster  | Domain name for Mosip’s pre-registration portal. The portal is accessible publicly.                                                                                                                                                             |
| 7  | [activemq.sandbox.xyx.net](http://activemq.sandbox.xyx.net)         | Private Load balancer of MOSIP cluster | Provides direct access to activemq dashboard. Its limited and can be used only over wireguard                                                                                                                                                   |
| 8  | [kibana.sandbox.xyx.net](http://kibana.sandbox.xyx.net)             | Private Load balancer of MOSIP cluster | Optional instalation. Used to access kibana dashboard over wireguard                                                                                                                                                                            |
| 9  | [regclient.sandbox.xyz.net](http://regclient.sandbox.xyz.net)       | Private Load balancer of MOSIP cluster | Regclient can be downloaded from this domain. It should be used over wireguard.                                                                                                                                                                 |
| 10 | [admin.sandbox.xyz.net](http://admin.sandbox.xyz.net)               | Private Load balancer of MOSIP cluster | Mosip’s admin portal is exposed using this domain. This is an internal domain and is restricted to access over wireguard                                                                                                                        |
| 11 | [object-store.sandbox.xyx.net](http://object-store.sandbox.xyx.net) | Private Load balancer of MOSIP cluster | Optional- This domain is used to access the object server. Based on the object server that you choose map this domain accordingly. In our reference implementation Minio is used and this domain lets you access Minio’s Console over wireguard |
| 12 | [kafka.sandbox.xyz.net](http://kafka.sandbox.xyz.net)               | Private Load balancer of MOSIP cluster | Kafka UI is installed as part of the Mosip’s default installation. We can access kafka ui over wireguard. Mostly used for administrative needs.                                                                                                 |
| 13 | [iam.sandbox.xyz.net](http://iam.sandbox.xyz.net)                   | Private Load balancer of MOSIP cluster | Mosip uses an Openid connect server to limit and manage access across all the services. The default installation comes with Keycloak. This domain is used to access the keycloak server over wireguard                                          |
| 14 | [postgres.sandbox.xyz.net](http://postgres.sandbox.xyz.net)         | Private Load balancer of MOSIP cluster | This domain points to the postgres server. You can connect to postgres via port forwarding over wireguard                                                                                                                                       |
| 15 | [pmp.sandbox.xyz.net](http://pmp.sandbox.xyz.net)                   | Public Load balancer of MOSIP cluster  | Mosip’s partner management portal is used to manage partners accessing partner management portal over wireguard                                                                                                                                 |
| 16 | [resident.sandbox.xyz.net](http://resident.sandbox.xyz.net)         | Public Load balancer of MOSIP cluster  | accessident resident portal publically                                                                                                                                                                                                          |
| 17 | [esignet.sandbox.xyz.net](http://idp.sandbox.xyz.net)               | Public Load balancer of MOSIP cluster  | accessing IDP over public                                                                                                                                                                                                                       |
| 18 | [smtp.sandbox.xyz.net](http://smtp.sandbox.xyz.net)                 | Private Load balancer of MOSIP cluster | Accessing mock-smtp UI over wireguard                                                                                                                                                                                                           |

**Note:**

* Only proceed to DNS mapping after the ingressgateways are installed and the load balancer is already configured.
* The above table is just a placeholder for hostnames, the actual name itself varies from organisation to organisation.

## Certificate requirements

As only secured `https` connections are allowed via nginx server, you will need the below mentioned valid ssl certificates:

* One valid wildcard ssl certificate related to domain used for accesing Observation cluster which will be created using ACM (Amazon certificate manager). In above e.g. \*.[org.net](http://org.net/) is the similiar example domain.
* One valid wildcard ssl certificate related to domain used for accessing MOSIP cluster which will be created using ACM (Amazon certificate manager). In above e.g. \*.[sandbox.xyz.net](http://sandbox.xyz.net/) is the similiar example domain.

## Prerequisite for complete deployment in Personal Computer

* [kubectl](https://kubernetes.io/docs/tasks/tools/#kubectl) client version 1.23.6
* [helm](https://helm.sh/docs/intro/install/) client version 3.8.2 and add below repos as well :
  * ```java
    helm repo add bitnami https://charts.bitnami.com/bitnami
    helm repo add mosip https://mosip.github.io/mosip-helm
    ```
* [istioctl](https://istio.io/latest/docs/setup/getting-started/#download) : version: 1.15.0
* [eksctl](https://docs.aws.amazon.com/eks/latest/userguide/eksctl.html) : version: 0.121.0
* AWS account and credentials with permissions to create EKS cluster.
* AWS credentials in `~/.aws/` folder as given [here](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html).
* Save `~/.kube/config` file with another name. _(IMPORTANT. As in this process your existing_ `~/.kube/config` file will be overridden).
* Save `.pem` file from AWS console and store it in `~/.ssh/` folder. (Generate a new one if you do not have this key file).
* Create a directory as mosip in your PC and
  * clone k8’s infra repo with tag : 1.2.0.1-B2 inside mosip directory.\
    `git clone https://github.com/mosip/k8s-infra -b v1.2.0.1-B2`
  * clone mosip-infra with tag : 1.2.0.1-B2 inside mosip directory\
    `git clone https://github.com/mosip/mosip-infra -b v1.2.0.1-B2`
  * Set below mentioned variables in bashrc
    * ```java
      export MOSIP_ROOT=<location of mosip directory>
      export K8_ROOT=$MOSIP_ROOT/k8s-infra
      export INFRA_ROOT=$MOSIP_ROOT/mosip-infra
      ```
    * `source .bashrc`\
      **Note:**\
      Above mentioned environment variables will be used throughout the installation to move between one directory to other to run install scripts.
