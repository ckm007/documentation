# Pre-requisites

## Hardware requirements

* VM’s required can be with any OS as per convenience.
* Here, we are referting to Ubuntu OS throughout this installation guide.

| Sl no. | Purpose                                                 | vCPU's | RAM   | Storage (HDD) | no. ofVM's | HA                               |
| ------ | ------------------------------------------------------- | ------ | ----- | ------------- | ---------- | -------------------------------- |
| 1.     | Wireguard Bastion Host                                  | 2      | 4 GB  | 8 GB          | 1          | (ensure to setup active-passive) |
| 2.     | Observation Cluster nodes                               | 2      | 8 GB  | 32 GB         | 2          | 2                                |
| 3.     | Observation Nginx server (use Loadbalancer if required) | 2      | 4 GB  | 16 GB         | 2          | Nginx+                           |
| 4.     | MOSIP Cluster nodes                                     | 12     | 32 GB | 128 GB        | 6          | 6                                |
| 5.     | MOSIP Nginx server ( use Loadbalancer if required)      | 2      | 4 GB  | 16 GB         | 1          | Nginx+                           |

## Network requirements

* All the VM's should be able to communicate with each other.
* Need stable Intra network connectivity between these VM's.
* All the VM's should have stable internet connectivity for docker image download (in case of local setup ensure to have a locally accessible docker registry).
* Server Interface requirement as mentioned in below table:

| Sl no. | Purpose                  | Network Interfaces                                                                                                                                                                                                                                                                                         |
| ------ | ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.     | Wireguard Bastion Host   | <p><em>One Private interface</em> : that is on the same network as all the rest of nodes (e.g.: inside local NAT Network).<br><br><em>One public interface</em> : Either has a direct public IP, or a firewall NAT (global address) rule that forwards traffic on 51820/udp port to this interface IP.</p> |
| 2.     | K8 Cluster nodes         | One internal interface: with internet access and that is on the same network as all the rest of nodes (e.g.: inside local NAT Network )                                                                                                                                                                    |
| 3.     | Observation Nginx server | One internal interface: with internet access and that is on the same network as all the rest of nodes (e.g.: inside local NAT Network).                                                                                                                                                                    |
| 4.     | Mosip Nginx server       | <p><em>One internal interface</em> : that is on the same network as all the rest of nodes (e.g.: inside local NAT Network).<br><br><em>One public interface</em> : Either has a direct public IP, or a firewall NAT (global address) rule that forwards traffic on 443/tcp port to this interface IP.</p>  |

## DNS requirements

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

## Certificate requirements

As only secured https connections are allowed via nginx server will need below mentioned valid ssl certificates:

* One valid wildcard ssl certificate related to domain used for accessing Observation cluster, this needs to be stored inside the nginx server VM for Observation cluster. In above e.g.: \*.org.net is the similar example domain.
* One valid wildcard ssl certificate related to domain used for accessing Mosip cluster, this needs to be stored inside the nginx server VM for mosip cluster. In above e.g.: \*.sandbox.xyz.net is the similar example domain.

## Personal computer requirements

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

    * clone k8’s infra repo with tag : 1.2.0.1 (**whichever is the latest version**) inside mosip directory. `git clone https://github.com/mosip/k8s-infra -b v1.2.0.1`
    * clone mosip-infra with tag : 1.2.0.1 (**whichever is the latest version**) inside mosip directory. `git clone https://github.com/mosip/mosip-infra -b v1.2.0.1`
    * Set below mentioned variables in bashrc

    ```
    export MOSIP_ROOT=<location of mosip directory>
    export K8_ROOT=$MOSIP_ROOT/k8s-infra
    export INFRA_ROOT=$MOSIP_ROOT/mosip-infra
    ```

    `source .bashrc`

    > Note: Above mentioned environment variables will be used throughout the installation to move between one directory to other to run install scripts.
